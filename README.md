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

FIRMWARE_VER=307624caa-dirty
EXTRA_OPTIONS=-D
Setting build parallellism to 8 processes
PLATFORM_NAME=Hikey970 (AARCH64)
PLATFORM_PREBUILD_CMDS=
PLATFORM_BUILDFLAGS= -D FIRMWARE_VER=307624caa-dirty
PLATFORM_BUILDCMD=
PLATFORM_DSC=OpenPlatformPkg/Platforms/Hisilicon/HiKey970/HiKey970.dsc
PLATFORM_ARCH=AARCH64
PLATFORM_PACKAGES_PATH=:/home/kamiyoru/work/c/hikey/hikey970/edk2:
Target: AARCH64
Build: X64
Building Hikey970 (AARCH64) - AARCH64
CROSS_COMPILE="aarch64-linux-gnu-"
hikey970_BUILDFLAGS=' -D FIRMWARE_VER=307624caa-dirty'
PLATFORM_TOOLCHAIN is GCC5
Toolchain prefix: GCC5_AARCH64_PREFIX=aarch64-linux-gnu-
build -n 8 -a "AARCH64" -t GCC5 -p "OpenPlatformPkg/Platforms/Hisilicon/HiKey970/HiKey970.dsc" -b RELEASE  -D FIRMWARE_VER=307624caa-dirty
Build environment: Linux-5.4.0-42-generic-x86_64-with-Ubuntu-18.04-bionic
Build start time: 13:21:07, Aug.24 2020

WORKSPACE        = /home/kamiyoru/work/c/hikey/hikey970/edk2
PACKAGES_PATH    = :/home/kamiyoru/work/c/hikey/hikey970/edk2:
ECP_SOURCE       = /home/kamiyoru/work/c/hikey/hikey970/edk2/EdkCompatibilityPkg
EDK_SOURCE       = /home/kamiyoru/work/c/hikey/hikey970/edk2/EdkCompatibilityPkg
EFI_SOURCE       = /home/kamiyoru/work/c/hikey/hikey970/edk2/EdkCompatibilityPkg
EDK_TOOLS_PATH   = /home/kamiyoru/work/c/hikey/hikey970/edk2/BaseTools
CONF_PATH        = /home/kamiyoru/work/c/hikey/hikey970/edk2/Conf


Architecture(s)  = AARCH64
Build target     = RELEASE
Toolchain        = GCC5

Active Platform          = /home/kamiyoru/work/c/hikey/hikey970/edk2/OpenPlatformPkg/Platforms/Hisilicon/HiKey970/HiKey970.dsc
Flash Image Definition   = /home/kamiyoru/work/c/hikey/hikey970/edk2/OpenPlatformPkg/Platforms/Hisilicon/HiKey970/HiKey970.fdf
Generate Region at Offset 0x0
   Region Size = 0xF0000
   Region Name = FV

Generating FVMAIN_COMPACT FV

Generating FVMAIN FV
###############
Generate Region at Offset 0x0
   Region Size = 0xF0000
   Region Name = FV

GUID cross reference file can be found at /home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC5/FV/Guid.xref

FV Space Information
FVMAIN_COMPACT [60%Full] 983040 total, 599312 used, 383728 free
FVMAIN [99%Full] 3436224 total, 3436208 used, 16 free

- Done -
Build end time: 13:24:03, Aug.24 2020
Build total time: 00:00:19

/home/kamiyoru/work/c/hikey/hikey970/uefi-tools/atf-build.sh -e /home/kamiyoru/work/c/hikey/hikey970/edk2 -t RELEASE_GCC5 hikey970
PLATFORM_NAME=Hikey970
PLATFORM_ARCH=AARCH64
PLATFORM_IMAGE_DIR=HiKey970
PLATFORM_BUILDFLAGS=
Target: AARCH64
Build: X64
Building ARM Trusted Firmware for Hikey970 - RELEASE_GCC5
CROSS_COMPILE="aarch64-linux-gnu-"
BL30=/home/kamiyoru/work/c/hikey/hikey970/edk2/OpenPlatformPkg/Platforms/Hisilicon/HiKey970/Binary/lpm3.img
SCP_BL2=/home/kamiyoru/work/c/hikey/hikey970/edk2/OpenPlatformPkg/Platforms/Hisilicon/HiKey970/Binary/lpm3.img
BL31=
BL32=
BL32_EXTRA1=
BL32_EXTRA2=
BL33=/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC5/FV/BL33_AP_UEFI.fd

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
Copying bl1.bin bl2.bin and fip.bin to /home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC5/FV/
Copying images to '/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC5/FV/':
'build/hikey970/release/bl1.bin' -> '/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC5/FV/bl1.bin'
'build/hikey970/release/bl2.bin' -> '/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC5/FV/bl2.bin'
'build/hikey970/release/fip.bin' -> '/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC5/FV/fip.bin'
------------------------------------------------------------
                               Hikey970 (AARCH64) RELEASE	pass
------------------------------------------------------------
pass	1
fail	0
```
#### Step 2: Install fastboot (Linux)

```bash
sudo apt-get update
sudo apt-get install android-tools-fastboot  # on Debian/Ubuntu
```

or

```bash
sudo yum update
sudo yun install android-tools               # on Fedora, CentOS
```


