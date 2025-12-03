# スタイラスSDK統合ガイド
## 他のアプリへの適用と一般化

このドキュメントは、検出されたスタイラスSDK（Huawei PenEngine、Vivo Stylus、HiPaint Stylus）を他のAndroidアプリに統合するための包括的なガイドです。

---

## 📋 目次

1. [概要](#概要)
2. [検出されたSDK](#検出されたsdk)
3. [SDK統合の前提条件](#sdk統合の前提条件)
4. [統合手順](#統合手順)
5. [実装パターン](#実装パターン)
6. [トラブルシューティング](#トラブルシューティング)

---

## 🎯 概要

### SDKの配置形式

解析の結果、スタイラスSDKは以下の形式で配置されていることが判明しました：

| SDK | 配置形式 | 抽出方法 |
|-----|---------|---------|
| Huawei PenEngine | **DEXファイル内** | DEXからクラスファイルを抽出 |
| Vivo Stylus | **DEXファイル内** | DEXからクラスファイルを抽出 |
| HiPaint Stylus | **DEXファイル内** | DEXからクラスファイルを抽出 |
| 標準Android API | **Android Framework** | 不要（標準API） |

> [!IMPORTANT]
> **独立した.jarや.aarファイルは見つかりませんでした。**
> これらのSDKはAPKのDEXファイルに直接コンパイルされています。

## 🔍 検出されたSDK

### 1. Huawei PenEngine SDK

**パッケージ名:** `com.huawei.stylus.penengine`

**主要コンポーネント:**

```
com.huawei.stylus.penengine/
├── HwPenEngineManager           # メインマネージャー
├── eink/                         # E-ink最適化
│   ├── IHwEinkListener
│   ├── StrokeInfo
│   └── StrokePoint
├── estimate/                     # ストローク推定
│   ├── HwStrokeEstimate
│   ├── HwMotionEventInfo
│   └── HwMotionEventQueue
├── instantshape/                 # 図形認識
│   └── InstantShapeGenerator
└── view/                         # UI コンポーネント
    ├── HwHandWritingView
    ├── HwEinkSurfaceView
    └── HwConstants
```

**主要機能:**
- ストローク推定と最適化
- E-inkディスプレイ最適化
- 手書き図形認識
- 高性能手書きビュー

### 2. Vivo Stylus SDK

**パッケージ名:** `com.vivo.penengine.impl`

**主要コンポーネント:**

```
com.vivo.penengine.impl/
├── VivoStylusManagerImpl        # メインマネージャー
└── VivoStylusGestureManagerImpl # ジェスチャーマネージャー
    └── OnGestureCallback
```

**主要機能:**
- スタイラス書き込み時の触覚フィードバック
- 振動強度のカスタマイズ
- スタイラスジェスチャー認識
- ボタンイベント処理

### 3. HiPaint Stylus SDK

**パッケージ名:** 調査中（DEXファイルから検出）

**主要機能:**
- スタイラス振動モード設定（StylusVibrationMode）
- 高度な筆圧カーブカスタマイズ（PressureCurve）
- 筆圧フロー制御（StylusPressureFlow）
- 筆圧混色制御（StylusPressureMixPigment）
- 傾き角度制御（TiltAngle、TiltFlow、TiltGradual）
- ジッターテクスチャ筆圧（JitterTexturePressure）
- 標準Android MotionEvent/InputDevice API

**検出されたキーワード:**
```
stylus/Stylus - 10件以上
  - onStylusVibrationModeValueChange
  - refreshPaintStylusPressureCurve
  - refreshPaintStylusPressureFlow
  - refreshPaintStylusPressureMixPigment

pressure/Pressure - 10件以上
  - DialogPressureCurveInner
  - pressureCurveRepositoryProvider
  - providePressureCurveDataStoreModel
  - refreshPaintJitterTexturePressure

tilt/Tilt - 10件以上
  - onControllerTiltAngleValueChange
  - onControllerTiltFlowValueChange
  - onControllerTiltGradualValueChange

MotionEvent - 10件以上
InputDevice - 8件
```

**抽出元:**
- APKS: com.aige.hipaint_6.1.7.apks
- メインAPK: base.apk

### 4. OPPO/OPlus API

**検出結果:** スタイラス専用のSDKは検出されませんでした。

**見つかった項目:**
- デバイスID取得関連（`OppoDeviceIDHelper`）
- 画面異形対応（`com.oppo.feature.screen.heteromorphism`）

> [!NOTE]
> OPPO/OPlusデバイスでは、標準Android APIまたは他のベンダーSDKを使用している可能性があります。

---

## 📦 SDK統合の前提条件

### 必要なファイルの抽出

<function_calls>スタイラスSDKを統合するには、以下のファイルを抽出する必要があります：

#### 方法1: DEXファイルからクラスを抽出（推奨）

**使用ツール:**
- [jadx](https://github.com/skylot/jadx) - DEXからJavaソースへのデコンパイラー
- [dex2jar](https://github.com/pxb1988/dex2jar) - DEXからJARへの変換

**手順:**

```bash
# 1. JADXをダウンロード
# https://github.com/skylot/jadx/releases

# 2. APKをデコンパイル
jadx -d output_dir target_app.apk

# 3. 必要なパッケージをコピー
# output_dir/sources/com/huawei/stylus/penengine/
# output_dir/sources/com/vivo/penengine/impl/
```

#### 方法2: DEXからJARを作成

```bash
# 1. APKからclasses.dexを抽出
unzip target_app.apk classes*.dex

# 2. DEXをJARに変換
d2j-dex2jar classes.dex -o classes.jar

# 3. JARから必要なクラスを抽出
jar xf classes.jar com/huawei/stylus/
jar xf classes.jar com/vivo/penengine/
```

---

## 🔧 統合手順

### ステップ1: ソースコードの抽出

#### JADXを使用した抽出（最も簡単）

1. **JNotes APK をデコンパイル:**

```bash
jadx -d jnotes_decompiled com.jideos.jnotes_3.2.0.1.apk
```

2. **スタイラス関連パッケージを特定:**

```
jnotes_decompiled/sources/
├── com/huawei/stylus/penengine/
├── com/huawei/penkit/impl/eink/
└── com/vivo/penengine/impl/
```

3. **必要なパッケージをコピー:**

```bash
# プロジェクトのsrcディレクトリにコピー
cp -r jnotes_decompiled/sources/com/huawei/stylus your_project/src/main/java/com/huawei/
cp -r jnotes_decompiled/sources/com/vivo/penengine your_project/src/main/java/com/vivo/
```

### ステップ2: 依存関係の解決

抽出したコードには、以下の依存関係が含まれる可能性があります：

#### build.gradle に追加

```gradle
dependencies {
    // 標準Android SDK
    implementation 'androidx.core:core:1.12.0'
    implementation 'androidx.appcompat:appcompat:1.6.1'
    
    // 潜在的な依存関係（必要に応じて）
    implementation 'androidx.annotation:annotation:1.7.0'
    
    // Canvas/Graphics関連
    // （通常は不要、Android標準）
}
```

#### 不足しているクラスの特定

```bash
# コンパイルエラーを確認
./gradlew build

# 不足しているクラスをログから特定し、
# 同様にJADXでデコンパイルして追加
```

### ステップ3: AndroidManifest.xml の設定

#### 必要な権限

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="your.package.name">
    
    <!-- タッチ入力（通常は自動で付与） -->
    <uses-feature 
        android:name="android.hardware.touchscreen"
        android:required="false" />
    
    <!-- 低レイテンシ入力（オプション） -->
    <uses-feature 
        android:name="android.hardware.touchscreen.multitouch.distinct"
        android:required="false" />
        
    <!-- Huawei固有の機能（必要な場合） -->
    <uses-permission android:name="android.permission.WRITE_SETTINGS" />
    
    <!-- Vivo固有の機能（振動フィードバック） -->
    <uses-permission android:name="android.permission.VIBRATE" />
    
</manifest>
```

### ステップ4: プロジェクト構造の整理

推奨されるプロジェクト構造：

```
your_project/
├── src/main/java/
│   ├── your/package/           # あなたのアプリコード
│   ├── com/huawei/stylus/      # Huawei SDK
│   │   └── penengine/
│   └── com/vivo/penengine/     # Vivo SDK
│       └── impl/
├── src/main/res/
└── build.gradle
```

---

## 💻 実装パターン

### パターン1: アダプターパターンによる抽象化

ベンダーSDKを直接使用するのではなく、アダプターを作成して抽象化します。

#### 共通インターフェースの定義

```java
/**
 * スタイラスSDKの共通インターフェース
 */
public interface StylusSDKAdapter {
    /**
     * SDKの初期化
     */
    void initialize(Context context);
    
    /**
     * このデバイスでサポートされているか
     */
    boolean isSupported();
    
    /**
     * ストローク推定機能
     */
    StrokeEstimator getStrokeEstimator();
    
    /**
     * 触覚フィードバックの設定
     */
    void setHapticFeedback(boolean enabled, int intensity);
    
    /**
     * ジェスチャーリスナーの設定
     */
    void setGestureListener(StylusGestureListener listener);
}

/**
 * ストローク推定のインターフェース
 */
public interface StrokeEstimator {
    /**
     * モーションイベントを処理
     */
    StrokeInfo processMotionEvent(MotionEvent event);
}

/**
 * ジェスチャーリスナー
 */
public interface StylusGestureListener {
    void onGesture(int gestureType);
    void onButtonClick(int buttonType);
}
```

#### Huawei SDK アダプター実装

```java
public class HuaweiStylusAdapter implements StylusSDKAdapter {
    
    private Context context;
    private HwPenEngineManager penEngineManager;
    private HwStrokeEstimate strokeEstimate;
    
    @Override
    public void initialize(Context context) {
        this.context = context;
        try {
            penEngineManager = new HwPenEngineManager(context);
            strokeEstimate = new HwStrokeEstimate();
        } catch (Exception e) {
            // SDKが利用できない場合
            Log.w("HuaweiStylusAdapter", "SDK not available", e);
        }
    }
    
    @Override
    public boolean isSupported() {
        try {
            Class.forName("com.huawei.stylus.penengine.HwPenEngineManager");
            return true;
        } catch (ClassNotFoundException e) {
            return false;
        }
    }
    
    @Override
    public StrokeEstimator getStrokeEstimator() {
        return new StrokeEstimator() {
            @Override
            public StrokeInfo processMotionEvent(MotionEvent event) {
                if (strokeEstimate == null) {
                    return null;
                }
                
                // HuaweiのAPIを使用
                HwMotionEventInfo eventInfo = new HwMotionEventInfo(event);
                HwMotionEventQueue queue = new HwMotionEventQueue();
                queue.add(eventInfo);
                
                return strokeEstimate.estimate(queue);
            }
        };
    }
    
    @Override
    public void setHapticFeedback(boolean enabled, int intensity) {
        // Huawei SDKには触覚フィードバック機能はない
        // （または未実装）
    }
    
    @Override
    public void setGestureListener(StylusGestureListener listener) {
        // Huawei SDKのジェスチャー機能を実装
    }
}
```

#### Vivo SDK アダプター実装

```java
public class VivoStylusAdapter implements StylusSDKAdapter {
    
    private Context context;
    private VivoStylusManagerImpl stylusManager;
    private VivoStylusGestureManagerImpl gestureManager;
    
    @Override
    public void initialize(Context context) {
        this.context = context;
        try {
            stylusManager = new VivoStylusManagerImpl();
            gestureManager = new VivoStylusGestureManagerImpl();
        } catch (Exception e) {
            Log.w("VivoStylusAdapter", "SDK not available", e);
        }
    }
    
    @Override
    public boolean isSupported() {
        try {
            Class.forName("com.vivo.penengine.impl.VivoStylusManagerImpl");
            return true;
        } catch (ClassNotFoundException e) {
            return false;
        }
    }
    
    @Override
    public StrokeEstimator getStrokeEstimator() {
        // Vivo SDKにはストローク推定機能がない
        return null;
    }
    
    @Override
    public void setHapticFeedback(boolean enabled, int intensity) {
        if (stylusManager == null) {
            return;
        }
        
        // 振動の有効/無効
        stylusManager.setSetting(
            VivoStylusManagerImpl.STYLUS_WRITING_VIBRATE_SWITCH,
            enabled ? VivoStylusManagerImpl.STYLUS_WRITING_VIBRATE_SWITCH_ON 
                    : VivoStylusManagerImpl.STYLUS_WRITING_VIBRATE_SWITCH_OFF
        );
        
        // 強度の設定
        int level;
        if (intensity < 33) {
            level = VivoStylusManagerImpl.STYLUS_WRITING_VIBRATE_STRENGTH_LEVEL_WEAK;
        } else if (intensity < 66) {
            level = VivoStylusManagerImpl.STYLUS_WRITING_VIBRATE_STRENGTH_LEVEL_NORMAL;
        } else {
            level = VivoStylusManagerImpl.STYLUS_WRITING_VIBRATE_STRENGTH_LEVEL_STRONG;
        }
        
        stylusManager.setSetting(
            VivoStylusManagerImpl.STYLUS_WRITING_VIBRATE_STRENGTH_LEVEL,
            level
        );
    }
    
    @Override
    public void setGestureListener(StylusGestureListener listener) {
        if (gestureManager == null || listener == null) {
            return;
        }
        
        gestureManager.setOnGestureCallback(
            new VivoStylusGestureManagerImpl.OnGestureCallback() {
                @Override
                public void onGesture(int gestureType) {
                    listener.onGesture(gestureType);
                }
            }
        );
    }
}
```

#### 標準Android APIアダプター

```java
public class StandardStylusAdapter implements StylusSDKAdapter {
    
    private Context context;
    
    @Override
    public void initialize(Context context) {
        this.context = context;
    }
    
    @Override
    public boolean isSupported() {
        // 標準APIは常に利用可能
        return true;
    }
    
    @Override
    public StrokeEstimator getStrokeEstimator() {
        // 基本的なストローク推定
        return new StrokeEstimator() {
            @Override
            public StrokeInfo processMotionEvent(MotionEvent event) {
                // 標準APIを使用した簡易実装
                StrokeInfo info = new StrokeInfo();
                info.x = event.getX();
                info.y = event.getY();
                info.pressure = event.getPressure();
                info.timestamp = event.getEventTime();
                return info;
            }
        };
    }
    
    @Override
    public void setHapticFeedback(boolean enabled, int intensity) {
        // Android標準の振動を使用
        if (enabled && context != null) {
            Vibrator vibrator = (Vibrator) context.getSystemService(Context.VIBRATOR_SERVICE);
            if (vibrator != null && vibrator.hasVibrator()) {
                if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
                    vibrator.vibrate(VibrationEffect.createOneShot(
                        intensity / 10, 
                        VibrationEffect.DEFAULT_AMPLITUDE
                    ));
                } else {
                    vibrator.vibrate(intensity / 10);
                }
            }
        }
    }
    
    @Override
    public void setGestureListener(StylusGestureListener listener) {
        // 標準APIにはジェスチャー機能がない
    }
}
```

### パターン2: ファクトリーパターンで自動選択

```java
public class StylusSDKFactory {
    
    /**
     * 現在のデバイスに最適なSDKアダプターを返す
     */
    public static StylusSDKAdapter createAdapter(Context context) {
        // Huawei SDK を優先的に試す
        HuaweiStylusAdapter huaweiAdapter = new HuaweiStylusAdapter();
        if (huaweiAdapter.isSupported()) {
            huaweiAdapter.initialize(context);
            return huaweiAdapter;
        }
        
        // Vivo SDK を試す
        VivoStylusAdapter vivoAdapter = new VivoStylusAdapter();
        if (vivoAdapter.isSupported()) {
            vivoAdapter.initialize(context);
            return vivoAdapter;
        }
        
        // HiPaint SDK を試す
        // 注: HiPaintのアダプター実装が必要
        // HiPaintStylusAdapter hipaintAdapter = new HiPaintStylusAdapter();
        // if (hipaintAdapter.isSupported()) {
        //     hipaintAdapter.initialize(context);
        //     return hipaintAdapter;
        // }
        
        // フォールバック: 標準APIを使用
        StandardStylusAdapter standardAdapter = new StandardStylusAdapter();
        standardAdapter.initialize(context);
        return standardAdapter;
    }
    
    /**
     * デバイスのベンダーを検出
     */
    public static String detectVendor() {
        String manufacturer = Build.MANUFACTURER.toLowerCase();
        String brand = Build.BRAND.toLowerCase();
        
        if (manufacturer.contains("huawei") || brand.contains("huawei")) {
            return "Huawei";
        } else if (manufacturer.contains("vivo") || brand.contains("vivo")) {
            return "Vivo";
        } else if (manufacturer.contains("oppo") || brand.contains("oppo") ||
                   manufacturer.contains("oplus") || brand.contains("oplus")) {
            return "OPPO/OPlus";
        } else if (manufacturer.contains("samsung") || brand.contains("samsung")) {
            return "Samsung";
        }
        
        return "Unknown";
    }
}
```

### パターン3: 実際の使用例

```java
public class DrawingView extends View {
    
    private StylusSDKAdapter stylusSDK;
    private Paint paint;
    private Path path;
    
    public DrawingView(Context context, AttributeSet attrs) {
        super(context, attrs);
        init(context);
    }
    
    private void init(Context context) {
        // SDKの自動選択と初期化
        stylusSDK = StylusSDKFactory.createAdapter(context);
        
        // 触覚フィードバックを有効化（中程度の強度）
        stylusSDK.setHapticFeedback(true, 50);
        
        // ジェスチャーリスナーの設定
        stylusSDK.setGestureListener(new StylusGestureListener() {
            @Override
            public void onGesture(int gestureType) {
                // ジェスチャーに応じた処理
                Log.d("DrawingView", "Gesture detected: " + gestureType);
            }
            
            @Override
            public void onButtonClick(int buttonType) {
                // ボタンクリックに応じた処理
                if (buttonType == 0) {
                    // 消しゴムモードに切り替えなど
                    switchToEraserMode();
                }
            }
        });
        
        // ペイント設定
        paint = new Paint();
        paint.setAntiAlias(true);
        paint.setStyle(Paint.Style.STROKE);
        paint.setStrokeCap(Paint.Cap.ROUND);
        paint.setStrokeJoin(Paint.Join.ROUND);
        
        path = new Path();
    }
    
    @Override
    public boolean onTouchEvent(MotionEvent event) {
        int toolType = event.getToolType(0);
        
        // スタイラス入力のみ処理
        if (toolType != MotionEvent.TOOL_TYPE_STYLUS && 
            toolType != MotionEvent.TOOL_TYPE_ERASER) {
            return super.onTouchEvent(event);
        }
        
        // SDK経由でストローク推定
        StrokeEstimator estimator = stylusSDK.getStrokeEstimator();
        if (estimator != null) {
            StrokeInfo strokeInfo = estimator.processMotionEvent(event);
            if (strokeInfo != null) {
                // 推定されたストローク情報を使用
                processSmoothStroke(strokeInfo);
            }
        }
        
        // 標準的な処理も実行
        float x = event.getX();
        float y = event.getY();
        float pressure = event.getPressure();
        
        // 筆圧に基づいてブラシサイズを調整
        paint.setStrokeWidth(10 + pressure * 20);
        
        switch (event.getAction()) {
            case MotionEvent.ACTION_DOWN:
                path.moveTo(x, y);
                return true;
                
            case MotionEvent.ACTION_MOVE:
                path.lineTo(x, y);
                invalidate();
                return true;
                
            case MotionEvent.ACTION_UP:
                // ストローク完了
                return true;
        }
        
        return super.onTouchEvent(event);
    }
    
    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        canvas.drawPath(path, paint);
    }
    
    private void processSmoothStroke(StrokeInfo strokeInfo) {
        // SDK提供のスムージング結果を使用
        // （実装は省略）
    }
    
    private void switchToEraserMode() {
        // 消しゴムモードの実装
        paint.setXfermode(new PorterDuffXfermode(PorterDuff.Mode.CLEAR));
    }
}
```

---

## 🚀 簡易統合手順（クイックスタート）

### 最小限の実装

もっとも簡単に統合する方法：

#### ステップ1: 必要なクラスだけをコピー

```bash
# JADXでデコンパイル
jadx -d decompiled com.jideos.jnotes_3.2.0.1.apk

# 必要なクラスのみコピー
# Huaweiの場合
cp -r decompiled/sources/com/huawei/stylus/penengine/estimate your_project/src/main/java/com/huawei/stylus/penengine/

# Vivoの場合
cp -r decompiled/sources/com/vivo/penengine/impl your_project/src/main/java/com/vivo/penengine/
```

#### ステップ2: 簡易アダプター作成

```java
public class SimpleStylusHelper {
    
    private static Object stylusManager;
    
    public static void init(Context context) {
        try {
            // Huawei SDKを試す
            Class<?> hwClass = Class.forName(
                "com.huawei.stylus.penengine.HwPenEngineManager"
            );
            stylusManager = hwClass.getDeclaredConstructor(Context.class)
                                   .newInstance(context);
        } catch (Exception e) {
            try {
                // Vivo SDKを試す
                Class<?> vivoClass = Class.forName(
                    "com.vivo.penengine.impl.VivoStylusManagerImpl"
                );
                stylusManager = vivoClass.getDeclaredConstructor()
                                         .newInstance();
            } catch (Exception ex) {
                // 標準APIのみ使用
                stylusManager = null;
            }
        }
    }
    
    public static boolean hasStylusSDK() {
        return stylusManager != null;
    }
}
```

#### ステップ3: 最小限の使用

```java
public class MainActivity extends AppCompatActivity {
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        // SDKの初期化
        SimpleStylusHelper.init(this);
        
        if (SimpleStylusHelper.hasStylusSDK()) {
            Toast.makeText(this, "スタイラスSDK利用可能", Toast.LENGTH_SHORT).show();
        }
        
        setContentView(R.layout.activity_main);
    }
}
```

---

## 🔍 トラブルシューティング

### 問題1: クラスが見つからない (ClassNotFoundException)

**原因:** 依存クラスが不足している

**解決方法:**

```bash
# 1. エラーログから不足しているクラスを特定
# 例: com.huawei.stylus.penengine.estimate.HwStrokeEstimate$Helper

# 2. JADXで該当クラスを検索
grep -r "HwStrokeEstimate" decompiled/sources/

# 3. 見つかったファイルをプロジェクトに追加
```

### 問題2: NoSuchMethodError

**原因:** Android バージョンの不一致

**解決方法:**

```gradle
android {
    defaultConfig {
        minSdkVersion 21  // 必要に応じて調整
        targetSdkVersion 33
    }
}
```

### 問題3: ProGuard/R8でクラスが削除される

**解決方法:** proguard-rules.pro に追加

```proguard
# Huawei Stylus SDK
-keep class com.huawei.stylus.** { *; }
-keep interface com.huawei.stylus.** { *; }

# Vivo Stylus SDK
-keep class com.vivo.penengine.** { *; }
-keep interface com.vivo.penengine.** { *; }

# HiPaint Stylus SDK  
# 注: HiPaintの正確なパッケージ名は要確認
-keep class com.aige.hipaint.** { *; }

# リフレクションで使用されるクラス
-keepclassmembers class * {
    public <init>(android.content.Context);
}
```

### 問題4: ネイティブライブラリ (.so) が見つからない

**原因:** 一部のSDKはネイティブライブラリに依存している可能性がある

**解決方法:**

```bash
# 1. 元のAPKからsoファイルをコピー
unzip com.jideos.jnotes_3.2.0.1.apk "lib/*" -d extracted

# 2. プロジェクトにコピー
cp -r exacted/lib/* your_project/src/main/jniLibs/

# 3. build.gradleで設定
android {
    sourceSets {
        main {
            jniLibs.srcDirs = ['src/main/jniLibs']
        }
    }
}
```

---

## 📚 参考資料とツール

### 必須ツール

| ツール | 用途 | ダウンロード |
|--------|------|-------------|
| JADX | DEXからJavaへのデコンパイル | [GitHub](https://github.com/skylot/jadx) |
| dex2jar | DEXからJARへの変換 | [GitHub](https://github.com/pxb1988/dex2jar) |
| APK Analyzer | APK内容の検査 | Android Studio内蔵 |

### 推奨デコンパイル手順

```bash
# 1. JADXで視覚的に探索
jadx-gui com.jideos.jnotes_3.2.0.1.apk

# 2. 必要なパッケージを特定
# GUIで com.huawei.stylus, com.vivo.penengine を探す

# 3. コマンドラインで一括エクスポート
jadx -d output com.jideos.jnotes_3.2.0.1.apk

# 4. 必要なパッケージをコピー
cp -r output/sources/com/huawei/stylus your_project/src/main/java/com/huawei/
```

---

## ✅ チェックリスト

プロジェクトに統合する前に、以下を確認してください：

- [ ] JADXまたはdex2jarをインストール済み
- [ ] 対象APKをデコンパイル済み
- [ ] 必要なパッケージ（com.huawei.stylus、com.vivoなど）を特定済み
- [ ] 依存クラスをすべて抽出済み
- [ ] AndroidManifest.xmlに必要な権限を追加済み
- [ ] build.gradleに必要な依存関係を追加済み
- [ ] ProGuardルールを設定済み（リリースビルドの場合）
- [ ] 実際のデバイスでテスト済み

---

## 🎯 まとめ

### 推奨アプローチ

1. **JADXを使用してソースコードを抽出**
2. **アダプターパターンで抽象化**
3. **ファクトリーパターンで自動デバイス検出**
4. **標準Android APIをフォールバックとして使用**

### 統合の利点

| 機能 | 標準API | Huawei SDK | Vivo SDK |
|------|---------|-----------|----------|
| 筆圧感知 | ✅ | ✅ | ✅ |
| ストローク最適化 | ❌ | ✅ | ❌ |
| E-ink最適化 | ❌ | ✅ | ❌ |
| 触覚フィードバック | 基本 | ❌ | ✅ 高度 |
| ジェスチャー認識 | ❌ | 部分的 | ✅ |
| 図形認識 | ❌ | ✅ | ❌ |

### 次のステップ

1. 実際のデバイスでテスト
2. パフォーマンスの測定と最適化
3. エラーハンドリングの強化
4. ユーザー向けドキュメントの作成

---

> [!WARNING]
> **ライセンスと法的注意事項**
> 
> - これらのSDKは各ベンダーの知的財産です
> - 商用利用の際は、必ず各ベンダーのライセンス条項を確認してください
> - リバースエンジニアリングは教育目的に限定してください
> - 配布する場合は、適切なライセンスを取得してください

---

*最終更新: 2025-12-04*
