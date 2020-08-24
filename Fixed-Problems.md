

#### 方便使用http代理

如果需要走git协议，请将`https://git.savannah.gnu.org/git`替换为`git://git.savannah.gnu.org`

```xml
<!--fetch="git://git.savannah.gnu.org"-->
<remote name="savannah" fetch="https://git.savannah.gnu.org/git" />
```

#### EDK2 build.py报1005错误

```plain
build.py...
 : error 1005: Not supported target [platform/hisilicon/hikey970/hikey970.dsc].
	Please select one of: all genc genmake modules libraries fds clean cleanall cleanlib run

- Failed -
```

遇到这种错误请查看输出的环境变量：

```plain
Setting build parallellism to 8 processes
PLATFORM_NAME=Hikey970 (AARCH64)
PLATFORM_PREBUILD_CMDS=
PLATFORM_BUILDFLAGS= -D FIRMWARE_VER=307624caa
PLATFORM_BUILDCMD=
PLATFORM_DSC=Platform/Hisilicon/HiKey970/HiKey970.dsc
PLATFORM_ARCH=AARCH64
PLATFORM_PACKAGES_PATH=:/home/kamiyoru/work/c/hikey/hikey970/edk2:
Target: AARCH64
Build: X64
Building Hikey970 (AARCH64) - AARCH64
CROSS_COMPILE="aarch64-linux-gnu-"
hikey970_BUILDFLAGS=' -D FIRMWARE_VER=307624caa'
PLATFORM_TOOLCHAIN is  # here
Toolchain prefix: _AARCH64_PREFIX=aarch64-linux-gnu-
```

由于`PLATFORM_TOOLCHAIN`未识别，可能是1005错误产生的原因之一。

解决办法：

让gcc交叉编译器全局可访问，例如`_AARCH64_PREFIX=aarch64-linux-gnu-`，则将`aarch64`编译器bin路径加入`PATH`，使得`aarch64-linux-gnu-gcc`全局可访问。

#### EDK2 build.py报000E错误

```
build.py...
 : error 000E: File/directory not found in workspace
	Platform/Hisilicon/HiKey970/HiKey970.dsc is not found in packages path:
	.
	/home/kamiyoru/work/c/hikey/hikey970/edk2/.
	.
- Failed -
```

在`uefi-tools`中有两套平台配置，其中`edk2-platforms.config`是V2配置，`platforms.config`是V1配置，这里面的路径配置不一致。

解决办法：

如果你需要V1配置，请添加`-c path/to/uefi-tools/platforms.config`到edk2-build.sh选项。

如果你需要V2配置，请修改config中两个参数。

```ini
[hikey970]
DSC=OpenPlatformPkg/Platforms/Hisilicon/HiKey970/HiKey970.dsc
SCP_BIN=OpenPlatformPkg/Platforms/Hisilicon/HiKey970/Binary/lpm3.img
```

#### Compile Failed

###### Bad definition for symbol '<unknown>'@0 or unsupported symbol type

```
GenFw: ERROR 3000: Invalid
make[1]: *** [/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC5/AARCH64/MdeModulePkg/Core/RuntimeDxe/RuntimeDxe/DEBUG/RuntimeDxe.efi] Error 1
  /home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC5/AARCH64/MdeModulePkg/Core/RuntimeDxe/RuntimeDxe/DEBUG/RuntimeDxe.dll: Bad definition for symbol '<unknown>'@0 or unsupported symbol type.  For example, absolute and undefined symbols are not supported.
GNUmakefile:364: recipe for tar

GenFw: ERROR 3000: Invalid
  /home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC49/AARCH64/ArmPlatformPkg/PrePi/PeiUniCore/DEBUG/ArmPlatformPrePiUniCore.dll: Bad definition for symbol '<unknown>'@0 or unsupported symbol type.  For example, absolute and undefined symbols are not supported.
GNUmakefile:404: recipe for target '/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC49/AARCH64/ArmPlatformPkg/PrePi/PeiUniCore/DEBUG/ArmPlatformPrePiUniCore.efi' failed
make[1]: *** [/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC49/AARCH64/ArmPlatformPkg/PrePi/PeiUniCore/DEBUG/ArmPlatformPrePiUniCore.efi] Error 1
make[1]: Leaving directory '/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/RELEASE_GCC49/AARCH64/ArmPlatformPkg/PrePi/PeiUniCore'
```

强制修改编译版本为`DEBUG`可能解决此问题。

###### AARCH64 small code model requires identical ELF and PE/COFF section offsets modulo 4 KB. 

```
GenFw: ERROR 3000: Invalid
  WriteSections64(): /home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/DEBUG_GCC5/AARCH64/ArmPlatformPkg/PrePi/PeiUniCore/DEBUG/ArmPlatformPrePiUniCore.dll AARCH64 relative relocations require identical ELF and PE/COFF section offsets
GenFw: ERROR 3000: Invalid
  WriteSections64(): /home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/DEBUG_GCC5/AARCH64/ArmPlatformPkg/PrePi/PeiUniCore/DEBUG/ArmPlatformPrePiUniCore.dll AARCH64 small code model requires identical ELF and PE/COFF section offsets modulo 4 KB.
make[1]: *** [/home/kamiyoru/work/c/hikey/hikey970/edk2/Build/HiKey970/DEBUG_GCC5/AARCH64/ArmPlatformPkg/PrePi/PeiUniCore/DEBUG/ArmPlatformPrePiUniCore.efi] Error 1
```


根据[tianocore-edk2-cbf0065](https://github.com/tianocore/edk2/commit/cbf00651eda6818ca3c76115b8a18e3f6b23eef4)，在第4344行修改：

```
DEFINE GCC_AARCH64_CC_FLAGS        = DEF(GCC_ALL_CC_FLAGS) -mlittle-endian -fno-short-enums -fverbose-asm -funsigned-char  -ffunction-sections -fdata-sections -fno-builtin -Wno-address -fno-asynchronous-unwind-tables
```

为

```
DEFINE GCC_AARCH64_CC_FLAGS        = DEF(GCC_ALL_CC_FLAGS) -mlittle-endian -fno-short-enums -fverbose-asm -funsigned-char  -ffunction-sections -fdata-sections -fno-builtin -Wno-address -fno-asynchronous-unwind-tables -fno-unwind-tables
```

#### Brotli Error

```
gcc: error: brotli/c/tools/brotli.o: No such file or directory
gcc: error: brotli/c/common/dictionary.o: No such file or directory
gcc: error: brotli/c/common/transform.o: No such file or directory
gcc: error: brotli/c/dec/bit_reader.o: No such file or directory
gcc: error: brotli/c/dec/decode.o: No such file or directory
gcc: error: brotli/c/dec/huffman.o: No such file or directory
gcc: error: brotli/c/dec/state.o: No such file or directory
gcc: error: brotli/c/enc/backward_references.o: No such file or directory
gcc: error: brotli/c/enc/backward_references_hq.o: No such file or directory
gcc: error: brotli/c/enc/bit_cost.o: No such file or directory
gcc: error: brotli/c/enc/block_splitter.o: No such file or directory
gcc: error: brotli/c/enc/brotli_bit_stream.o: No such file or directory
gcc: error: brotli/c/enc/cluster.o: No such file or directory
gcc: error: brotli/c/enc/compress_fragment.o: No such file or directory
gcc: error: brotli/c/enc/compress_fragment_two_pass.o: No such file or directory
gcc: error: brotli/c/enc/dictionary_hash.o: No such file or directory
gcc: error: brotli/c/enc/encode.o: No such file or directory
gcc: error: brotli/c/enc/encoder_dict.o: No such file or directory
gcc: error: brotli/c/enc/entropy_encode.o: No such file or directory
gcc: error: brotli/c/enc/histogram.o: No such file or directory
gcc: error: brotli/c/enc/literal_cost.o: No such file or directory
gcc: error: brotli/c/enc/memory.o: No such file or directory
gcc: error: brotli/c/enc/metablock.o: No such file or directory
gcc: error: brotli/c/enc/static_dict.o: No such file or directory
gcc: error: brotli/c/enc/utf8_util.o: No such file or directory
```

说明库不存在，使用下面方式下载库

```
git submodule update --init
```
