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
<!DOCTYPE html>
<html>
<head>
  <title>Minepi Demo</title>
  <script src="https://sdk.minepi.com/pi-sdk.js"></script> 
  <script>
    document.addEventListener('DOMContentLoaded', () => { 
      const startMiningBtn = document.getElementById('start-mining');
      const statusMessage = document.getElementById('status-message');

      // Initialize Pi SDK here (hypothetical, refer to Minepi documentation)
      // Example:  Pi.init({ apiKey: 'YOUR_API_KEY' })
      //            .then(() => {  // SDK is ready! })
      //            .catch(err => console.error('SDK initialization error:', err));

      startMiningBtn.addEventListener('click', async () => { 
        startMiningBtn.disabled = true;
        statusMessage.textContent = "Attempting to start mining...";

        try {
          // Authenticate the user first (replace with Minepi's method)
          // const isUserLoggedIn = await Pi.authenticateUser(); 
          // if (!isUserLoggedIn) {
          //   statusMessage.textContent = "Please log in to your Pi account."; 
          //   return;
          // }

          // Assume startMining is an async operation (could be different) 
          const miningResult = await Pi.startMining();  
          if (miningResult.success) {
            statusMessage.textContent = "Mining started successfully!";
          } else {
            statusMessage.textContent = "Mining failed to start. " + miningResult.error;
          }
        } catch (error) {
          console.error('Error starting mining:', error);
          statusMessage.textContent = "An error occurred. Please try again later.";
        } finally {
          startMiningBtn.disabled = false;
        }
      });
    });
  </script>
</head>
<body>
  <button id="start-mining">Start Mining Pi</button>
  <div id="status-message"></div>
</body>
</html>
