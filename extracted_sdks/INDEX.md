# 抽出されたスタイラスSDK - インデックス

## 📁 フォルダ構造

```
extracted_sdks/
├── huawei_penengine/          # Huawei PenEngine SDK
│   ├── README.md
│   └── dex/                   # 12個のDEXファイル
│       ├── classes.dex
│       ├── classes2.dex
│       ├── classes3.dex
│       ├── classes4.dex
│       ├── classes5.dex
│       ├── classes6.dex
│       ├── classes7.dex
│       ├── classes8.dex
│       ├── classes9.dex
│       ├── classes10.dex
│       ├── classes11.dex
│       └── classes12.dex
│
├── vivo_stylus/               # Vivo Stylus SDK
│   ├── README.md
│   └── dex/                   # 12個のDEXファイル
│       └── （同上）
│
├── hipaint_stylus/            # HiPaint Stylus SDK (NEW!)
│   ├── README.md
│   └── dex/                   # 13個のDEXファイル
│       ├── classes.dex
│       ├── classes2.dex
│       ├── ... (classes13.dex まで)
│
├── native_libs/               # ネイティブライブラリ
│   ├── arm64-v8a/            # 43個の.soファイル
│   └── armeabi-v7a/          # 40個の.soファイル
│
├── HOW_TO_USE.md             # 使用ガイド
└── INDEX.md                  # このファイル
```

## 🎯 含まれるSDK

### 1. Huawei PenEngine SDK

**フォルダ:** `huawei_penengine/`

**パッケージ:**
- `com.huawei.stylus.penengine` - メインSDK
- `com.huawei.penkit.impl.eink` - E-ink実装

**主要機能:**
- ストローク推定と最適化（HwStrokeEstimate）
- E-inkディスプレイ最適化（HwEinkSurfaceView）
- 手書き図形認識（InstantShapeGenerator）
- 高性能手書きビュー（HwHandWritingView）
- モーションイベントキューイング（HwMotionEventQueue）

**抽出元:**
- APK: com.jideos.jnotes_3.2.0.1.apk
- 抽出日: 2025-12-04

---

### 2. Vivo Stylus SDK

**フォルダ:** `vivo_stylus/`

**パッケージ:**
- `com.vivo.penengine.impl` - メインSDK

**主要機能:**
- スタイラス書き込み振動フィードバック（VivoStylusManagerImpl）
- 振動強度カスタマイズ（弱/通常/強）
- スタイラスジェスチャー認識（VivoStylusGestureManagerImpl）
- ボタンイベント処理

**抽出元:**
- APK: com.jideos.jnotes_3.2.0.1.apk
- 抽出日: 2025-12-04

---

### 3. HiPaint Stylus SDK

**フォルダ:** `hipaint_stylus/`

**パッケージ:**
- 調査中（DEXファイルから検索）

**主要機能:**
- スタイラス振動モード（StylusVibrationMode）
- 筆圧カーブ設定（PressureCurve）
- 筆圧フロー制御（StylusPressureFlow）
- 筆圧混色制御（StylusPressureMixPigment）
- 傾き角度制御（TiltAngle, TiltFlow, TiltGradual）
- ジッターテクスチャ筆圧（JitterTexturePressure）
- 標準Android MotionEvent/InputDevice API

**検出されたキーワード:**
- stylus/Stylus - 10件以上
- pressure/Pressure - 10件以上
- tilt/Tilt - 10件以上
- MotionEvent - 10件以上
- InputDevice - 8件

**抽出元:**
- APKS: com.aige.hipaint_6.1.7.apks
- メインAPK: base.apk (171.81 MB)
- 抽出日: 2025-12-04

---

### 4. ネイティブライブラリ

**フォルダ:** `native_libs/`

**アーキテクチャ:**
- `arm64-v8a/` - 64ビットARMアーキテクチャ（43ファイル）
- `armeabi-v7a/` - 32ビットARMアーキテクチャ（40ファイル）

**注意:** これらは全てのネイティブライブラリを含んでおり、スタイラス専用ではないものも含まれます。

---

## 🔧 使用方法

### ステップ1: DEXファイルをJavaソースに変換

```bash
# JADXを使用（推奨）
jadx -d huawei_java huawei_penengine/dex/classes.dex
jadx -d vivo_java vivo_stylus/dex/classes.dex
jadx -d hipaint_java hipaint_stylus/dex/classes.dex

# またはすべてのDEXを一度に
jadx -d huawei_java_all huawei_penengine/dex/*.dex
jadx -d hipaint_java_all hipaint_stylus/dex/*.dex
```

### ステップ2: 必要なパッケージを特定

変換されたJavaソースから以下のパッケージを探します：

**Huawei SDK:**
```
huawei_java/sources/com/huawei/stylus/penengine/
huawei_java/sources/com/huawei/penkit/impl/eink/
```

**Vivo SDK:**
```
vivo_java/sources/com/vivo/penengine/impl/
```

### ステップ3: プロジェクトに統合

```bash
# 1. 必要なパッケージをコピー
cp -r huawei_java/sources/com/huawei/stylus your_project/src/main/java/com/huawei/
cp -r vivo_java/sources/com/vivo/penengine your_project/src/main/java/com/vivo/

# 2. ネイティブライブラリをコピー（必要な場合）
cp -r native_libs/* your_project/src/main/jniLibs/
```

---

## 📊 統計情報

| 項目 | 数量 |
|------|------|
| **SDKフォルダ** | 3 (Huawei + Vivo + HiPaint) |
| **DEXファイル総数** | 37 (Huawei: 12 + Vivo: 12 + HiPaint: 13) |
| **ネイティブライブラリ** | 83個（.so） |
| **対応アーキテクチャ** | 2（arm64-v8a, armeabi-v7a） |
| **元APKサイズ合計** | 約318 MB |

---

## 📚 関連ドキュメント

プロジェクトルートにある以下のドキュメントも参照してください：

1. **README.md** - プロジェクト総括
2. **stylus_sdk_integration_guide.md** - 詳細な統合手順
3. **stylus_sdk_comprehensive_report.md** - SDK解析レポート
4. **HOW_TO_USE.md** - このフォルダ内の簡易ガイド

---

## 🛠️ 必要なツール

### JADXのインストール

```bash
# Windowsの場合
# https://github.com/skylot/jadx/releases から最新版をダウンロード
# jadx-gui-<version>.exe を実行

# Linuxの場合
sudo apt install jadx

# macOSの場合
brew install jadx
```

### dex2jarのインストール（代替手段）

```bash
# https://github.com/pxb1988/dex2jar/releases
# ダウンロードして解凍後、PATHに追加
```

---

## ⚠️ 重要な注意事項

### ライセンス

> [!WARNING]
> これらのSDKはリバースエンジニアリングによって抽出されたものです。
> 
> - 教育・研究目的でのみ使用してください
> - 商用利用の場合は各ベンダーのライセンスを確認してください
> - 再配布には十分注意してください

### 技術的制約

1. **依存関係の解決が必要:** 
   - これらのSDKは他のクラスに依存している可能性があります
   - コンパイルエラーが発生した場合は、不足しているクラスを追加で抽出してください

2. **ネイティブライブラリ:**
   - 一部の機能はネイティブライブラリ（.so）に依存している可能性があります
   - 必要に応じて`native_libs/`からコピーしてください

3. **Android バージョン:**
   - これらのSDKは特定のAndroidバージョンで動作確認されています
   - 互換性の問題が発生する可能性があります

---

## 🚀 クイックスタート

最も簡単に始める方法：

```bash
# 1. JADXでGUIを開く
jadx-gui

# 2. huawei_penengine/dex/classes.dex をドラッグ&ドロップ

# 3. Sources → com → huawei → stylus → penengine を確認

# 4. 必要なクラスを右クリック → Save as... でエクスポート
```

---

## 📞 サポート

このSDK抽出に関する質問や問題がある場合は：

1. `stylus_sdk_integration_guide.md` のトラブルシューティングセクションを確認
2. プロジェクトルートの `README.md` を参照
3. 公式Androidドキュメントを確認

---

**抽出完了日:** 2025-12-04  
**抽出元APK:** 
- com.jideos.jnotes_3.2.0.1.apk (Huawei SDK, Vivo SDK)
- com.aige.hipaint_6.1.7.apks (HiPaint SDK)

**抽出ツール:** カスタムPythonスクリプト

---

*Happy Coding! 🎨✏️*
