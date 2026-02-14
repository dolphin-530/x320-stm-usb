# x320-stm-usb
adding ability to stream evt data from  GENX320 sensor on stm32 board to host over usb

Use .ioc configuration file in Prophesee's demo source code for the stm32 discovery kit.
Open the .ioc with CubeMX, and in pins & configuration set USB_OTG_FS to device_only. Disable usart1 to enable vbus sensing for USB_OTG_FS.
Go to clocking tab, auto resolve clocks to achieve 48 MHz USB. This will interfere with ToughGFX on the LCD display, but you will still be able to see the event stream visualized.
Replace main.c task_decoder.c and task_decoder.h with files provided here.
Build .elf file in CubeIDE and now when you connect to the USB_FS port you should see the device enumerate.
If you open the port for the device you can begin streaming to your host, but WARNING if USB is not fast enough it just drops bytes, resulting in some corrupted words. Working to fix this.
