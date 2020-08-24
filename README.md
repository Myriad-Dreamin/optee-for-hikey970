## OP-TEE for HiKey 970

在根目录文件夹下：

```
make init
```

#### Step1: 编译`edk2`

```
cd build
make edk2
```

期待关键输出：

```

Generate Region at Offset 0x0
   Region Size = 0xF0000
   Region Name = FV

Generating FVMAIN_COMPACT FV
####
Generating FVMAIN FV
####################################
########################################
########################################
########################################
#######
Generate Region at Offset 0x0
   Region Size = 0xF0000
   Region Name = FV

GUID cross reference file can be found at /home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/DEBUG_GCC5/FV/Guid.xref

FV Space Information
FVMAIN_COMPACT [84%Full] 983040 total, 830064 used, 152976 free
FVMAIN [99%Full] 7216960 total, 7216912 used, 48 free

- Done -
Build end time: 12:46:34, Aug.24 2020
Build total time: 00:01:05

/home/kamiyoru/work/c/hikey/hikey970/uefi-tools/atf-build.sh -e /home/kamiyoru/work/c/hikey/hikey970/edk2 -t DEBUG_GCC5 hikey970
PLATFORM_NAME=Hikey970
PLATFORM_ARCH=AARCH64
PLATFORM_IMAGE_DIR=HiKey970
PLATFORM_BUILDFLAGS=
Target: AARCH64
Build: X64
Building ARM Trusted Firmware for Hikey970 - DEBUG_GCC5
CROSS_COMPILE="aarch64-linux-gnu-"
BL30=/home/kamiyoru/work/c/hikey/hikey970/edk2/OpenPlatformPkg/Platforms/Hisilicon/HiKey970/Binary/lpm3.img
SCP_BL2=/home/kamiyoru/work/c/hikey/hikey970/edk2/OpenPlatformPkg/Platforms/Hisilicon/HiKey970/Binary/lpm3.img
BL31=
BL32=
BL32_EXTRA1=
BL32_EXTRA2=
BL33=/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/DEBUG_GCC5/FV/BL33_AP_UEFI.fd

BUILD_TYPE=release
Calling ARM Trusted Firmware build:
CROSS_COMPILE=aarch64-linux-gnu- make -j8 PLAT=hikey970  DEBUG=0  all fip
Built fiptool successfully

Built build/hikey970/release/bl2.bin successfully
Built build/hikey970/release/bl1.bin successfully


  LD      build/hikey970/release/bl31/bl31.elf
  BIN     build/hikey970/release/bl31.bin
  OD      build/hikey970/release/bl31/bl31.dump

Built build/hikey970/release/bl31.bin successfully

Trusted Boot Firmware BL2: offset=0xD8, size=0x4248, cmdline="--tb-fw"
SCP Firmware SCP_BL2: offset=0x4320, size=0x36064, cmdline="--scp-fw"
EL3 Runtime Firmware BL31: offset=0x3A384, size=0x8010, cmdline="--soc-fw"
Non-Trusted Firmware BL33: offset=0x42394, size=0xF0000, cmdline="--nt-fw"

Built build/hikey970/release/fip.bin successfully

make[1]: Leaving directory '/home/kamiyoru/work/c/hikey/hikey970/arm-trusted-firmware'
Copying bl1.bin bl2.bin and fip.bin to /home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/DEBUG_GCC5/FV/
Copying images to '/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/DEBUG_GCC5/FV/':
'build/hikey970/release/bl1.bin' -> '/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/DEBUG_GCC5/FV/bl1.bin'
'build/hikey970/release/bl2.bin' -> '/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/DEBUG_GCC5/FV/bl2.bin'
'build/hikey970/release/fip.bin' -> '/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/DEBUG_GCC5/FV/fip.bin'
------------------------------------------------------------
                               Hikey970 (AARCH64) DEBUG	pass
------------------------------------------------------------
pass	1
fail	0
```

