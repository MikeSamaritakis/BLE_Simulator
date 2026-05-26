# Submission Notes

This repository contains the BLE Simulator helper tool used during the Bachelor's thesis work.

The main thesis implementation is a separate Android Studio project named OIPASFT.

This BLE Simulator was used only as a supporting tool to generate configurable iBeacon advertisements for testing and validation.

## Confirmed Device Roles

1. Samsung Galaxy A15: BLE Simulator advertiser, Android 14.
2. Xiaomi Redmi Note 10: BLE Simulator advertiser, Android 13.
3. Ulefone Armor 22: scanner and detector running OIPASFT, Android 13.

Testing was not limited to one fixed arrangement. In some tests, one smartphone was used at a time as the simulated BLE beacon. In other tests, physical BLE beacons were used together with smartphones running the BLE Simulator software. The Ulefone Armor 22 was used as the scanner and detector device.

## Recommended Thesis Submission Placement

```text
Thesis_Submission_Samaritakis/
  01_Thesis_Document/
  02_Main_Thesis_Project/
  03_BLE_Simulator_Helper_Tool/
    Source_Code/
    APK/
    Documentation/
    Validation/
  04_Experiment_Evidence/
```

## Recommended Included Files For This Tool

1. Full source code.
2. `README.md`.
3. `THESIS_DOCUMENTATION.md`.
4. `VALIDATION_TEMPLATE.md`.
5. APK file.
6. Logcat success example.
7. `validation/DEVICE_INFORMATION.md`.
8. `validation/VALIDATION_NOTES.md`.
9. Evidence from the Ulefone Armor 22 scanner and detector.

## Files That Should Not Be Included

1. `local.properties`.
2. Keystore files.
3. Passwords.
4. API keys.
5. Build folders.
6. IDE cache files.
