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


#### 4. Call game-ready event  
  Call this method when the game is ready and visible to the user.  
=== "JavaScript"  
```js
window.PortalSDK.gameReady()
```  
  
**Notes:**  
*Ensure you handle exceptions gracefully, especially when requesting ads.
Initialization should occur as early as possible in your application lifecycle to prevent delays.*
