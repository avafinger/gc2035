GC2035 (Experimental)
=====================

This is my modified GC2035 driver for the H3 that incorporates many image resolutions and/or image quality.
You can take advantage of a higher FPS, Image Quality or Window size, choosing the one that best fit your needs.

You load the driver and pass a parameter for the best case you need:

hres=0 => 640x480|1280x720|1600x1200 and 15 fps (good light condition), 640x480 good quality

hres=1 => 800x600|1600x1200 and 10 fps (good light condition), 800x600 good quality

hres=2 => 320x240|640x480|800x600 and 20 fps (good light condition), 640x480 medium quality

hres=3 => 320x240|352x288|640x480 and 15 fps (good light condition), low quality, cropped to this window sizes

Loading the driver:

modprobe gc2035 hres=1

or

modprobe gc2035 hres=0 (or simply modprobe gc2035 without parameter)

or

modprobe gc2035 hres=2


Sample:

modprobe gc2035 hres=1

modprobe vfe_v4l2



You can test other formats unloading the driver in reverse order:

modprobe -r -v vfe_v4l2

modprobe -r -v gc2035


Tip
===

For best quality/performance, load the driver with this: modprobe gc2035 hres=0 mclk=34
The drawback is you should not change window size on the fly (without unloading the driver)

Now load the drivers with the new parameters.

Building from source (BSP example)
====================

If your preferred distro does not provide the modified driver you can build it yourself.

git clone https://github.com/avafinger/gc2035.git

copy file gc2035.c to:

  drivers/media/video/sunxi-vfe/device


compile: 

make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j2 INSTALL_MOD_PATH=output SUBDIRS=drivers/media/video/sunxi-vfe/device modules
  CC [M]  drivers/media/video/sunxi-vfe/device/gc2035.o
  Building modules, stage 2.
  MODPOST 40 modules
  CC      drivers/media/video/sunxi-vfe/device/gc2035.mod.o
  LD [M]  drivers/media/video/sunxi-vfe/device/gc2035.ko

Driver will be in:

  output/lib/modules/3.4.39/kernel/drivers/media/video/sunxi-vfe/device/gc2035.ko


copy the file to: 

  /lib/modules/3.4.39/kernel/drivers/media/video/sunxi-vfe/device/.



