from flask import Flask, request, render_template_string
import subprocess

app = Flask(__name__)

@app.route('/')
def index():
    return render_template_string(open('index.html').read())

@app.route('/execute', methods=['POST'])
def execute():
    note = request.form['note']
# 简单示例：将文本转换为Python代码
    code = f'print("{note}")'
    try:
# 执行代码并捕获输出
        result = subprocess.run(['python3', '-c', code], capture_output=True, text=True)
        output = result.stdout
    except Exception as e:
        output = str(e)
    return f"<pre>{output}</pre>"

if __name__ == '__main__':
    app.run(debug=True)             <!DOCTYPE html>
<html>
<head>
    <title>记事本</title>
</head>
<body>
    <h1>记事本</h1>
    <form action="/execute" method="post">
        <textarea name="note" rows="10" cols="30"></textarea><br>
        <input type="submit" value="提交">
    </form>
</body>
</html>app.runresult.stdout<!DOCTYPE html>
<html>
<head>
    <title>记事本</title>
</head>
<body>
    <h1>记事本</h1>
    <form action="/execute" method="post">
        <textarea name="note" rows="10" cols="30"></textarea><br>
        <input type="submit" value="提交">
    </form>
</body>
