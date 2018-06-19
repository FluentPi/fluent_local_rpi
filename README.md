Local manifests to build LineageOS 14.1 for [Raspberry Pi 3](#).

How to build:
-------------

1. Set up [Android build environment](https://source.android.com/setup/initializing).

2. Install additional packages:

```
sudo apt-get install kpartx python-mako
```

3. Initialize repo:

```
repo init -u git://github.com/FluentOS/fluent_manifest.git -b fluent-1.0
curl --create-dirs -L -o .repo/local_manifests/fluent_manifest-rpi.xml -O -L https://raw.githubusercontent.com/FluentPi/fluent_manifests/fluent-1.0/fluent_manifest-rpi.xml
repo sync
```

4. Apply [patches](https://github.com/FluentPi/fluent_manifest/tree/fluent-1.0/patches):

```
cd path/to/project
git am patchname.patch
```

5. Compile:

```
. build/envsetup.sh
lunch fluent_rpi-userdebug
mka kernel ramdisk systemimage
```

6. Create writable image:

```
cd device/brcm/rpi
sudo ./mkimg.sh
```
