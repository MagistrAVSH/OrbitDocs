# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the documentation repository for **Orbit Platform** (formerly Portal), a platform that enables developers to publish WebGL games and JavaScript apps as Telegram Mini Apps. The documentation is built using MkDocs with Material theme and deployed to https://docs.portalapp.games/.

## Key Commands

### Development
```bash
# Serve documentation locally with live reload
mkdocs serve

# Build static site (output to site/)
mkdocs build

# Deploy to GitHub Pages (if configured)
mkdocs gh-deploy
```

### Python Environment
```bash
# Install dependencies
pip install mkdocs mkdocs-material mkdocs-awesome-pages-plugin

# Check installed MkDocs version
mkdocs --version
```

## Architecture

### Documentation Structure

The site uses a hybrid navigation system:

1. **Automatic page ordering** via `mkdocs-awesome-pages-plugin`
   - Each section has a `.pages` file defining navigation order
   - Root navigation is defined in `docs/.pages`

2. **Section hierarchy:**
   - `introduction/` - Platform overview and FAQ
   - `setup/` - SDK installation for JavaScript, Unity, and Defold, plus local testing guide
   - `integration/` - Feature integration guides (ads, IAP, localization, persistent state, safe area, startup config, TG devtools, ad callbacks, telegram bot ID)
   - `upload-game/` - Game deployment and admin panel

### Custom Theme Components

Located in `overrides/`:

- `home.html` - Custom landing page with hero section and background image
- `main.html` - Base template override
- `hooks/shortcodes.py` - MkDocs hook for processing custom markdown shortcodes (badges, icons)
- `hooks/translations.py` and `hooks/translations.html` - Translation support
- `assets/` - Custom images and static assets

The `shortcodes.py` hook processes comments like `<!-- md:version 1.0 -->` to generate badges and special formatting.

### SDK Integration Patterns

The documentation covers three SDK implementations:

1. **JavaScript SDK**: Browser-based, loaded via script tag from Google Cloud Storage
2. **Unity SDK**: Package installed via Git URL or local folder, requires custom WebGL template
3. **Defold SDK**: Dependency added to `game.project`, requires custom HTML5 template

All SDKs follow a consistent API pattern:
- `initialize()` - SDK setup
- `initializeOverlay()` - UI overlay setup
- `gameReady()` - Signal game is loaded
- `requestAd()` / `requestRewardAd()` - Ad integration
- `getShopItems()` / `openPurchaseConfirmModal()` - IAP integration

#### SDK Initialization Options

The `initialize()` method accepts configuration options to control SDK behavior:

```javascript
await PortalSDK.initialize(undefined, {
  disable_startup_ads: true,
});
```

**Configuration Options:**
- `disable_startup_ads` - When set to `true`, prevents ads from automatically displaying at game startup. Useful for games that want full control over when ads are shown.

#### Ad Integration

**Ad Types:**
1. **Interstitial ads** (`requestAd()`) - Full-screen ads shown during natural gameplay breaks
2. **Rewarded ads** (`requestRewardAd()`) - Optional ads where users receive in-game rewards for watching

**Ad Lifecycle Callbacks:**
- `PortalSDK.onAdStart` - Called when ad begins displaying
- `PortalSDK.onAdEnd(success: boolean)` - Called when ad finishes (success indicates if ad was shown successfully)

Both callbacks work with `requestAd()` and `requestRewardAd()`. Set to `null` to disable.

**Important:** Always disable game audio and input during ad playback to prevent interference.

#### Local Testing

Developers can test their games locally with full SDK functionality before deployment:

1. Extract `initData` from Telegram WebApp console (`window.Telegram.WebApp.initData`)
2. Modify SDK initialization to include `botId` and `authData` parameters
3. Build and run locally
4. **Critical:** Remove test parameters before uploading to production

The local testing documentation is in `setup/local-testing.md` and is linked from all three setup guides (JavaScript, Unity, Defold).

**Important:** Games cannot run with full SDK functionality locally without either:
- Using the local testing configuration (with `botId` and `authData`)
- Being deployed to the platform via GitHub

This is emphasized in the Unity setup guide which explains both testing options.

## Content Guidelines

### Writing Style

- Use tabbed code blocks for multi-platform examples (Unity/Defold/JavaScript)
- Include screenshots in `docs/*/images/` directories
- Keep API examples concise and practical

### Code Tabs Format

Use MkDocs tabbed extension syntax:

```markdown
=== "Unity"
    ```C#
    await PortalSDK.RequestAd();
    ```

=== "JavaScript"
    ```JS
    await window.PortalSDK.requestAd()
    ```

=== "Defold"
    ```LUA
    portalsdk.request_ad(function(self, success) end)
    ```
```

### Important Constraints

- Platform handles Telegram Mini App creation (developers cannot use their own)
- Games must use Orbit's hosting (no external hosting allowed)
- Build files are deployed via GitHub to `/public/` directory
- Access to admin panel and upload repositories is by request only

## File Organization

- **Configuration**: `mkdocs.yml` - Site config with Material theme settings
- **Content**: `docs/**/*.md` - All documentation pages
- **Overrides**: `overrides/` - Custom templates and hooks
- **Build output**: `site/` - Generated static site (gitignored)
- **Static files**: `docs/static/` - Downloadable resources (e.g., icons.zip for IAP integration)

## Material Theme Features

Enabled features in `mkdocs.yml`:
- Instant navigation with prefetch
- Tabbed navigation
- Code annotation and copy buttons
- Search suggestions
- Navigation tracking and breadcrumbs

## Important Notes

- The landing page (`docs/index.md`) uses `template: home.html` in frontmatter to trigger custom hero layout
- Image paths in docs use relative paths (e.g., `images/game-and-iap/2.png`)
- The site uses JetBrains Mono for code and Inter for body text
- Navigation structure is controlled by `.pages` files, not `mkdocs.yml`
