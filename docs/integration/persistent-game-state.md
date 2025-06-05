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

```
import WebApp from "@twa-dev/sdk";
import { promisify } from "es6-promisify";
import { version } from "../package.json";
import { createOverlay } from "./Overlay";
import i18n from "./i18n";

import { delay } from "es-toolkit";
import ReactGA from "react-ga4";
import { checkAdStatus, showAd } from "./lib/tma-network";
import { getGlobalObj } from "./utils/global";

const CloudStorageGetItem = promisify(WebApp.CloudStorage.getItem);
const CloudStorageSetItem = promisify(WebApp.CloudStorage.setItem);
const CloudStorageRemoveItem = promisify(WebApp.CloudStorage.removeItem);

export const BASE_URL =
	"https://crypto-steam-backend-461697090571.europe-west3.run.app/sdk";

const G_MEASUREMENT_ID = "G-4RMXVE2K75";

async function makeRequest<T>(
	path: string,
	method: "POST" | "GET" | "PUT" | "DELETE",
	body?: any,
): Promise<T> {
	const url = `${BASE_URL}/${path}`;

	try {
		const response = await fetch(url, {
			method,
			headers: {
				"X-Auth": TelegramWebApp.initData,
				"Content-Type": "application/json",
			},
			body: body ? JSON.stringify(body) : null,
		});

		if (!response.ok) {
			throw new Error(
				`Request to ${path} failed with status ${response.status}`,
			);
		}

		return response.json();
	} catch (error) {
		console.error(`Error during request to ${path}:`, error);
		throw error;
	}
}

export interface CryptoSteamSDKConfig {
	supported_screen_formats: ("landscape" | "portrait" | "fullscreen")[];
	supported_devices: string[];
}

export interface CryptoSteamSDKProfile {
	id: number;
	is_admin?: boolean;
	experience: number;
	level_up_exp: number;
	level: number;
	user_name: string;
	first_name: string;
	last_name: string;
	avatar?: string;
	balance: number;
	ads_free: boolean;

	game_id?: string | number;
	games_count: number;
	invited: number;

	email?: string;
	phone_number?: string;
	location?: string;
	birth_date?: string;
	avatar_ug?: string;
	background_color?: string;
}

export interface CryptoSteamSDKShopItem {
	id: number;
	name: string;
	description: string;
	price: number;
	created: string;
	updated: string;
}

export enum CryptoSteamSDKAdMediaType {
	Image = "image",
	Gif = "gif",
	Video = "video",
}

export interface CryptoSteamSDKAd {
	is_available: boolean;
	url?: string;
	mediaType?: CryptoSteamSDKAdMediaType;
	durationS?: number;
}

export interface OverlayConfig {
	onOverlayOpen?: () => void;
	onOverlayClose?: () => void;
	variant?: "light" | "dark" | "translucent";
	initialPosition?: "topLeft" | "topRight" | "bottomLeft" | "bottomRight";
}

interface CreateInvoiceRequest {
	title: string;
	description: string;
	to_user_id: number;
	amount: number;
}

interface InvoiceResponse {
	invoice_link: string;
}

export interface CryptoSteamSDKTask {
	id: number;
	title: string;
	description: string;
	reward: number;
	group?: string;
	group_position?: number;
	sub_title?: string;
	is_claimable: boolean;
	is_done: boolean;
}

interface PurchaseConfirmResponse {
	status: "success" | "error";
}

interface TelegramCloudStorage {
	getValue: (key: string) => Promise<string>;
	setValue: (key: string, value: string) => Promise<boolean>;
	removeValue: (key: string) => Promise<boolean>;
}

interface TMANetworkInterstitialResponse {
	id: string;
	reward: boolean;
}

export type AdType = "REWARD" | "INTERSTITIAL";

export interface RequestAdOptions {
	onStart?: () => void;
}

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

declare global {
	interface Window {
		TMANetwork: {
			init: (apiKey: string) => void;
			reloadAd: () => void;
			addEventListener: (event: string, callback: () => void) => void;
			hasInterstitialAd: () => boolean;
			showInterstitialAd: () => Promise<TMANetworkInterstitialResponse>;
		};
	}
}

declare global {
	namespace NodeJS {
		interface ProcessEnv {
			NODE_ENV: "development" | "production";
			version: string;
		}
	}
}

interface ConfirmMessage {
	type: "confirm" | "cancel" | "error";
	message?: string;
}

const CryptoSteamSDK: CryptoSteamSDK = {
	version: process.env.version,
	initialize: async () => {
		try {
			console.log("FOOTBAR", process.env.version);
			console.log("Starting SDK and TMANetwork initialization...");

			const launchResponse = (await makeRequest("launch", "POST")) as {
				tma_ads_key: string;
			};

			await new Promise<void>((resolve) => {
				if (document.readyState === "complete") {
					resolve();
				} else {
					window.addEventListener("load", () => resolve());
				}
			});

			await new Promise<void>((resolve, reject) => {
				if (
					document.querySelector(
						'script[src="https://files.tmanetwork.tech/tmanetwork.min.js"]',
					)
				) {
					console.log("TMANetwork script already loaded.");
					resolve();
					return;
				}

				const script = document.createElement("script");
				script.src = "https://files.tmanetwork.tech/tmanetwork.min.js";
				script.async = true;

				script.onload = () => {
					console.log("TMANetwork script loaded successfully.");
					resolve();
				};

				script.onerror = (error) => {
					console.error("Failed to load TMANetwork script:", error);
					reject(new Error("Failed to load TMANetwork script"));
				};

				document.head.appendChild(script);
			});

			if (window.TMANetwork) {
				await window.TMANetwork.init(launchResponse.tma_ads_key);
				console.log("TMANetwork initialized successfully.");
			} else {
				throw new Error("TMANetwork object not found.");
			}

			console.log("TMANetwork fully initialized.");
		} catch (error) {
			console.error("Error during TMANetwork initialization:", error);
		}

		try {
			const profile = await CryptoSteamSDK.getProfile();

			if (!profile) {
				console.error("Profile not found");
				return;
			}

			ReactGA.initialize(G_MEASUREMENT_ID, {
				gaOptions: {
					userId: profile.id,
					gameId: profile.game_id,
				},
			});
			ReactGA.event("init", {
				gameId: profile.game_id,
			});
		} catch (error) {
			console.error("Error during GA initialization:", error);
		}
	},
	getConfig: async () => {
		const response = (await makeRequest(
			"config",
			"GET",
		)) as CryptoSteamSDKConfig;
		return response;
	},
	isAdEnabled: async () => {
		const response = (await makeRequest("ads/status", "GET")) as {
			enabled: boolean;
		};
		return response.enabled;
	},
	requestAd: async (options = {}) => {
		try {
			await showAd(options);
			return true;
		} catch (error) {
			console.error("Error showing ad", error);
			throw error;
		}
	},
	requestRewardAd: async (options = {}) => {
		try {
			const response = await showAd(options);

			// Wait a bit to ensure the ad has time to be registered
			await delay(1000);

			const status = await checkAdStatus(response.id);
			return status === "SHOWED" || status === "CLICKED";
		} catch (error) {
			console.error("Error showing reward ad", error);
			throw error;
		}
	},
	getProfile: async () => {
		const response = (await makeRequest(
			"profile",
			"GET",
		)) as CryptoSteamSDKProfile;
		return response;
	},
	getBalance: async () => {
		const response = (await makeRequest("balance", "GET")) as {
			balance: number;
		};
		return response.balance;
	},
	trackGameTimeTick: () => {
		makeRequest("ping", "POST");
	},
	getVersion: () => {
		return version;
	},
	initializeOverlay: (config) => {
		const rootElement = document.createElement("div");
		rootElement.id = "overlay-root";
		document.body.appendChild(rootElement);
		createOverlay(config);
	},
	getShopItems: async () => {
		return (
			(await makeRequest("shop/items", "GET")) as {
				items: CryptoSteamSDKShopItem[];
			}
		).items;
	},
	getPurchasedShopItem: async (itemId: number) => {
		const response = (await makeRequest(
			`shop/purchases/${itemId}`,
			"GET",
		)) as CryptoSteamSDKShopItem;
		return response;
	},
	getPurchasedShopItems: async () => {
		const response = (await makeRequest(
			`shop/purchases`,
			"GET",
		)) as CryptoSteamSDKShopItem[];
		return response;
	},
	buyShopItem: async (itemId: number) => {
		await makeRequest(`shop/items/${itemId}/buy`, "POST");
	},
	openPurchaseConfirmModal: async (
		shopItem: CryptoSteamSDKShopItem,
		position?: {
			x: number;
			y: number;
			width: number;
			height: number;
		},
	): Promise<PurchaseConfirmResponse> => {
		return new Promise((resolve, reject) => {
			const overlay = document.createElement("div");
			overlay.style.position = "fixed";
			overlay.style.top = "0";
			overlay.style.left = "0";
			overlay.style.width = "100%";
			overlay.style.height = "100%";
			overlay.style.backgroundColor = "transparent";
			overlay.style.zIndex = "9999";

			const iframe = document.createElement("iframe");
			iframe.style.position = "fixed";
			if (position) {
				const margin = 8;
				const iframeWidth = 210;
				const iframeHeight = 108;
				const arrowOffset = 20; // Space above the element for the "cloud" effect

				// Try to position above the element first
				let left = position.x + (position.width - iframeWidth) / 2;
				let top = position.y - iframeHeight - arrowOffset;

				// If not enough space above, try below
				if (top < margin) {
					top = position.y + position.height + arrowOffset;
				}

				// If not enough space on left/right, adjust horizontally
				if (left + iframeWidth > window.innerWidth - margin) {
					left = window.innerWidth - margin - iframeWidth;
				}
				if (left < margin) {
					left = margin;
				}

				// If still no space vertically, center on screen
				if (top + iframeHeight > window.innerHeight - margin || top < margin) {
					top = (window.innerHeight - iframeHeight) / 2;
					left = (window.innerWidth - iframeWidth) / 2;
				}

				iframe.style.left = `${left}px`;
				iframe.style.top = `${top}px`;
			} else {
				iframe.style.left = "50%";
				iframe.style.top = "50%";
				iframe.style.transform = "translate(-50%, -50%)";
			} /* Post */

			iframe.style.boxShadow =
				"0px 0px 2px 1px rgba(0, 0, 0, 0.22), 0px 32px 64px rgba(0, 0, 0, 0.34)";
			iframe.style.borderRadius = "24px";

			iframe.style.border = "none";
			iframe.style.zIndex = "10000";
			iframe.referrerPolicy = "origin";

			iframe.style.width = "210px";
			iframe.style.height = "108px";
			iframe.style.backgroundColor = "white";

			const iframeParams = new URLSearchParams();

			iframeParams.set("itemId", shopItem.id.toString());
			iframeParams.set("price", shopItem.price.toString());
			iframeParams.set("__tg_x_auth", TelegramWebApp.initData);

			const translations = {
				confirm: {
					pay: i18n.t("confirmIframe.pay"),
					cancel: i18n.t("confirmIframe.cancel"),
				},
			};
			iframeParams.set("translations", JSON.stringify(translations));

			iframe.src = `${BASE_URL}/shop/payment_iframe?${iframeParams.toString()}`;

			const handleMessage = (event: MessageEvent<ConfirmMessage>) => {
				if (event.data.type === "confirm") {
					window.removeEventListener("message", handleMessage as EventListener);
					document.body.removeChild(overlay);
					document.body.removeChild(iframe);
					resolve({ status: "success" });
				} else if (event.data.type === "cancel") {
					window.removeEventListener("message", handleMessage as EventListener);
					document.body.removeChild(overlay);
					document.body.removeChild(iframe);
					resolve({ status: "error" });
				} else if (event.data.type === "error") {
					window.removeEventListener("message", handleMessage as EventListener);
					document.body.removeChild(overlay);
					document.body.removeChild(iframe);
					reject(new Error(event.data.message));
				}
			};

			window.addEventListener("message", handleMessage as EventListener);

			overlay.onclick = () => {
				window.removeEventListener("message", handleMessage as EventListener);
				document.body.removeChild(overlay);
				document.body.removeChild(iframe);
				resolve({ status: "error" });
			};

			document.body.appendChild(overlay);
			document.body.appendChild(iframe);
		});
	},
	createInvoice: async (
		title: string,
		description: string,
		to_user_id: number,
		amount: number,
	) => {
		// is passing "to_user_id" safe? otherwise we need state management
		return await makeRequest<InvoiceResponse>("invoices", "POST", {
			title,
			description,
			to_user_id,
			amount,
		});
	},
	getTasks: async () => {
		const response = (await makeRequest("tasks", "GET")) as {
			tasks: CryptoSteamSDKTask[];
		};
		return response.tasks;
	},
	claimTask: async (taskId: number) => {
		await makeRequest(`tasks/${taskId}/mint`, "POST");
	},
	getAllKeyValues: async () => {
		const response = (await makeRequest("storage/", "GET")) as {
			data: Record<string, string>;
		};
		return response.data;
	},
	getValue: async (key: string) => {
		const response = (await makeRequest(`storage/${key}`, "GET")) as {
			value: string;
		};
		return response.value;
	},
	setValue: async (key: string, value: string) => {
		await makeRequest(`storage/${key}`, "PUT", {
			value,
		});
	},
	removeValue: async (key: string) => {
		await makeRequest(`storage/${key}`, "DELETE");
	},
	getData: async (key: string) => {
		console.warn("[DEPRECATED] Use PortalSDK.getValue instead");
		const response = (await makeRequest(`storage/${key}`, "GET")) as {
			value: string;
		};
		return response.value;
	},
	setData: async (key: string, value: string) => {
		console.warn("[DEPRECATED] Use PortalSDK.setValue instead");
		await makeRequest(`storage/${key}`, "PUT", {
			value,
		});
	},
	getLocale: () => {
		return TelegramWebApp.initDataUnsafe.user?.language_code || "en";
	},
	showSharing: (url: string, text?: string) => {
		const sharingURL = `https://t.me/share/url?text=${encodeURIComponent(
			text || "",
		)}&url=${encodeURIComponent(url)}`;
		TelegramWebApp.openTelegramLink(sharingURL);
	},
	telegramCloudStorage: {
		getValue: async (key: string) => {
			return CloudStorageGetItem(key);
		},
		setValue: async (key: string, value: string) => {
			return CloudStorageSetItem(key, value);
		},
		removeValue: async (key: string) => {
			return CloudStorageRemoveItem(key);
		},
	},
	gameReady: async () => {
		console.log("CryptoSteamSDK: gameReady received");

		const profile = await CryptoSteamSDK.getProfile();

		if (!profile) {
			console.error("Profile not found");
			return;
		}

		ReactGA.event("game_loaded", {
			gameId: profile.game_id,
		});
	},
};

const globalObj = getGlobalObj() as any;

globalObj.CryptoSteamSDK = CryptoSteamSDK;
globalObj.PortalSDK = CryptoSteamSDK;

export default CryptoSteamSDK;

export { CryptoSteamSDK as PortalSDK };

export const TelegramWebApp = WebApp;
```