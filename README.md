# OSX setup guide for exhibitions

+ **[System preferences](#system-preferences)**
  + **[Login & user](#login--user)**
    + [limit privileges](#limit-privileges)
    + [automatic login](#automatic-login)
    + [start apps on login](#start-apps-on-login)
  + **[Energy](#energy)**
    + [prevent display from turning off](#prevent-display-from-turning-off)
    + [prevent hard disk(s) from sleeping](#prevent-hard-disks-from-sleeping)
    + [scheduled wake / sleep](#scheduled-wake--sleep)
    + [handle power failure](#handle-power-failure)
    + [prevent screensaver from turning on](#prevent-screensaver-from-turning-on)
  + **[Notifications & updates](#notifications--updates)**
    + [prevent notifications](#prevent-notifications)
    + [disable bluetooth keyboard/mouse auto-assistant](#disable-bluetooth-keyboard--mouse-auto--assitant)
    + [prevent updates](#prevent-updates)
  + **[UI](#ui)**
    + [autohide menu bar](#autohide-menu-bar)
    + [autohide dock](#autohide-dock)
    + [hide desktop icons](#hide-desktop-icons)
    + [setup a desktop background](#setup-a-desktop-background)
+ **[App handling](#app-handling)**
  + **[autostart app](#autostart-app)**
  + **[handle app crash](#handle-app-crash)**
  + **[disable app nap](#disable-app-nap)**
+ **[Misc](#misc)**
  + **[Useful apps](#useful-apps)**
  + **[CLI](#cli)**
+ **[Ressources](#ressources)**
+ **[License](#license)**




--- 

## System preferences

### Login & user

#### limit privileges
+ open _Users & Groups_
+ create a new user (not a guest) with standard privileges and no password

#### automatic login
+ open _Users & Groups_
+ _Login Options_ > _Automatic Login_

#### start apps on login
+ open _Users & Groups_
+ go to the desired user
+ open the _Login Items_ tab
+ a the desired app by clicking the _+_ button

<sup>for more advanced startup options, see **[Autostart](autostart)** below</sup>

### Energy

#### prevent display from turning off
+ open _Energy Saver_
+ set _Turn display off after_ to `never`

#### prevent hard disk(s) from sleeping
+ open _Energy Saver_
+ set _Put hard disks to sleep when possible_ to `false`

#### scheduled wake / sleep
+ open _Energy Saver_
+ open _Schedule..._
+ set _Start up or wake_ to `Every day` at desired time
+ set _Sleep_ to `Every day` at desired time

#### handle power failure
+ open _Energy Saver_
+ enable _Start up automatically after a power failure_

#### prevent screensaver from turning on
+ open _Desktop & Screen Saver_
+ go to the _Screen Saver_ tab
+ set _Start after_ to `Never`

### Notifications & updates

#### prevent notifications
+ open _Notifications_
+ set _Turn on Do Not Disturb_ to `from` to `00:00` from `23:59`

### disable bluetooth keyboard/mouse auto-assistant
+ open _Bluetooth_
+ go to _Advanced..._
+ set _Open Bluetooth Setup Assistant at startup if no keyboard is detected_ to `false`
+ set _Open Bluetooth Setup Assistant at startup if no mouse or trackpad is detected_ to `false`

#### prevent updates
+ open _App Store_ preferences pane
+ set _Automatically check for updates_ to `false`

### UI

#### autohide menu bar
+ open _General_
+ set _Automatically hide and show the menu bar_ to `true`

#### autohide dock
+ open _Dock_
+ set _Automatically hide and show the Dock_ to `true`

#### hide desktop icons
+ open _Terminal.app_
+ enter `defaults write com.apple.finder CreateDesktop -bool false && killall Finder`

<sup>to revert it : `defaults write com.apple.finder CreateDesktop -bool true && killall Finder`</sup>

#### setup a desktop background
+ open _Desktop & Screen Saver_
+ select a neutral solid color

---
## App handling

### autostart app

### handle app crash
`~/Library/LaunchAgents/APPNAME.restart.plist`
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
        <key>RunAtLoad</key>  
        <true/>  
        <key>KeepAlive</key>
        <true/>
        <key>Label</key>
        <string>APPNAME.restart</string>
        <key>ProgramArguments</key>
        <array>
                <string>/path/to/APPNAME.app/Contents/MacOS/APPNAME</string>
        </array>
</dict>
</plist>
```

`launchctl load ~/Library/LaunchAgents/APPNAME.restart.plist && sudo shutdown -r now
`

+ _`RunAtLoad` will launch the application the first time launchctl runs this_
+ _`KeepAlive` will restart it if the application quits (CMD+Q or crash)_

### disable App Nap
_App Nap automatically reduces system resources to certain applications that are not currently in use. In some cases, it will prevent your app from running continuously._
+ right click you app and click _Get Info_
+ in _General_, set _Prevent App Nap_ to `true`

---
## Misc

### Useful apps
+ [TeamViewer](https://www.teamviewer.com/)
+ [Dropbox](https://www.dropbox.com/)
+ [Github Desktop]()

### CLI
+ `echo 'my message' | mail -s 'test' 'your@email.com'`

---
## Ressources
+ http://paulbourke.net/exhibition/automation/
+ http://vormplus.be/blog/article/configuring-mac-os-x-for-interactive-installations
+ http://apple.stackexchange.com/questions/837/automatically-relaunch-a-closed-application
+ https://github.com/laserpilot/Installation_Up_4evr
+ https://www.tekrevue.com/tip/disable-app-nap-os-x-mavericks/
+ https://sfpc.hackpad.com/rPi-run-4-ever-qFgafqYPM54

## License
[MIT](https://tldrlegal.com/license/mit-license).
