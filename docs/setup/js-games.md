# JS Games

## Getting Started
**Quick start**  
1. **Install the SDK Run the following command to [install the SDK](https://www.npmjs.com/package/@orbit-software/sdk) via npm:**  <blockquote>npm i @orbit-software/sdk </blockquote>
2. **(Alternate) Install through "script tag"**  
      ```<script src="https://storage.googleapis.com/social-networth/scripts/sdk.umd.js"></script>```  
3. **Initialize the SDK**   
  Call the initialization functions at the start of your application:  
```await PortalSDK.initialize();```  
```PortalSDK.initializeOverlay();```  
4. **Launch an Advertisement (Optional):**  
   If you need to launch an ad at the start, check if ads are enabled and then request one:  
```
if (await PortalSDK.isAdEnabled()) {
    try {
        await PortalSDK.requestAd();
    } catch (ex) {
        console.error(ex);
    }
}
```
5. **Setup game time tracking**  
  You must add the code for tracking game time as shown here:  
  let timer
```
const trackTimeEveryS = 20 // 20 seconds

function startGameTimeTrack() {
   if (timer) clearInterval(timer)

   window.PortalSDK.trackGameTimeTick()

   timer = setInterval(() => {
       window.PortalSDK.trackGameTimeTick()
   }, trackTimeEveryS * 1000)
}
```
And call the code above at the moment of loading the game instance.  
```startGameTimeTrack()```  
6. **Call game-ready event**  
  Call this method when the game is ready and visible to the user.  
  ```window.PortalSDK.gameReady()  ```  
  
  _Notes:_  
  *Ensure you handle exceptions gracefully, especially when requesting ads.
Initialization should occur as early as possible in your application lifecycle to prevent delays.*
