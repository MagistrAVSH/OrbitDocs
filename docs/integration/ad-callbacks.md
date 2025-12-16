# **Ad Lifecycle Callbacks**

The SDK provides two callback properties for tracking the advertisement lifecycle:

* `onAdStart` — Called when the advertisement begins showing.  
* `onAdEnd` — Called when the advertisement has finished.

### **onAdStart**

* The callback is called before the ad display begins.  
* **Signature:** `PortalSDK.onAdStart = () => void`
* **Parameters:** None.  
* **Usage Example:**
=== "JavaScript"
    ```js
    PortalSDK.onAdStart = function() {  
        console.log('Ad started');  
        pauseGame();  
        muteSound();
    };
    ```

### **onAdEnd**

* The callback is called after the ad finishes (whether successful or not).  
* **Signature:** `PortalSDK.onAdEnd = (result: boolean) => void`
* **Parameters:**  
  * result (boolean) — true if the ad was shown successfully, false if the ad was not shown (e.g., `error`, `cooldown`, `ads_free`, etc.).  
* **Usage Example:**
=== "JavaScript"
    ```js
    PortalSDK.onAdEnd = function(success) {  
        console.log('Ad ended, success:', success);  
        resumeGame();  
        unmuteSound();
        if (success) {  
            giveRewardToPlayer();  
        }  
    };
    ```

### **Disabling Callbacks**

To disable a callback, set its value to null:

=== "JavaScript"
    ```js
    PortalSDK.onAdStart = null;  
    PortalSDK.onAdEnd = null;
    ```

### **Notes**

* Callbacks are triggered for both methods: `requestAd()` and `requestRewardAd()`.  
* `onAdEnd` is called in all completion scenarios (`success`, `error`, `cooldown`, `ads_free`).  
* Callbacks are synchronous — they do not block the execution of the ad display logic.  
* By default, both properties are set to null.