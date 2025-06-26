# Advertisement setup
SDK suggests for now several ways for ad integration into your apps:

### Interstitial ads
Interstitial ads are used to display video ads and should be triggered on natural breaks in your game.

=== "Unity"

	```C#
    // gameplay stops
    await PortalSDK.RequestAd();
	```

=== "Defold"

	```LUA
    -- gameplay stops
    portalsdk.request_ad(function(self, success) end)
	```


=== "JavaScript"

	```JS
    // gameplay stops
    await window.PortalSDK.requestAd()
	```
### Rewarded ads

Rewarded ads allow for a user to choose to watch a rewarded video ad in exchange for a certain benefit in the game (e.g. more coins, etc.). 
When using  🎬 `requestRewardAd()` , please make it clear to the player beforehand that they’re about to watch an ad.

=== "Unity"

	```C#
    // gameplay stops
    var success = await PortalSDK.RequestRewardAd();
    if(success) {
        // give a reward to a user
    }
	```

=== "Defold"

	```LUA
    -- gameplay stops
    portalsdk.request_reward_ad(function(self, success)
        if succcess then
            -- give a reward to a user
        end
    end)
	```


=== "JavaScript"

	```JS
    // gameplay stops
    const success = await window.PortalSDK.requestRewardAd()
    if(success) {
        // give a reward to a user
    }
	```



### Disable sound and input during ads

Make sure that audio and keyboard input are disabled during ads, so that the game doesn’t interfere with the ad:


=== "Unity"

	```C#
    // gameplay stops
    // fire your mute audio function
    var success = await PortalSDK.RequestAd();
    // fire your unmute audio function
    // fire your function to continue to game
	```

=== "Defold"

	```LUA
    -- gameplay stops
    -- fire your mute audio function
    portalsdk.request_ad(function(self, success)
        -- fire your unmute audio function
        -- fire your function to continue to game
    end)
	```


=== "JavaScript"

	```JS
    // gameplay stops
    // fire your mute audio function
    await window.PortalSDK.requestAd()
    // fire your unmute audio function
    // fire your function to continue to game

	```