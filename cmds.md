
# Commands

```
lsusb
emulator -cores 4 -memory 6144 -usb-passthrough vendorid=0x0b05,productid=0x17cb
```

```
adb shell dumpsys bluetooth_manager
```

```
adb root; adb shell cmd car_service enable-feature <FEATURE_STRING_VALUE>; adb reboot
```

```
#video4linux: `sudo apt install v4l2-utils`

v4l2-ctl --list-devices
```


# Links

https://gist.github.com/Pulimet/5013acf2cd5b28e55036c82c91bd56d8#file-adbcommands
