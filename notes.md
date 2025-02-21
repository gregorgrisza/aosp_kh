# Notes


## GUI.py

Start emulator: `lunch mycar_cf_x86-trunk_staging-userdebug && HOME=$PWD launch_cvd --daemon`
Open browser on https://localhost:8443/ and start device
```bash
python vendor/v/tools/emulator/gui.py
```


_Notes_

_Get sockets ports: lsof -i -a -p "$(pgrep -f gui.py)"_

_Use wireshark to check traffic on ports on any interface_

---
**AIDL and emu-metadata generation**

Tools in: `hardware/interfaces/automotive/vehicle/tools`

---
**VHAL Host emulator tools**

https://android.googlesource.com/platform/packages/services/Car/+/master/tools/emulator/README.md

---
**Vendor VHAL service implementation**

AOSP provides default set of VHAL and its services and suggests to reuse it to customize:

https://source.android.com/docs/automotive/vhal/reference-implementation

https://android.googlesource.com/platform/hardware/interfaces/+/refs/heads/main/automotive/vehicle/aidl/impl/

**Cloud emulators**

https://source.android.com/docs/automotive/start/avd/cloud_emulator

https://github.com/google/android-emulator-webrtc
