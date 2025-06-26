# Localization
Highly recommended to request the user's local language provided by the SDK and set it as the app language:

=== "Unity"

	```C#
    var locale = PortalSDK.GetLocale();
	```

=== "Defold"

	```LUA
    local locale = portal_sdk.get_locale();
	```


=== "JavaScript"

	```JS
    const locale = window.PortalSDK.getLocale()
	```

Locale strings in IETF language tag [https://en.wikipedia.org/wiki/IETF_language_tag](https://en.wikipedia.org/wiki/IETF_language_tag)

Example: `en de hy pl` and etc