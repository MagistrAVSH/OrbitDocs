# Requirements

## Unity Games
1. **Mobile (touch) controls**
2. **Build Size**
    - **Main build:** Up to **50 MB** maximum for the main WebGL build + larger assets hosted.
    - Up to **500 MB** full game size. 
3. Networking
    - All network code must use WebSockets transport.
4. Unity Version
    - **Unity** 6+ is strongly recommended, due to improved WebGL features and optimizations.
5. Performance
    - Target stable frame rates (ideally 30-60 FPS) on mid-range mobile devices.
    - Game load time must be as low as possible, but the maximum is 20 seconds.

## JavaScript and Defold Games
1. **Mobile (touch) controls**
2. **Bundle Size**
   - Up to **10 MB** for all initial JavaScript, CSS, and other essential assets.
   - Up to **200 MB** full game size
3. **Performance**
   - Aim for at least 30-60 FPS on mobile devices.
   - Game load time must be as low as possible, but the maximum is 20 seconds.