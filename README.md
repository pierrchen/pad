
# Poplar Android Flash Tool Docker Image

1. donwload

```
git clone xxx ~/poplar_flash_docker
cd poplar_flash_docker
```

1. Build Docker image
```
sudo docker build -t linaro/android_poplar .
```

2. Run the flash tool in the Docker
```
export POPLAR_FLASH_IN=~/poplar_android/out/target/product/poplar
export POPLAR_FLASH_OUT=~/poplar_flash_docker/flash_output
mkdir flash_output      # used for putting the output generated by the flash tool 
./pat
```

`POPLAR_FLASH_IN` points to the ANdriod images genreated by Android build, or prebuilt images.
`POPLAR_FLASH_OUT` is what we just created to put the generated artifacts that will be used to flash with.

3. copy all the stuffs in `~/poplar_flash_docker/flash_output` to a USB disk and following the instructions here to flash.

Notes: currently the Docker image can only flash Android partitions. Actually, for partition tables and bootloader,
you can copy all stuff in [recovery_installer](https://github.com/pierrchen/pat/tree/master/recovery-installer) into usb and flash it directly using the files there.

```
usb reset
fatload usb 0:1 ${scriptaddr} flash_pt.scr;source ${scriptaddr};
fatload usb 0:1 ${scriptaddr} flash_bootloader.scr;source ${scriptaddr};
```