
# Commands

```
lsusb
emulator -cores 4 -memory 6144 -usb-passthrough vendorid=0x0b05,productid=0x17cb
```

```
adb shell dumpsys bluetooth_manager
adb shell dumpsys SurfaceFlinger --display-id
```

```
adb root; adb shell cmd car_service enable-feature <FEATURE_STRING_VALUE>; adb reboot
```

```
#video4linux: `sudo apt install v4l2-utils`

v4l2-ctl --list-devices
v4l2-ctl --device=/dev/video15 --list-ctrls
```

```
# Record and play: `sudo apt install ffmpeg`
v4l2-ctl --device=/dev/video0 --set-fmt-video=width=640,height=480,pixelformat=YUYV --stream-mmap --stream-to=video100.yuv --stream-count=100
ffplay -video_size 640x480 -pixel_format yuyv422 -framerate 10 -i video100.yuv 
```

```
adb shell dumpsys car_service --services CarFeatureController
```

# Links

https://gist.github.com/Pulimet/5013acf2cd5b28e55036c82c91bd56d8#file-adbcommands
