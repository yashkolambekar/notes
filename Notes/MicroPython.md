### setting up and upgrading firmware

    sudo apt-get update && sudo apt-get upgrade

    sudo apt-get install python3-pip

    sudo pip3 install esptool

    sudo pip3 install mpfshell

    dmesg | grep ttyUSB (find the correct port, should be ttyUSB0)
    sudo esptool.py --port /dev/ttyUSB0 flash_id (check the device)

    Download the firmware [https://micropython.org/download#esp32](MicroPython ESP32 Firmware)

    sudo esptool.py --port /dev/ttyUSB0 write_flash 0x1000 file.bin (now we flash with the file you downloaded`''


### Interrupts

```py
btn = machine.Pin(0, machine.Pin.IN)

btn.irq(trigger=machine.Pin.IRQ_FALLING, handler=handle_interrupt)
```