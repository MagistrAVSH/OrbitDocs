# Defold Engine
## Getting Started

### Repository:
[PortalsdK Defold](https://github.com/orbit-software/portalsdk-defold)

### How to install:

1. Copy a link from releases on GitHub:
[Download v0.1.6.2](https://github.com/orbit-software/portalsdk-defold/archive/refs/tags/v0.1.6.2.zip)

2. Install into dependencies of game.project:
=== "game.project"
```ini
[project]
title = TestGame
version = 1.0
dependencies#0 = https://github.com/orbit-software/portalsdk-defold/archive/refs/tags/v0.1.6.2.zip
```
3. Set a template for HTML5 export:

=== "game.project"
```ini
[html5]
htmlfile = /portalsdk/manifests/web_template/engine_template.html
cssfile = /portalsdk/manifests/web_template/style.css
```
### API Description
The API is documented in detail: 


[Script API](https://github.com/orbit-software/portalsdk-defold/blob/master/portalsdk/api/portalsdk.script_api)  
[API Usage Example](https://github.com/orbit-software/portalsdk-defold/blob/master/main/main.script)
