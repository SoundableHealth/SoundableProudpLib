# iOS SDK usage guide

### Sample App link: 
https://github.com/SoundableHealth/soundable-proudp-sample

### 1. Add SoundableProudPLib package

1. Xcode > File > Add Packages Dependencies...
<img width="400" alt="image" src="https://github.com/user-attachments/assets/12abf0e6-b87e-4ce6-9d33-36b4a44db905">

2. Input respository url: https://github.com/SoundableHealth/SoundableProudpLib
<img width="800" alt="image" src="https://github.com/user-attachments/assets/4d196efa-3738-4f8c-8247-a51f1d438f77">

4. Click "Add Package"


### 2. Allow microphone usage
1. In Xcode, click "Info" for your Targets application.
2. Click "+" and select "Privacy - Microphone Usage Description".
3. Write a microphone permission request message.
<img width="800" alt="image" src="https://github.com/user-attachments/assets/c1453697-bffd-4455-abb2-b30c2aa474d7">


### 3. Initialize SDK

1. import SoundableProudpLib

```swift
import SoundableProudpLib
```
2. Set backend server configuration
```swift
let soundableProudpLib = SoundableProudpLib()
// contact to dev@soundable.health to get server configration keys
soundableProudpLib.setServerConfig(serverUrl: "serverApiUrl", apiKey: "xApiKey", websocketUrl: "webSocketUrl")
```
3. Check microphone usage permission
```swift
soundableProudpLib.checkPermission()
```

### 4. Start recording

1. Enter 3 key values before recording
    - userId: user's de-identified ID
    - gener: m(male) or f(female)
    - clinic : clinic name or company name


```swift
soundableProudpLib.startRecording(userId: "soundableTest", gender: "m", clinic: "soundable")
```

### 5. Cancel recording

- Cancel recording and delete the recorded file.

```swift
soundableProudpLib.cancelRecording()
```

### 6. Stop recording

- Finish recording and upload the recording file to the server.

```swift
soundableProudpLib.stopRecording()
```

### 7. Get result

- Register Notificaiton Observer
- Notification name is "SoundableProudpLib"
- Implement the observer's method to perform actions when the notification is received.

```swift
.onReceive(NotificationCenter.default.publisher(for: Notification.Name("SoundableProudpLib"))) { notification in
    if let result = notification.userInfo?["result"] as? String {
        print("received result", result)
    }
}
```
