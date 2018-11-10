# arm_adb

ARM的Android adb源码，基于automake

[![捐赠](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=Q8BH5C48PA9SC)

## 配置编译环境

> 注: 无论是本地编译还是交叉编译，请确保你的gcc/g++版本大于4.9

```bash
sudo apt-get install libtool automake
```
交叉编译环境:
### ARM
```bash
sudo apt-get install linux-libc-dev-armhf-cross libc6-armhf-cross libc6-dev-armhf-cross
```
### AARCH64
```bash
sudo apt-get install linux-libc-dev-arm64-cross libc6-arm64-cross libc6-dev-arm64-cross
```

## 编译运行

### arm机器上编译 

#### 编译并安装openssl
```bash
git clone https://github.com/qhuyduong/openssl-1.0.2l.git
cd openssl-1.0.2l/
./Configure --prefix=/tmp/openssl os/compiler:gcc
make && make install
cd -
```

#### 编译arm_adb
```bash
git clone https://github.com/qhuyduong/arm_adb
cd arm_adb
./configure --includedir=/tmp/openssl/include --libdir=/tmp/openssl/lib
make
```
### arm机器上编译（adb v1.0.40）

#### 安装golang:

```bash
apt install golang
```
#### 编译并安装boringssl:
```bash
git clone https://github.com/qhuyduong/boringssl.git
cd boringssl
mkdir build && cd build
cmake -DCMAKE_ARCHIVE_OUTPUT_DIRECTORY=/tmp/openssl ../
make
make install
```
#### 编译arm_adb:
```bash
git clone https://github.com/qhuyduong/arm_adb -b v1.0.40
cd arm_adb
./configure --includedir=/tmp/openssl/include --libdir=/tmp/openssl
make
```

### 交叉编译
#### 编译并安装Openssl
```bash
git clone https://github.com/qhuyduong/openssl-1.0.2l.git
cd openssl-1.0.2l/
./Configure --prefix=/tmp/openssl os/compiler:$TOOLCHAIN_PREFIX-gcc
make && make install
cd -
```

#### 编译arm_adb
```bash
git clone https://github.com/qhuyduong/arm_adb
cd arm_adb
./configure --host=$TOOLCHAIN_PREFIX --includedir=/tmp/openssl/include --libdir=/tmp/openssl/lib
make
```

## 故障排除
### 1. WARNING: 'aclocal-1.xx' is missing on your system
在配置前执行以下命令：
```bash
autoreconf -i --force
```

## 捐赠

如果该项目对你的开发有帮助, 请原作者喝杯咖啡吧 :)

[![Paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=Q8BH5C48PA9SC)
