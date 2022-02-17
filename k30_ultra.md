# 安装环境
```bash
# zlib1g-dev:i386、python-networkx没有安装包所以没有安装
sudo apt-get install git ccache automake flex lzop bison \
gperf build-essential zip curl zlib1g-dev  \
g++-multilib  libxml2-utils bzip2 libbz2-dev \
libbz2-1.0 libghc-bzlib-dev squashfs-tools pngcrush \
schedtool dpkg-dev liblz4-tool make optipng maven libssl-dev \
pwgen libswitch-perl policycoreutils minicom libxml-sax-base-perl \
libxml-simple-perl bc libc6-dev-i386 lib32ncurses5-dev \
x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev xsltproc unzip
```
# 代码
源码&编译工具gcc&编译工具clang  在同一位置.当前目录中包括以下3个文件夹
- toolgcc：需要回退到95280
- toolclang：需要回退到b800f
- Xiaomi_Kernel_OpenSource：小米源代码
```bash
# 当前目录
export source_dir=${PWD}
# 源代码
git clone https://github.com/MiCode/Xiaomi_Kernel_OpenSource.git -b cezanne-r-oss
# 编译工具gcc   版本号 95280bf
git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9 toolgcc
cd toolgcc && git reset --hard 95280   # 最新版本没有gcc。所以要回退到95280
cd $source_dir #回退完之后，返回上一层目录
# clang  如果git clone中途中断可以添加 --recursive，添加代理http.proxy="http://127.0.0.1:1082"下载
git clone  --recursive -c http.proxy="http://127.0.0.1:1082" https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86  toolclang
cd toolclang && git reset --hard b800f   # 最新版本没有r383902。所以要回退到b800f
```
# 设置环境
添加环境变量。因为使用了${PWD}命令，所以需要在原始目录添加环境变量。
```bash
export ARCH=arm64
export SUBARCH=arm64
# toolgcc中bin文件夹的位置 
export CROSS_COMPILE=${source_dir}/toolgcc/bin/aarch64-linux-android-
# 添加环境变量    clang版本号b800f
export PATH=${source_dir}/toolgcc/bin:${source_dir}/toolclang/clang-r383902/bin:$PATH
```
# 编译
```bash
# 进入代码文件夹
cd $source_dir/Xiaomi_Kernel_OpenSource
ARCH=arm64 make CC=clang HOSTCC=gcc AR=llvm-ar NM=llvm-nm OBJCOPY=llvm-objcopy OBJDUMP=llvm-objdump STRIP=llvm-strip O=out CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-android- LD=ld.lld cezanne_user_defconfig
ARCH=arm64 make CC=clang HOSTCC=gcc AR=llvm-ar NM=llvm-nm OBJCOPY=llvm-objcopy OBJDUMP=llvm-objdump STRIP=llvm-strip O=out CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-android- LD=ld.lld -j4
```
## MTK编译
```bash
# 进入代码文件夹
cd Xiaomi_Kernel_OpenSource

make CC=clang HOSTCC=gcc AR=llvm-ar NM=llvm-nm OBJCOPY=llvm-objcopy OBJDUMP=llvm-objdump STRIP=llvm-strip O=${PWD}/out CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-android- LD=ld.lld -C ${PWD} M=$(PWD) AUTOCONF_H=${PWD}/out/include/generated/autoconf.h
make CC=clang HOSTCC=gcc AR=llvm-ar NM=llvm-nm OBJCOPY=llvm-objcopy OBJDUMP=llvm-objdump STRIP=llvm-strip O=${PWD}/out CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-android- LD=ld.lld -C ${PWD} M=$(PWD) AUTOCONF_H=${PWD}/out/include/generated/autoconf.h
```

# 参考
[小米官方](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/wiki/How-to-compile-kernel-standalone)
[个人编译](https://gitee.com/erlkonig/xiaomi_kernel_cezanne_r_oss/blob/cezanne-r-oss/kernel_compile_step.txt)
[咨询的人]()
