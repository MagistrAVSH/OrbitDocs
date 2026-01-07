# Changelog

All notable changes to the Orbit Platform documentation are documented in this file.

## [Unreleased] - 2026-01-07

### Added
- **Filter Telegram Logs** feature documentation (`docs/integration/filter-telegram-logs.md`)
  - New guide for filtering Telegram console logs in production
  - Added 2 screenshots showing the feature in action
  - Helps developers debug games in production environment

- **Telegram Bot ID** integration guide (`docs/integration/telegram-botid.md`)
  - Complete guide for obtaining and using bot IDs
  - Added 5 screenshots for step-by-step instructions
  - Required for local testing and SDK integration

- **Local Testing** comprehensive guide (`docs/setup/local-testing.md`)
  - Step-by-step instructions for testing games locally before deployment
  - Explains how to extract `initData` from Telegram WebApp
  - Documents `botId` and `authData` parameters for local development
  - Added 6 screenshots showing the testing process
  - Includes critical warnings about removing test parameters before production

### Updated
- **JavaScript Setup** (`docs/setup/0-javascript.md`)
  - Added Bot ID section with detailed instructions
  - Enhanced SDK initialization documentation with local testing parameters
  - Added link to local testing guide

- **Unity Setup** (`docs/setup/unity.md`)
  - Added comprehensive local testing section
  - Explained two testing options: local testing vs. GitHub deployment
  - Added link to local testing guide

- **Defold Setup** (`docs/setup/defold.md`)
  - Added link to local testing guide for consistency

- **Ad Integration** (`docs/integration/ad.md`)
  - Added documentation for `disable_startup_ads` configuration option
  - Explains how to control automatic ad display at game startup

- **CLAUDE.md** Project Documentation
  - Enhanced SDK initialization options section
  - Added detailed ad integration lifecycle documentation
  - Expanded local testing section with critical constraints
  - Added 160+ lines of comprehensive developer guidance

### Fixed
- Documentation consistency across setup guides
- Image path references in filter telegram logs
- Admin panel documentation references (`docs/upload-game/admin-panel.md`)
- IAP documentation minor corrections (`docs/integration/iap.md`)

### Removed
- Unused README.txt file from filter telegram logs images directory

## [2025-12-16] - Previous Session

### Added
- **Ad Callbacks** integration guide (`docs/integration/ad-callbacks.md`)
  - Documentation for `onAdStart` and `onAdEnd` callbacks
  - Explains ad lifecycle management
  - Provides code examples for handling ad events
  - Guidance on disabling game audio/input during ads

## [2025-08-27 to 2025-09-01] - Earlier Updates

### Changed
- Documentation cleanup and organization
- SDK documentation updates
- JavaScript setup guide improvements

### Removed
- Startup ad section (replaced with configuration option)

## [2025-08-19 to 2025-08-26] - IAP and Resources Update

### Added
- Icon image resources for IAP integration
- New paragraph and upload resources documentation
- Static resources (`docs/static/icons.zip`) for developers
- Introduction FAQ fixes

### Fixed
- Multiple URL and link corrections
- Download link fixes for static resources
- Documentation URL references

---

## Summary by Feature Area

### Setup & Local Testing (Jan 7, 2026)
- Complete local testing workflow documented
- Bot ID integration guide added
- All three SDK setup guides updated with local testing info

### Integration Features (Dec 16, 2025 - Jan 7, 2026)
- Ad callbacks lifecycle management
- Filter Telegram logs for production debugging
- Startup ad configuration option

### Documentation Infrastructure (Aug-Sep 2025)
- IAP integration resources
- Documentation cleanup
- Link and URL fixes
