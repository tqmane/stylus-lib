# スタイラス関連SDK/API抽出レポート

このレポートは4つのノートアプリAPKから抽出されたスタイラス関連のAPI/SDKをまとめたものです。


## FreeNotes (com.freenotes.freenotes)

検出されたキーワード数: 1

### キーワード: `pen|Pen(?!ding)`

マッチ数: 3

```
Ljava/util/zip/ZipEntry;
append
open
```


## JNotes (com.jideos.jnotes)

検出されたキーワード数: 16

### キーワード: `InputDevice`

マッチ数: 2

```
InputDeviceCompat.java
Landroidx/core/view/InputDeviceCompat;
```

### キーワード: `MPen`

マッチ数: 42

```
copyListenerFromPendingTask
mPenStateListener
mPendingAccessibilityImportanceChange
mPendingAccessibilityState
mPendingActions
mPendingAdapterState
mPendingAdditions
mPendingBroadcasts
mPendingCallbacks
mPendingChanges
mPendingCheckpoints
mPendingCheckpoints.remove(p)
mPendingCleanup
mPendingConnections
mPendingCurrentItem
mPendingData
mPendingDelayMet
mPendingFragmentActivityResults
mPendingInitialRun
mPendingIntent
mPendingInvalidate
mPendingMenus
mPendingMoves
mPendingOverflowIcon
mPendingOverflowIconSet
mPendingPosition
mPendingRebind
mPendingRefresh
mPendingRemovals
mPendingResult
mPendingSavedState
mPendingScrollPosition
mPendingScrollPositionOffset
mPendingSpanCountChange
mPendingSync
mPendingUpdates
mTempEndValues
performPendingDeferredStart
tempEndValues
updateAnchorFromPendingData
```

### キーワード: `MotionEvent`

マッチ数: 39

```
 not found. Did any MotionEvents get skipped?
HwMotionEventInfo.java
HwMotionEventQueue.java
Landroid/view/MotionEvent$PointerCoords;
Landroid/view/MotionEvent$PointerProperties;
Landroid/view/MotionEvent;
Landroidx/core/view/MotionEventCompat;
Landroidx/test/core/view/MotionEventBuilder;
Lcom/huawei/stylus/penengine/estimate/HwMotionEventInfo;
Lcom/huawei/stylus/penengine/estimate/HwMotionEventQueue;
Lcom/umeng/socialize/shareboard/widgets/MotionEventCompat;
MotionEventBuilder.java
MotionEventCompat.java
[Landroid/view/MotionEvent$PointerCoords;
[Landroid/view/MotionEvent$PointerProperties;
addFakeMotionEvent
android:splitMotionEvents
dispatchGenericMotionEvent
getTransformedMotionEvent
injectMotionEvent
mIgnoreMotionEventTillDown
onGenericMotionEvent
setMotionEventSplittingEnabled
toGlobalMotionEvent
toLocalMotionEvent
zeusSuperDispatchGenericMotionEvent
zeusSuperOnGenericMotionEvent
```

### キーワード: `SOURCE_STYLUS`

マッチ数: 1

```
SOURCE_STYLUS
```

### キーワード: `SPen`

マッチ数: 139

```
 (Last suspension stacktrace, not an actual stacktrace)
 lastSuspendedTime=
: suspend properties are not supported yet
Bad suspend function in metadata with constructor: 
CONNECT_STATE_SUSPENDED
COROUTINE_SUSPENDED
Cannot access database on a different coroutine context inherited from a suspending transaction.
Cannot callSuspend on a property 
Cannot callSuspendBy on a property 
Connection Suspended
Coroutines with restricted suspension must have EmptyCoroutineContext
IHwIDRespEntity.java
IS_SUSPEND.get(flags)
Implementation of suspendCoroutineUninterceptedOrReturn is intrinsic
Incompatible suspendability
KSuspendFunction
Landroidx/room/RoomDatabaseKt$acquireTransactionThread$$inlined$suspendCancellableCoroutine$lambda$1;
Landroidx/room/RoomDatabaseKt$acquireTransactionThread$$inlined$suspendCancellableCoroutine$lambda$2$1;
Landroidx/room/RoomDatabaseKt$acquireTransactionThread$$inlined$suspendCancellableCoroutine$lambda$2;
Lcom/huawei/hms/support/api/entity/hwid/IHwIDRespEntity;
Lkotlin/coroutines/RestrictsSuspension;
Lkotlin/coroutines/intrinsics/IntrinsicsKt__IntrinsicsJvmKt$createCoroutineFromSuspendFunction$1;
Lkotlin/coroutines/intrinsics/IntrinsicsKt__IntrinsicsJvmKt$createCoroutineFromSuspendFunction$2;
Lkotlin/coroutines/intrinsics/IntrinsicsKt__IntrinsicsJvmKt$createCoroutineUnintercepted$$inlined$createCoroutineFromSuspendFunction$IntrinsicsKt__IntrinsicsJvmKt$1;
Lkotlin/coroutines/intrinsics/IntrinsicsKt__IntrinsicsJvmKt$createCoroutineUnintercepted$$inlined$createCoroutineFromSuspendFunction$IntrinsicsKt__IntrinsicsJvmKt$2;
Lkotlin/coroutines/intrinsics/IntrinsicsKt__IntrinsicsJvmKt$createCoroutineUnintercepted$$inlined$createCoroutineFromSuspendFunction$IntrinsicsKt__IntrinsicsJvmKt$3;
Lkotlin/coroutines/intrinsics/IntrinsicsKt__IntrinsicsJvmKt$createCoroutineUnintercepted$$inlined$createCoroutineFromSuspendFunction$IntrinsicsKt__IntrinsicsJvmKt$4;
Lkotlin/coroutines/jvm/internal/RestrictedSuspendLambda;
Lkotlin/coroutines/jvm/internal/RunSuspend;
Lkotlin/coroutines/jvm/internal/RunSuspendKt;
Lkotlin/coroutines/jvm/internal/SuspendFunction;
Lkotlin/coroutines/jvm/internal/SuspendLambda;
Lkotlin/reflect/full/KCallables$callSuspend$1;
Lkotlin/reflect/full/KCallables$callSuspendBy$1;
Lkotlin/reflect/jvm/internal/impl/serialization/deserialization/MemberDeserializer$containsSuspendFunctionType$1;
Lkotlinx/coroutines/flow/FlowKt__EmittersKt$transform$1$invokeSuspend$$inlined$collect$1$1;
Lkotlinx/coroutines/flow/FlowKt__EmittersKt$transform$1$invokeSuspend$$inlined$collect$1;
Lkotlinx/coroutines/flow/FlowKt__LimitKt$transformWhile$1$invokeSuspend$$inlined$collectWhile$1$1;
Lkotlinx/coroutines/flow/FlowKt__LimitKt$transformWhile$1$invokeSuspend$$inlined$collectWhile$1;
Lkotlinx/coroutines/flow/StartedLazily$command$1$invokeSuspend$$inlined$collect$1$1;
Lkotlinx/coroutines/flow/StartedLazily$command$1$invokeSuspend$$inlined$collect$1;
Lkotlinx/coroutines/flow/internal/ChannelFlowTransformLatest$flowCollect$3$invokeSuspend$$inlined$collect$1$1;
Lkotlinx/coroutines/flow/internal/ChannelFlowTransformLatest$flowCollect$3$invokeSuspend$$inlined$collect$1;
Lkotlinx/coroutines/flow/internal/CombineKt$combineInternal$2$1$invokeSuspend$$inlined$collect$1$1;
Lkotlinx/coroutines/flow/internal/CombineKt$combineInternal$2$1$invokeSuspend$$inlined$collect$1;
Lkotlinx/coroutines/sync/MutexImpl$lockSuspend$2$1$1;
Lretrofit2/HttpServiceMethod$SuspendForBody;
Lretrofit2/HttpServiceMethod$SuspendForResponse;
Lretrofit2/KotlinExtensions$await$$inlined$suspendCancellableCoroutine$lambda$1;
Lretrofit2/KotlinExtensions$await$$inlined$suspendCancellableCoroutine$lambda$2;
```

*(81件のマッチを省略)*

### キーワード: `StylusManager`

マッチ数: 5

```
Lcom/vivo/penengine/impl/VivoStylusManagerImpl$STYLUS_WRITING_VIBRATE_TYPE;
Lcom/vivo/penengine/impl/VivoStylusManagerImpl;
VivoStylusManagerImpl
VivoStylusManagerImpl.java
[Lcom/vivo/penengine/impl/VivoStylusManagerImpl$STYLUS_WRITING_VIBRATE_TYPE;
```

### キーワード: `TOOL_TYPE_STYLUS`

マッチ数: 1

```
TOOL_TYPE_STYLUS
```

### キーワード: `azimuth|Azimuth`

マッチ数: 3

```
azimuth_unit
getAzimuth
getAzimuthDegrees
```

### キーワード: `getAxisValue`

マッチ数: 2

```
getAxisValue
```

### キーワード: `getOrientation`

マッチ数: 6

```
getOrientation
getOrientationHelper
getOrientationInternal
```

### キーワード: `getPressure`

マッチ数: 5

```
TRANSACTION_getPressureLevel
getPressure
getPressureLevel
```

### キーワード: `orientation|Orientation`

マッチ数: 176

```

配置示例如下: 
<activity
     android:name="com.tencent.connect.common.AssistActivity"
     android:screenOrientation="behind"
     android:theme="@android:style/Theme.Translucent.NoTitleBar"
     android:configChanges="orientation|keyboardHidden">
&orientation=portrait
, mOrientation=
--==-- orientation, a1: 
?orientation=portrait
ANDROID_ORIENTATION
AXIS_ORIENTATION
AppBarLayout is always vertical and does not support horizontal orientation
Cannot add invalid orientation: 
ConstraintLayout_Layout_android_orientation
ConstraintSet_android_orientation
Constraint_android_orientation
DEFAULT_ORIENTATION
ExifOrientationStream.java
Got byte count > 4, not orientation, continuing, formatCode=
Hardware config disallowed because exif orientation is required
IMREAD_IGNORE_ORIENTATION
Invalid orientation. It should be either HORIZONTAL or VERTICAL
Landroid/graphics/drawable/GradientDrawable$Orientation;
Landroid/view/OrientationEventListener;
Landroidx/appcompat/widget/LinearLayoutCompat$OrientationMode;
Landroidx/recyclerview/widget/OrientationHelper$1;
Landroidx/recyclerview/widget/OrientationHelper$2;
Landroidx/recyclerview/widget/OrientationHelper;
Landroidx/recyclerview/widget/RecyclerView$Orientation;
Landroidx/viewpager2/widget/ViewPager2$Orientation;
Layout_android_orientation
Lcom/bumptech/glide/load/ImageHeaderParserUtils$OrientationReader;
Lcom/bumptech/glide/load/data/ExifOrientationStream;
Lcom/bytedance/sdk/openadsdk/TTAdConstant$ORIENTATION_STATE;
LinearLayoutCompat_android_orientation
ORIENTATION
ORIENTATION_FLIP_HORIZONTAL
ORIENTATION_FLIP_VERTICAL
ORIENTATION_HORIZONTAL
ORIENTATION_LANDSCAPE
ORIENTATION_NORMAL
ORIENTATION_PORTRAIT
ORIENTATION_POSITION
ORIENTATION_ROTATE_180
ORIENTATION_ROTATE_270
ORIENTATION_ROTATE_90
ORIENTATION_STATE
ORIENTATION_TAG_TYPE
ORIENTATION_TRANSPOSE
ORIENTATION_TRANSVERSE
ORIENTATION_UNDEFINED
ORIENTATION_VERTICAL
Orientation
OrientationHelper.java
```

*(54件のマッチを省略)*

### キーワード: `pen|Pen(?!ding)`

マッチ数: 7183

```



This file uses Microsoft Information Protection solutions.
Open it using an application that supports protected files.

You can download Microsoft's protected file viewer from: https://go.microsoft.com/fwlink/?LinkId=280381
Learn more about Information Protection solutions at https://www.microsoft.com/rms

Do not change this file in any way -- doing so will result in data loss.


  Open: 
 (Last suspension stacktrace, not an actual stacktrace)
 AND (SELECT COUNT(*)=0 FROM dependency WHERE     prerequisite_id=id AND     work_spec_id NOT IN         (SELECT id FROM workspec WHERE state IN (2, 3, 5)))
 because ACTION_DOWN was not received for this pointer before ACTION_MOVE. It likely happened because  ViewDragHelper did not receive all the events in the event stream.
 is not contained in its own dependencies, this is probably a misconfiguration
 lastSuspendedTime=
 open_news open_news_u_s/
 openid profile offline_access
 pendingTasks.size:
 threw an IOException (should never happen).
 to openssh private key
 was not initialized by the time contents of dependent module 
 | openid: 
#openLinkInBrowser
$AppFirstOpen
$HA_FIRST_OPEN
$OpenAppFromAppLinking
$PBEWithMD5And128BitAESCBCOpenSSL
$PBEWithMD5And192BitAESCBCOpenSSL
$PBEWithMD5And256BitAESCBCOpenSSL
$ReOpenAppFromAppLinking
$SerpentGMAC
$TSerpentGMAC
$this$appendBytes
$this$appendText
$this$prependIndent
&fopen_id=
&open_id=
&openid=
' because the database is locked.  This usually means that there are other open connections to the database which prevents the database from enabling or disabling write-ahead logging mode.  Proceeding without changing the journal mode.
' is not open.
';    var head = document.getElementsByTagName('head')[0];    var script = document.createElement('script');    script.type = 'text/javascript';    script.src = JS_ACTLOG_URL;    head.appendChild(script);})();
(Ljava/lang/CharSequence;Ljava/lang/Appendable;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
(Ljava/lang/CharSequence;Ljava/lang/Appendable;Lkotlin/jvm/functions/Function2;)Ljava/lang/Appendable;
(Ljava/lang/Iterable;Ljava/lang/Appendable;Ljava/lang/CharSequence;Ljava/lang/CharSequence;Ljava/lang/CharSequence;ILjava/lang/CharSequence;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
(Ljava/nio/file/Path;[Ljava/nio/file/OpenOption;)Lokio/Sink;
(Ljava/nio/file/Path;[Ljava/nio/file/OpenOption;)Lokio/Source;
(Lkotlin/sequences/Sequence;Ljava/lang/Appendable;Ljava/lang/CharSequence;Ljava/lang/CharSequence;Ljava/lang/CharSequence;ILjava/lang/CharSequence;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
(TOpen;)V
([BLjava/lang/Appendable;Ljava/lang/CharSequence;Ljava/lang/CharSequence;Ljava/lang/CharSequence;ILjava/lang/CharSequence;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
([CLjava/lang/Appendable;Ljava/lang/CharSequence;Ljava/lang/CharSequence;Ljava/lang/CharSequence;ILjava/lang/CharSequence;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
([DLjava/lang/Appendable;Ljava/lang/CharSequence;Ljava/lang/CharSequence;Ljava/lang/CharSequence;ILjava/lang/CharSequence;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
([FLjava/lang/Appendable;Ljava/lang/CharSequence;Ljava/lang/CharSequence;Ljava/lang/CharSequence;ILjava/lang/CharSequence;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
([ILjava/lang/Appendable;Ljava/lang/CharSequence;Ljava/lang/CharSequence;Ljava/lang/CharSequence;ILjava/lang/CharSequence;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
([JLjava/lang/Appendable;Ljava/lang/CharSequence;Ljava/lang/CharSequence;Ljava/lang/CharSequence;ILjava/lang/CharSequence;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
([Ljava/lang/Object;Ljava/lang/Appendable;Ljava/lang/CharSequence;Ljava/lang/CharSequence;Ljava/lang/CharSequence;ILjava/lang/CharSequence;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
([SLjava/lang/Appendable;Ljava/lang/CharSequence;Ljava/lang/CharSequence;Ljava/lang/CharSequence;ILjava/lang/CharSequence;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
([ZLjava/lang/Appendable;Ljava/lang/CharSequence;Ljava/lang/CharSequence;Ljava/lang/CharSequence;ILjava/lang/CharSequence;Lkotlin/jvm/functions/Function1;)Ljava/lang/Appendable;
(function() {
    if (window.AlipayJSBridge) {
        return
    }

    function alipayjsbridgeFunc(url) {
        var iframe = document.createElement("iframe");
        iframe.style.width = "1px";
        iframe.style.height = "1px";
        iframe.style.display = "none";
        iframe.src = url;
        document.body.appendChild(iframe);
        setTimeout(function() {
            document.body.removeChild(iframe)
        }, 100)
    }
    window.alipayjsbridgeSetTitle = function(title) {
        document.title = title;
        alipayjsbridgeFunc("alipayjsbridge://setTitle?title=" + encodeURIComponent(title))
    };
    window.alipayjsbridgeRefresh = function() {
        alipayjsbridgeFunc("alipayjsbridge://onRefresh?")
    };
    window.alipayjsbridgeBack = function() {
        alipayjsbridgeFunc("alipayjsbridge://onBack?")
    };
    window.alipayjsbridgeExit = function(bsucc) {
        alipayjsbridgeFunc("alipayjsbridge://onExit?bsucc=" + bsucc)
    };
    window.alipayjsbridgeShowBackButton = function(bshow) {
        alipayjsbridgeFunc("alipayjsbridge://showBackButton?bshow=" + bshow)
    };
    window.AlipayJSBridge = {
        version: "2.0",
        addListener: addListener,
        hasListener: hasListener,
        callListener: callListener,
        callNativeFunc: callNativeFunc,
        callBackFromNativeFunc: callBackFromNativeFunc
    };
    var uniqueId = 1;
    var h5JsCallbackMap = {};

    function iframeCall(paramStr) {
        setTimeout(function() {
        	var iframe = document.createElement("iframe");
        	iframe.style.width = "1px";
        	iframe.style.height = "1px";
        	iframe.style.display = "none";
        	iframe.src = "alipayjsbridge://callNativeFunc?" + paramStr;
        	var parent = document.body || document.documentElement;
        	parent.appendChild(iframe);
        	setTimeout(function() {
            	parent.removeChild(iframe)
        	}, 0)
        }, 0)
    }

    function callNativeFunc(nativeFuncName, data, h5JsCallback) {
        var h5JsCallbackId = "";
        if (h5JsCallback) {
            h5JsCallbackId = "cb_" + (uniqueId++) + "_" + new Date().getTime();
            h5JsCallbackMap[h5JsCallbackId] = h5JsCallback
        }
        var dataStr = "";
        if (data) {
            dataStr = encodeURIComponent(JSON.stringify(data))
        }
        var paramStr = "func=" + nativeFuncName + "&cbId=" + h5JsCallbackId + "&data=" + dataStr;
        iframeCall(paramStr)
    }

    function callBackFromNativeFunc(h5JsCallbackId, data) {
        var h5JsCallback = h5JsCallbackMap[h5JsCallbackId];
        if (h5JsCallback) {
            h5JsCallback(data);
            delete h5JsCallbackMap[h5JsCallbackId]
        }
    }
    var h5ListenerMap = {};

    function addListener(jsFuncName, jsFunc) {
        h5ListenerMap[jsFuncName] = jsFunc
    }

    function hasListener(jsFuncName) {
        var jsFunc = h5ListenerMap[jsFuncName];
        if (!jsFunc) {
            return false
        }
        return true
    }

    function callListener(h5JsFuncName, data, nativeCallbackId) {
        var responseCallback;
        if (nativeCallbackId) {
            responseCallback = function(responseData) {
                var dataStr = "";
                if (responseData) {
                    dataStr = encodeURIComponent(JSON.stringify(responseData))
                }
                var paramStr = "func=h5JsFuncCallback" + "&cbId=" + nativeCallbackId + "&data=" + dataStr;
                iframeCall(paramStr)
            }
        }
        var h5JsFunc = h5ListenerMap[h5JsFuncName];
        if (h5JsFunc) {
            h5JsFunc(data, responseCallback)
        } else if (h5JsFuncName == "h5BackAction") {
            if (!window.alipayjsbridgeH5BackAction || !alipayjsbridgeH5BackAction()) {
                var paramStr = "func=back";
                iframeCall(paramStr)
            }
        } else {
            console.log("AlipayJSBridge: no h5JsFunc " + h5JsFuncName + data)
        }
    }
    var event;
    if (window.CustomEvent) {
        event = new CustomEvent("alipayjsbridgeready")
    } else {
        event = document.createEvent("Event");
        event.initEvent("alipayjsbridgeready", true, true)
    }
    document.dispatchEvent(event);
    setTimeout(excuteH5InitFuncs, 0);

    function excuteH5InitFuncs() {
        if (window.AlipayJSBridgeInitArray) {
            var h5InitFuncs = window.AlipayJSBridgeInitArray;
            delete window.AlipayJSBridgeInitArray;
            for (var i = 0; i < h5InitFuncs.length; i++) {
                try {
                    h5InitFuncs[i](AlipayJSBridge)
                } catch (e) {
                    setTimeout(function() {
                        throw e
                    })
                }
            }
        }
    }
})();

```

*(6689件のマッチを省略)*

### キーワード: `pressure|Pressure`

マッチ数: 64

```
$SwitchMap$io$reactivex$BackpressureOverflowStrategy
$SwitchMap$io$reactivex$BackpressureStrategy
, pressure=
AXIS_PRESSURE
BackpressureBufferSubscriber
BackpressureDropSubscriber
BackpressureErrorSubscriber
BackpressureHelper.java
BackpressureKind.java
BackpressureLatestSubscriber
BackpressureOverflowStrategy.java
BackpressureStrategy.java
BackpressureSupport.java
FlowableOnBackpressureBuffer.java
FlowableOnBackpressureBufferStrategy.java
FlowableOnBackpressureDrop.java
FlowableOnBackpressureError.java
FlowableOnBackpressureLatest.java
Lio/reactivex/BackpressureOverflowStrategy;
Lio/reactivex/BackpressureStrategy;
Lio/reactivex/annotations/BackpressureKind;
Lio/reactivex/annotations/BackpressureSupport;
Lio/reactivex/exceptions/MissingBackpressureException;
Lio/reactivex/internal/operators/flowable/FlowableOnBackpressureBuffer$BackpressureBufferSubscriber;
Lio/reactivex/internal/operators/flowable/FlowableOnBackpressureBuffer;
Lio/reactivex/internal/operators/flowable/FlowableOnBackpressureBufferStrategy$1;
Lio/reactivex/internal/operators/flowable/FlowableOnBackpressureBufferStrategy$OnBackpressureBufferStrategySubscriber;
Lio/reactivex/internal/operators/flowable/FlowableOnBackpressureBufferStrategy;
Lio/reactivex/internal/operators/flowable/FlowableOnBackpressureDrop$BackpressureDropSubscriber;
Lio/reactivex/internal/operators/flowable/FlowableOnBackpressureDrop;
Lio/reactivex/internal/operators/flowable/FlowableOnBackpressureError$BackpressureErrorSubscriber;
Lio/reactivex/internal/operators/flowable/FlowableOnBackpressureError;
Lio/reactivex/internal/operators/flowable/FlowableOnBackpressureLatest$BackpressureLatestSubscriber;
Lio/reactivex/internal/operators/flowable/FlowableOnBackpressureLatest;
Lio/reactivex/internal/util/BackpressureHelper;
MissingBackpressureException.java
OnBackpressureBufferStrategySubscriber
TRANSACTION_getPressureLevel
TRANSACTION_onPressureLevelChange
TRANSACTION_onPressureStateChange
TRANSACTION_setPressureLevel
[Lio/reactivex/BackpressureOverflowStrategy;
[Lio/reactivex/BackpressureStrategy;
[Lio/reactivex/annotations/BackpressureKind;
backpressure
getHistoricalPressure
getPointPressure
getPressure
getPressureLevel
onBackpressureBuffer
```

*(7件のマッチを省略)*

### キーワード: `stylus|Stylus`

マッチ数: 64

```
Lcom/huawei/penkit/impl/eink/HwEinkStylusImpl;
Lcom/huawei/stylus/penengine/BuildConfig;
Lcom/huawei/stylus/penengine/HwPenEngineManager;
Lcom/huawei/stylus/penengine/R;
Lcom/huawei/stylus/penengine/VersionInfo;
Lcom/huawei/stylus/penengine/eink/constants/Constants;
Lcom/huawei/stylus/penengine/eink/listener/IHwEinkListener;
Lcom/huawei/stylus/penengine/eink/model/StrokeInfo;
Lcom/huawei/stylus/penengine/eink/model/StrokePoint;
Lcom/huawei/stylus/penengine/eink/throwable/VersionNotCompatibleException;
Lcom/huawei/stylus/penengine/estimate/HwMotionEventInfo;
Lcom/huawei/stylus/penengine/estimate/HwMotionEventQueue;
Lcom/huawei/stylus/penengine/estimate/HwStrokeEstimate;
Lcom/huawei/stylus/penengine/estimate/IHwRecycleQueue;
Lcom/huawei/stylus/penengine/estimate/IHwStrokeEstimate;
Lcom/huawei/stylus/penengine/instantshape/InstantShapeGenerator;
Lcom/huawei/stylus/penengine/version/IVersionInfo;
Lcom/huawei/stylus/penengine/view/HwConstants$Colors;
Lcom/huawei/stylus/penengine/view/HwConstants$Pen;
Lcom/huawei/stylus/penengine/view/HwConstants$ViewArea;
Lcom/huawei/stylus/penengine/view/HwConstants;
Lcom/huawei/stylus/penengine/view/HwEinkSurfaceView;
Lcom/huawei/stylus/penengine/view/HwHandWritingView;
Lcom/huawei/stylus/penengine/view/IHwHandWritingView;
Lcom/huawei/stylus/penengine/view/IPaintViewListener;
Lcom/vivo/penengine/impl/VivoStylusGestureManagerImpl$1;
Lcom/vivo/penengine/impl/VivoStylusGestureManagerImpl$2;
Lcom/vivo/penengine/impl/VivoStylusGestureManagerImpl$3;
Lcom/vivo/penengine/impl/VivoStylusGestureManagerImpl$OnGestureCallback;
Lcom/vivo/penengine/impl/VivoStylusGestureManagerImpl;
Lcom/vivo/penengine/impl/VivoStylusManagerImpl$STYLUS_WRITING_VIBRATE_TYPE;
Lcom/vivo/penengine/impl/VivoStylusManagerImpl;
SOURCE_STYLUS
STYLUS_ALGO_PKG_NAME
STYLUS_HAPTIC_FEEDBACK_GESTURE_SWITCH
STYLUS_HAPTIC_FEEDBACK_GESTURE_SWITCH_OFF
STYLUS_HAPTIC_FEEDBACK_GESTURE_SWITCH_ON
STYLUS_PRIMARY_BUTTON_CLICK
STYLUS_SECONDLY_BUTTON_CLICK
STYLUS_WRITING_VIBRATE_INTENSITY_NORMAL
STYLUS_WRITING_VIBRATE_INTENSITY_STRONG
STYLUS_WRITING_VIBRATE_INTENSITY_WEAK
STYLUS_WRITING_VIBRATE_STRENGTH_LEVEL
STYLUS_WRITING_VIBRATE_STRENGTH_LEVEL_NORMAL
STYLUS_WRITING_VIBRATE_STRENGTH_LEVEL_OFF
STYLUS_WRITING_VIBRATE_STRENGTH_LEVEL_STRONG
STYLUS_WRITING_VIBRATE_STRENGTH_LEVEL_WEAK
STYLUS_WRITING_VIBRATE_SWITCH
STYLUS_WRITING_VIBRATE_SWITCH_OFF
STYLUS_WRITING_VIBRATE_SWITCH_ON
```

*(14件のマッチを省略)*

### キーワード: `tilt|Tilt`

マッチ数: 9

```
AXIS_TILT
CALIB_TILTED_MODEL
CAP_PROP_TILT
MARKER_TILTED_CROSS
enablePencilTilt
enablePencilTilt :
getTilt
mTilt
setTilt
```


## Onyx Galaxy Note (com.onyx.galaxy.note)

検出されたキーワード数: 1

### キーワード: `pen|Pen(?!ding)`

マッチ数: 2

```
append
open
```


## Orion NoteIn (com.orion.notein)

検出されたキーワード数: 1

### キーワード: `pen|Pen(?!ding)`

マッチ数: 3

```
Ljava/util/zip/ZipEntry;
append
open
```

