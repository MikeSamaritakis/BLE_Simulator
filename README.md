# BLE Simulator

BLE Simulator is a small Android application used to simulate Bluetooth Low Energy iBeacon advertisements from an Android phone.

This repository is mainly included as a supporting helper tool for thesis testing. It is not the main thesis application. Its purpose is to provide configurable BLE beacon values so that the main scanner/detector application can be tested in a controlled way.

## What the app does

The app allows an Android device to advertise iBeacon style BLE data with configurable values such as:

- UUID
- Major value
- Minor value
- Measured power
- TX power level
- Local beacon label used inside the app

The local beacon label is only used by the application and logs. It is not part of the actual iBeacon advertisement payload.

## How it was used

During thesis testing, this app was installed on Android smartphones that acted as simulated BLE beacon advertisers.

The main thesis application, OIPASFT, was used separately as the scanner/detector application. BLE Simulator provided repeatable beacon identity values for testing, observation, and validation.

## Repository structure

Reviewers should start with the following locations:

| Location | Purpose |
|---|---|
| `Documentation/README.md` | Main usage explanation, build steps, running instructions, and validation procedure. |
| `Documentation/THESIS_DOCUMENTATION.md` | More formal explanation of the tool's role in the thesis methodology. |
| `Documentation/SUBMISSION_NOTES.md` | Notes explaining how this helper tool fits into the thesis submission package. |
| `Evidence/` | Supporting device information, validation notes, screenshots, or Logcat evidence where available. |
| `app/` | Android application source code. |
| `LICENSE` | Repository license information. |

## For reviewers

If you only need a quick understanding of the project, read this file first and then open:

1. `Documentation/README.md`
2. `Documentation/THESIS_DOCUMENTATION.md`
3. `Documentation/SUBMISSION_NOTES.md`

If you want to check how the app works technically, review the source code inside:

```text
app/
```

If you want to check how the tool was used during testing, review:

```text
Evidence/
Documentation/THESIS_DOCUMENTATION.md
```

## Basic build and run information

Open the project in Android Studio and run the `app` configuration on a physical Android device that supports BLE advertising.

A physical device is required because the app depends on Android Bluetooth Low Energy advertising functionality.

## Important note

This project should be treated as a practical experimental helper tool. It is useful for generating repeatable beacon identity data, but it should not be treated as a calibrated radio frequency measurement instrument.

## License

This repository is licensed under the GNU General Public License v3.0. See `LICENSE` for details.
