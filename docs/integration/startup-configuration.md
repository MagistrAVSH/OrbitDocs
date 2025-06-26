# Startup configuration 
If you think that updating the game's interface is not rational in terms of time costs, you can disable full-screen mode in `startupConfig`.
You can also set the initial position of the overlay on the screen in it.
`startupConfig` can be modified either through the `index.html` file

=== "JavaScript"
```JS
window.startupConfig = {
 isFullscreen: false,
 overlayPosition: "bottomRight"
 // "topLeft" | "topRight" | "bottomLeft" |"bottomRight"
}; 
```
![Disabled full screen](images/startup-configuration/3.png)