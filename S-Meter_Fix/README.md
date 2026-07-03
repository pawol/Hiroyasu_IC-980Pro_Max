# 📡 Hiroyasu IC-980Pro Max S-Meter Calibration

## Overview

The original calibration procedure was proposed by **[pawol](https://github.com/pawol)/[SP6PW](https://www.qrz.com/db/SP6PW)** in the GitHub [discussion](https://github.com/vegos/Hiroyasu_IC-980Pro_Max/issues/1).

This document describes the calibration procedure that was followed, together with the measured results obtained on **my own radio**.

> **Important:** Calibration values are **radio-specific** and should **not** be copied blindly. Always calibrate your own unit.

---

## Tested Firmware

**Software Version:** `V20251031.01`

---

## ⚠️ Note

**Always read first the current service values and save them as a backup before making any changes.**

---

# Equipment Used

* Hiroyasu IC-980Pro Max
* TinySA Ultra+
* 30 dB SMA attenuator
* 40 dB SMA attenuator
* Total attenuation: **70 dB**
* SMA pigtail
* SMA-to-UHF adapter

---

# Radio Preparation

* Set **Squelch = 0**
* Switch to **Single VFO** mode (`MENU` → `V/M`)
* Tune to **145.000 MHz**
* Enter the hidden **WW01 Service Menu**
* Read and save (backup) the current calibration values

---

# TinySA Configuration

* Put TinySA in **Frequency Generator** mode
* Output Mode: **LOW Output ON**
* Frequency: **145.000 MHz**
* Modulation: **FM**
* Audio Tone: **1000 Hz**
* FM Deviation: **3.0 kHz**
* External Gain: **-70 dB**

The TinySA output was connected directly to the radio antenna connector through two fixed attenuators (30 dB + 40 dB, total 70 dB).

![TinySA settings](images/TinySA.jpg)  

![Attenuators Used](images/Attenuators.jpg)  
  
---

# Calibration Procedure

## SQ-1

Set the TinySA output level to **-129 dBm**.

Adjust **SQ-1** until the radio displays exactly **S3**.

Verify the following levels:

| RF Level | Expected Display |
| -------: | ---------------- |
| -135 dBm | S2               |
| -129 dBm | S3               |
| -123 dBm | S4               |

Repeat changes on SQ-1 until all three levels are displayed correctly.

> **Important:** Unlike SQ-5 and SQ-9, **SQ-1 should not simply be copied from the CPS "Signal" value**. It must be adjusted manually until the displayed S-meter matches the expected levels.

![S1](images/S1.jpg)  
  
---

## SQ-5

Set the TinySA output level to **-117 dBm**.

Open **Read Status** in the CPS.

Copy the **Signal** value into **SQ-5**.

Verify that the radio displays **S5**.

![S5](images/S5.jpg)  
  
---

## SQ-9

Set the TinySA output level to **-93 dBm**.

Open **Read Status**.

Copy the **Signal** value into **SQ-9**.

![S9](images/S9.jpg)  
  
---

# Final Calibration Values

| Parameter |   Value |
| --------- | ------: |
| SQ-1      |  **80** |
| SQ-5      | **119** |
| SQ-9      | **165** |

---

# Calibration Verification

The resulting calibration was verified on **both amateur bands**.

## VHF (145 MHz)

| RF Level | Display                           |
| -------: | --------------------------------- |
| -135 dBm | S2                                |
| -129 dBm | S3                                |
| -123 dBm | S4                                |
| -117 dBm | S5                                |
| -103 dBm | S8                                |
| -102 dBm | Beginning of MAX (2 red segments) |
|  -96 dBm | MAX (full scale)                  |

---

## UHF (435 MHz)

| RF Level | Display                                |
| -------: | -------------------------------------- |
| -129 dBm | S3                                     |
| -123 dBm | S4                                     |
| -117 dBm | S4/S5 initially, then stabilizes at S5 |
| -106 dBm | Beginning of S8                        |
| -103 dBm | S8                                     |
|  -96 dBm | Approximately half of the MAX region   |
|  -94 dBm | MAX (full scale)                       |

---

# Read Status Reference Values

These values were observed **before** calibration (using my old/*rough calibration procedure*).

## 145 MHz – Antenna Connected

| Parameter | Value |
| --------- | ----: |
| Signal    |   120 |
| Noise     |    64 |
| Glitch    |    44 |
| Volt      |   114 |
| VOX       |     0 |

---

## 145 MHz – No Antenna Connected

| Parameter | Value |
| --------- | ----: |
| Signal    |   101 |
| Noise     |    63 |
| Glitch    |    56 |

---

## 145 MHz – TinySA Connected (Generator OFF, 70 dB attenuation)

| Parameter | Value |
| --------- | ----: |
| Signal    |    90 |
| Noise     |    61 |
| Glitch    |    43 |

---

# Observations

* The calibration procedure proposed by **[pawol](https://github.com/pawol)/[SP6PW](https://www.qrz.com/db/SP6PW)** works correctly.
* The resulting calibration values differ from those measured on SP6PW's radio.
* This indicates that calibration is **radio-specific**. The values may only be useful as a starting point.
* **SQ-1** must be adjusted manually based on the displayed S-meter.
* **SQ-5** and **SQ-9** matched the values obtained from the CPS **Read Status → Signal** field.
* The calibration was successfully verified on **both 145 MHz and 435 MHz**.
* The upper end of the S-meter is compressed by the firmware. The display transitions directly from **S8** into the **MAX** region without a dedicated **S9** indication.

---

## Comparison with Other Receivers

The following measurements were performed using the **same TinySA Ultra+ generator setup** and the **same 70 dB attenuation chain** (at 145.000MHz).

These results are intended only as a comparison between different receiver S-meter implementations. They should **not** be considered absolute laboratory measurements.

| TinySA Output | Hiroyasu IC-980Pro Max | Quansheng UV-K1* | Alinco DJ-X30E | Yaesu VX-3 |
|--------------:|------------------------|------------------|----------------|------------|
| Noise floor | — | -125...-126 dBm (S3) | No bars | 2 bars |
| -135 dBm | S2 | -123...-125 dBm (S3/S4) | No bars | 2 bars |
| -129 dBm | S3 | — | 1 bar (barely visible) | 2 bars |
| -123 dBm | S4 | — | 1 bar | 2 bars |
| -117 dBm | S5 | -111 dBm (S6) | 2 bars | 2 bars |
| -111 dBm | ~S6 | -106 dBm (S6) | 4 bars | 2 bars |
| -105 dBm | ~S7 | -100 dBm (S7) | Full scale | 2 bars |
| -103 dBm | S8 | — | Full scale | ~2–3 bars |
| -101 dBm | — | — | — | 3 bars |
| -99 dBm | — | -93 dBm (S9) | Full scale | 3 bars |
| -98 dBm | — | — | — | 4 bars |
| -95 dBm | — | — | Full scale | 5 bars (stabilizes at -94 dBm) |
| -94 dBm | — | — | Full scale | 5 bars (stable) |
| -93 dBm | MAX | -87 dBm (S9) | Full scale | 5 bars |
| -91 dBm | MAX | — | Full scale | 6 bars (maximum) |

\* The UV-K1 was running [Armel's](https://github.com/armel) [v5.6.1 firmware](https://github.com/armel/uv-k1-k5v3-firmware-custom/releases/tag/v5.6.1) displaying both RSSI (dBm) and S-meter.

### Notes

- Different manufacturers implement S-meters differently.
- The Hiroyasu calibration described in this document aligns the internal thresholds with known RF levels.
- It does **not** guarantee identical S-meter behaviour compared to other radios.
- The Yaesu, Alinco and Quansheng receivers all showed significantly different S-meter scaling despite receiving the same RF signal level.

---

# Conclusion

After calibration, the S-meter behaves significantly better than the factory configuration.

Instead of switching almost directly from no indication to full scale, the radio now displays intermediate signal levels consistently across both VHF and UHF.

Although the upper part of the display remains compressed due to firmware behavior, the resulting calibration provides a much more useful and realistic indication of received signal strength.
  
---

## Related Documentation

- 📊 [RF Power Measurements](../Measurements/README.md)
- ⚙️ [CPS Explained](../CPS_Explained/README.md)
- 🐍 [Import / Export Tool](../Import-Export_Script/README.md)
