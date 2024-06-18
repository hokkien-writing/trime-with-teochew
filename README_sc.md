# 同文输入法伴潮州话打字方案(trime-with-teochew)

附带[潮州话打字方案](https://github.com/hokkien-writing/rime-teochew)的同文输入法，适用于 Android平台 (TRIME IM for Android with rime-teochew schema)。

[潮语文](README.md) | 简体中文

## 源起

本项目是为方便大家在 Android上使用[潮州话打字方案](https://github.com/hokkien-writing/rime-teochew)进行打字而设立。

同文输入法是一款开源的 Android输入法，它基于 RIME引擎，可定制各种打字方案，为地方语言的存续作出了不小的贡献。

不过，配置这款输入法也不是件简单的事。复杂的配置是它的特色，也是令很多普通人头痛的问题。

好在，我会懂一些 Android 开发，花费几天的时间和精力，创设了此个项目，打包了内置潮州打字方案的同文输入法。

若是你想用他的打字方案，可照我下面的方式打包。

## 下载

转 [Release](https://github.com/hokkien-writing/trime-with-teochew/releases) 页面下载。

## 打包

## 环境准备

1. 安装 Android Studio。
2. 安装 JDK (OpenJDK) 17。

### 拖取代码

为稳定起见，一般使用最新版本的上一个版本，现在最新是 v3.2.18，所以这里使用 v3.2.17。

```bash
git clone git@github.com:osfans/trime.git
git checkout v3.2.17
git submodule update --init --recursive
```

### 整合配置

```bash
# 请将下面的配置换成自己的
TRIME_DIR=~/Desktop/trime/
SCHEMA_NAME=rime-teochew
SCHEMA_URL=https://github.com/hokkien-writing/rime-teochew.git

# 创建工作目录
rm -rf "workdir/$SCHEMA_NAME"
mkdir -p "workdir/$SCHEMA_NAME"
cd workdir || return

# 下载并解压 rimerc-trime
curl -LO https://github.com/Bambooin/rimerc/releases/download/v0.1.7/rimerc-trime-v0.1.7.zip
unzip rimerc-trime-v0.1.7.zip

# 下载打字方案并复制到trime目录
git clone --depth 1 "$SCHEMA_URL"
cp "$SCHEMA_NAME/*.yaml" trime

# 复制所有配置文件到 TRIME_DIR
cp -rf trime/* "$TRIME_DIR/app/src/main/assets/rime"
```

### 打包调试版

```bash
# On Linux or macOS
make debug

# On Windows
.\gradlew assembleDebug
```

### 打包正式版

在 Andoroid Studio 中，`Build` => `Generate Signed App Bundle / APK... `。

## 致谢

1. [osfans/trime](https://github.com/osfans/trime)
2. [Bambooin/rimerc](https://github.com/Bambooin/rimerc)
3. [RIME](https://rime.im/)
4. [潮州话打字方案](https://github.com/hokkien-writing/rime-teochew)
5. [【朙月拼音】输入方案](https://github.com/rime/rime-luna-pinyin)
