# Package Manager

// 2020/04/26 Homebrew by jean tran

tl;dr: `brew update && brew upgrade`

After years of studies on Linux system and now using OSX as developer career. Here are some of my routines usage of **Homebrew**. 

Why **Homebrew**? The idea is to have the lightest, cleanest system installation. 

What does it do? From here it help to install specifics stuff that you need on demand (since every developer usage required different setup). 

What kind of packaged could you find? Most if it's not all GNU softwares, in my usage most my CLI (Command-Line Interface) tools (git, ruby, python etc...).

## Installation

In Linux Shell or OSX Terminal, you past the following command. The script will prompt explanation of what it does then pause before to do it.

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

## Usage Routine

### Commands

1. brew -v update
2. brew upgrade --force-bottle
3. brew cask upgrade
4. brew cleanup -s 

Optionals commands to run helping for maintenance and to have more information with 
brew installation.

* brew doctor
* brew missing

### Explanations

1. Fetch the newest version of Homebrew and all formulae from GitHub using git.
2. Basically upgrade is to upgrade outdated installed packages, --force-bottle Install from a bottle if it exists for the current or newest version of macOS, even if it would not normally be used for installation.
3. Homebrew Cask provides a friendly CLI workflow for the administration of macOS applications distributed as binaries.
4. Remove stale lock files and outdated downloads. '-s' will only keep linked version diskspace saver. (FI: 'brew cask cleanup' is merged into 'brew cleanup').

## Tips & Tricks

### Relevant commands

* `brew update` - Update brew itself and fetches info about what's available for your other software

* `brew upgrade` - Upgrade/update everything you've installed with Homebrew

* `brew list` - Display software you've installed

* `brew cask list` - Display GUI apps you've installed

* `brew cask upgrade` - Update GUI apps you've installed (u/_zio_pane)

* `brew outdated` - Display available updates

* `brew upgrade whatever_package` - Upgrade only a specific thing

* `brew cleanup` - Remove old versions

* `brew leaves` - Shows only packages you installed without their dependencies 

### Termminal Notifier

Terminal-notifier is a quite cool command-line tool to send macOS User Notifications, which are available on macOS 10.10 and higher. (available on Homebrew)

#### Installation

`brew install terminal-notifier`

#### Use cases

* terminal-notifier -message "my custom notification message :)"
* echo 'piped message ;)' | terminal-notifier -sound default

For more advanced usage please refers to the following link: [terminal-notifier](https://github.com/julienXX/terminal-notifier)



## Refences

* link to the [official homepage.](https://brew.sh/)
* link to the [official documentation.](https://docs.brew.sh/)

Thank you for reading. I suppose that you've got the main purpose the usage. Please contact me if you have any suggestions or ideas to make it better? Or did I miss something? I will be please to read about your feedbacks.