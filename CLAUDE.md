# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Language Preference
**日本語で回答してください** - Always respond in Japanese when working with this repository.

## Project Overview

This is a ZMK firmware configuration for the SOA44, a custom 44-key split keyboard with integrated trackball. The keyboard features:
- 44-key split layout with ergonomic design
- Trackball integration with mouse automation
- RGB LED visual feedback system
- NiMH battery support with custom voltage management
- Enhanced Bluetooth connectivity (+8dBm output)
- ZMK Studio support

## Build System

### Build Configuration
- **Main build file**: `build.yaml` - defines the build matrix for GitHub Actions
- **Boards**: Seeeduino Xiao BLE controllers
- **Shields**: `soa44_L` (left half), `soa44_R` (right half) with `rgbled_adapter`
- **Build triggers**: GitHub Actions on push, PR, or manual dispatch

### Dependencies (West manifest in config/west.yml)
- **zmk-feature-non-lipo-battery-management**: Custom battery voltage management for NiMH batteries
- **zmk-pmw3610-driver**: Trackball (PMW3610 sensor) driver
- **zmk-rgbled-widget**: RGB LED status and layer indication system

## Architecture

### Hardware Configuration
- **Keyboard definition**: `boards/shields/soa44/soa44.dtsi` - physical layout and key matrix
- **Left half config**: `boards/shields/soa44/soa44_L.{conf,overlay}`
- **Right half config**: `boards/shields/soa44/soa44_R.{conf,overlay}`
- **Layout JSON**: `config/soa44.json` - keymap-drawer compatible layout definition

### Keymap Structure
- **Main keymap**: `config/soa44.keymap`
- **Layers**: 7 layers total (0-6) with specific purposes:
  - Layer 0: Default
  - Layer 1: Mouse (automouse with trackball)
  - Layer 2: Function
  - Layer 3: Number
  - Layer 4: Arrow
  - Layer 5: Scroll (trackball scrolling)
  - Layer 6: Bluetooth
- **RGB layer indication**: Each layer has assigned color (red, green, yellow, blue, magenta, cyan)
- **Combos**: Key combinations for special functions (tab, shift+tab, quotes, etc.)

### Features
- **Trackball configuration**: Automouse layer activation, scroll layers, configurable movement-to-key bindings
- **RGB widgets**: Battery status, connection status, and layer indication
- **Non-LiPo battery**: Custom voltage management for NiMH batteries
- **Enhanced Bluetooth**: +8dBm output power configuration

## Development Commands

### Testing Changes
```bash
# Build is handled by GitHub Actions automatically on push
git add . && git commit -m "description" && git push
```

### Local Development
- ZMK firmware builds require the ZMK build environment
- Use GitHub Actions for official builds
- Check `.github/workflows/build.yml` for build status

## Key Configuration Files
- `config/soa44.keymap` - Main keymap and behavior definitions
- `build.yaml` - Build matrix configuration
- `config/west.yml` - Dependency manifest
- `config/soa44.json` - Layout definition for keymap visualization