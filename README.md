# Velux Keypad Emulator (ESPHome)

A simple Velux keypad emulator based on ESPHome.  
This is a proof-of-concept code to control old (1997-2006) Velux/WindowMaster systems (e.g.: Velux WLC 100 ** **).

---

## Overview

This project provides a minimal working **PoC** implementation for emulating a Velux keypad using ESPHome.  
The packets was reverse-engineered with a Rigol DS1054Z oscilloscope by sniffing a **WLI 130** keypad connected to a **WLC 100** controller.

I wasn’t able to reverse-engineer the protocol; I don’t think it’s UART, RS232, I²C, or any other known standard. The WLI keypad contains an infrared receiver as well, since remote controls were available for it. Because of that, and based on the waveform, it seems that the device also uses some kind of proprietary pulse-modulated IR protocol on the DATA wire. In the ESPHome code, we therefore transmit the same sequences with the appropriate timing.

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
To interface safely, use an **NPN transistor level shifter** (e.g.: BC547).  

- The controller's **DATA input** (usually the blue-marked terminal) already has an internal pull-up resistor.  
- With the level shifter, the signal becomes **inverted** – this is already handled in the ESPHome code.  

**Wiring:**
- Velux DATA (blue) → transistor collector
- Velux GND (red) → transistor emitter, ESP GND
- ESP GPIO (D2 on Wemos D1 mini) → transistor base (through a 4.7K resistor)

The **WLC 100** controllers can handle multiple keypads connected in **simple parallel wiring**, so you can connect your ESP alongside an existing keypad without issues. Therefore, the ESP can be placed either at the keypad (connected to its terminals) or at the WLC controller (I installed mine there, since there’s more space and it stays hidden) — it doesn’t make a difference.  

⚡ **Powering the ESP:**  
It has not been tested whether the WLC 100 can reliably power an ESP device directly. I used a **Wemos D1 Mini** with an external USB power supply. Since multiple keypads can be daisy-chained to the WLC 100, it is *possible* that it could also supply an ESP – but this is unverified. If you try this and it works, feel free to open a **PR** to document it!  

---

## Disclaimer

This project is provided as-is, without any warranty.  
Use at your own risk – especially when controlling motorized windows and shutters.

---
