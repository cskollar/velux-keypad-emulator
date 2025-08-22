# Velux Keypad Emulator (ESPHome)

A very simple Velux keypad emulator based on ESPHome.  
This is a proof-of-concept code to control old (1997-2018) Velux/WindowMaster systems (e.g.: Velux WLC 100 51).

---

## Overview

This project provides a minimal working **PoC (Proof of Concept)** implementation for emulating a Velux keypad using ESPHome.  
The communication protocol was reverse-engineered with a Rigol DS1054Z oscilloscope by sniffing a **WLI 130** keypad connected to a **WLC 100** controller.

The code is expected to be compatible with other Velux/Windowmaster keypads from the same era (e.g. **WLI 110**), but this has not been tested.

---

## Limitations

- **No motor addressing implemented** – only motor **#1** on the WLC 100 is operated.
- Three sequences are implemented:  
  - `OPEN`  
  - `STOP`  
  - `CLOSE`

---

## Hardware / Electronics

⚠️ **Do not connect your ESP device directly to the Velux controller**, as the controller uses **5V signal levels**.  
To interface safely, use an **NPN transistor level shifter**.  

- The controller's **DATA input** (usually the blue-marked terminal) already has an internal pull-up resistor.  
- With the transistor interface, the signal becomes **inverted** – this is already handled in the ESPHome code.  

The **WLC 100** controllers can handle multiple keypads connected in **simple parallel wiring**, so you can connect your ESP alongside an existing keypad without issues.  

⚡ **Powering the ESP:**  
It has not been tested whether the WLC 100 can reliably power an ESP device directly.  
- I used a **Wemos D1 Mini** with an external USB power supply.  
- Since multiple keypads can be daisy-chained to the WLC 100, it is *possible* that it could also supply an ESP – but this is unverified.  
- If you try this and it works, feel free to open a **PR** to document it!  

---

## Disclaimer

This project is provided as-is, without any warranty.  
Use at your own risk – especially when controlling motorized windows and shutters.

---
