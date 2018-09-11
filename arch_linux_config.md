Arch Linux
===

### Table of content
- [Bluetooth](#bluetooth)
    - [Bluetooth speaker](#bluetooth_speaker) 
    - [Reference](#bluetoothctl_ref)
- [Multi Monitor](#multi_monitor)
    - [VGA](#multi_monitor_vga)
    - [Reference](#multi_monitor_ref)
- [Mount USB drive](#mount_usb)
    - [Use Built-in Tool](#mount_usb_builtin)
    - [Use udisks](#mount_usb_udisks)
- [Key Binding](#key_bind) 
    - [Backlight](#key_bind_backlight)
    - [Volumn](#key_bind_volumn)
- [Useful Applications](#apps)
    - [Screen Lock](#screen_lock)
    - [Chinese Font](#chinese_font)
    - [Screenshot](#screenshot)


<a name="bluetooth"></a>
# Bluetooth 

<a name="bluetooth_speaker"></a>
## Bluetooth Speaker
1. Start the `bluetoothctl` interactive command
```
$ bluetoothctl
```
2. Turn the power to the controller
```
$ power on
```
3. Turn on the agent
```
$ agent on
```
4. Use default agent setting
```
$ default-agent
```
5. Search available devices
```
$ devices
```
6. Pair device MAC address
```
$ pair MAC_ADDRESS
```
7. Connect to device
```
$ connect MAC_ADDRESS
```
8. To disconnect to device
```
$ disconnect MAC_ADDRESS
```

<a name="bluetoothctl_ref"></a>
## Reference
- [Bluetooth headset](https://wiki.archlinux.org/index.php/Bluetooth_headset)
- [Bluetooth](https://wiki.archlinux.org/index.php/bluetooth#Using_your_computer.27s_speakers_as_a_bluetooth_headset)


<a name="multi_monitor"></a>
# Multi Monitor 

<a name="multi_monitor_vga"></a>
## VGA 
1. Show available device
```
$ xrandr
```
2. Get modeline for the resolution we want
```
$ cvt 1366 768
```
3. Create new xrandr mode
```
$ xrandr --newmode "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync
```
4. Add newly created mode to our output device
```
$ xrandr --addmode DEVICE MODE_NAME
```
5. Now we change the resolution of the screen to the one we just added
```
$ xrandr --output DEVICE --mode MODE_NAME
```

<a name="multi_monitor_ref"></a>
## Reference 
[xrandr: Adding undetected resolution](https://wiki.archlinux.org/index.php/Xrandr#Adding_undetected_resolutions)
[Multihead: configure using xrandr](https://wiki.archlinux.org/index.php/Multihead#Configuration_using_xrandr)


<a name="mount_usb"></a>
# Mount USB Drive
DEVICE_PARTITION(ex: sdb2)

<a name="mount_usb_builtin"></a>
## Use Built-in Tool
1. Check device name
```
$ lsblk -f
```
2. Create mount point
```
$ mkdir /mnt/MNT_POINT
```
3. Mount device
```
$ mount /dev/DEVICE_PARTITION /mnt/MNT_POINT
```
4. To unmount device
```
$ umount /dev/DECIVE_PARTITION
```

<a name="mount_usb_udisks"></a>
## Use udisks
1. Check device name
```
$ lsblk -f
```
3. Mount block device
```
$ udisksctl mount -b /dev/DEVICE_PARTITION
```
4. To unmount device
```
$ udisksctl unmount -b /dev/DEVICE_PARTITION
```
5. Safely remove drive
```
$ udisksctl power-off -b /dev/DEVICE_PARTITION
```


<a name="key_bind"></a>
# Key Binding 
> see [arch_wiki/xbindkeys](https://wiki.archlinux.org/index.php/Xbindkeys)
1. intall **xbindkeys**
2. generate default config file
```
$ xbindkeys -d > ~/.xbindkeysrc
```
4. set the config file
> **Tip:** Use `xbindkey -k` to find keycodes for a particular key

> **Tip:** After you made a change, execute `xbindkeys -p` to reload the configuration file and apply the changes.

> **Tip:** To apply the change permanently, add `xbindkey` in _~/.xinitrc_ before starting your windows manager.

<a name="key_bind_backlight"></a>
## Backlight
> see [arch_wiki/backlight/xbacklight](https://wiki.archlinux.org/index.php/backlight#xbacklight)
1. install **xorg-xbacklight**
2. set backlight dir for xbacklight in _/etc/X11/xorg.conf_
```
Section "Device"
    Identifier  "Card0"
    Driver      "intel"
    Option      "Backlight"  "intel_backlight"
EndSection
```
4. add keybinding in _~/.xbindkeysrc_
```
# Increase bakclight by 4% 
"xbacklight -inc 4"
  F86MonBrightnessUp
  
# Decrease bakclight by 4% 
"xbacklight -dec 4"
  F86MonBrightnessDown
```

<a name="key_bind_volumn"></a>
## Volumn
1. install **alsamixer**
2. add keybinding in _~/.xbindkeysrc_
```
# Increase volumn by 4% 
"amixer -c 1 set Master 4%+"
  F86AudioRaiseVolumn
  
# Decrease volumn by 4% 
"amixer -c 1 set Master 4%-"
  F86AudioLowerVolumn
  
# Mute/Unmute volumn
# double press to unmute
"amixer -c 1 set Master toggle;amixer -c 1 set Headphone toggle; amixer -c 1 set Speaker toggle"
  F86AudioMute
```
> **Info:** amixer `-c` option is for selecting sound cards index


<a name="apps"></a>
# Useful Applications

<a name="screen_lock"></a>
## Screen Lock
I use **i3lock** for i3wm to lock screen
1. install from source
2. to execute
```
$ i3lock
```
3. type your password to unlock

<a name="chinese_font"></a>
## Chinese Font
[ttf-tw](https://aur.archlinux.org/packages/ttf-tw/): 台灣教育部的字體

<a name="screenshot"></a>
## Screenshot
[deepin-screenshot](https://www.deepin.org/en/original/deepin-screenshot/)
