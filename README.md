
WAYS TO EDIT DEVICE TREE (NOT OVERLAYS)

 1. EDIT DEVICE TREE DIRECTLY

#1) edit dts files in below directrory and recompile kernel with step 2.

$cd /home/tarak/bbb/build/tmp/work-shared/beaglebone/kernel-source/arch/arm/boot/dts

#2) use this command for recompiling kernel.

$bitbake -c menuconfig virtual/kernel
$bitbake core-image-sato
#---------------------------------------------------------------------------------------------------------------------------#

2. DO IT IN A PROPER WAY

1) Create empty yocto layer ( and meta-(name) dir will be created) and add by following command. 

$yocto-layer create meta-(name) 

$bitbake-layers add-layer meta-(name)

#2) Use this command and replace ~/bbb/meta-(name) with your desired meta-layer and specify your dts path and name your dts file bellow

$recipetool appendsrcfile -wm beaglebone ~/bbb/meta-(name)/ virtual/kernel path/to/am335x-boneblack.dts \ 'arch//boot/dts/am335x-boneblack.dts'


#3) configure kernel and bibake whatever your want

$bitbake -c menuconfig virtual/kernel
$bitbake core-image-sato

#4) Edit uEnv.txt and assign that file to fdt file and enjoy


*NOTE 
THIS IS NOT OVERLAY FILE YOU NEED TO SPECIFY AND SET DT ACCORDINGLY i.e, specify bus and pins don't use _overlay_ keyword.
AND sanity file is needed otherwise it will fail for sanity check and the whole yocto will go insane and try to connect with www.example.com!!!!
Please see two dts file in meta-lpcmod/linux/linux-stable/beaglebone/ you will get the idea and also try to run in your build modprobe lpcspi and see it works.
