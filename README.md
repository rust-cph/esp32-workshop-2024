## Notes and Links
For ESP32-C3 LCDKit (and others with display) - there is a working application Spooky Maze Game: https://github.com/georgik/esp32-spooky-maze-game
Here you can find pinout used for Embedded Graphics: https://github.com/georgik/esp32-spooky-maze-game/blob/main/esp32-c3-lcdkit/src/main.rs#L137

Our BSP team at Espressif is working on Board Support packages, right now they're available only in C, yet it might be valuable to know it, because there is pinout and for some boards like M5Stack there is even initialization sequence for AXP:
https://github.com/espressif/esp-bsp

Regarding Rust GUI, we have open cooperation with Slint guys who has support for our boards both for std and no_std and published their component: 
https://components.espressif.com/components/slint/slint

One important thing is to understand how much memory a chip with combination of technology provides. I wrote small comparison which is using Wokwi as CI to get following data: https://github.com/georgik/esp32-lang-lab
There is also explanation why Rust no_std on ESP32 and ESP32-S2 provides just half of memory, with C3 and further chips there is no such problem.

Also if people would like to try upcoming P4, Wokwi has simulator support for it: https://github.com/georgik/esp32-p4-example-rs (VS Code, CTRL+ Shift +P - Start Wokwi simulation).
The simulator supports also MIPI-DSI demo with display of 1280x800 and 100 FPS, written in C, hopefully soon in Rust:

```
git clone git@github.com:georgik/esp-bsp.git --branch bsp/P4-disabled-touch
cd esp-bsp/examples/display
idf.py --preview -D SDKCONFIG_DEFAULTS=sdkconfig.bsp.esp32_p4_function_ev_board set-target esp32-p4
idf.py build
idf.py uf2
```

Now open the display folder in VS Code, e.g. "code ."

Command + Shift + P - Wokwi: Start Simulator

You should get this result:

![alt text](https://github.com/rust-cph/esp32-workshop-2024/blob/main/result.png?raw=true)
