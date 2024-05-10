# 工具链合集


### 1. Rust 相关工具安装

``` shell 
# 获得rustup
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# 获得rust所支持的所有架构相关
rustc --print target-list

# 增加LoongArch架构生成
rustup target add loongarch64-unknown-none

# 增加 cargo-binutils （objcopy, objdump）
cargo install cargo-binutils
rustup component add llvm-tools
```



### 2. GCC交叉编译器

在Release中下载gcc-13.2.0-loongarch64-linux-gnu.tgz， 这是X86_64平台的LoongArch GCC编译器，
在x86_64平台执行，可生产LoongArch架构代码。可以编译C，C++，Objc程序等。



### 3. 如何编译C程序

```shell
wget https://github.com/LoongsonLab/oscomp-toolchains-for-oskernel/releases/download/gcc-13.2.0-loongarch64/gcc-13.2.0-loongarch64-linux-gnu.tgz

tar zxf gcc-13.2.0-loongarch64-linux-gnu.tgz

# 在.bashrc中增加交叉编译器路径。假设当前路径为：/opt/gcc-13.2.0-loongarch64-linux-gnu
export PATH=${PATH}:/opt/gcc-13.2.0-loongarch64-linux-gnu/bin

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



### 4. 如何编译C++程序
GCC交叉编译器中集成了g++工具和相关的c++支持库。可使用如下编译c++程序

```shell
loongarch64-linux-gnu-g++ main.cc -o miancc -static

```



### 5. musl-loongarch64 libc库
musl-loongarch64-1.2.2是LoongArch64的musl c库。它提供了类似于glibc的基础C库，其简短代码风格良好，被广泛使用。其具体可查看官网[musl libc](https://musl.libc.org/)。



### 6. 如何使用musl libc库
musl库只是一个c环境执行库，如果想要使用它，则需要上述的交叉编译器支持。

首先将musl-loongarch64-1.2.2.tgz解压，然后设置环境变量。
```shell
## 解压
tar zxf musl-loongarch64-1.2.2.tgz

## 进入到musl-loongarch64-1.2.2 并且执行设置脚本
cd musl-loongarch64-1.2.2 && ./setup

## 在.bashrc中增加环境变量
export PATH=${PATH}:/xxx/xxx/musl-loongarch64-1.2.2/bin

#可以使用musl libc库
loongarch64-linux-musl-gcc main.c -o main -static

#查看生产的可执行文件类型
file main 

#显示如下：
main: ELF 64-bit LSB executable, LoongArch, version 1 (SYSV), statically linked, with debug_info, not stripped

```


### 工具列表

本仓库所有工具如下表所示：

| 工具名称    | 版本 | 说明    |   文件名称 |
|------|:------:|:------|:------|
|GCC | 13.2.0 | 支持硬件浮点| gcc-13.2.0-loongarch64-linux-gnu.tgz|
|GCC | 13.2.0 | 支持软浮点| gcc-13.2.0-loongarch64-linux-gnu-sf.tgz|
|GCC | 8.3.0  | 支持软浮点，适用于32版本| gcc-8.3.0-loongarch32r-linux-gnusf.tgz|
|MUSL | 1.2.2 | C库 | musl-loongarch64-1.2.2.tgz|
|Qemu | 8.2.50 | 模拟器 | qemu.tgz|
|GDB | 12.0.50 | 执行于x86_64的loongarch64-gdb | loongarch64-linux-gnu-gdb.tgz|



