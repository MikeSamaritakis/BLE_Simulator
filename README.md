# BLE Simulator

Android application for simulating a BLE iBeacon using a spare Android phone. The app was created to support thesis testing where a physical BLE beacon was unavailable.

## Simulated Beacon

Default beacon identity:

```text
Beacon ID: SamA15
UUID: f7826da6-4fa2-4e98-8024-bc5b71e0893e
Major: 20641
Minor: 50361
Measured power: -80
```

The beacon ID is shown inside the app for identification. Standard iBeacon advertisements do not include a free-form text ID, so BLE scanners identify the beacon by UUID, major, minor, and measured power.

## Features

- Advertises a standard iBeacon payload over Bluetooth Low Energy.
- Editable UUID, major, minor, measured power, and TX power level.
- Shows status messages for missing permissions, Bluetooth disabled, unsupported BLE advertising, and active advertising.
- Stops advertising when the user presses Stop or when the app is closed.

## Requirements

- Android phone with BLE advertising support.
- Android 6.0 or newer.
- Bluetooth enabled.
- Bluetooth advertising permission granted on Android 12 or newer.

Some Android phones can scan BLE devices but cannot advertise as one. If the phone does not support BLE advertising, the app will show a status message.

## Build

Open the project in Android Studio and run the `app` configuration on a connected Android device.

Command-line build using Android Studio's bundled JDK:

```powershell
$env:JAVA_HOME='C:\Program Files\Android\Android Studio\jbr'; .\gradlew.bat assembleDebug
```

The debug APK is generated at:

```text
app/build/outputs/apk/debug/app-debug.apk
```

To generate an unsigned release APK:

```powershell
$env:JAVA_HOME='C:\Program Files\Android\Android Studio\jbr'; .\gradlew.bat assembleRelease
```

The release APK is generated at:

```text
app/build/outputs/apk/release/app-release-unsigned.apk
```

## Testing

1. Install and open the app on the Android phone used as the simulated beacon.
2. Confirm the default values or edit them as needed.
3. Press **Start advertising**.
4. On a second phone, use a BLE scanner app such as nRF Connect or Beacon Scanner.
5. Scan for an iBeacon matching the UUID, major, and minor values above.

## Thesis Usage

For demonstration or appendix material, include:

```text
app-debug.apk
app-release-unsigned.apk
source code
```

For easy installation on a test phone, use the debug APK or generate a signed release APK from Android Studio with **Build > Generate Signed App Bundle / APK**.
