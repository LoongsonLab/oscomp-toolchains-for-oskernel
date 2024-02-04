# 工具链合集


## 说明

### gcc交叉编译器
在Release中下载gcc-13.2.0-loongarch64-linux-gnu-nw.tgz， 这是X86_64平台的LoongArch GCC编译器，
在x86_64平台执行，可生产LoongArch架构代码。

### 如何使用交叉编译器
```shell
wget https://github.com/LoongsonLab/oscomp-toolchains-for-oskernel/releases/download/gcc-13.2.0-loongarch64/gcc-13.2.0-loongarch64-linux-gnu-nw.tgz

tar zxf gcc-13.2.0-loongarch64-linux-gnu-nw.tgz

# 在.bashrc中增加交叉编译器路径。假设当前路径为：/opt/gcc-13.2.0-loongarch64-linux-gnu-nw
export PATH=${PATH}:/opt/gcc-13.2.0-loongarch64-linux-gnu-nw/bin

# 如果配置正确，输入如下命令
loongarch64-linux-gnu-gcc -v

#会显示如下：
Using built-in specs.
COLLECT_GCC=loongarch64-linux-gnu-gcc
COLLECT_LTO_WRAPPER=/home/airxs/local/gcc-13.2.0-loongarch64-linux-gnu/bin/../libexec/gcc/loongarch64-linux-gnu/13.2.0/lto-wrapper
Target: loongarch64-linux-gnu
Configured with: ../configure --prefix=/home/airxs/user/gnu/cross-tools --build=x86_64-cross-linux-gnu --host=x86_64-cross-linux-gnu --target=loongarch64-linux-gnu --with-sysroot=/home/airxs/user/gnu/cross-tools/sysroot --with-mpfr=/home/airxs/user/gnu/cross-tools --with-gmp=/home/airxs/user/gnu/cross-tools --with-mpc=/home/airxs/user/gnu/cross-tools --enable-__cxa_atexit --enable-threads=posix --with-system-zlib --enable-libstdcxx-time --enable-checking=release --enable-default-pie --enable-languages=c,c++,fortran,objc,obj-c++,lto
Thread model: posix
Supported LTO compression algorithms: zlib
gcc version 13.2.0 (GCC) 

#编译c文件
loongarch64-linux-gnu-gcc main.c -o mian -static

```

### musl-loongarch64 libc库
musl-loongarch64-1.2.2是LoongArch64的musl c库。它提供了类似于glibc的基础C库，其简短代码风格良好，被广泛使用。其具体可查看官网[musl libc](https://musl.libc.org/)。




### 如何使用musl libc库
musl库只是一个c环境执行库，如果想要使用它，则需要上述的交叉编译器支持。

首先将musl-loongarch64-1.2.2.tgz解压到/opt/musl-loongarch64-1.2.2

```shell

## 在.bashrc中增加环境变量
export PATH=${PATH}:/opt/musl-loongarch64-1.2.2/bin

#可以使用musl libc库
loongarch64-linux-musl-gcc main.c -o main -static

#查看生产的可执行文件类型
file main 

#显示如下：
main: ELF 64-bit LSB executable, LoongArch, version 1 (SYSV), statically linked, with debug_info, not stripped

```






