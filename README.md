# Custom MyCar

## Setup
### Environment
Ref.: https://source.android.com/docs/setup/start/requirements

```bash
sudo apt update
sudo apt install git-core gnupg flex bison build-essential zip curl zlib1g-dev libc6-dev-i386 x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig libncurses-dev software-properties-common repo ccache python3 python-is-python3 python3-pyqt5 python3-pip python3-protobuf python3-ply

# Configure ccache
mkdir -p ~/.ccache
ccache -M 50G -F 0
```

Install Bazel: https://bazel.build/install/ubuntu#install-on-ubuntu

```bash
# Install android-cuttlefish
git clone git@github.com:google/android-cuttlefish.git
cd android-cuttlefish && tools/buildutils/build_packages.sh

sudo dpkg -i ./cuttlefish-base_*_*64.deb || sudo apt-get install -f
sudo dpkg -i ./cuttlefish-user_*_*64.deb || sudo apt-get install -f
sudo usermod -aG kvm,cvdnetwork,render $USER
```

Update ~/.bashrc

```bash
echo """

export USE_CCACHE=1
export CCACHE_EXEC=$(which ccache)

""" >> ~/.bashrc
```

### Repository

```bash
mkdir $HOME/vaosp && cd $HOME/vaosp
repo init -u git@github.com:gregorgrisza/aosp_manifests.git
repo sync -j$(nproc)
. ./build/envsetup.sh
lunch
```

If `lunch` doesn't list targets:
```bash
export TARGET_RELEASE=trunk_staging
build_build_var_cache
```

### Development environment

#### Android Studio for Platform

1. Use IDEGen to generate android.ipr project file. Instruction can be found at: [development/tools/idegen/README](https://android.googlesource.com/platform/development/+/refs/heads/main/tools/idegen/README)

    ```bash
    cd $AOSP
    m idegen
    . development/tools/idegen/idegen.sh
    ```
    Import generated `$AOSP/android.ipr` in Android Studio

1.

## Goal

## VHAL extension

Add custom vendor VHAL property

ID: 557899439, (0x2140DEAF)
```
/**
 * Extension of VehicleProperty enum declared in Vehicle HAL 2.0
 */
enum VehicleProperty: android.hardware.automotive.vehicle@2.0::VehicleProperty {

    /**
     * For research needs 1s counter
     *
     * @change_mode VehiclePropertyChangeMode:ON_CHANGE
     * @access VehiclePropertyAccess:READ
     * @data_enum VendorInteriorLightning
     */
    VENDOR_INTERIOR_LIGHTNING = (
      0xDEAF
      | VehiclePropertyGroup:VENDOR
      | VehiclePropertyType:INT32
      | VehicleArea:GLOBAL),

};

/**
 * Used by VENDOR_INTERIOR_LIGHTNING.
 */
enum VendorInteriorLightning : int32_t {
    // Type is unknown or not in the list below.
    UNKNOWN = 0,
    THEME_BLUE = 1,
    THEME_GREEN = 2,
    THEME_YELLOW = 3,
};
``` 
