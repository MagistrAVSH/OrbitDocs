# Game & IAP Managment
## Admin dashboard

**_Note: The admin dashboard is in the pre-release stage and subject to change.
How to get access_**

1. Send command /admin to the Telegram bot  @cs_games_platform_bot
![Описание изображения](images/game-and-iap/1.png)  
  2. You will get a link to the admin dashboard where you can administrate your games

How to add, edit, or remove items in-game shop

1. Select one of your games and click the store icon
![Описание изображения](images/game-and-iap/2.png)  
  2. Now you can have access to change items, their description, and price in Telegram stars
![Описание изображения](images/game-and-iap/3.png)  
  
Change game configuration  
  1. Change supported devices and supported screen formats

![Описание изображения](images/game-and-iap/4.png)  
  2. Game name, Game description, Colors, Logo,
![Описание изображения](images/game-and-iap/5.png)  
## How to use Shop API

After you create your items, you can integrate them into your game.
Here is an example for Unity, and an example for JavaScript games is coming soon.  

1.First of all, you need to get all your items:
=== "Unity"
	```C#
	var items = await PortalSDK.GetShopItems();
	```
=== "JS"
	```js
 	const response = await PortalSDK.getShopItems();
	```
=== "Defold"
	```lua
    portalsdk.get_shop_items(function(self, data)
    print("GetShopItems: " .. table_to_string(data))
    end)
	```
ShopItem has the same fields as in the admin, and the most important is the id
=== "Unity"
    ```C#
    public class ShopItem
    {
        /// <summary>
        /// The unique identifier of the shop item.
        /// </summary>
        public int id;

        /// <summary>
        /// The name of the shop item.
        /// </summary>
        public string name;

        /// <summary>
        /// The description of the shop item.
        /// </summary>
        public string description;

        /// <summary>
        /// The price of the shop item.
        /// </summary>
        public int price;

        /// <summary>
        /// The date and time when the shop item was created.
        /// </summary>
        public DateTime created;

        /// <summary>
        /// The date and time when the shop item was last updated.
        /// </summary>
        public DateTime updated;
    }
    ```
=== "JS"
    ```JS
    interface CryptoSteamSDKShopItem {
        id: number;
        name: string;
        description: string;
        price: number;
        created: string;
        updated: string;
    }
    ```
=== "Defold"
	```lua
	local shopItem = {
	    id = 1,
	    name = "Sample Item",
	    description = "This is a sample shop item.",
	    price = 100,
	    created = "2025-06-12T10:00:00Z",
	    updated = "2025-06-12T12:00:00Z"
	}
	```
2.The second important API method is:
=== "Unity"
    ```C#
    var purchased = await PortalSDK.GetPurchasedShopItems();
    ```  
=== "JS"
    ```JS
    getPurchasedShopItems: () => Promise<CryptoSteamSDKShopItem[]>;
    ```
=== "Defold"
	```LUA
    portalsdk.get_purchased_shop_items(function(self, data)
    print("GetPurchasedShopItems: " .. table_to_string(data))
    end)
	```
It gives you all the purchased items by the current player.   
  Now you can display your shop screen and associate your items with ShopItems from the API and mark purchased it 
If your item can be purchased infinitely, you can just not mark it. SDK API does not limit you in the number of purchased items per player.   

3.Make a code to buy an item by id
=== "Unity"
	```C#
	var result = await PortalSDK.OpenPurchaseConfirmModal(itemId);
	if (result is { IsSuccessful: true })
	```
=== "JS"
	```JS
	const result = await PortalSDK.OpenPurchaseConfirmModal(itemId);
	if (result && result.IsSuccessful === true) {

	}
	```
=== "Defold"
	```lua
    portalsdk.open_purchase_confirm_modal(itemId, function(self, data)
    if data and data.IsSuccessful then
        print("Purchase successful!")
    else
        print("Purchase failed.")
    end
    end)
	```
After player will see modal window:  
  ![Описание изображения](images/game-and-iap/6.png)  
  If a user doesn't have enough balance, a top-up popup will be shown  
  ![Описание изображения](images/game-and-iap/7.png)  
  If the player confirms a purchase, after all, you will get the response IsSuccessful = true
