## 硬件

Right now, I2C pins are mapped to:

* SDA - PA2
* SCL - PA1

I2C pins could be remapped in [src/softi2c.c:13]

This firmware is using 'Software I2C', so speed is not as lightning, and equals near 70khz



## 编译

1. `git clone https://github.com/zdm110/fx2-i2c-tiny-usb.git -b dev`

2. `make -C libfx2/firmware`

3. `make -C src`



## 固件烧录

`fxload load_ram --ihex-path i2c-tiny-usb.hex  -t FX2LP --device 04b4:8613`

烧录到EEPROM, 注意拔掉J4

`fxload load_eeprom --ihex-path i2c-tiny-usb.hex  -t FX2LP --control-byte 0xC2 --device 04b4:8613`

注意：这个指令无法烧录成功，目前在Windows下用官方的USB Control Center烧录

## 使用

示例，读取LM75BD温度传感器模块

1. 读取配置

   `sudo i2cget -y 13 0x48 0x01`

2. 控制板上LED点亮

   `sudo i2cset -y 13 0x48 0x01 0x04`