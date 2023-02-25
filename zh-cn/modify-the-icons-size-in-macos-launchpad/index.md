# 修改macOS Launchpad的图标大小

通过调整Launchpad每一行和每一列的图标的数量，就可以调整图标的大小。
<!--more-->

## 方法

在Terminal中执行以下命令：
``` shell
# 例如设置为8列
defaults write com.apple.dock springboard-columns -int 8
# 例如设置为6行
defaults write com.apple.dock springboard-rows -int 6
# 重置Launchpad
defaults write com.apple.dock ResetLaunchPad -bool TRUE
# 重启Dock
killall Dock
```

恢复默认设置：
``` shell
defaults write com.apple.dock springboard-rows Default
defaults write com.apple.dock springboard-columns Default
defaults write com.apple.dock ResetLaunchPad -bool TRUE
killall Dock
```
