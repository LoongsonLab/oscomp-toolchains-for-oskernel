# 工具链合集


## 说明


### gcc-8.3.0
gcc-8.3.0-loongarch64-linux-gnu-rc1.1.novec.tgz 为LoongArch64的交叉编译器，
里面集成了openssl的库。此工具链是**非向量版本**。此版本是旧世界的编译器。

关于新旧世界编译器的区别在于：新世界使用了新的ABI，而旧世界则沿用之前的接口。


### gcc-13.2.0
在Release中下载gcc-13.2.0-loongarch64-linux-gnu-nw.tgz， 其是新世界的交叉编译器。


### musl-gcc
musl-gcc.tgz是使用了musl c库的交叉编译器，在链接阶段，会使用musl的相关libc等


### 如何使用
解压后，设置好环境变量即可使用：


```shell

loongarch64-linux-gnu-gcc main.c -o mian -static

```







