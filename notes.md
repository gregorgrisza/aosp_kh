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

### Task 1

Implement in gui.py handling setting new vendor property in dropbox.
- generate consts from types.hal
- add Widget in gui.py

### Task 2

In CVD device there is visible temperature. Change it via gui.py
- change in CVD on UI and observe gui.py log
- find property in types.hal and read how to use the property
- add combobox with allowed temperatures and function setting it

## Custom actions and custom actions server

```
HOME=$PWD launch_cvd --gpu_mode=gfxstream --resume=false
```
_Notes:_
_frontend logs can be visible in browser (chrome: F12), _
_server logs are visible in output from `launch_cv`_

**Hack/Patch to activate servers' actions buttons:**
```
roject device/google/cuttlefish/
diff --git a/host/frontend/webrtc/html_client/js/controls.js b/host/frontend/webrtc/html_client/js/controls.js
index 09d7ad5d1..ea3f114d9 100644
--- a/host/frontend/webrtc/html_client/js/controls.js
+++ b/host/frontend/webrtc/html_client/js/controls.js
@@ -236,7 +236,7 @@ function createControlPanelButton(
   let button = document.createElement('button');
   document.getElementById(parent_id).appendChild(button);
   button.title = title;
-  button.disabled = true;
+  button.disabled = false;
   addMouseListeners(button, listener);
   // Set the button image using Material Design icons.
   // See http://google.github.io/material-design-icons
```

---
**AIDL and emu-metadata generation**

Tools in: `hardware/interfaces/automotive/vehicle/tools`

https://cs.android.com/android/platform/superproject/+/main-cuttlefish-vendor-dev:hardware/interfaces/automotive/vehicle/aidl/emu_metadata/generate_emulator_metadata.py?authuser=1&hl=ja 

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
