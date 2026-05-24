# BLE Simulator

This repository contains an Android application that simulates a Bluetooth Low Energy (BLE) iBeacon by using a spare Android device. The application was developed to support thesis experimentation in cases where a physical BLE beacon is unavailable or where repeated controlled beacon configurations are required.

## Purpose

The application enables an Android device to advertise a configurable iBeacon payload. It is intended for experimental validation, indoor-positioning tests, BLE scanning workflows, and thesis demonstrations where beacon identity parameters must be reproduced in a controlled manner.

The simulator exposes the relevant iBeacon parameters through the user interface so that each device or experimental session can be configured independently.

## Configurable Beacon Parameters

The following parameters are editable in the application:

- **Beacon ID**: A local descriptive label used by the application and Logcat output.
- **UUID**: The iBeacon proximity UUID.
- **Major**: A 16-bit unsigned iBeacon major value.
- **Minor**: A 16-bit unsigned iBeacon minor value.
- **Measured power**: The calibrated RSSI value at one metre, encoded in the iBeacon payload.
- **TX power level**: Android advertising power level, represented as `0` to `3`.

The beacon ID is not transmitted inside the iBeacon advertisement. Standard iBeacon frames are identified by UUID, major, minor, and measured power.

## Sample Default Configuration

The current sample defaults are:

```text
Beacon ID: SamA15
UUID: f7826da6-4fa2-4e98-8024-bc5b71e0893e
Major: 20641
Minor: 50361
Measured power: -80
TX power level: 3
```

These values are experimental defaults and may be changed for each device or test session.

## System Requirements

- Android device with BLE advertising support.
- Android 6.0 or newer.
- Bluetooth enabled.
- Bluetooth advertising and connection permissions granted on Android 12 or newer.

Some Android devices support BLE scanning but do not support BLE advertising. In that case, the application reports the limitation both on screen and in Logcat.

## Build Instructions

Open the project in Android Studio and run the `app` configuration on a connected Android device.

Command-line debug build using Android Studio's bundled JDK:

```powershell
$env:JAVA_HOME='C:\Program Files\Android\Android Studio\jbr'; .\gradlew.bat assembleDebug
```

The debug APK is generated at:

```text
app/build/outputs/apk/debug/app-debug.apk
```

Command-line release build:

```powershell
$env:JAVA_HOME='C:\Program Files\Android\Android Studio\jbr'; .\gradlew.bat assembleRelease
```

The unsigned release APK is generated at:

```text
app/build/outputs/apk/release/app-release-unsigned.apk
```

For an installable release APK, generate a signed APK through Android Studio using **Build > Generate Signed App Bundle / APK**. Keystore files and passwords must not be committed to version control.

## Logcat Observation

The application uses the stable Logcat tag:

```text
BLEBeaconSimulator
```

Filter logs with:

```powershell
adb logcat -s BLEBeaconSimulator
```

The logs document application lifecycle events, permission results, configuration validation, Bluetooth adapter capability checks, advertising start and stop events, and advertising failures. The logged beacon parameters correspond to observable experimental identifiers and are suitable for reproducing test conditions.

## Manual Validation Procedure

1. Install and open the application on the Android device used as the simulated beacon.
2. Confirm or edit the beacon parameters.
3. Start Logcat filtering with `adb logcat -s BLEBeaconSimulator`.
4. Press **Start advertising** in the application.
5. Use a second phone with a BLE scanner, such as nRF Connect or Beacon Scanner.
6. Scan for an iBeacon matching the configured UUID, major, and minor values.
7. Press **Stop advertising** and confirm that the advertising shutdown is reflected in Logcat.

## Known Limitations

- BLE advertising support depends on the Android device hardware and firmware.
- The simulator advertises only while the application activity is active.
- The beacon ID is an application-level experimental label and is not part of the iBeacon radio payload.
- RSSI observed by scanners varies with distance, orientation, device chipset, and environmental interference.

## Thesis Use

For thesis submission or appendix material, include the source code, generated APK, and a short description of the device used for advertising. The file `THESIS_DOCUMENTATION.md` contains a more formal description of the implementation and suggested text that may be adapted for academic reporting.
