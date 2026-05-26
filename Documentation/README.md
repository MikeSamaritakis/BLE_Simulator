# BLE Simulator

## Overview

BLE Simulator is an Android application that simulates a Bluetooth Low Energy iBeacon advertisement by using an Android smartphone. The application allows a compatible smartphone to transmit configurable iBeacon identity parameters during controlled experimental work.

## Purpose in Thesis Work

This application was developed as a supporting helper tool for a Bachelor's thesis. It was used to generate configurable iBeacon advertisements during testing and validation of the main Android thesis project, OIPASFT. The simulator is not the primary thesis contribution. Its role is to provide repeatable BLE beacon identity parameters for controlled experiments.

The main thesis implementation is a separate Android Studio project. This repository contains only the BLE Simulator helper tool.

## Experimental Device Roles

The following device roles were used during thesis experimentation.

1. Samsung Galaxy A15: beacon advertiser running the BLE Simulator application.
2. Xiaomi Redmi Note 10: beacon advertiser running the BLE Simulator application.
3. Ulefone Armor 22: scanner and detector running the custom thesis application OIPASFT.

In some tests, one smartphone was used at a time as the simulated BLE beacon. In other tests, a mixed setup was used with physical BLE beacons and smartphones running the BLE Simulator software. The Ulefone Armor 22 was used as the scanner and detector device.

Android versions used in the documented setup:

1. Samsung Galaxy A15: Android 14
2. Xiaomi Redmi Note 10: Android 13
3. Ulefone Armor 22: Android 13

## Configurable Beacon Parameters

The following parameters are configurable in the application.

1. Beacon ID: Local descriptive label used by the application and Logcat output.
2. UUID: iBeacon proximity UUID.
3. Major: 16 bit unsigned iBeacon major value.
4. Minor: 16 bit unsigned iBeacon minor value.
5. Measured power: Calibrated RSSI value at one metre, encoded in the iBeacon payload.
6. TX power level: Android advertising power level represented as 0 to 3.

The Beacon ID is not transmitted in the iBeacon advertisement. Standard iBeacon frames are identified by UUID, major, minor, and measured power.

## Sample Default Configuration

The current sample experimental defaults are shown below.

```text
Beacon ID: SamA15
UUID: f7826da6-4fa2-4e98-8024-bc5b71e0893e
Major: 20641
Minor: 50361
Measured power: -80
TX power level: 3
```

These values are sample experimental defaults and may be changed for each device or test session.

## System Requirements

1. Android device with BLE advertising support.
2. Android 6.0 or newer.
3. Bluetooth enabled.
4. Required Bluetooth permissions on Android 12 or newer.
5. Awareness that some Android devices support BLE scanning but not BLE advertising.

## Build Instructions

Open the project in Android Studio and run the `app` configuration on a connected Android device.

The following command line examples are Windows PowerShell examples using Android Studio's bundled JDK.

Debug build:

```powershell
$env:JAVA_HOME='C:\Program Files\Android\Android Studio\jbr'; .\gradlew.bat assembleDebug
```

Debug APK output:

```text
app/build/outputs/apk/debug/app-debug.apk
```

Release build:

```powershell
$env:JAVA_HOME='C:\Program Files\Android\Android Studio\jbr'; .\gradlew.bat assembleRelease
```

Release APK output:

```text
app/build/outputs/apk/release/app-release-unsigned.apk
```

For an installable release APK, generate a signed APK through Android Studio using Build, then Generate Signed App Bundle or APK. Keystore files and passwords must not be committed to version control.

## Running the Application

1. Install the APK on the Android device that will act as the simulated beacon.
2. Open the BLE Simulator application.
3. Confirm or edit the beacon parameters.
4. Press Start advertising.
5. Use the Ulefone Armor 22 running OIPASFT to scan or detect the beacon.
6. Press Stop advertising when finished.

## Logcat Observation

The application uses the stable Logcat tag shown below.

```text
BLEBeaconSimulator
```

Filter logs with:

```powershell
adb logcat -s BLEBeaconSimulator
```

The logs record lifecycle events, permission results, validation results, Bluetooth capability checks, advertising start and stop events, and failures.

## Manual Validation Procedure

1. Install and open the BLE Simulator application on either the Samsung Galaxy A15 or the Xiaomi Redmi Note 10.
2. Confirm or edit the beacon parameters.
3. Start Logcat filtering with the following command.

   ```powershell
   adb logcat -s BLEBeaconSimulator
   ```

4. Press Start advertising in the BLE Simulator application.
5. Use the Ulefone Armor 22 running OIPASFT as the scanner and detector.
6. Confirm that the detected iBeacon matches the configured UUID, major, and minor values.
7. Press Stop advertising.
8. Save the Logcat output and scanner or detector evidence as validation evidence.

## Validation Example

```text
Advertising device 1: Samsung Galaxy A15
Advertising device 1 Android version: Android 14

Advertising device 2: Xiaomi Redmi Note 10
Advertising device 2 Android version: Android 13

Scanner and detector device: Ulefone Armor 22
Scanner and detector Android version: Android 13

Scanner and detector application: OIPASFT

Configured UUID: f7826da6-4fa2-4e98-8024-bc5b71e0893e
Major: 20641
Minor: 50361
Measured power: -80
TX power level: 3
```

Result:
The Samsung Galaxy A15 and Xiaomi Redmi Note 10 were used as Android devices capable of running the BLE Simulator application and advertising configurable iBeacon payloads. The Ulefone Armor 22 was used as the scanner and detector device running the custom thesis application OIPASFT. In the validation setup, the detected UUID, major, and minor values were checked against the configuration entered in the BLE Simulator application.

## Known Limitations

1. BLE advertising support depends on Android device hardware and firmware.
2. The simulator advertises only while the application activity is active.
3. Beacon ID is an application level label and is not part of the iBeacon radio payload.
4. RSSI values vary due to distance, orientation, device chipset, antenna placement, environmental interference, and multipath propagation.
5. The simulator should not be treated as a calibrated RF reference instrument.

The simulator should be treated as a practical experimental substitute for a beacon identity source rather than as a calibrated RF reference instrument.

## Repository Contents

1. `app/`: Android application source code and resources.
2. `README.md`: General repository overview and usage instructions.
3. `THESIS_DOCUMENTATION.md`: Formal thesis oriented documentation for the helper tool.
4. `VALIDATION_TEMPLATE.md`: Template for recording validation runs.
5. `SUBMISSION_NOTES.md`: Notes describing how this repository fits into the thesis submission package.
6. `validation/DEVICE_INFORMATION.md`: Confirmed device roles and Android versions.
7. `validation/VALIDATION_NOTES.md`: Notes file for real validation observations.
8. `validation/*.logcat`: Logcat evidence files, when available.

## Thesis Use

For thesis submission, this repository should be delivered together with the following materials.

1. Full source code.
2. APK file.
3. `README.md`.
4. `THESIS_DOCUMENTATION.md`.
5. `VALIDATION_TEMPLATE.md`.
6. Logcat success example.
7. Validation notes.
8. Device information file.
9. Evidence from the Ulefone Armor 22 scanner and detector, if available.

Raw evidence files should be reviewed before public upload because Logcat exports may contain device metadata.

## Citation

M. Samaritakis, "BLE Simulator: Android BLE iBeacon simulator," GitHub repository, 2026. [Online]. Available: https://github.com/MikeSamaritakis/BLE_Simulator
