# Mobile Core API reference

## Application reference \(Android only\)

When building Android applications, the `android.app.Application` reference must be passed to the Mobile SDK, which allows the Mobile SDK to access the `android.app.Context` and monitor the lifecycle of the Android application.

{% hint style="warning" %}
Android applications must call `MobileCore.setApplication()` before calling any other Mobile SDK API.
{% endhint %}

### Set Application

You can use this API to pass the Android `Application` instance to the SDK.

{% tabs %}
{% tab title="Android" %}
**Java**

### setApplication

**Syntax**

```java
public static void setApplication(final Application app)
```

**Example**

```java
public class CoreApp extends Application {

   @Override
   public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);
      MobileCore.start(null);
   }
}
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

### setApplication

**Example**

```csharp
public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
{
  protected override void OnCreate(Bundle savedInstanceState)
  {
    base.OnCreate(savedInstanceState);
    ACPCore.Application = this.Application;
    ACPCore.Start(null);
  }
}
```
{% endtab %}
{% endtabs %}

### Get Application

You can use this API to get the previously set Android `Application` instance, and this instance is mainly provided for the third-party extensions.

{% tabs %}
{% tab title="Android" %}
**Java**

### getApplication

{% hint style="warning" %}
`MobileCore.getApplication` might return `null` if the Application object was destroyed or if `MobileCore.setApplication` was not previously called.
{% endhint %}

**Syntax**

```java
public static Application getApplication()
```

**Example**

```java
Application app = MobileCore.getApplication();
if (app != null) {
    ...
}
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

### getApplication

{% hint style="warning" %}
`ACPCore.Application` might be `null` if the Application object was destroyed or if no application was set in the Core.
{% endhint %}

**Example**

```csharp
var app = ACPCore.Application;
if (app != null) {
    ...
}
```
{% endtab %}
{% endtabs %}

## Track app actions

Actions are events that occur in your app. You can use this API to track and measure an action. Each action has one or more corresponding metrics that are incremented each time the event occurs. For example, you might call this API for each new subscription each time an article is viewed, or each time a level is completed.

{% hint style="warning" %}
Call this API when an event that you want to track occurs. In addition to the action name, you can send additional context data with each track action call.
{% endhint %}

{% hint style="info" %}
If you installed and configured the Analytics extension, this method sends an Analytics action tracking hit with the optional context data that you provide.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

### trackAction

**Syntax**

```java
public static void trackAction(final String action, final Map<String, String> contextData)
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```java
Map<String, String> additionalContextData = new HashMap<String, String>();
additionalContextData.put("customKey", "value");
MobileCore.trackAction("loginClicked", additionalContextData);
```
{% endtab %}

{% tab title="iOS — Swift" %}
**Objective-C**

### trackAction

**Syntax**

```swift
@objc(trackAction:data:)
static func track(action: String?, data: [String: Any]?)
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```objectivec
 [AEPMobileCore trackAction:@"action name" data:@{@"key":@"value"}];
```

**Swift**

### trackAction

**Syntax**

```swift
static func track(action: String?, data: [String: Any]?)
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```swift
MobileCore.track(action: "action name", data: ["key": "value"])
```
{% endtab %}

{% tab title="iOS — Obj-C" %}
**Objective-C**

### trackAction

**Syntax**

```objectivec
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) contextData;
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```objectivec
 [ACPCore trackAction:@"action name" data:@{@"key":@"value"}];
```

**Swift**

### trackAction

**Syntax**

```swift
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) contextData;
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```swift
ACPCore.trackAction("action name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### trackAction

**Syntax**

```jsx
trackAction(action?: String, contextData?: { string: string });
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```jsx
ACPCore.trackAction("action name", {"key": "value"});
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

### trackAction

**Syntax**

```dart
Future<void> trackAction (String action, {Map<String, String> contextData});
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```dart
FlutterACPCore.trackAction("action name",  data: {"key": "value"});
```
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

### trackAction

**Syntax**

```jsx
ACPCore.trackAction = function(action, contextData, success, fail);
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on this hit.
* _success_ callback is invoked when trackAction executes successfully.
* _fail_ callback is invoked when trackAction fails.

**Example**

```jsx
ACPCore.trackAction("cordovaAction", {"cordovaKey":"cordovaValue"}, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Unity" %}
#### C\#

### trackAction

**Syntax**

```csharp
public static void TrackAction(string name, Dictionary<string, string> contextDataDict)
```

* _name_ contains the name of the action to track.
* _contextDataDict_ contains the context data to attach on this hit.

**Example**

```csharp
var contextData = new Dictionary<string, string>();
contextData.Add("key", "value");
ACPCore.TrackAction("action", contextData);
```
{% endtab %}

{% tab title="Xamarin" %}
#### C\#

### trackAction

**iOS Syntax**

```csharp
public static void TrackAction (string action, NSMutableDictionary<NSString, NSString> data);
```

* _action_ contains the name of the action to track.
* _data_ contains the context data to attach on this hit.

**Android Syntax**

```csharp
public unsafe static void TrackAction (string action, IDictionary<string, string> contextData);
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

**iOS**

```csharp
var data = new NSMutableDictionary<NSString, NSString>
{
  ["key"] = new NSString("value")
};
ACPCore.TrackAction("action", data);
```

**Android**

```csharp
var data = new Dictionary<string, string>();
data.Add("key", "value");
ACPCore.TrackAction("action", data);
```
{% endtab %}
{% endtabs %}

## Track app states and views

States represent screens or views in your app. Each time a new state is displayed in your application, for example, when a user navigates from the home page to the news feed, this API can be called. This method sends an Analytics state tracking hit with optional context data.

{% hint style="info" %}
If you installed and configured the Analytics extension, this API increments page views and an Analytics state tracking hit with the optional context data that you provide.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

In Android, `trackState` is typically called each time a new Activity is loaded.

### trackState

**Syntax**

```java
public static void trackState(final String state, final Map<String, String> contextData)
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```java
Map<String, String> additionalContextData = new HashMap<String, String>();        
additionalContextData.put("customKey", "value");
MobileCore.trackState("homePage", additionalContextData);
```
{% endtab %}

{% tab title="iOS — Swift" %}
**Objective-C**

### trackState

**Syntax**

```swift
@objc(trackState:data:)
static func track(state: String?, data: [String: Any]?)
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```objectivec
 [AEPMobileCore trackState:@"state name" data:@{@"key":@"value"}];
```

**Swift**

### trackState

**Syntax**

```swift
static func track(state: String?, data: [String: Any]?)
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```swift
MobileCore.track(state: "state name", data: ["key": "value"])
```
{% endtab %}

{% tab title="iOS — Obj-C" %}
**Objective-C**

### trackState

**Syntax**

```objectivec
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) contextData;
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```objectivec
 [ACPCore trackState:@"state name" data:@{@"key":@"value"}];
```

**Swift**

### trackState

**Syntax**

```objectivec
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) contextData;
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```swift
ACPCore.trackState("state name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### trackState

**Syntax**

```jsx
trackState(state?: String, contextData?: { string: string });
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```jsx
ACPCore.trackState("state name", {"key": "value"});
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

### trackState

**Syntax**

```dart
Future<void> trackState (String state, {Map<String, String> contextData});
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```dart
FlutterACPCore.trackState("state name",  data: {"key1: "value"})
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

#### trackState

**Syntax**

```jsx
ACPCore.trackState = function(state, contextData, success, fail);
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on this hit.
* _success_ callback is invoked when trackState executes successfully.
* _fail_ callback is invoked when trackState fails.

**Example**

```jsx
ACPCore.trackState("cordovaState", {"cordovaKey":"cordovaValue"}, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Unity" %}
### C\#

#### trackState

**Syntax**

```csharp
public static void TrackState(string name, Dictionary<string, string> contextDataDict)
```

* _name_ contains the name of the state to track.
* _contextDataDict_ contains the context data to attach on this hit.

**Example**

```csharp
var dict = new Dictionary<string, string>();
dict.Add("key", "value");
ACPCore.TrackState("state", dict);
```
{% endtab %}

{% tab title="Xamarin" %}
#### C\#

### trackState

**iOS Syntax**

```csharp
public static void TrackState (string state, NSMutableDictionary<NSString, NSString> data);
```

* _state_ contains the name of the state to track.
* _data_ contains the context data to attach on this hit.

**Android Syntax**

```csharp
public unsafe static void TrackState (string state, IDictionary<string, string> contextData);
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

**iOS**

```csharp
var data = new NSMutableDictionary<NSString, NSString>
{
  ["key"] = new NSString("value")
};
ACPCore.TrackState("state", data);
```

**Android**

```csharp
var data = new Dictionary<string, string>();
data.Add("key", "value");
ACPCore.TrackState("state", data);
```
{% endtab %}
{% endtabs %}

## Collect PII

This API allows the SDK to collect sensitive or personally identifiable information \(PII\) data.

{% hint style="warning" %}
Although this API enables the collection of sensitive data, no data is sent to any Adobe or third-party endpoints. To send the data to an endpoint, use a postback of the PII type.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

### collectPii

**Syntax**

```java
public static void collectPII(final Map<String, String> piiData);
```

**Example**

```java
Map<String, String> data = new HashMap<String, String>();
data.put("firstname", "customer");
//The rule to trigger a PII needs to be setup for this call
//to result in a network send
MobileCore.collectPII(data);
```
{% endtab %}

{% tab title="iOS — Swift" %}
**Objective-C**

### collectPii

**Syntax**

```swift
@objc(collectPii:)
public static func collectPii(_ data: [String: Any])
```

**Example**

```objectivec
[AEPMobileCore collectPii:data:@{@"key1" : @"value1",
                           @"key2" : @"value2"
                           }];
```

**Swift**

### collectPii

**Syntax**

```swift
public static func collectPii(_ data: [String: Any])
```

**Example**

```objectivec
MobileCore.collectPii(["key1" : "value1","key2" : "value2"]);
```
{% endtab %}

{% tab title="iOS — Obj-C" %}
**Objective-C**

### collectPii

**Syntax**

```objectivec
+ (void) collectPii: (nonnull NSDictionary<NSString*, NSString*>*) data;
```

**Example**

```objectivec
[ACPCore collectPii:data:@{@"key1" : "@value1",
                           @"key2" : "@value2"
                           }];
```

**Swift**

### collectPii

**Syntax**

```swift
ACPCore.collectPii(data: [String : String])
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
ACPCore.collectPii({"myPii": "data"});
```
{% endtab %}
{% endtabs %}

## Collect launch information

You can provide the user information to the SDK from various launch points in your application.

{% hint style="info" %}
If the Analytics extension is enabled in your SDK, collecting this launch data results in an Analytics request being sent. Other extensions in the SDK might use the collected data, for example, as a rule condition for an In-App Message.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
Coming soon
{% endtab %}

{% tab title="iOS — Swift" %}
**Objective-C**

This method should be called to support the following use cases:

* Tracking Deep Link click-throughs
  * From `application:didFinishLaunchingWithOptions`
  * Extract `userInfo` from `UIApplicationLaunchOptionsURLKey`
* Tracking Push Message click-through
  * From `application:didReceiveRemoteNotification:fetchCompletionHandler:`

#### collectLaunchInfo

**Syntax**

```text
@objc(collectLaunchInfo:)
public static func collectLaunchInfo(_ userInfo: [String: Any])
```

**Example**

```text
 [AEPMobileCore collectLaunchInfo:launchOptions];
```

**Swift**

This method should be called to support the following use cases:

* Tracking Deep Link click-throughs
  * From `application(_:didFinishLaunchingWithOptions:)`
  * Extract `userInfo` from `url: UIApplication.LaunchOptionsKey`
* Tracking Push Message click-through
  * From `application(_:didReceiveRemoteNotification:fetchCompletionHandler:)`

#### collectLaunchInfo

**Syntax**

```swift
public static func collectLaunchInfo(_ userInfo: [String: Any])
```

**Example**

```swift
AEPCore.collectLaunchInfo(userInfo)
```
{% endtab %}

{% tab title="iOS — Obj-C" %}
**Objective-C**

This method should be called to support the following use cases:

* Tracking Deep Link click-throughs
  * From `application:didFinishLaunchingWithOptions`
  * Extract `userInfo` from `UIApplicationLaunchOptionsURLKey`
* Tracking Push Message click-through
  * From `application:didReceiveRemoteNotification:fetchCompletionHandler:`

#### collectLaunchInfo

**Syntax**

```text
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

**Example**

```text
 [ACPCore collectLaunchInfo:launchOptions];
```

**Swift**

This method should be called to support the following use cases:

* Tracking Deep Link click-throughs
  * From `application(_:didFinishLaunchingWithOptions:)`
  * Extract `userInfo` from `url: UIApplication.LaunchOptionsKey`
* Tracking Push Message click-through
  * From `application(_:didReceiveRemoteNotification:fetchCompletionHandler:)`

#### collectLaunchInfo

**Syntax**

```swift
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

**Example**

```swift
ACPCore.collectLaunchInfo(userInfo)
```
{% endtab %}
{% endtabs %}

## Retrieving stored identifiers

The following SDK identities \(as applicable\) are locally stored:

* Company Context - IMS Org IDs
* Experience Cloud ID \(MID\)
* User IDs
* Integration codes \(ADID, push IDs\)
* Data source IDs \(DPID, DPUUID\)
* Analytics IDs \(AVID, AID, VID, and associated RSIDs\)
* Target legacy IDs \(TNTID, TNT3rdpartyID\)
* Audience Manager ID \(UUID\)

To retrieve data as a JSON string from the SDKs, and send this data to your servers, use the following:

{% hint style="warning" %}
You must call the API below and retrieve identities stored in the SDK, **before** the user opts out.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

### getSdkIdentities

#### Syntax

```java
void getSdkIdentities(AdobeCallback<String> callback);
```

* _callback_ is invoked with the SDK identities as a JSON string.
* If an instance of  `AdobeCallbackWithError` is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 5000ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate `AdobeError`.

#### Example

```java
MobileCore.getSdkIdentities(new AdobeCallback<String>() {
    @Override
    public void call(String value) {
        // handle the json string
    }
});
```
{% endtab %}

{% tab title="iOS — Swift" %}
#### Objective-C

### getSdkIdentities

#### Syntax

```objectivec
@objc(getSdkIdentities:)
static func getSdkIdentities(completion: @escaping (String?, Error?) -> Void)
```

* _callback_ is invoked with the SDK identities as a JSON string.
* _completionHandler_ is invoked with the SDK identities as a JSON string, or _error_ if an unexpected error occurs or the request times out. The default timeout is 1000ms.

#### Example

**Objective-C**

```objectivec
[AEPMobileCore getSdkIdentities:^(NSString * _Nullable content, NSError * _Nullable error) {
    if (error) {
      // handle error here
    } else {
      // handle the retrieved identities
    }
}];
```

**Swift**

```swift
MobileCore.getSdkIdentities { (content, error) in
    // handle completion
}
```
{% endtab %}

{% tab title="iOS — Obj-C" %}
#### Objective-C

### getSdkIdentities

#### Syntax

```objectivec
+ (void) getSdkIdentities: (nullable void (^) (NSString* __nullable content)) callback;
+ (void) getSdkIdentitiesWithCompletionHandler: (nullable void (^) (NSString* __nullable content, NSError* _Nullable error)) completionHandler;
```

* _callback_ is invoked with the SDK identities as a JSON string.
* _completionHandler_ is invoked with the SDK identities as a JSON string, or _error_ if an unexpected error occurs or the request times out. The default timeout is 5000ms.

#### Example

```objectivec
[ACPCore getSdkIdentities:^(NSString * _Nullable content){
    NSLog(content);
}];

[ACPCore getSdkIdentitiesWithCompletionHandler:^(NSString * _Nullable content, NSError * _Nullable error) {
        if (error) {
            // handle error here
        } else {
            // handle the retrieved identities
            NSLog(content);
        }
    }];
```
{% endtab %}
{% endtabs %}

## Set Icons for local notification \(Android only\)

You can set the small and large icons that will be used for notifications that are created by the SDK. The small icon appears in the status bar and is the secondary image that is displayed when the user sees the complete notification in the notification center. The large icon is the primary image that is displayed when the user sees the complete notification in the notification center.

{% hint style="warning" %}
Those APIs are **only** available in Android and Xamarin Android.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

### setSmallIconResourceID

**Syntax**

```java
public static void setSmallIconResourceID(int resourceID)
```

**Example**

```java
 MobileCore.setSmallIconResourceID(R.mipmap.ic_launcher_round);
```

### setLargeIconResourceID

**Syntax**

```java
public static void setLargeIconResourceID(int resourceID)
```

**Example**

```java
 MobileCore.setLargeIconResourceID(R.mipmap.ic_launcher_round);
```
{% endtab %}

{% tab title="Xamarin" %}
#### C\#

### setSmallIconResourceID

**Syntax**

```csharp
public unsafe static void SetSmallIconResourceID (int resourceID);
```

**Example**

```csharp
ACPCore.SetSmallIconResourceID(Resource.Mipmap.icon_round);
```

### setLargeIconResourceID

**Syntax**

```csharp
public unsafe static void SetLargeIconResourceID (int resourceID);
```

**Example**

```csharp
 ACPCore.SetLargeIconResourceID(Resource.Mipmap.icon_round);
```
{% endtab %}
{% endtabs %}

## Logging

The logging APIs allow log messages to be tagged and filtered with the Mobile SDK log messages and allow application developers to filter the logged messages based on the current logging mode.

Application developers can use the `setLogLevel` API to filter the log messages that are coming from the Mobile SDK. When debugging, use `LoggingMode.VERBOSE` \(Android\) / `ACPMobileLogLevelVerbose` \(iOS\) to enable all the logging messages that are coming from the Mobile SDK and partner extensions. In a production application, we recommend that you use a less verbose logging mode, for example `LoggingMode.ERROR` \(Android\) / `ACPMobileLogLevelError` \(iOS\).

By default, the Mobile SDK logging mode is set to `LoggingMode.ERROR` \(Android\) / `ACPMobileLogLevelError` \(iOS\).

As a Mobile SDK extension developer, you should use the MobileCore \(Android\) / ACPCore \(iOS\) `log` API to include extension log messages with Mobile SDK core log messages.

From least to most verbose, here is the order of the mobile SDK logging modes:

* ERROR
* WARNING
* DEBUG
* VERBOSE

{% hint style="info" %}
* In **Android**, the Mobile SDK uses the `android.util.Log` class to print the messages.
* In **iOS**, the Mobile SDK uses the `NSLog` for logging the message to Apple System Log facility.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

### setLogLevel

**Syntax**

```java
public static void setLogLevel(LoggingMode mode)
```

**Example**

```java
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
...

MobileCore.setLogLevel(LoggingMode.VERBOSE);
```
{% endtab %}

{% tab title="iOS — Swift" %}
**Objective C**

#### setLogLevel

**Syntax**

```swift
@objc(setLogLevel:)
public static func setLogLevel(_ level: LogLevel)
```

**Example**

```text
[AEPMobileCore setLogLevel: AEPLogLevelTrace];
```

**Swift**

#### setLogLevel

**Syntax**

```swift
public static func setLogLevel(_ level: LogLevel)
```

**Example**

```swift
MobileCore.setLogLevel(.trace)
```
{% endtab %}

{% tab title="iOS — Obj-C" %}
**Objective C**

#### setLogLevel

**Syntax**

```text
+ (void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```text
#import "ACPCore.h"
...

[ACPCore setLogLevel: ACPMobileLogLevelVerbose];
```

**Swift**

#### setLogLevel

**Syntax**

```swift
+ (void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```swift
import ACPCore
...

ACPCore.setLogLevel(ACPMobileLogLevel.verbose);
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

#### setLogLevel

```jsx
import {ACPMobileLogLevel} from '@adobe/react-native-acpcore';

ACPCore.setLogLevel(ACPMobileLogLevel.VERBOSE);
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

#### setLogLevel

```dart
import 'package:flutter_acpcore/src/acpmobile_logging_level.dart';

FlutterACPCore.setLogLevel(ACPLoggingLevel.VERBOSE);
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

#### setLogLevel

From least to most verbose, here is the order of the mobile SDK logging modes for the Cordova version of the ACPCore extension:

* ACPCore.ACPMobileLogLevelError
* ACPCore.ACPMobileLogLevelWarning
* ACPCore.ACPMobileLogLevelDebug
* ACPCore.ACPMobileLogLevelVerbose

**Syntax**

```jsx
ACPCore.setLogLevel = function(logLevel, success, fail);
```

**Example**

```jsx
ACPCore.setLogLevel(ACPCore.ACPMobileLogLevelVerbose, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Unity" %}
### C\#

#### setLogLevel

From least to most verbose, here is the order of the mobile SDK logging modes for the Unity version of the ACPCore extension:

* ACPCore.ACPMobileLogLevel.ERROR
* ACPCore.ACPMobileLogLevel.WARNING
* ACPCore.ACPMobileLogLevel.DEBUG
* ACPCore.ACPMobileLogLevel.VERBOSE

**Syntax**

```csharp
public static void SetLogLevel(ACPMobileLogLevel logLevel)
```

**Example**

```csharp
ACPCore.SetLogLevel(ACPCore.ACPMobileLogLevel.ERROR);
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

#### setLogLevel

From least to most verbose, here is the order of the mobile SDK logging modes for the Xamarin version of the ACPCore iOS extension:

* ACPMobileLogLevel.Error;
* ACPMobileLogLevel.Warning;
* ACPMobileLogLevel.Debug;
* ACPMobileLogLevel.Verbose;

The ACPCore Android extension uses the following logging modes:

* LoggingMode.Error;
* LoggingMode.Warning;
* LoggingMode.Debug;
* LoggingMode.Verbose;

**iOS Syntax**

```csharp
public static ACPMobileLogLevel LogLevel { get, set }
```

**iOS Example**

```csharp
ACPCore.LogLevel = ACPMobileLogLevel.Verbose;
```

**Android Syntax**

```csharp
public unsafe static LoggingMode LogLevel { get, set }
```

**Android Example**

```csharp
ACPCore.LogLevel = LoggingMode.Verbose;
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Android" %}
**Java**

### getLogLevel

**Syntax**

```java
public static LoggingMode getLogLevel()
```

**Example**

```java
LoggingMode mode = MobileCore.getLogLevel();
```
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

### getLogLevel

**Syntax**

```text
+ (ACPMobileLogLevel) logLevel;
```

**Example**

```text
var logLevel:ACPMobileLogLevel = [ACPCore logLevel];
```

**Swift**

### getLogLevel

**Syntax**

```swift
+ (ACPMobileLogLevel) logLevel;
```

**Example**

```swift
let logLevel:ACPMobileLogLevel = ACPCore.logLevel();
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

#### getLogLevel

```jsx
ACPCore.getLogLevel().then(level => console.log("AdobeExperienceSDK: Log Level = " + level));
```
{% endtab %}

{% tab title="Unity" %}
### C\#

#### getLogLevel

```csharp
ACPCore.ACPMobileLogLevel logLevel = ACPCore.GetLogLevel();
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

#### getLogLevel

```csharp
var logLevel = ACPCore.LogLevel;
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Android" %}
**Java**

The `MobileCore` logging APIs use the `android.util.Log` APIs to log messages to Android. Based on the `LoggingMode` that is passed to `MobileCore.log()`, the following Android method is called:

* `LoggingMode.VERBOSE` uses `android.util.Log.v`
* `LoggingMode.DEBUG` uses `android.util.Log.d`
* `LoggingMode.WARNING` uses `android.util.Log.w`
* `LoggingMode.ERROR` uses `android.util.Log.e`

All log messages from the Adobe Experience SDK to Android use the same log tag of `AdobeExperienceSDK`. For example, if logging an error message is using `MobileCore.log()`, the call to `android.util.Log.e` looks like `Log.e("AdobeExperienceSDK", tag + " - " + message)`.

#### log

**Syntax**

```java
public static void log(final LoggingMode mode, final String tag, final String message)
```

**Example**

```java
MobileCore.log(LoggingMode.DEBUG, "MyClassName", "Provided data was null");
```

**Output Example**

```text
D/AdobeExperienceSDK: MyClassName - Provided data was null
```
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

The log messages from the Adobe Experience SDK are printed to the Apple System Log facility and use a common format that contains the tag `AdobeExperienceSDK`. For example, if logging an error message using `ACPCore.log()`, the printed output looks like `[AdobeExperienceSDK ERROR <tag>]: message`.

#### log

**Syntax**

```text
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

**Example**

```text
[ACPCore log: ACPMobileLogLevelDebug, tag:@"MyClassName", message:@"Provided data was nil"];
```

**Output Example**

```text
[AdobeExperienceSDK DEBUG <MyClassName>]: Provided data was nil
```

**Swift**

#### log

**Syntax**

```swift
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

**Example**

```swift
ACPCore.log(ACPMobileLogLevel.debug, tag: "MyClassName", message: "Provided data was nil");
```

**Output Example**

```text
[AdobeExperienceSDK DEBUG <MyClassName>]: Provided data was nil
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

The log messages from the Adobe Experience SDK are printed to the Log facility and use a common format that contains the tag `ACPMobileLogLevel`. For example, if logging an error message using `ACPCore.log()`, the printed output looks like

```jsx
ACPCore.log(ACPMobileLogLevel.ERROR, "React Native Tag", "React Native Message");
```

Note: `ACPMobileLogLevel` contains the following getters:

```jsx
const ERROR = "ACP_LOG_LEVEL_ERROR";
const WARNING = "ACP_LOG_LEVEL_WARNING";
const DEBUG = "ACP_LOG_LEVEL_DEBUG";
const VERBOSE = "ACP_LOG_LEVEL_VERBOSE";
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

The log messages from the Adobe Experience SDK are printed to the Log facility and use a common format that contains the tag `AdobeExperienceSDK`. For example, if logging an error message using `ACPCore.Log()`, the api call and logging output on Xamarin iOS look like

```csharp
ACPCore.Log(ACPMobileLogLevel.Error, "xamarin tag", "xamarin message");
```

```text
[AdobeExperienceSDK ERROR <xamarin tag>]: xamarin message
```

On Xamarin Android, the api call and logging output are

```csharp
ACPCore.Log(LoggingMode.Error, "xamarin tag", "xamarin message");
```

```text
[AdobeExperienceSDK] xamarin tag - xamarin message
```
{% endtab %}
{% endtabs %}

## Handle open URL action

The Mobile SDK allows you to add a callback function that is triggered before the [`open url`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#consequence-types) action occurs. If the callback function returns **Yes**, the SDK does not complete the `open url` action. If the callback function returns **No**, the SDK completes the `open url` action.

{% tabs %}
{% tab title="iOS" %}
**Objective C**

### registerURLHandler

**Syntax**

```objectivec
+ (void) registerURLHandler: (nonnull BOOL (^) (NSString* __nullable url)) callback;
```

**Example**

```objectivec
[ACPCore registerURLHandler:^BOOL(NSString * _Nullable url) {
    ...
}];
```
{% endtab %}
{% endtabs %}

## Set App Group \(iOS only\)

You can use this API to set the app group used to share user defaults and files among the containing app and the extension apps.

Note: This API _must_ be called in AppDidFinishLaunching and before any other interactions with the Adobe Experience SDK have happened. Only the first call to this function will have any effect.

{% tabs %}
{% tab title="iOS" %}
**Objective-C**

### setAppGroup

**Objective-C**

#### setAppGroup

**Syntax**

```text
+ (void) setAppGroup: (nullable NSString*) appGroup;
```

**Example**

```text
[ACPCore setAppGroup:@"app-group-id"];
```

**Swift**

#### setAppGroup

**Syntax**

```swift
+ (void) setAppGroup: (nullable NSString*) appGroup;
```

**Example**

```swift
ACPCore.setAppGroup("app-group-id")
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

### setAppGroup

**Syntax**

```csharp
public static void SetAppGroup (string appGroup);
```

**Example**

```csharp
ACPCore.SetAppGroup("app_group");
```
{% endtab %}
{% endtabs %}

## Public Classes

{% tabs %}
{% tab title="Android" %}
#### Android

**AdobeCallback**

This class provides the interface to receive results when the async APIs perform the requested action.

```java
public interface AdobeCallback<T> {    
    void call(final T value);
}
```

**AdobeCallbackWithError**

This class provides the interface to receive results or an error when the async APIs perform the requested action. When using this class, if the request cannot be completed within the default timeout or an unexpected error occurs, the request is aborted and the _fail_ method is called with the corresponding _AdobeError_.

```java
public interface AdobeCallbackWithError<T> extends AdobeCallback<T> {
    void fail(final AdobeError error);
}
```

**AdobeError**

Errors which may be passed to an AdobeCallbackWithError:

* `UNEXPECTED_ERROR` - An unexpected error occurred.
* `CALLBACK_TIMEOUT` - The timeout was met.
* `CALLBACK_NULL` - The provided callback function is null.
* `EXTENSION_NOT_INITIALIZED` - The extension is not initialized.

**Example**

```java
MobileCore.getPrivacyStatus(new AdobeCallbackWithError<MobilePrivacyStatus>() {
  @Override
  public void fail(final AdobeError error) {
    if (error == AdobeError.UNEXPECTED_ERROR) {
      // handle unexpected error
    } else if (error == AdobeError.CALLBACK_TIMEOUT) {
      // handle timeout error
    } else if (error == AdobeError.CALLBACK_NULL) {
      // handle null callback error
    } else if (error == AdobeError.EXTENSION_NOT_INITIALIZED) {
      // handle extension not initialized error
    }
  }

  @Override
  public void call(final MobilePrivacyStatus value) {
    // use MobilePrivacyStatus value
  }
});
```
{% endtab %}

{% tab title="iOS" %}
#### iOS

**ACPError**

Errors which may be passed to a completion handler callback from any API which uses one:

* `ACPErrorUnexpected` - An unexpected error occurred.
* `ACPErrorCallbackTimeout` - The timeout was met.
* `ACPErrorCallbackNil` - The provided callback function is nil.
* `ACPErrorExtensionNotInitialized` - The extension is not initialized.

**Examples**

**Objective C**

```text
[ACPCore getPrivacyStatusWithCompletionHandler:^(ACPMobilePrivacyStatus status, NSError * _Nullable error) {
  if (error) {
    if (error.code == ACPErrorCallbackTimeout) {
      // handle timeout error
    } else if (error.code == ACPErrorCallbackNil) {
      // handle nil callback error
    } else if (error.code == ACPErrorExtensionNotInitialized) {
      // handle extension not initialized error
    } else if (error.code == ACPErrorUnexpected) {
      // handle unexpected error
    }
  } else {
    // use privacy status
  }
}];
```

**Swift**

```swift
ACPCore.getPrivacyStatus { (privacyStatus, error) in
  if let error = error {
    let callbackError: NSError = (error as NSError)
    if (callbackError.code == ACPError.callbackTimeout.rawValue) {
      // handle timeout error
    } else if (callbackError.code == ACPError.callbackNil.rawValue) {
      // handle nil callback error
    } else if (callbackError.code == ACPError.extensionNotInitialized.rawValue) {
      // handle extension not initialized error
    } else if (callbackError.code == ACPError.unexpected.rawValue) {
      // handle unexpected error
    }
  } else {
    // use privacyStatus
  }
}
```
{% endtab %}

{% tab title="Xamarin" %}
#### Android

**IAdobeCallback**

This class provides the interface to receive results when the async APIs perform the requested action.

```csharp
public interface IAdobeCallback : IJavaObject, IDisposable, IJavaPeerable
{
    void Call (Java.Lang.Object p0);
}
```

**IAdobeCallbackWithError**

This class provides the interface to receive results or an error when the async APIs perform the requested action. When using this class, if the request cannot be completed within the default timeout or an unexpected error occurs, the request is aborted and the _fail_ method is called with the corresponding _AdobeError_.

```csharp
public interface IAdobeCallbackWithError : IAdobeCallback, IJavaObject, IDisposable, IJavaPeerable
{
    void Fail (AdobeError p0);
}
```

**AdobeError**

Errors which may be passed to an AdobeCallbackWithError:

* `UnexpectedError` - An unexpected error occurred.
* `CallbackTimeout` - The timeout was met.
* `CallbackNull` - The provided callback function is null.
* `ExtensionNotInitialized` - The extension is not initialized.

**Example**

```csharp
ACPCore.GetPrivacyStatus(new AdobeCallbackWithError());

class AdobeCallbackWithError : Java.Lang.Object, IAdobeCallbackWithError
{
  public void Call(Java.Lang.Object stringContent)
  {
    if (stringContent != null)
    {
      Console.WriteLine("String callback content: " + stringContent);
    }
    else
    {
      Console.WriteLine("null content in string callback");
    }
  }

  public void Fail(AdobeError error)
  {
    if (error == AdobeError.UnexpectedError)
    {
      // handle unexpected error
    }
    else if (error == AdobeError.CallbackTimeout)
    {
      // handle timeout error
    }
    else if (error == AdobeError.CallbackNull)
    {
      // handle null callback error
    }
    else if (error == AdobeError.ExtensionNotInitialized)
    {
      // handle extension not initialized error
    }
  }
}
```

#### iOS

**ACPError**

Errors which may be passed to a completion handler callback from any API which uses one:

* `ACPError.Unexpected` - An unexpected error occurred.
* `ACPError.CallbackTimeout` - The timeout was met.
* `ACPError.CallbackNil` - The provided callback function is nil.
* `ACPError.ExtensionNotInitialized` - The extension is not initialized.

**Example**

```csharp
ACPCore.GetPrivacyStatusWithCompletionHandler((privacyStatus, error) => {
  if (error != null)
  {
    if ( error.Code == (int)ACPError.CallbackTimeout)
    {
      // handle timeout error
    }
    else if (error.Code == (int)ACPError.CallbackNil) 
    {
      // handle nil callback error
    }
    else if (error.Code == (int)ACPError.ExtensionNotInitialized)
    {
      // handle extension not initialized error
    }
    else if (error.Code == (int)ACPError.Unexpected)
    {
      // handle unexpected error
    }
  }
  else
  {
    Console.WriteLine("privacy status: " + privacyStatus);
  }
});
```
{% endtab %}
{% endtabs %}

### Additional Information

* What is [context data](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=en#vars)?

