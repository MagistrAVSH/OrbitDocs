# Persistent Game State Management
To maintain a persistent game state for each player, you can use the SDK API to write and read key-value pairs. The storage supports up to 5 MB per player.

The most convenient approach is to save and retrieve the game state serialized in JSON format.

The SDK provides three methods for data access. All operations are asynchronous due to their cloud nature. Still, we provide sync methods as the main because it may be difficult to adapt existing games with async methods, especially in the Unity environment

=== "Unity"

	```C#
	// Write
	PortalSDK.SetValue("string key", "string value");
	
    // Read
	string content = PortalSDK.GetValue("string key");
	
    // Remove
	PortalSDK.RemoveValue("string key");
	```

=== "Defold"

	```LUA
    -- Write
    portalsdk.set_value_sync("string key", "string value");
    
    -- Read
    local content = portalsdk.get_value_sync("string key");
    
    -- Remove
    portalsdk.remove_value("string key");
	```


=== "JavaScript"

	```JS
	// Write
	window.PortalSDK.setValue("string key", "string value");

	// Read
	const content = await window.PortalSDK.getValue("string key");

	// Remove
	window.PortalSDK.removeValue("string key");
	```