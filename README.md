





# Adreno && Mali OpenCL GPU && aarch64 CPU miner for android

>> Original developers

This code is provided entirely free of charge by the programmer in his spare
time so donations would be greatly appreciated. Please consider donating to the
address below.

Con Kolivas <kernel@kolivas.org>
15qSxP1SQcUX3o4nhkfdbgyoWEFMomJ4rZ

GIT TREE:

https://github.com/ckolivas/cgminer

Support thread:

http://bitcointalk.org/index.php?topic=28402.0

IRC Channel:

irc://irc.freenode.net/cgminer 

Forked from https://github.com/JordanRulz/cgminer.git

# warning

# This Projects have no warranty, so everyone use your own risk

> building dependency 
`pkg up && pkg upg && pkg i build-essential libtool cmake yasm make wget git libjansson libgmp opencl-headers libmicrohttpd libuv* clang binutils`

android pthread-cancel not supported , for android you shoud install `libbthread`

```
git clone https://github.com/tux-mind/libbthread

cd libbthread

autoreconf -i

nano bthread.h
```

under `<bthread.h>` add `#include <pthread.h>`

then run

```
./configure --prefix$PREFIX

make install
```
then install `gcc` because `clang` cannot compile `cgminer-android`

```

curl -LO https://its-pointless.github.io/setup-pointless-repo.sh

pkg i gcc-11 libgccjit-11-dev

```

now you should install OpenCL driver for (Adreno && Arm-Mali)


```
Adreno

ln -s /system/vendor/lib64/libOpenCL.so $PREFIX/lib/libOpenCL.so

ARM-Mali

ln -s /system/vendor/lib64/egl/libmali.so $PREFIX/lib/libOpenCL.so

```

add OPENCL LIB  PATH to .bashrc

```
nano ~/.bashrc

export LD_LIBRARY_PATH=$PREFIX/lib:/vendor/lib64:/vendor/lib64/egl
```

press `control+x` then type `y` exit from termux && re-open termux

> dependency build completed 

> now install the miner


```
git clone https://github.com/Saikatsaha1996/cgminer-android.git

cd cgminer-android

setupgcc-11 && setup-patchforgcc

autoreconf -i

CFLAGS="-O3 -march=armv8-a+crypto -mtune=cortex-a73" ./configure --enable-cpumining --enable-scrypt --disable-adl

```

now you can see in your screen `OPENCL FOUND && GPU MINING SUPPORT ENABLED`

now just run `make -j4`


now start mining `./cgminer -a scrypt -o stratum+tcp://scrypt.asia.mine.zergpool.com:3433 -u dgb1q805va2mff2umrtfg5qx5k0xh2l2lzupq4n9a4r -p c=DGB -I 1 -w 6 -d 0 --thread-concurrency 80`


for more info `./cgminer --help`

![Screenshot_2022-05-24-06-22-39-335_com termux](https://user-images.githubusercontent.com/72664192/170066315-6886791b-690c-493b-9bd0-e15986ade1ff.jpg)

