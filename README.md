# Custom MyCar

## Setup

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
