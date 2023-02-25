# Modify the Icons Size in MacOS Launchpad

Icons can be resized by adjusting the number of icons per row and column of Launchpad.
<!--more-->

## method

Execute the following commands in the Terminal:
```shell
# For example, set to 8 columns
defaults write com.apple.dock springboard-columns -int 8
# For example, set to 6 lines
defaults write com.apple.dock springboard-rows -int 6
# Reset Launchpad
defaults write com.apple.dock ResetLaunchPad -bool TRUE
# Restart the Dock
killall Dock
```

Restore default settings:
```shell
defaults write com.apple.dock springboard-rows Default
defaults write com.apple.dock springboard-columns Default
defaults write com.apple.dock ResetLaunchPad -bool TRUE
killall Dock
```
