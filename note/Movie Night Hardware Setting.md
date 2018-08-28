Movie Night Hardware Setting
===

## Audio

### connect to bluetooth speaker
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

### adjust volumn
1. Start `alsamixer` controll interface
```
$ alsamixer
```
3. adjust master directly through arrow keys

### reference
- [Bluetooth headset](https://wiki.archlinux.org/index.php/Bluetooth_headset)
- [Bluetooth](https://wiki.archlinux.org/index.php/bluetooth#Using_your_computer.27s_speakers_as_a_bluetooth_headset)

## Display

### VGA
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

### Reference
[xrandr: Adding undetected resolution](https://wiki.archlinux.org/index.php/Xrandr#Adding_undetected_resolutions)
[Multihead: configure using xrandr](https://wiki.archlinux.org/index.php/Multihead#Configuration_using_xrandr)