<!DOCTYPE html>
<html>
<head>
  <title>Minepi Demo</title>
  <script src="https://sdk.minepi.com/pi-sdk.js"></script>
</head>
<body>
  <button id="start-mining">Start Mining Pi</button>
  <div id="status">Status: Not Mining</div>
  <script>
    document.getElementById('start-mining').addEventListener('click', () => {
      const statusDiv = document.getElementById('status');
      try {
        Pi.startMining();
        statusDiv.textContent = "Status: Mining...";
      } catch (error) {
        console.error("Error starting mining:", error);
        statusDiv.textContent = "Status: Error Starting Mining";
      }
    });
  </script>
</body>
</html>
