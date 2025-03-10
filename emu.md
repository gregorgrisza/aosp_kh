# Emulator extension


## Emulator development


### Setup & build

See: https://android.googlesource.com/platform/external/qemu/+/refs/heads/emu-33-release/android/docs/DARWIN-DEV.md

#### Development tools

- settings.json

```json
    "files.watcherExclude": {
        "**/.repo/**": true,
        "**/external/qemu/objs/**": true,
        "**/out/**": true
    }
```

- watching files

MacOS: `sudo sysctl -w kern.maxfiles=524288`

Ubuntu: Change/Add to /etc/sysctl.conf: `fs.inotify.max_user_watches=524288`

- 


### VHAL extension

Decribes way to extend emulator UI within custom VHAL definition


#### Generate extended VHAL definition

```bash
mkdir $HOME/aosp && $HOME/aosp
repo init --partial-clone -b main -u https://android.googlesource.com/platform/manifest && repo sync
```

Edit VHAL definition in: `hardware/interfaces/automotive/vehicle/2.0/types.hal`

Generate new definition: `python3 packages/services/Car/tools/emulator/vhal_const_generate.py`

#### GUI

Simply run: `python3 packages/services/Car/tools/emulator/gui.py`

It's example fo GUI implementation to interact with VHAL in emulator. It works with default VHAL, but it seems to be 
possible to extend, so it can consume custom vendor VHAL definition and generate consts, so can be used in vendor's 
GUI implementation.
