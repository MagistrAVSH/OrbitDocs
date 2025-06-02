# Requirments
Unity Games
Mobile (touch) controls
Build Size
Main build: Up to 50 MB maximum for the main WebGL build + larger assets hosted.
Up to 500 MB full game size. 
Networking
All network code must use WebSockets transport.
Often this means game studios must rewrite their code significantly
Unity Version
Unity 6+ is strongly recommended, due to improved WebGL features and optimizations.
Performance
Target stable frame rates (ideally 30-60 FPS) on mid-range mobile devices.
Game load time must be as low as possible, but the maximum is 20 seconds.
JavaScript Games
Mobile (touch) controls
Bundle Size
Up to 10 MB for all initial JavaScript, CSS, and other essential assets.
Up to 200 MB full game size
Performance 
Aim for at least 30-60 FPS on mobile devices.
Game load time must be as low as possible, but the maximum is 20 seconds.

Safe Area
A Safe Area in mobile design refers to the portion of the screen where essential UI elements should be placed to ensure they are not obscured by notches, rounded corners, or system navigation bars. 
Telegram has mostly the same safe area that we can see in native mobile apps and simulators. For example, Unity Editor has an embedded Simulator:

![Описание изображения](assets/requirments/1.png)

![Описание изображения](assets/requirments/2.png)

UI in games needs to be updated according to these references
Startup configuration
However, if you think that updating the game's interface is not rational in terms of time costs, you can disable full-screen mode in startupConfig.
You can also set the initial position of the overlay on the screen in it.
startupConfig can be modified either through the index.html file of the unity-web-template or js-web-template
...
window.startupConfig = {
 isFullscreen: false,
 overlayPosition: bottomRight' // "topLeft" | "topRight" | "bottomLeft" |"bottomRight"
}
...

![Описание изображения](assets/requirments/3.png)