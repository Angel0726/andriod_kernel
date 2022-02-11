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
# 必须用python，将python链接到python3
sudo ln -s /usr/bin/python3 /usr/bin/python
```
# 下载编译工具
```
git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9 toolgcc
git clone  --recursive -c http.proxy="http://127.0.0.1:1082" https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86  toolclang
git clone https://android.googlesource.com/platform/prebuilts/build-tools;
```

# 编译环境


|                                                         |                                                              | google-gcc | google-clang | build-tools |      |
| ------------------------------------------------------- | ------------------------------------------------------------ | ---------- | ------------ | ----------- | ---- |
| [k30_ultra](k30_ultra.md)                               | R                                                            | 95280      | b800f        |             |      |
| [realme_6pro_7pro_8pro_X2](realme_6pro_7pro_8pro_X2.md) | [R](https://github.com/realme-kernel-opensource/realme_6pro_7pro_8pro_X2-AndroidR-kernel-source/blob/master/How-To-Compile) | 95280      | b800f        |             |      |
|                                                         |                                                              |            |              |             |      |



如何编译andriod教程
honor8: https://github.com/Angel0726/android_kernel_hisi_hi3650

# [编译问题](编译问题.md)
