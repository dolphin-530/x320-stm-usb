# x320-stm-usb
## Adds ability to stream EVT2 data from Prophesee GENX320 sensor on stm32 board (discovery kit) to host over USB_FS port
Usage:

Use .ioc configuration file in Prophesee's demo source code for the stm32 discovery kit.
Open the .ioc with CubeMX, and in pins & configuration set USB_OTG_FS to device_only. Disable usart1 to enable vbus sensing for USB_OTG_FS.

Go to clocking tab, auto resolve clocks to achieve 48 MHz USB. This will interfere with ToughGFX on the LCD display, but you will still be able to see the event stream visualized. (Trying to interact with the touch screen will crash the board)

Replace main.c task_decoder.c and task_decoder.h with files provided here.

Build .elf file in CubeIDE and now when you connect to the USB_FS port you should see the device enumerate.

If you open the port for the device you can begin streaming to your host. 

Current implementation drops some words under high event-load, but does not corrupt any EVT2 words transmitted, resulting in semi-random compression.

NOTE: Sometimes a stream's X and Y coordinates will become corrupted for a currently unknown reason. This is resolved by simply resetting the device and restarting the stream. This will be resolved in future update.
