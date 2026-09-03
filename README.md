# bmi-270 board

Compact wireless 6-axis motion sensor board. Single-cell LiPo or USB powered,
with USB-serial for flashing and debug. Part of a larger project aimed at playing fighting games using the body.

## Hardware

| Part | Function |
|------|----------|
| ESP32-C3-MINI-1-N4 | RISC-V MCU, 4 MB flash, Wi-Fi + BLE |
| BMI270 | 6-axis IMU (accel + gyro), I²C @ 0x68 |
| AP2112K-3.3 | 600 mA LDO |
| CH343P | USB-serial bridge |
| SS-12D00-G3 | SPDT slide switch — selects VBAT or VBUS as LDO input |
| JST-PH 2-pin | Battery input (no onboard charger) |

2-layer, ~40 × 42 mm. Module antenna overhangs the board edge.

![3D View](3d-View.png)
*3D View*

## Notes

- **No auto-reset.** CH343P DTR/RTS are unconnected. To flash: hold SW1, tap SW2,
  release SW1.
- **No native USB.** IO18/IO19 are used for LEDs, so USB-CDC and USB-JTAG are
  unavailable. All flashing and console goes through the CH343P.
- **No charger.** Cells must be charged externally. LDO dropout puts the practical
  low-battery cutoff around 3.6 V.
- **No reverse-polarity protection** on the battery connector. Verify cell polarity
  against CN1 (pin 1 = +) before connecting.

## Status

Board 1 assembled and under test.

- [x] Pre-power continuity checks
- [x] 3.3 V rail up
- [x] USB enumerates (CH343P)
- [ ] ROM boot log
- [ ] Flash / firmware
- [ ] IMU bring-up

### Rework log (board 1)

- One USB-C CC pin had a cold joint — board only powered with the cable in one
  orientation. Reflow CC1/CC2.
- D2 not conducting; 3.3 V rail dead until reworked.