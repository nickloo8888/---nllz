https://sdk.minepi.com/pi-sdk.js
<!DOCTYPE html>
<html>
<head>
  <title>Minepi Demo</title>
  <script src="https://sdk.minepi.com/pi-sdk.js"></script> 
</head>
<body>
  <button id="start-mining">Start Mining Pi</button>
  <script>
    // When the "Start Mining Pi" button is clicked:
    document.getElementById('start-mining').addEventListener('click', () => {
      Pi.startMining();
    });
  </script>
</body>
</html>
