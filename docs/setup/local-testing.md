# Local Testing

This guide explains how to test your game locally with the PortalSDK before uploading it to the platform.

### Prerequisites

Before you begin, ensure you have:
- Built your game for WebGL/HTML5
- Access to the game in Telegram Portal
- Your game's `index.html` file ready to edit

### How to test your game locally

#### 1. Step: Get Authentication Data

First, you need to enable DevTools in Telegram. For detailed instructions, see [how to enable DevTools in Telegram](/integration/tg-devtools/).

1. Open the browser DevTools console
2. Paste the following command into the console:

```js
window.Telegram.WebApp.initData
```

3. Copy the output string. It will look like this:

```
user=%7B%22id%22%3A122374628%2C%22first_name%22%3A...
```

![Console output example](images/local-testing/first-image.png)

!!! warning "Important"
    The `botId` and `authData` must be from the same Telegram mini app. Do not mix authentication data from different apps.

#### 2. Step: Modify Your Index File

Locate your game's initialization code:

=== "Unity"

    For Unity projects, you need to edit the WebGL template `index.html` file. See the [Unity setup guide](/setup/unity/) for details on WebGL templates.

=== "Defold"

    For Defold projects, you need to edit the HTML5 template. See the [Defold setup guide](/setup/defold/) for details on HTML5 templates.

=== "JavaScript"

    For plain JavaScript projects, edit your `index.html` or wherever you initialize the game.

**Original Code**

Your initialization code currently looks like this:

```js
(async function () {
  await window.PortalSDK.initialize();
  window.PortalSDK.initializeOverlay();
})();
```

**Modified Code for Local Testing**

Change it to include the `botId` and `authData`:

```js
(async function () {
  await window.PortalSDK.initialize(
    8433755170,
    {
      authData: 'user=%7B%22id%22%3A122374628%2C%22first_n...'
    }
  );
  window.PortalSDK.initializeOverlay();
})();
```

Replace:
- `8433755170` with your actual bot ID (see [How to find your game bot ID](/integration/telegram-botid/))
- `'user=%7B%22id%22%3A122374628%2C%22first_n...'` with your actual `authData` string from Step 1

#### 3. Step: Build and Run

=== "Unity"

    1. In Unity, go to **File > Build Settings**
    2. Click **Build and Run**
    3. Your game will open in the browser with the overlay, ads, IAPs, and all other PortalSDK features working

    ![Game running with Portal overlay](images/local-testing/second-image.png)

=== "Defold"

    1. Go to **Project > Build**
    2. Select **HTML5** as the platform
    3. Build and run your project
    4. Open the built `index.html` in your browser

=== "JavaScript"

    Launch your game using your preferred method (local server, file opening, etc.)

You should now see your game running locally with the Portal overlay, ads, IAPs, and all other SDK features working.

#### 4. Step: Restore Original Code Before Upload

!!! danger "Critical - Do Not Skip This Step"
    Before uploading your game to GitHub, you **must** restore the original initialization code.

Change the code back to:

```js
(async function () {
  await window.PortalSDK.initialize();
  window.PortalSDK.initializeOverlay();
})();
```

Remove the `botId` and `authData` parameters. If you forget this step, your game may not work correctly in production.

### Troubleshooting

If local testing isn't working:

1. **Verify authentication data**: Make sure the `authData` string is copied completely
2. **Check bot ID**: Ensure the bot ID matches the mini app you got the auth data from
3. **Clear browser cache**: Old cached data can sometimes interfere
4. **Check console errors**: Open browser DevTools and look for error messages
5. **Verify SDK version**: Make sure you're using the latest PortalSDK version
