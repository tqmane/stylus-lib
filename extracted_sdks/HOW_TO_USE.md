# スタイラスSDK使用ガイド

このフォルダには、JNotes APKから抽出されたスタイラスSDKが含まれています。

## 📁 フォルダ構造

```
extracted_sdks/
├── huawei_penengine/
│   ├── README.md
│   └── dex/
│       └── *.dex (DEXファイル)
├── vivo_stylus/
│   ├── README.md
│   └── dex/
│       └── *.dex (DEXファイル)
├── native_libs/
│   ├── arm64-v8a/
│   └── armeabi-v7a/
└── HOW_TO_USE.md (このファイル)
```

## 🔧 使用方法

### 方法1: JADXでJavaソースに変換

```bash
# JADXをダウンロード
# https://github.com/skylot/jadx/releases

# DEXファイルをデコンパイル
jadx -d output_java huawei_penengine/dex/classes.dex
```

### 方法2: dex2jarでJARに変換

```bash
# dex2jarをダウンロード
# https://github.com/pxb1988/dex2jar

# DEXをJARに変換
d2j-dex2jar huawei_penengine/dex/classes.dex -o huawei_sdk.jar
```

### 方法3: Androidプロジェクトに統合

1. JADXでJavaソースを生成
2. 必要なパッケージをプロジェクトの`src/main/java/`にコピー
3. `build.gradle`に依存関係を追加
4. 必要に応じてネイティブライブラリを`src/main/jniLibs/`にコピー

## 📚 詳細ドキュメント

より詳しい統合手順については、以下を参照してください：

- `stylus_sdk_integration_guide.md` - 統合ガイド
- `stylus_sdk_comprehensive_report.md` - 包括的レポート
- `README.md` - プロジェクト概要

## ⚠️ 注意事項

> これらのSDKは教育・研究目的で抽出されました。
> 商用利用の際は、各ベンダーのライセンスを確認してください。
