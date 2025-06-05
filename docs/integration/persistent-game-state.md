# Persistent Game State Management
To maintain a persistent game state for each player, you can use the SDK API to write and read key-value pairs. The storage supports up to 5 MB per player.

The most convenient approach is to save and retrieve the game state serialized in JSON format.

The SDK provides three methods for data access. All operations are asynchronous due to their cloud nature. Still, we provide sync methods as the main because it may be difficult to adapt existing games with async methods, especially in the Unity environment
```C#
// Write
PortalSDK.SetValue("string key", "string value");

// Read
string content = PortalSDK.GetValue("string key");

// Remove
PortalSDK.RemoveValue("string key");


//
// Async versions:
//

// Write
string content = await PortalSDK.GetValueAsync("string key");

// Read
await PortalSDK.SetValueAsync("string key", "string value");
```



=== "LUA"
			```lua
			    -- Cloud Saves
			    --
			    print("Test: GetValueSync() before set")
			    local result = portalsdk.get_value_sync("key")
			    print("GetValueSync: " .. result);
			
			    print("Test: SetValueSync()")
			    portalsdk.set_value_sync("key", "test-value 42")
			
			    print("Test: GetValueSync()")
			    local result = portalsdk.get_value_sync("key")
			    print("GetValueSync: " .. result);
			
			    print("Test: RemoveValue()")
			    portalsdk.remove_value("key")
			
			    print("Test: GetValueSync() after remove")
			    local result = portalsdk.get_value_sync("key")
			    print("GetValueSync: " .. result);
			```


=== "TS"
			```ts
			export interface CryptoSteamSDK {
				version: string;
				initialize: () => Promise<void>;
				getConfig: () => Promise<CryptoSteamSDKConfig>;
				isAdEnabled: () => Promise<boolean>;
				requestAd: (options?: RequestAdOptions) => Promise<true>;
				requestRewardAd: (options?: RequestAdOptions) => Promise<boolean>;
				getProfile: () => Promise<CryptoSteamSDKProfile>;
				getBalance: () => Promise<number>;
				trackGameTimeTick: () => void;
				getVersion: () => string;
				initializeOverlay: (config?: OverlayConfig) => void;
				getShopItems: () => Promise<CryptoSteamSDKShopItem[]>;
				getPurchasedShopItem: (itemId: number) => Promise<CryptoSteamSDKShopItem>;
				getPurchasedShopItems: () => Promise<CryptoSteamSDKShopItem[]>;
				buyShopItem: (itemId: number) => Promise<void>;
				openPurchaseConfirmModal: (
					shopItem: CryptoSteamSDKShopItem,
					rect?: {
						x: number;
						y: number;
						width: number;
						height: number;
					},
				) => Promise<PurchaseConfirmResponse>;
				createInvoice: (
					title: string,
					description: string,
					to_user_id: number,
					amount: number,
				) => Promise<InvoiceResponse>;
				getTasks: () => Promise<CryptoSteamSDKTask[]>;
				claimTask: (taskId: number) => Promise<void>;
				getValue: (key: string) => Promise<string>;
				setValue: (key: string, value: string) => Promise<void>;
				/**
				 * @deprecated
				 * @param key
				 */
				getData: (key: string) => Promise<string>;
				/**
				 * @deprecated
				 * @param key
				 * @param value
				 */
				setData: (key: string, value: string) => Promise<void>;
				removeValue: (key: string) => Promise<void>;
				getAllKeyValues: () => Promise<Record<string, string>>;
				getLocale: () => string;
				showSharing: (url: string, text?: string) => void;
				telegramCloudStorage: TelegramCloudStorage;

				gameReady: () => void;
			}
			```