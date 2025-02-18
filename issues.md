# Issues

_Note: issues are `stupid` and solutions not generic. It's more list of what happened and steps after issues disappeared._


---
## Missing hostapd

**Log**
```
greg@xmag:~/repos/vaosp$ m -j16
09:08:14 Build sandboxing disabled due to nsjail error.
build/make/core/config.mk:798: warning: This device does not have Treble enabled. This is unsafe.
build/make/core/config.mk:798: warning: This device does not have Treble enabled. This is unsafe.
============================================
PLATFORM_VERSION_CODENAME=VanillaIceCream
PLATFORM_VERSION=VanillaIceCream
PRODUCT_INCLUDE_TAGS=com.android.mainline mainline_module_prebuilt_nightly
TARGET_PRODUCT=mycar_x86
TARGET_BUILD_VARIANT=userdebug
TARGET_ARCH=x86_64
TARGET_ARCH_VARIANT=x86_64
TARGET_2ND_ARCH_VARIANT=x86_64
HOST_OS=linux
HOST_OS_EXTRA=Linux-6.8.0-52-generic-x86_64-Ubuntu-24.04.1-LTS
HOST_CROSS_OS=windows
BUILD_ID=AD1A.240905.004
OUT_DIR=out
============================================
out/soong/make_vars-mycar_x86.mk was modified, regenerating...
build/make/core/config.mk:798: warning: This device does not have Treble enabled. This is unsafe.
out/soong/make_vars-mycar_x86.mk was modified, regenerating...
[100% 411/411] initializing legacy Make module parser ...
build/make/core/config.mk:798: warning: This device does not have Treble enabled. This is unsafe.
[ 99% 552/553] finishing legacy Make module parsing ...
FAILED: 
external/wpa_supplicant_8/hostapd/Android.mk: error: "hostapd (EXECUTABLES android-x86_64) missing lib_driver_cmd_simulated (STATIC_LIBRARIES android-x86_64)" 
You can set ALLOW_MISSING_DEPENDENCIES=true in your environment if this is intentional, but that may defer real problems until later in the build.
external/wpa_supplicant_8/hostapd/Android.mk: error: "hostapd_noaidl (EXECUTABLES android-x86_64) missing lib_driver_cmd_simulated (STATIC_LIBRARIES android-x86_64)" 
You can set ALLOW_MISSING_DEPENDENCIES=true in your environment if this is intentional, but that may defer real problems until later in the build.
external/wpa_supplicant_8/wpa_supplicant/Android.mk: error: "wpa_supplicant_macsec (EXECUTABLES android-x86_64) missing lib_driver_cmd_simulated (STATIC_LIBRARIES android-x86_64)" 
You can set ALLOW_MISSING_DEPENDENCIES=true in your environment if this is intentional, but that may defer real problems until later in the build.
external/wpa_supplicant_8/wpa_supplicant/Android.mk: error: "wpa_supplicant (EXECUTABLES android-x86_64) missing lib_driver_cmd_simulated (STATIC_LIBRARIES android-x86_64)" 
You can set ALLOW_MISSING_DEPENDENCIES=true in your environment if this is intentional, but that may defer real problems until later in the build.
build/make/core/main.mk:1158: error: exiting from previous errors.
09:09:25 ckati failed with: exit status 1

#### failed to build some targets (01:11 (mm:ss)) ####
```

**Solution**

Wrong definition in device configuration device-mycar_x86.mk, there was incomplete inherit-product value chosen


---
## Compilation interrupted without reason

Decrease amount of cores to use during compilation, e.g. if was `m -j16`, use `m -j8`


---
## launch_cvd fails

**Log**
```
sh: 1: /usr/lib/cuttlefish-common/bin/capability_query.py: not found
```

**Solution**
Install android-cuttlefish:


---
## Cuttlefish Virtual Device doesn't start

```bash
launch_cvd
```

**Log**
```
Caused by:
    0: failed to open virtual socket device /dev/vhost-vsock
    1: Permission denied (os error 13)
```

**Solution**

Add permissions, or check if $USER is in proper group: cvdnetwork, kvm


---
## .ccache read-only

**Log**
```
ccache: error: Failed to create directory /home/grzegorz.michalak/.ccache/tmp: Read-only file system
\nWrite to a read-only file system detected. Possible fixes include
1. Generate file directly to out/ which is ReadWrite, #recommend solution
2. BUILD_BROKEN_SRC_DIR_RW_ALLOWLIST := <my/path/1> <my/path/2> #discouraged, subset of source tree will be RW
3. BUILD_BROKEN_SRC_DIR_IS_WRITABLE := true #highly discouraged, entire source tree will be RW
18:28:15 ninja failed with: exit status 1
```

**Solution**

Add to ~/.bashrc
```
export CCACHE_EXEC=$(which ccache)
export USE_CCACHE=1
export CCACHE_DIR=/mnt/ccache
```

```bash
sudo mkdir /mnt/ccache
sudo mount --bind /home/$USER/.ccache /mnt/ccache
ccache -M 100G -F 0
```
