# Unity Games

Getting Started
Prerequisites
To work with PortalSDK, you’ll need the following:

Unity Versions: Unity 2021 LTS, Unity 2022 LTS, or Unity 6 LTS (Unity 6 is preferable due to updated WebGL support).
Installed WebGL Platform: Ensure that the WebGL Platform module is installed in your Unity setup.
Unity WebGL Limitations
Unity’s WebGL platform offers a powerful way to run games on the web, but there are some limitations to keep in mind:

Performance Constraints: WebGL applications run within a browser and have different performance limits than desktop builds.
Memory Management: WebGL has specific memory constraints and handles memory differently, which can affect large games.
Networking: WebGL networking relies on the browser’s capabilities and may not support all network configurations.
Texture Compression: Only certain types of texture compression are supported, which can impact visual quality and loading times.

For more detailed information, check the links below.
Links to Unity Documentation on WebGL Performance and Limitations
For in-depth information about optimizing and working within Unity’s WebGL platform, refer to these resources:

WebGL Performance
WebGL Texture Compression
WebGL Embedded Resources
WebGL Networking
WebGL Memory Management
WebGL Audio


How to set up Unity Game with PortalSDK
Step 1: Set up the package from Git

      Unity documentation https://docs.unity3d.com/Manual/upm-ui-giturl.html


Open your Unity project.
Access the Package Manager in Unity, and select Add package from git URL...
Enter the repository URL: https://github.com/orbit-software/com.orbit.portalsdk.git

![Описание изображения](/assets/unity_games/1.png)

Step 1.1: Set up the package from a local folder (alternative way 1)

      Unity documentation https://docs.unity3d.com/Manual/upm-ui-local.html


1. Open repository https://github.com/orbit-software/com.orbit.portalsdk
2. Download repository as zip and unarchive

![Описание изображения](/assets/unity_games/2.png)

3. Move com.orbit.portalsdk directory into Assets/ directory of your Unity Project

![Описание изображения](/assets/unity_games/3.png)

Step 1.2: Set up the Unity Package directly into project (alternative way 2)
1. Open repository https://github.com/orbit-software/com.orbit.portalsdk
2. Download repository as zip and unarchive

![Описание изображения](/assets/unity_games/4.png)

3. Move com.orbit.portalsdk directory into Assets/ directory of your Unity Project

![Описание изображения](/assets/unity_games/5.png)

Step 2: Download the WebGL Template
1. Go to the repository unity-web-template and download the template files.
2. Extract the contents if they are compressed.

Step 3: Copy the WebGL Template into Your Project
1. In your Unity project directory, navigate to Assets/WebGLTemplates/.
2. If it doesn’t already exist, create a folder named PortalSDK.
3. Copy the downloaded PortalSDK WebGL template directory into this location.

![Описание изображения](/assets/unity_games/6.png)

Step 4: Set the WebGL Template in Player Settings
1. Go to Edit > Project Settings > Player in Unity.
2. Under the WebGL settings, find the WebGL Template selector.
3. Select PortalSDK from the selector to apply it as your template.

4. ![Описание изображения](/assets/unity_games/7.png)

Step 4.1 !!!! VERY IMPORTANT Setup game time tracking
If you are not using the Unity Web Template from SDK, you must add the code for tracking game time as shown here:
let timer

const trackTimeEveryS = 20 // 20 seconds

function startGameTimeTrack() {
   if (timer) clearInterval(timer)

   window.PortalSDK.trackGameTimeTick()

   timer = setInterval(() => {
       window.PortalSDK.trackGameTimeTick()
   }, trackTimeEveryS * 1000)
}


And call the code above at the moment of loading the Unity instance.
unity.createUnityInstance(canvas, config,
   (progress) => progressBarFull.style.width = 100 * progress + "%")
   .then((unityInstance) => {
      
       // ------------------
       startGameTimeTrack()
       // ------------------
      
       loadingBar.style.display = "none";
      
   })
};  - лишняя скобка


A game without a functional game time tracking system will not be approved by moderators.
Step 5: Set WebGL Publishing settings

Important settings:


Compression Format: Brotli
Name Files As Hashes: true
Target WebAssembly 2023: false
Use WebAssembly.Table: false
Enable BigInt: false

![Описание изображения](/assets/unity_games/8.png)

Step 6: Build and Run for Testing
1. Go to File > Build Settings in Unity.
2. Select WebGL as your platform and click Switch Platform.
3. Click Build and Run to test your setup.
