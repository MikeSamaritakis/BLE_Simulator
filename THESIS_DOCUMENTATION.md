# Thesis Documentation: Android BLE iBeacon Simulator

## Abstract

This application implements an Android-based simulator for Bluetooth Low Energy iBeacon advertisements. It was developed to support experimental work in which a physical beacon was unavailable or where configurable beacon identities were required for repeated thesis measurements. The simulator provides an editable interface for the main iBeacon parameters and records operational events through structured Logcat output.

## Implementation Overview

The application is implemented as a single Android activity using Jetpack Compose for the user interface. The BLE advertising functionality is provided by Android's `BluetoothLeAdvertiser` API. When the user starts advertising, the application validates the entered beacon parameters, checks Bluetooth capability and permission state, constructs the iBeacon manufacturer payload, and submits a non-connectable BLE advertisement request.

The simulator is designed for foreground experimental use. Advertising is stopped when the user presses the stop control or when the activity is destroyed. This behaviour makes the advertising period explicit and easier to correlate with experimental logs.

## iBeacon Data Model

The transmitted iBeacon payload contains:

- A fixed iBeacon prefix.
- The proximity UUID.
- The major value.
- The minor value.
- The measured power value.

The application also exposes a **Beacon ID** field. This field is used for human-readable identification in the interface and in Logcat, but it is not part of the standard iBeacon advertisement frame. Therefore, external BLE scanners should verify the simulated beacon through UUID, major, minor, and measured power.

Current sample defaults:

```text
Beacon ID: SamA15
UUID: f7826da6-4fa2-4e98-8024-bc5b71e0893e
Major: 20641
Minor: 50361
Measured power: -80
TX power level: 3
```

These values should be treated as configurable experimental parameters rather than fixed system constants.

## Logcat Instrumentation

The application records operational events under the following Logcat tag:

```text
BLEBeaconSimulator
```

Recommended observation command:

```powershell
adb logcat -s BLEBeaconSimulator
```

The logging strategy supports experimental traceability by recording:

- Activity creation and destruction.
- User requests to start or stop advertising.
- Runtime Bluetooth permission results.
- Invalid configuration values.
- Bluetooth adapter availability and state.
- BLE advertising capability checks.
- Advertisement start success.
- Advertisement start failure with Android error-code interpretation.
- Advertisement shutdown.

No signing credentials, passwords, or private keystore information are logged.

## Expected Successful Log Sequence

A typical successful session should contain entries similar to:

```text
I/BLEBeaconSimulator: Activity created for BLE beacon simulation.
I/BLEBeaconSimulator: User requested advertising start.
D/BLEBeaconSimulator: All required runtime Bluetooth permissions are granted.
I/BLEBeaconSimulator: Validated beacon configuration: beaconId=SamA15, uuid=f7826da6-4fa2-4e98-8024-bc5b71e0893e, major=20641, minor=50361, measuredPower=-80, txPowerLevel=3
D/BLEBeaconSimulator: Bluetooth adapter detected.
D/BLEBeaconSimulator: Bluetooth adapter is enabled.
D/BLEBeaconSimulator: BLE multiple advertisement support is available.
I/BLEBeaconSimulator: Submitting iBeacon advertisement request: beaconId=SamA15, uuid=f7826da6-4fa2-4e98-8024-bc5b71e0893e, major=20641, minor=50361, measuredPower=-80, txPowerLevel=3
I/BLEBeaconSimulator: Advertising started successfully: beaconId=SamA15, uuid=f7826da6-4fa2-4e98-8024-bc5b71e0893e, major=20641, minor=50361, measuredPower=-80, txPowerLevel=3
I/BLEBeaconSimulator: Stopping BLE advertisement due to: user request.
I/BLEBeaconSimulator: Advertising state cleared.
```

## Common Failure Cases

If Bluetooth is disabled:

```text
W/BLEBeaconSimulator: Bluetooth adapter is present but disabled.
```

If the device does not support BLE advertising:

```text
W/BLEBeaconSimulator: BLE multiple advertisement support is not available on this device.
```

If an invalid UUID is entered:

```text
W/BLEBeaconSimulator: Configuration validation failed: invalid UUID value '<entered value>'.
```

If Android rejects the advertisement request:

```text
E/BLEBeaconSimulator: Advertising failed with code <code> (<interpreted reason>).
```

## Reproducibility Notes

For reproducible measurements, the following information should be recorded for each session:

- Android device model used as the simulator.
- Android version.
- Beacon ID.
- UUID, major, minor, measured power, and TX power level.
- Approximate physical placement of the simulator device.
- BLE scanner application and scanner device model.
- Logcat output for the advertising session.

RSSI values observed by receivers are expected to vary because of device orientation, antenna placement, environmental interference, and multipath propagation. The simulator should therefore be treated as a practical experimental substitute for a beacon identity source rather than as a calibrated RF reference instrument.

## Suggested Thesis Appendix Text

The BLE beacon used in the experimental setup was simulated with a custom Android application running on a spare Android device. The application used Android's `BluetoothLeAdvertiser` API to emit a non-connectable iBeacon advertisement containing configurable UUID, major, minor, and measured-power values. A local beacon identifier was maintained in the application interface and Logcat output for documentation purposes; however, this identifier was not transmitted in the iBeacon payload. Experimental runs were monitored through Logcat using the tag `BLEBeaconSimulator`, which recorded permission state, configuration validation, Bluetooth capability checks, and advertising start or failure events.
