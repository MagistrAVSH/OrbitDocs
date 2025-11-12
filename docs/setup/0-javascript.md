# JavaScript

#### 1. Install through "script tag"  

=== "HTML"
```HTML
<script src="https://storage.googleapis.com/social-networth/scripts/sdk.umd.js"></script>
```


#### 2. Initialize the SDK   
Call the initialization functions at the start of your application:

=== "JavaScript"
```JS
await window.PortalSDK.initialize();  
```

Initialize overlay with default options or with [startup configuration](/integration/startup-configuration/)

=== "JavaScript"
```JS
window.PortalSDK.initializeOverlay();
```


#### 3. Call game-ready event  
  Call this method when the game is ready and visible to the user.  
=== "JavaScript"  
```js
window.PortalSDK.gameReady()
```  
  
**Notes:**  
*Initialization should occur as early as possible in your application lifecycle to prevent delays.*
