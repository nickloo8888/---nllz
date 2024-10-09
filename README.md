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
document.addEventListener('DOMContentLoaded', () => { 
    const startMiningBtn = document.getElementById('start-mining');
    const statusMessage = document.getElementById('status-message');

    // ---- SDK INITIALIZATION ----
    // Let's pretend Minepi's SDK needs an API key and returns a promise on init: 
    Pi.init({ apiKey: 'YOUR_ACTUAL_API_KEY_FROM_MINEPI' })
        .then(() => { 
            console.log("Minepi SDK initialized successfully!"); 
            statusMessage.textContent = "SDK ready. Log in to start mining."
        })
        .catch(err => {
            console.error("Minepi SDK initialization error:", err);
            statusMessage.textContent = "Error loading Minepi. Please try again later."
        });

    // ---- MINING LOGIC ---- 
    startMiningBtn.addEventListener('click', async () => {
        startMiningBtn.disabled = true;
        statusMessage.textContent = "Attempting to start mining...";

        try {
            // ---- AUTHENTICATION ----
            // Assuming Minepi has a pop-up login:
            const isUserLoggedIn = await Pi.authenticateUser();  

            if (isUserLoggedIn) {
                // ---- START MINING ----
                // Imagining startMining returns an object with { success, error }
                const miningResult = await Pi.startMining();  
                if (miningResult.success) {
                    statusMessage.textContent = "Mining started successfully!";
                } else {
                    statusMessage.textContent = "Mining failed: " + miningResult.error;
                } 
            } else {
                statusMessage.textContent = "Please log in to your Pi account.";
            }

        } catch (error) {
            console.error('Error starting mining:', error);
            statusMessage.textContent = "An unexpected error occurred.";
        } finally {
            startMiningBtn.disabled = false; 
        }
    });
});
document.addEventListener('DOMContentLoaded', () => {
    const startMiningBtn = document.getElementById('start-mining');
    const statusMessage = document.getElementById('status-message');

    // SDK Initialization (Improved)
    async function initializeSDK() {
        try {
            await Pi.init({ apiKey: 'YOUR_ACTUAL_API_KEY_FROM_MINEPI' }); // Still a placeholder
            console.log("Minepi SDK initialized successfully!");
            statusMessage.textContent = "SDK ready. Log in to start mining.";
        } catch (err) {
            console.error("Minepi SDK initialization error:", err);
            statusMessage.textContent = "Error loading Minepi. Please try again later.";
        }
    }

    initializeSDK(); // Call initialization function

    startMiningBtn.addEventListener('click', async () => {
        startMiningBtn.disabled = true;
        statusMessage.textContent = "Attempting to start mining...";

        try {
            const isUserLoggedIn = await Pi.authenticateUser();

            if (!isUserLoggedIn) {
                statusMessage.textContent = "Please log in to your Pi account.";
                return;
            }
 const miningResult = await Pi.startMining();
            if (miningResult.success) {
                statusMessage.textContent = "Mining started successfully!";
                // Add periodic mining status updates if applicable:
                // setInterval(async () => {
                //     const status = await Pi.getMiningStatus();  // Hypothetical 
                //     statusMessage.textContent = `Mining: ${status.speed} Pi/hr, ${status.earned} Pi earned`; 
                // }, 5000); // Example update every 5 seconds
            } else {
               handleError(miningResult.error);   // Delegate error handling
            }
        } catch (error) {
           handleError(error);                // Delegate error handling
        } finally {
            startMiningBtn.disabled = false;
        }
    });
 function handleError(error) {       // Centralized Error Handling
        console.error("Mining or Authentication Error:", error);
        let userMessage = "An unexpected error occurred.";  // Generic
        if (error.code) {                    // Hypothetical codes - from SDK docs
            if (error.code === "INSUFFICIENT_BALANCE") {    
                userMessage = "Not enough Pi for mining."
            } else if (error.code === "NETWORK_ERROR") {
                userMessage = "Network error. Check your connection."
            } else if (error.code === "AUTH_FAILED") {         
                userMessage = "Login failed. Check your credentials.";
            } else {                      // Default case 
                userMessage = "Error " + error.code + ": " + (error.message || "Unknown"); 
            }
        }

        statusMessage.textContent = userMessage; // Set message in UI
        if(error.detailedMessage) {            // Display detailed messages to the developer console
            console.error(error.detailedMessage);  // Only if present and relevant for debugging
        }    
    }


});
if (error.code === "INSUFFICIENT_BALANCE") {
    userMessage = `Not enough Pi for mining. Required: ${error.requiredBalance}, You have: ${error.currentBalance}`; 
}
// ... other error cases ...
class AuthenticationError extends Error { 
    constructor(message, reason) {
        super(message);
        this.name = "AuthenticationError";
        this.reason = reason; // e.g., "INVALID_CREDENTIALS", "NETWORK_ERROR"
    }
}

// Then in authentication:
if (!isUserLoggedIn) {
    const authError = new AuthenticationError("Login failed", "INVALID_CREDENTIALS"); // Pass a reason
    handleError(authError); // The type of error can now be understood later via error.name and detailed info if present as properties such as error.reason
    return;
}
async function retryStartMining(retries = 3, delay = 1000) { // Example 3 retries 
    try {
        const miningResult = await Pi.startMining();
        // ... success handling 
    } catch (error) {
        if (error.code === "NETWORK_ERROR" && retries > 0) {
            console.warn("Network error, retrying...", retries);
            setTimeout(() => retryStartMining(retries - 1, delay * 2), delay); // Increase delay 
        } else {
            handleError(error);
        }
    }
} 
// In the mining section, call  retryStartMining();  
