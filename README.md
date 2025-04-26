# macOS Developer Environment Setup

A guide how I set up development environment on a new Mac.

*Last updated: April 2025 - Tested on macOS Sequonia (10.4)*

## Table of Contents

- [Initial Setup](#initial-setup)
  - [System Update](#system-update)
  - [System Preferences](#system-preferences)
  - [Security Basics](#security-basics)
- [Developer Tools](#essential-developer-tools)
  - [Homebrew](#homebrew)
  - [iTerm2](#iterm2)
  - [Git](#git)
  - [Visual Studio Code](#visual-studio-code)
- [Recommended Apps](#recommended-apps)

## Initial Setup

### System Update

First, make sure your system is up to date:
1. Click **Apple Icon > System Preferences > General > Software Updates**
2. Install any available updates

### System Preferences

#### System Settings

- **Trackpad**: Enable "Tap to click"
- **Keyboard**: 
  - Set Key Repeat to Fast
  - Set Delay Until Repeat to Short
- **Dock**: 
  - Move to left side of screen
  - Remove unused apps
  - Disable "Show suggested and recent apps"
  - Disable "Show recent applications in Dock"
  - Disable "Show recent documents in Dock"

#### Finder Preferences

- **General**: 
  - Show hard disks and external disks on desktop
  - New Finder windows show your home directory
- **Advanced**: Show all filename extensions
- **View**: 
  - Show Status Bar
  - Show Path Bar
 - **Tags**:
  - Disable All

### Security Basics

- **Users & Groups**: Set a strong password if not already done
- **Security & Privacy > General**: Require password immediately after sleep/screen saver
- **Security & Privacy > FileVault**: Enable disk encryption
- **iCloud**: Enable Find My Mac

## Developer Tools

### Homebrew

[Homebrew](https://brew.sh/) is the most popular package manager for macOS.

#### Installation

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Verify installation:
```bash
brew doctor
```

#### Common Commands

| Command | Description |
|---------|-------------|
| `brew install <formula>` | Install a package |
| `brew outdated` | Check for outdated packages |
| `brew upgrade <formula>` | Update a package |
| `brew cleanup` | Remove old versions |
| `brew list --versions` | List installed packages |

### iTerm2

A better terminal for macOS with more features than the default Terminal.app.

#### Installation

```bash
brew install --cask iterm2
```

#### Configuration

1. Open **iTerm2 > Preferences**
2. **General > Closing**: Uncheck confirm closing options
3. **Profiles**:
   - Create a new profile and set as default
   - **General**: Set "Working Directory" to "Reuse previous session's directory"
   - **Window**: Set size to Columns: 125, Rows: 35

#### Terminal Theme

Install the Atom One Dark theme:

```bash
cd ~/Downloads
curl -o "Atom One Dark.itermcolors" https://raw.githubusercontent.com/nathanbuchar/atom-one-dark-terminal/master/scheme/iterm/One%20Dark.itermcolors
```

Apply the theme:
1. **iTerm2 > Preferences > Profiles > Colors**
2. **Color Presets > Import**
3. Select the downloaded .itermcolors file
4. **Color Presets** and select the theme

### Git

Install the latest version of Git:

```bash
brew install git
```

Configure Git:

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

### Visual Studio Code

#### Installation

```bash
brew install --cask visual-studio-code
```

#### Essential Configuration

Open Settings (Cmd+,) and add these configurations:

```json
{
  "editor.tabSize": 2,
  "editor.rulers": [80],
  "files.insertFinalNewline": true,
  "files.trimTrailingWhitespace": true,
  "workbench.editor.enablePreview": false
}
```

#### Command Line Integration

1. Open the Command Palette (Cmd+Shift+P)
2. Type "Shell Command: Install 'code' command in PATH"
3. Press Enter

Now you can open folders from the terminal:
```bash
code .
```

#### Extensions

Some helpful extensions to install:
- Theme: Dracula
- Prettier
- Python
- Docker

## Recommended Apps

Install these apps with a single Homebrew command:

```bash
brew install --cask \
  raycast \
  google-chrome \
  slack \
  discord \
  vlc \
  1password \
  obsidian \
  maccy \
  spotify
```

### Raycast Setup

1. We installed raycast in thInstall: `brew install --cask raycast`
2. Open Raycast and follow setup wizard
3. System Settings > Keyboard > Keyboard Shortcuts > Spotlight
   - Disable "Show Spotlight search"
4. Set Raycast hotkey to Cmd+Space

### Development Folder Structure

Create an organized folder for development projects:

```bash
mkdir -p ~/Development/{personal,work,open-source,experiments}
```

---

*This document is a work in progress and will be updated as new tools or workflows are adopted.*



