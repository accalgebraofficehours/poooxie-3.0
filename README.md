<!DOCTYPE html>
<html lang="en">
   <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Run In Google Sites Pls you dipshit</title>
   </head>
   <body>
      Loading...
      <script>
         // Configuration
         const CONFIG = {
           sourceUrl: 'https://raw.githubusercontent.com/accalgebraofficehours/accalgebraofficehours.github.io/main/poodle_test/panel.html',
           loadingTimeout: 600000 // 60 seconds
         };
         
         async function loadGSRP() {
           const container = document.getElementById('gsrp-container');
         
           try {
             const controller = new AbortController();
             const timeoutId = setTimeout(() => controller.abort(), CONFIG.loadingTimeout);
         
             const response = await fetch(CONFIG.sourceUrl, {
               signal: controller.signal
             });
         
             clearTimeout(timeoutId);
         
             if (!response.ok) {
               throw new Error(`HTTP ${response.status}: ${response.statusText}`);
             }
         
             let html = await response.text();
         
             // Replace the entire document
             document.open();
             document.write(html);
             document.close();
         
           } catch (error) {
             console.error('Failed to load GSRP:', error);
         
             let errorMessage = 'Failed to load GSRP.';
             if (error.name === 'AbortError') {
               errorMessage = 'Loading timed out. Please try again.';
             } else if (error.message.includes('HTTP')) {
               errorMessage = `Server error: ${error.message}`;
             } else if (error.message.includes('fetch')) {
               errorMessage = 'Network error. Please check your connection.';
             }
         
             container.innerHTML = `
               <div class="error-message">${errorMessage}</div>
               <button onclick="location.reload()">Retry</button>
             `;
           }
         }
         
         if (document.readyState === 'loading') {
           document.addEventListener('DOMContentLoaded', loadGSRP);
         } else {
           loadGSRP();
         }
      </script>
      <!-- Required placeholder for errors -->
      <div id="gsrp-container"></div>
   </body>
</html>
