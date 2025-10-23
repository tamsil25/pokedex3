# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an iOS Pokedex application built with Swift and UIKit. The app displays Pokemon data sourced from a CSV file, with corresponding image assets for 718+ Pokemon.

## Building and Testing

### Build Commands
```bash
# Build the project (requires Xcode)
xcodebuild -project pokedex3.xcodeproj -scheme pokedex3 -configuration Debug build

# Build for specific SDK
xcodebuild -project pokedex3.xcodeproj -scheme pokedex3 -sdk iphoneos

# Clean build folder
xcodebuild -project pokedex3.xcodeproj -scheme pokedex3 clean
```

### Running Tests
```bash
# Run unit tests
xcodebuild test -project pokedex3.xcodeproj -scheme pokedex3 -destination 'platform=iOS Simulator,name=iPhone 14'

# Run UI tests only
xcodebuild test -project pokedex3.xcodeproj -scheme pokedex3 -destination 'platform=iOS Simulator,name=iPhone 14' -only-testing:pokedex3UITests

# Run specific test
xcodebuild test -project pokedex3.xcodeproj -scheme pokedex3 -destination 'platform=iOS Simulator,name=iPhone 14' -only-testing:pokedex3Tests/pokedex3Tests/testExample
```

Note: If xcodebuild is not available, open `pokedex3.xcodeproj` in Xcode and use Cmd+B to build, Cmd+U to run tests.

## Architecture

### Data Structure

**Pokemon CSV (`pokedex3/pokemon.csv`)**
- Contains 719 Pokemon entries
- Schema: `id,identifier,species_id,height,weight,base_experience,order,is_default`
- Example: `1,bulbasaur,1,7,69,64,1,1`

### Assets

**Image Assets (`pokedex3/Assets.xcassets/`)**
- 718 Pokemon image sets organized as numbered folders (1.imageset, 2.imageset, etc.)
- Each imageset corresponds to a Pokemon ID from the CSV
- Images are referenced by their Pokemon ID number

### Source Files

**AppDelegate.swift**
- Standard iOS application lifecycle management
- Entry point: `@UIApplicationMain`

**ViewController.swift**
- Main view controller (currently basic template)
- Location for primary Pokemon display logic

**Storyboards**
- `Base.lproj/Main.storyboard` - Main UI interface
- `Base.lproj/LaunchScreen.storyboard` - Launch screen

### Test Structure

**Unit Tests (`pokedex3Tests/`)**
- Framework: XCTest
- Import with `@testable import pokedex3` for internal access
- Template test class: `pokedex3Tests`

**UI Tests (`pokedex3UITests/`)**
- Framework: XCTest with XCUIApplication
- Launches full application for each test
- Template test class: `pokedex3UITests`

## Development Guidelines

### Working with Pokemon Data

When implementing CSV parsing:
1. Parse `pokemon.csv` from the app bundle
2. Map CSV columns to a Pokemon model struct/class
3. Use the `id` field to reference corresponding images in Assets.xcassets

### Adding New Swift Files

Place new Swift files in the `pokedex3/` directory and ensure they're added to the target in Xcode project settings.

### Asset Management

Pokemon images are indexed by ID. To reference an image:
```swift
let image = UIImage(named: "\(pokemonId)")
```

## Platform Support

- Minimum iOS version: Defined in Info.plist (LSRequiresIPhoneOS)
- Supported orientations (iPhone): Portrait, Landscape Left/Right
- Supported orientations (iPad): All orientations including upside down
- Architecture: armv7+
