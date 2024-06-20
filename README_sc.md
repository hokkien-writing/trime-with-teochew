# 同文输入法伴潮州话打字方案(trime-with-teochew)

附带[潮州话打字方案](https://github.com/hokkien-writing/rime-teochew)的同文输入法，适用于 Android平台 (TRIME IM for Android with rime-teochew schema)。

[潮语文](README.md) | 简体中文

## 源起

以前，我介绍过如何在 iPhone手机上用潮州话打字。后来，收到一些读者反馈，其中有部分读者希望在 Android手机上也能安装即用潮州话打字。

本人照了一支 Android手机按照网上教程亲自操作了一遍，发现同文输入法的配置相当复杂，且经常出问题，连我这懂一些 Android开发的人都没心情搞了，何况普通人？

> 📌 同文输入法是一款开源的 Android输入法，它基于 RIME引擎，可定制各种打字方案，为地方语言的存续作出了不小的贡献。不过灵活定制意味着配置很复杂，普通人看了头疼。

好彩，我花费了几天的时间和精力，创设了这个项目，打包了内置潮州打字方案的同文输入法，实现免配置、安装即用潮州话打字 🎉。

## 下载

现在大家舒服了，只要在 [腾讯微云](https://share.weiyun.com/yxVJfsN7) 、 [微软云盘](https://1drv.ms/f/s!AgqX3Jd3VLa4gS3ujqPC7hpY4lKt?e=Wc8xvk)  或者 [GitHub Release](https://github.com/hokkien-writing/trime-with-teochew/releases) 下载同文输入法潮州话定制版，然后按照下底视频方式安装即用。

## 打包

如果你想要自己打包，添加新的打字方案或使用更新版本的同文输入法，可按照我下面的方式来操作。

### 环境准备

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
# 請掠下底配置換成家己其
TRIME_DIR=~/Desktop/trime/
SCHEMA_NAME=rime-teochew
SCHEMA_URL=https://github.com/hokkien-writing/rime-teochew.git

# 創建工作文件夾
rm -rf "workdir/trime"
mkdir -p "workdir/trime"
cd workdir || return

# 下載並解壓 rimerc-trime
mkdir rimerc-trime
curl -LO https://github.com/Bambooin/rimerc/releases/download/v0.1.7/rimerc-trime-v0.1.7.zip
unzip rimerc-trime-v0.1.7.zip -d rimerc-trime
find rimerc-trime/trime/* -type f ! -name "luna*" -exec cp {} trime \;

# 下載朙月拼音
git clone https://github.com/rime/rime-luna-pinyin.git
cp rime-luna-pinyin/*.yaml trime

# 下載五筆畫
git clone https://github.com/rime/rime-stroke.git
cp rime-stroke/*.yaml trime

# 下載拍字方案並複製到trime文件夾
git clone --depth 1 "$SCHEMA_URL"
cp "$SCHEMA_NAME"/*.yaml trime

# 複製所有配置文件到 TRIME_DIR
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

在 Andoroid Studio 中，点击 `Build` => `Generate Signed App Bundle / APK... `。

## 致谢

1. [osfans/trime](https://github.com/osfans/trime)
2. [Bambooin/rimerc](https://github.com/Bambooin/rimerc)
3. [RIME](https://rime.im/)
4. [潮州话打字方案](https://github.com/hokkien-writing/rime-teochew)
5. [【朙月拼音】输入方案](https://github.com/rime/rime-luna-pinyin)
