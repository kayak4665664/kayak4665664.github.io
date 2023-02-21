# Modify the Icons Size in MacOS Launchpad

Icons can be resized by adjusting the number of icons per row and column of Launchpad.
<!--more-->

## method

Execute the following commands in Terminal:
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

<div align="center">
{{< image src="https://cdn.kayak4665664.com/Screenshot%202023-02-21%20at%2012.34.40.jpg" title="8*6 Launchpad" alt="8*6 Launchpad">}}
</div>

Restore default settings:
```shell
defaults write com.apple.dock springboard-rows Default
defaults write com.apple.dock springboard-columns Default
defaults write com.apple.dock ResetLaunchPad -bool TRUE
killall Dock
```
