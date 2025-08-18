# JavaScript


#### 1. Install the SDK Run the following command to [install the SDK](https://www.npmjs.com/package/@orbit-software/sdk) via npm:

=== "Bash"
```bash
npm i @orbit-software/sdk
```


#### 2. (Alternate) Install through "script tag"  

=== "HTML"
```HTML
<script src="https://storage.googleapis.com/social-networth/scripts/sdk.umd.js"></script>
```


#### 3. Initialize the SDK   
Call the initialization functions at the start of your application:

=== "JavaScript"
```JS
await PortalSDK.initialize();  
```

Initialize overlay with default options or with [startup configuration](/integration/startup-configuration/)

=== "JavaScript"
```JS
PortalSDK.initializeOverlay();
```




#### 4. Launch an Advertisement *(Optional)*:  
If you need to launch an ad at the start, check if ads are enabled and then request one:  

=== "JavaScript"
```JS
if (await PortalSDK.isAdEnabled()) {
    try {
        await PortalSDK.requestAd();
    } catch (ex) {
        console.error(ex);
    }
}
```

#### 5. Setup game time tracking  
You must add the code for tracking game time as shown here:

=== "JavaScript"
```JS

let timer;
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
=== "JavaScript"
```js
startGameTimeTrack()
```

#### 6. Call game-ready event  
  Call this method when the game is ready and visible to the user.  
=== "JavaScript"  
```js
window.PortalSDK.gameReady()
```  
  
**Notes:**  
*Ensure you handle exceptions gracefully, especially when requesting ads.
Initialization should occur as early as possible in your application lifecycle to prevent delays.*
