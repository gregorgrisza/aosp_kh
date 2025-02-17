# Custom MyCar

## Setup
### Environment
Ref.: https://source.android.com/docs/setup/start/requirements

```bash
sudo apt update
sudo apt install git-core gnupg flex bison build-essential zip curl zlib1g-dev libc6-dev-i386 x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig libncurses-dev software-properties-common repo ccache

# Configure ccache
mkdir -p ~/.ccache
ccache -M 50G -F 0

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
