# macOS Dev Setup

This document describes how I set up my developer environment on a new MacBook or iMac. 

The document assumes you are new to Mac, but can also be useful if you are reinstalling a system and need some reminder. The steps below were tested on **macOS High Sierra** (10.13), but should work for more recent versions as well.

**Contributing**: If you find any mistakes in the steps described below, or if any of the commands are outdated, do let me know! For any other suggestions, please understand if I don't include everything. This guide was originally written for some friends getting started with programming on a Mac, and as a personal reference for myself. I'm trying to keep it simple!

- [System update](#system-update)
- [System preferences](#system-preferences)
- [Security](#security)
- [iTerm2](#iterm2)
- [Homebrew](#homebrew)
- [Git](#git)
- [Visual Studio Code](#visual-studio-code)
- [Vim](#vim)
- [Python](#python)
- [Node.js](#nodejs)
- [Ruby](#ruby)
- [Heroku](#heroku)
- [PostgreSQL](#postgresql)
- [Redis](#redis)
- [Elasticsearch](#elasticsearch)
- [Projects folder](#projects-folder)
- [Apps](#apps)

## System update

First thing you need to do, on any OS actually, is update the system! For that: **Apple Icon > About This Mac** then **Software Update...**.

## System preferences

If this is a new computer, there are a couple of tweaks I like to make to the System Preferences and Finder. Feel free to follow these, or to ignore them, depending on your personal preferences.

In **Apple Icon > System Preferences**:

- Trackpad > Tap to click
- Keyboard > Key Repeat > Fast (all the way to the right)
- Keyboard > Delay Until Repeat > Short (all the way to the right)
- Dock > Automatically hide and show the Dock

In **Finder > System Preferences**:

- Preferences > General > Show Hard disks, External disks
- Preferences > General > New Finder windows show > Your home directory
- Preferences > Advanced > Show all filename extensions
- View > Show Status Bar 
- View > Show Path Bar 

## Security

I recommend checking that basic security settings are enabled. You will be happy to have done so if ever your Mac is lost or stolen.

In **Apple Icon > System Preferences**:

- Users & Groups: If you haven't already set a password for your user during the initial set up, you should do so now
- Security & Privacy > General: Require password immediately after sleep or screen saver begins (you can keep a grace period of a couple minutes if you prefer, but I like to know that my computer locks as soon as I close it)
- Security & Privacy > FileVault: Make sure FileVault disk encryption is enabled
- iCloud: If you haven't already done so during set up, enable Find My Mac

## iTerm2

### Install

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/).

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder.

You can now launch iTerm, through the **Launchpad** for instance.

Let's just quickly change some preferences. In **iTerm2 > Preferences...**, under the tab **General**, uncheck **Confirm closing multiple sessions** and **Confirm "Quit iTerm2 (Cmd+Q)" command** under the section **Closing**.

In the tab **Profiles**, create a new one with the "+" icon, and rename it to your first name for example. Then, select **Other Actions... > Set as Default**. Under the section **General** set **Working Directory** to be **Reuse previous session's directory**. Finally, under the section **Window**, change the size to something better, like **Columns: 125** and **Rows: 35**.

When done, hit the red "X" in the upper left (saving is automatic in macOS preference panes). Close the window and open a new one to see the size change.

### Beautiful terminal

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place. What follows might seem like a lot of work, but trust me, it'll make the development experience so much better.

First let's add some color. There are many great color schemes out there, but if you don't know where to start you can try [Atom One Dark](https://github.com/nathanbuchar/atom-one-dark-terminal). Download the iTerm presets for the theme by running:

```
cd ~/Downloads
curl -o "Atom One Dark.itermcolors" https://raw.githubusercontent.com/nathanbuchar/atom-one-dark-terminal/master/scheme/iterm/One%20Dark.itermcolors
curl -o "Atom One Light.itermcolors" https://raw.githubusercontent.com/nathanbuchar/atom-one-dark-terminal/master/scheme/iterm/One%20Light.itermcolors
```

Then, in **iTerm2 Preferences**, under **Profiles** and **Colors**, go to **Color Presets... > Import...**, find and open the **Atom One Dark.itermcolors** file we just downloaded. Repeat these steps for **Atom One Light.itermcolors**.  Now open **Color Presets...** again and select **Atom One Dark** to activate the dark theme (or choose the light them if that's your preference).

Not a lot of colors yet. We need to tweak a little bit our Unix user's profile for that. This is done (on macOS and Linux), in the `~/.bash_profile` text file (`~` stands for the user's home directory).

We'll come back to the details of that later, but for now, just download the files [.bash_profile](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_profile), [.bash_prompt](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_prompt), [.aliases](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.aliases) attached to this document into your home directory (`.bash_profile` is the one that gets loaded, I've set it up to call the others):

```
cd ~
curl -O https://raw.githubusercontent.com/natalieanguyen/mac-dev-setup/master/.bash_profile
curl -O https://raw.githubusercontent.com/natalieanguyen/mac-dev-setup/master/.bash_prompt
curl -O https://raw.githubusercontent.com/natalieanguyen/mac-dev-setup/master/.aliases
```

With that, open a new terminal tab (**Cmd+T**) and see the change! Try the list commands: `ls`, `ls -lh` (aliased to `ll`), `ls -lha` (aliased to `la`).

Now we have a terminal we can work with!

(Thanks to Mathias Bynens for his awesome [dotfiles](https://github.com/mathiasbynens/dotfiles).)

## Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for macOS is [Homebrew](http://brew.sh/).

### Install

An important dependency before Homebrew can work is the **Command Line Developer Tools** for **Xcode**. These include compilers that will allow you to build things from source. You can install them directly from the terminal with:

```
xcode-select --install
```

Once that is done, we can install Homebrew by copy-pasting the installation command from the [Homebrew homepage](http://brew.sh/) inside the terminal:

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Follow the steps on the screen. You will be prompted for your user password so Homebrew can set up the appropriate permissions.

Once installation is complete, you can run the following command to make sure everything works:

```
brew doctor
```

### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

```
brew install <formula>
```

To see if any of your packages need to be updated:

```
brew outdated
```

To update a package:

```
brew upgrade <formula>
```

Homebrew keeps older versions of packages installed, in case you want to rollback. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

```
brew cleanup
```

To see what you have installed (with their version numbers):

```
brew list --versions
```

### Homebrew Services

A nice extension to Homebrew is [Homebrew Services](https://github.com/Homebrew/homebrew-services). It will automatically launch things like databases when your computer starts, so you don't have to do it manually every time.

Homebrew Services will automatically install itself the first time you run it, so there is nothing special to do.

After installing a service (for example a database), it should automatically add itself to Homebrew Services. If not, you can add it manually with:

```
brew services <formula>
```

Start a service with:

```
brew services start <formula>
```

At anytime you can view which services are running with:

```
brew services list
```

## Git

macOS comes with a pre-installed version of [Git](http://git-scm.com/), but we'll install our own through Homebrew to allow easy upgrades and not interfere with the system version. To do so, simply run:

```
brew install git
```

When done, to test that it installed fine you can run:

```
which git
```

The output should be `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](https://raw.githubusercontent.com/natalieanguyen/mac-dev-setup/master/.gitconfig) file to your home directory:

```
cd ~
curl -O https://raw.githubusercontent.com/natalieanguyen/mac-dev-setup/master/.gitconfig
```

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

```
git config --global user.name "Your Name Here"
git config --global user.email "your_email@youremail.com"
```

They will get added to your `.gitconfig` file.

On a Mac, it is important to remember to add `.DS_Store` (a hidden macOS system file that's put in folders) to your project `.gitignore` files. You also set up a global `.gitignore` file, located for instance in your home directory (but you'll want to make sure any collaborators also do it):

```
cd ~
curl -O https://raw.githubusercontent.com/natalieanguyen/mac-dev-setup/master/.gitignore
git config --global core.excludesfile ~/.gitignore
```

## Visual Studio Code

With the terminal, the text editor is a developer's most important tool. Everyone has their preferences, but if you're just getting started and looking for something simple that works, [Visual Studio Code](https://code.visualstudio.com/) is a pretty good option.

Go ahead and [download](https://code.visualstudio.com/Download) it. Open the **.dmg** file, drag-and-drop in the **Applications** folder, you know the drill now. Launch the application.

**Note**: At this point I'm going to create a shortcut on the macOS Dock for both for Visual Studio Code and iTerm. To do so, right-click on the running application and select **Options > Keep in Dock**.

Just like the terminal, let's configure our editor a little. Go to **Code > Preferences > Settings**. In the very top-right of the interface you should see an icon with brackets that appeared **{ }** (on hover, it should say "Open Settings (JSON)"). Click on it, and paste the following:

```json
{
  "editor.tabSize": 2,
  "editor.rulers": [80],
  "files.insertFinalNewline": true,
  "files.trimTrailingWhitespace": true,
  "workbench.editor.enablePreview": false
}
```

Feel free to tweak these to your preference. When done, save the file and close it.

Pasting the above JSON snippet was handy to quickly customize things, but for further setting changes feel free to search in the "Settings" panel that opened first (shortcut **Cmd+,**). When you're happy with your setup, you can save the JSON to quickly restore it on a new machine.

If you remember only one keyboard shortcut in VS Code, it should be **Cmd+Shift+P**. This opens the **Command Palette**, from which you can run pretty much anything.

Let's open the command palette now, and search for `Shell Command: Install 'code' command in PATH`. Hit enter when it shows up. This will install the command-line tool `code` to quickly open VS Code from the terminal. When in a projects directory, you'll be able to run:

```
cd myproject/
code .
```

VS Code is very extensible. To customize it further, open the **Extensions** tab on the left.

Let's do that now to customize the color of our editor. Search for the [Atom One Dark Theme](https://marketplace.visualstudio.com/items?itemName=akamud.vscode-theme-onedark) extension, select it and click **Install**. Repeat this for the [Atom One Light Theme](https://marketplace.visualstudio.com/items?itemName=akamud.vscode-theme-onelight).

Finally, activate the theme by going to **Code > Preferences > Color Theme** and selecting **Atom One Dark** (or **Atom One Light** if that is your preference).

## Projects folder

This really depends on how you want to organize your files, but I like to put all my version-controlled projects in `~/Projects`. Other documents I may have, or things not yet under version control, I like to put in `~/Dropbox` (if you have [Dropbox](https://www.dropbox.com/) installed), or `~/Documents` if you prefer to use [iCloud Drive](https://support.apple.com/en-ca/HT206985).

## Apps

Here is a quick list of some apps I use, and that you might find useful as well:

- [LastPass](https://www.lastpass.com): Securely store your login and passwords, and access them from all your devices.
- [Dropbox](https://www.dropbox.com/): File syncing to the cloud. It is cross-platform, but if all your devices are Apple you may prefer [iCloud Drive](https://support.apple.com/en-ca/HT206985). **(Free for 2GB)**
- [Postman](https://www.getpostman.com/): Easily make HTTP requests. Useful to test your REST APIs. **(Free for basic features)**
- [GitHub Desktop](https://desktop.github.com/): I do everything through the `git` command-line tool, but I like to use GitHub Desktop just to review the diff of my changes. **(Free)**
- [Rectangle](https://rectangleapp.com): Move and resize windows with keyboard shortcuts. **(Free)**
