# 安装

## 目录

* [平台](#平台)
* [获取源代码](#获取源代码)
* [依赖](#依赖)
  * [Linux 依赖](#linux-依赖)
  * [Windows 依赖](#windows-依赖)
  * [MacOS 依赖](#macos-依赖)
* [编译](#编译)
  * [Linux 说明](#linux-说明)
  * [Windows 说明](#windows-说明)
  * [MacOS 说明](#macos-说明)
  * [Android 说明](#android-说明)
* [安装程序](#安装程序)

## 平台

你可以从[官网](https://libresprite.github.io/)下载安装包。
如果你想从源码编译 LibreSprite，请继续阅读。

你应该可以在以下平台编译 LibreSprite：

* Windows 10 + VS2015 Community Edition + Windows 10 SDK
* Mac OS X 11.0 Big Sur + Xcode 7.3 + OS X 11.0 SDK
* Linux + GCC 8.5 或更高版本（支持 C++14）

编译 LibreSprite 需要：

* [CMake](http://www.cmake.org/)（3.4 或更高）
* [Ninja](https://ninja-build.org)
* [Msys2](https://www.msys2.org/)（仅 Windows）

## 获取源代码

使用以下命令克隆仓库及其子模块：

    git clone --recursive https://github.com/LibreSprite/LibreSprite

（Windows 上可使用 [Git for Windows](https://git-for-windows.github.io/) 克隆仓库。）

如需更新已有克隆，使用以下命令：

    cd LibreSprite
    git pull
    git submodule update --init --recursive

## 依赖

编译 LibreSprite 需要以下依赖：

### Linux 依赖

Debian/Ubuntu:

    sudo apt-get install cmake g++ libcurl4-gnutls-dev libfreetype6-dev libgif-dev libgtest-dev libjpeg-dev libpixman-1-dev libpng-dev libsdl2-dev libsdl2-image-dev libtinyxml2-dev libnode-dev ninja-build zlib1g-dev libarchive-dev

Fedora:

    sudo dnf install g++ cmake libcurl-devel freetype-devel giflib-devel gtest-devel libjpeg-devel pixman-devel libpng-devel SDL2-devel SDL2_image-devel tinyxml2-devel zlib-devel ninja-build nodejs-devel libarchive-devel

### Windows 依赖

使用 msys2 安装所需依赖，请在 mingw32 中运行：

    pacman -S base-devel mingw-w64-i686-gcc mingw-w64-i686-cmake mingw-w64-i686-make mingw-w64-i686-curl mingw-w64-i686-freetype mingw-w64-i686-giflib mingw-w64-i686-libjpeg-turbo mingw-w64-i686-libpng mingw-w64-i686-libwebp mingw-w64-i686-pixman mingw-w64-i686-SDL2 mingw-w64-i686-SDL2_image mingw-w64-i686-tinyxml2 mingw-w64-i686-v8 mingw-w64-i686-zlib mingw-w64-i686-libarchive

个人踩坑避坑指南：
> 如果你使用上述的命令出现报错，并且你知道自己的系统是64位的，请使用下方的命令

```
pacman -S base-devel mingw-w64-ucrt-x86_64-gcc mingw-w64-ucrt-x86_64-cmake mingw-w64-ucrt-x86_64-make mingw-w64-ucrt-x86_64-curl mingw-w64-ucrt-x86_64-freetype mingw-w64-ucrt-x86_64-giflib mingw-w64-ucrt-x86_64-libjpeg-turbo mingw-w64-ucrt-x86_64-libpng mingw-w64-ucrt-x86_64-libwebp mingw-w64-ucrt-x86_64-pixman mingw-w64-ucrt-x86_64-SDL2 mingw-w64-ucrt-x86_64-SDL2_image mingw-w64-ucrt-x86_64-tinyxml2 mingw-w64-ucrt-x86_64-v8 mingw-w64-ucrt-x86_64-zlib mingw-w64-ucrt-x86_64-libarchive
```

### MacOS 依赖

在 MacOS 上你需要 Mac OS X 11.0 SDK 和对应的 Xcode。
在终端中用 brew 安装依赖：

    brew install gnutls freetype jpeg webp pixman sdl2 sdl2_image tinyxml2 libarchive v8 ninja zlib xmlto dylibbundler cmake

## 编译

首先用以下命令创建 `build` 目录：

    cd LibreSprite
    mkdir build
    cd build

然后根据下方的平台说明进行编译。

编译结果会输出到 `build` 目录。
如果想重新编译一个干净版本，请删除 `build` 目录后重新编译。

### Linux 说明

编译 LibreSprite，请运行以下命令：

    cmake -G Ninja ..
    ninja libresprite

### Windows 说明

请在 mingw32.exe 中运行：

    cmake -G Ninja ..

### MacOS 说明

编译 LibreSprite，请运行以下命令：
```
    cmake \
      -DCMAKE_OSX_SYSROOT=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk \
      -G Ninja \
      ..
    ninja libresprite
```
### Android 说明

在构建 Android 版本之前，你必须先为你的操作系统完成一次原生构建，
请按上面的说明操作。完成后，将
https://github.com/LibreSprite/ls-android-deps
下载为 LibreSprite 目录下的 `android/`。然后你可以在 Android Studio
中打开 android 子目录并构建 LibreSprite 的 Android 版本。


## 安装程序

编译完成后，可以在 `build` 目录运行以下命令安装 LibreSprite：

    ninja install
