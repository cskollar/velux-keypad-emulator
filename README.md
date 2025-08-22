# Velux Keypad Emulator (ESPHome)

A very simple Velux keypad emulator based on ESPHome.  
This is a proof-of-concept code to control old (1997-2018) Velux/WindowMaster systems (e.g.: Velux WLC 100 51).

---

## Overview

This project provides a minimal working **PoC (Proof of Concept)** implementation for emulating a Velux wall keypad using ESPHome.  
The communication protocol was reverse-engineered with a Rigol DS1054Z oscilloscope by sniffing a **WLI 130** wall keypad connected to a **WLC 100** controller.

The code is expected to be compatible with other Velux Windowmaster keypads from the same era (e.g. **WLI 110**), but this has not been tested.

---

## Limitations

- **No motor addressing implemented** – only motor **#1** on the WLC 100 is operated.
- Three sequences are implemented:  
  - `OPEN`  
  - `STOP`  
  - `CLOSE`

---

## Disclaimer

This project is provided as-is, without any warranty.  
Use at your own risk – especially when controlling motorized windows and shutters.

---
