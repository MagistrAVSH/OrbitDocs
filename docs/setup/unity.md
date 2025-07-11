# Unity Engine

### **Prerequisites**  
  To work with PortalSDK, you’ll need the following:

**Unity Versions:** Unity 2022 LTS, or Unity 6 LTS (Unity 6 is preferable due to updated WebGL support).  
**Installed WebGL Platform:** Ensure that the WebGL Platform module is installed in your Unity setup.

### Unity WebGL Limitations
Unity’s WebGL platform offers a powerful way to run games on the web, but there are some limitations to keep in mind:

- **Performance Constraints:** WebGL applications run within a browser and have different performance limits than desktop builds.
- **Memory Management:** WebGL has specific memory constraints and handles memory differently, which can affect large games.
- **Networking:** WebGL networking relies on the browser’s capabilities and may not support all network configurations.
- **Texture Compression:** Only certain types of texture compression are supported, which can impact visual quality and loading times.

For more detailed information, check the links below.
### Links to Unity Documentation on WebGL Performance and Limitations
For in-depth information about optimizing and working within Unity’s WebGL platform, refer to these resources:

- [WebGL Performance](https://docs.unity3d.com/Manual/webgl-performance.html)
- [WebGL Texture Compression](https://docs.unity3d.com/Manual/webgl-texture-compression.html)
- [WebGL Embedded Resources](https://docs.unity3d.com/Manual/webgl-embeddedresources.html)
- [WebGL Networking](https://docs.unity3d.com/Manual/webgl-networking.html)
- [WebGL Memory Management](https://docs.unity3d.com/Manual/webgl-memory.html)
- [WebGL Audio](https://docs.unity3d.com/Manual/webgl-audio.html)


### How to set up Unity Game with PortalSDK
#### 1. Set up the package from Git

[Unity documentation](https://docs.unity3d.com/Manual/upm-ui-giturl.html)

1. Open your Unity project.
2. Access the Package Manager in Unity, and select Add package from git URL...
3. Enter the repository URL [https://github.com/orbit-software/com.orbit.portalsdk.git](https://github.com/orbit-software/com.orbit.portalsdk.git)

![img](images/unity-games/1.png)

#### 1.1. Set up the package from a local folder (alternative way 1)

[Unity documentation](https://docs.unity3d.com/Manual/upm-ui-local.html)
    
1. Open repository [https://github.com/orbit-software/com.orbit.portalsdk](https://github.com/orbit-software/com.orbit.portalsdk)
2. Download repository as zip and unarchive

![img](images/unity-games/2.png)  

Move `com.orbit.portalsdk` directory into `Assets/` directory of your Unity Project

![img](images/unity-games/3.png)  
#### 1.2. Step: Set up the Unity Package directly into project (alternative way 2)
1. Open repository [https://github.com/orbit-software/com.orbit.portalsdk](https://github.com/orbit-software/com.orbit.portalsdk)  
2. Download repository as zip and unarchive

![img](images/unity-games/4.png)  

Move `com.orbit.portalsdk` directory into `Assets/` directory of your Unity Project

![img](images/unity-games/5.png)  

#### 2. Step: Download the WebGL Template  
  - Go to the repository unity-web-template and download the template files.  
  - Extract the contents if they are compressed.

#### 3. Step: Copy the WebGL Template into Your Project    
- In your Unity project directory, navigate to `Assets/WebGLTemplates/`.  
- If it doesn’t already exist, create a folder named `PortalSDK`.  
- Copy the downloaded PortalSDK WebGL template directory into this location.

![img](images/unity-games/6.png)  

#### 4. Set the WebGL Template in Player Settings  
  - Go to Edit > Project Settings > Player in Unity.  
  - Under the WebGL settings, find the WebGL Template selector.  
  - Select *PortalSDK* from the selector to apply it as your template.

![img](images/unity-games/7.png)  
 
### ***5. Step: Set WebGL Publishing settings***

**Important settings:**

  - Compression Format: `Brotli`  
  - Name Files As Hashes: `true`  
  - Target WebAssembly 2023: `false`  
  - Use WebAssembly.Table: `false`  
  - Enable BigInt: `false`

![img](images/unity-games/8.png)  
### 6. ***Step: Build and Run for Testing***  
  - Go to File > Build Settings in Unity.  
  - Select WebGL as your platform and click Switch Platform.  
  - Click Build and Run to test your setup.  

