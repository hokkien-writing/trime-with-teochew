# 同文輸入法伴潮州拍字方案(trime-with-teochew)

附帶潮州拍字方案其同文輸入法，適用於 Android平臺 (TRIME IM for Android with rime-teochew schema)。

潮語文 | [简体中文](README_sc.md)

## 源起

本項目是爲方便大家儂在Android上使用潮州拍字方案進行拍字而設立。

同文輸入法是一款開源其Android輸入法，伊基於 RIME引擎，好定製各種拍字方案，爲地方語言其存續作出了不小其貢獻。

不過，配置這款輸入法也毋是件簡單其事。複雜其配置是伊其特色，也是酷㩼平常儂頭痛其問題。

好在，我會別(pat) 加減 Android 開發，所費寡日其時間佮精力，創設了此個項目，拍包了內置潮州拍字方案其同文輸入法。

若是汝想欲其他拍字方案，可綴我下底其方式拍包。

## 下載

轉 [Release](https://github.com/hokkien-writing/trime-with-teochew/releases) 頁面下載。

## 拍包

## 環境準備

1. 安裝 Android Studio。
2. 安裝 JDK (OpenJDK) 17。

### 拖取代碼

爲穩定起見，一般使用最新版本其上一個版本，現在最新是 v3.2.18，所以此地方使用 v3.2.17。

```bash
git clone git@github.com:osfans/trime.git
git checkout v3.2.17
git submodule update --init --recursive
```

### 整合配置

```bash
# please replace it with your own config
TRIME_DIR=~/Desktop/trime/
SCHEMA_NAME=rime-teochew
SHEMA_URL=https://github.com/hokkien-writing/rime-teochew.git

# create workdir
rm -rf "workdir/$SCHEMA_NAME"
mkdir -p "workdir/$SCHEMA_NAME"
cd workdir || return

# download rimerc-trime
curl -LO https://github.com/Bambooin/rimerc/releases/download/v0.1.7/rimerc-trime-v0.1.7.zip
unzip rimerc-trime-v0.1.7.zip

# download your schema
git clone --depth 1 "$SHEMA_URL"
cp "$SCHEMA_NAME/*.yaml" trime
cp -rf trime/* "$TRIME_DIR/app/src/main/assets/rime"
```

### 拍包調試版

```bash
# On Linux or macOS
make debug

# On Windows
.\gradlew assembleDebug
```

### 拍包正式版

在 Andoroid Studio 中，`Build` => `Generate Signed App Bundle / APK... `。

## 致謝

1. [osfans/trime](https://github.com/osfans/trime)
2. [Bambooin/rimerc](https://github.com/Bambooin/rimerc)
3. [RIME](https://rime.im/)
