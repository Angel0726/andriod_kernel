# 安装环境
```bash
sudo apt-get install git ccache automake flex lzop bison \
gperf build-essential zip curl zlib1g-dev zlib1g-dev:i386 \
g++-multilib python-networkx libxml2-utils bzip2 libbz2-dev \
libbz2-1.0 libghc-bzlib-dev squashfs-tools pngcrush \
schedtool dpkg-dev liblz4-tool make optipng maven libssl-dev \
pwgen libswitch-perl policycoreutils minicom libxml-sax-base-perl \
libxml-simple-perl bc libc6-dev-i386 lib32ncurses5-dev \
x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev xsltproc unzip
```
# 代码
源码&编译工具gcc&编译工具clang  在同一位置
```bash
# 源代码
git clone https://github.com/MiCode/Xiaomi_Kernel_OpenSource.git -b cezanne-r-oss
# 编译工具gcc   版本号 95280bf
git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9 toolgcc
# clang  如果git clone中途中断可以添加 --recursive，添加代理http.proxy="http://127.0.0.1:1082"下载
git clone  --recursive -c http.proxy="http://127.0.0.1:1082" https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86  toolclang
```
# 设置环境
```bash
export ARCH=arm64
export SUBARCH=arm64
# toolgcc中bin文件夹的位置 
export CROSS_COMPILE=${pwd}/toolgcc/bin/aarch64-linux-android-
# 添加环境变量
export PATH=${pwd}/toolgcc/bin:/mnt/d/kernel/toolclang/clang-r433403/bin:$PATH
```
# 编译
```bash
# 进入代码文件夹
cd Xiaomi_Kernel_OpenSource
make CC=clang HOSTCC=gcc AR=llvm-ar NM=llvm-nm OBJCOPY=llvm-objcopy OBJDUMP=llvm-objdump STRIP=llvm-strip O=out CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-android- LD=ld.lld cezanne_user_defconfig
make CC=clang HOSTCC=gcc AR=llvm-ar NM=llvm-nm OBJCOPY=llvm-objcopy OBJDUMP=llvm-objdump STRIP=llvm-strip O=out CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-android- LD=ld.lld -j4
```
或者
```bash
# 进入代码文件夹
cd Xiaomi_Kernel_OpenSource

make CC=clang HOSTCC=gcc AR=llvm-ar NM=llvm-nm OBJCOPY=llvm-objcopy OBJDUMP=llvm-objdump STRIP=llvm-strip O=${pwd}/out CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-android- LD=ld.lld -C ${pwd} M=$(pwd) AUTOCONF_H=${pwd}/out/include/generated/autoconf.h
make CC=clang HOSTCC=gcc AR=llvm-ar NM=llvm-nm OBJCOPY=llvm-objcopy OBJDUMP=llvm-objdump STRIP=llvm-strip O=${pwd}/out CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-android- LD=ld.lld -C ${pwd} M=$(pwd) AUTOCONF_H=${pwd}/out/include/generated/autoconf.h
```

# 参考
[小米官方](https://github.com/MiCode/Xiaomi_Kernel_OpenSource/wiki/How-to-compile-kernel-standalone)
[个人编译](https://gitee.com/erlkonig/xiaomi_kernel_cezanne_r_oss/blob/cezanne-r-oss/kernel_compile_step.txt)
[咨询的人]()
