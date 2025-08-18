# Startup configuration 

If you think that updating the game's interface is not rational in terms of time costs, you can disable full-screen mode in `startupConfig`.
You can also set the initial position of the overlay on the screen in it.
`startupConfig` can be modified either through the `index.html` file

**Important notice:** because the overlay position saves the position for the user, you maybe will not see the result of changing of initial overlay position.
You need to reset `localStorage` for that. Please refer to [how to enable dev tools in Telegram](/integration/tg-devtools/)

=== "Unity"

	```C#
	window.startupConfig = {
	 isFullscreen: false,
	 overlayPosition: "bottomRight"
	 // "topLeft" | "topRight" | "bottomLeft" |"bottomRight"
	}; 
	```

=== "Defold"

	```LUA
	window.startupConfig = {
	 isFullscreen: false,
	 overlayPosition: "bottomRight"
	 // "topLeft" | "topRight" | "bottomLeft" |"bottomRight"
	}; 
	```

#### JavaScript SDK

For changing overlay position when you use directly JavaScript SDK directly, you need to pass an argument to `PortalSDK.initializeOverlay` during [the initialization code of SDK](/setup/0-javascript/#3-initialize-the-sdk)

=== "JavaScript"

	```JS
	PortalSDK.initializeOverlay({
	    initialPosition: "bottomRight"
	    // "topLeft" | "topRight" | "bottomLeft" |"bottomRight"
	})

	```

To make the app fullscreen, you need to call `TelegramWebApp.requestFullscreen()` only for mobile devices, because otherwise you will force desktop users to use fullscreen.
Need to call this code as early as possible. Even before SDK initizalization.

=== "JavaScript"

	```JS
	// NOTE: `isMobile` function is an EXAMPLE. 
	// If you have one, already use your function.
	function isMobile() {
	  return (
	    ('ontouchstart' in window || navigator.maxTouchPoints > 0) &&
	    /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(
	      navigator.userAgent
	    )
	  );
	}

	if (isMobile()) {
	  
	  if(window.TelegramWebviewProxy){
      	window.TelegramWebviewProxy.postEvent('web_app_request_fullscreen', 
      	   JSON.stringify({}));
	  }

	}

	```

**Expected results**

![Disabled full screen](images/startup-configuration/3.png)

*Disabled fullscreen*

![Enabled fullscreeen](images/startup-configuration/2.jpg)

*Enabled fullscreen*


