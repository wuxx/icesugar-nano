iCESugar-nano
-----------
[中文](./README.md) [English](./README_en.md)
* [iCESugar-nano](#iCESugar-nano) 
* [Hardware](#hardware)
	* [iCE40LP1K](ice40lp1k)
	* [SPI-Flash](spi-flash)
	* [Peripheral](peripheral)
	* [iCELink](icelink)
* [virtual-machine-image](#virtual-machine-image)
* [How-to-setup](#how-to-setup-env)
* [How-to-buy](#how-to-buy)
* [Reference](#reference)

# iCESugar-nano
iCESugar-nano is a FPGA board base on Lattice iCE40LP1K-CM36, which is fully supported by the open source toolchain (yosys & nextpnr & icestorm), 14 usable IOs fan-out with 3 standard PMOD interface, the on board debugger iCELink (base on ARM Mbed DAPLink) support drag-and-drop program, you can just drag the FPGA bitstream into the virtual disk to program, the iCELink also provide a adjustable clock to FPGA, and with a additional USB CDC serial port direct connect to FPGA, so you can only use one TYPE-C cable to develop and test.  
<div align=center>
<img src="https://github.com/wuxx/icesugar-nano/blob/main/doc/icesugar_nano_1.jpg" width = "700" alt="" align=center />    
</div>

# Hardware
### iCE40LP1K
iCE40LP1K-CM36 (BGA36 0.4mm pitch)
1. 1280 Logic Cells (LUT + Flip-Flop)  
2. 64K bit RAM (4K bit RAM x 16)
3. High Current LED Drivers x 3

### SPI-Flash
 SPI Flash use W25Q16 (2MB)

### Peripheral
1. a yellow led is connected to B6.  
2. most IO out with standard PMOD Interface (one 2 x 6 PMOD and two 1 x 6 PMOD).

### iCELink
iCESugar-nano has a on board debugger named iCELink (base on APM32F1)，you can only use one USB wire to program the FPGA and debug, here is detail:   
1. drag-and-drop program, just drop the bitstream into the virtual USB DISK iCELink, then wait a few second, the iCELink firmware will do the total program work
3. USB CDC serial port, it can use to communicate with FPGA
3. the MCO can provide 8MHz/12MHz/36MHz/72MHz clock for FPGA as extern clock. 
4. use the command tool `icesprog` to flash or do more config, here is the help info
```
$icesprog -h
usage: /home/pi/oss/icesugar/tools/icesprog.arm [OPTION] [FILE]
             -w | --write                   write spi-flash or gpio
             -r | --read                    read  spi-flash or gpio
             -e | --erase                   erase spi-flash
             -p | --probe                   probe spi-flash
             -o | --offset                  spi-flash offset
             -l | --len                     len of write/read
             -g | --gpio                    icelink gpio write/read
             -m | --mode                    icelink gpio mode
             -j | --jtag-sel                jtag interface select (1 or 2)
             -c | --clk-sel                 clk source select (1 to 4)
             -h | --help                    display help info

             -- version 1.1a --

```
#### Tips
The iCELink on iCESugar-nano can adjust the mco clock between 8/12/36/72MHz, here is the usage. note: the mco clock will return to the default 12MHz after perform a board power-off power-on reset.
```
$icesprog -c ?
CLK -> [12MHz]
CLK-SELECT:
        [1]:  8MHz
        [2]: 12MHz
        [3]: 36MHz
        [4]: 72MHz
done

$icesprog -c 1
CLK -> [ 8MHz]
CLK-SELECT:
        [1]:  8MHz
        [2]: 12MHz
        [3]: 36MHz
        [4]: 72MHz
done

```

# virtual-machine-image
link：https://pan.baidu.com/s/1qVSdwM7DnFbaS0xdqsPNrA  
verify code：6gn3  
`user: ubuntu`  
`passwd: ubuntu`  
or
https://mega.nz/file/uvJTWKrK#1bBgBkJPZrszwHQSTHHL-RLjxGIru0Qv0qUgmULZZVs

the env include yosys, nextpnr, icestorm, gcc, sbt.

# How-to-setup-env
## Linux
recommend use the virtual machine, it simple and convenient  
FPGA toolchain reference [icestorm](http://www.clifford.at/icestorm/)  
gcc toolchain reference [riscv-gnu-toolchain](https://pingu98.wordpress.com/2019/04/08/how-to-build-your-own-cpu-from-scratch-inside-an-fpga/)  
Alternatively, you can download the pre-built toolchain provided by xPack or SiFive
+ https://xpack.github.io/riscv-none-embed-gcc/install/
+ https://www.sifive.com/software
`icesprog` is command tool for iCESugar program，it depend libusb and hidapi  
`$sudo apt-get install libhidapi-dev`  
`$sudo apt-get install libusb-1.0-0-dev`  

## Windows
now you can use the msys2 environment to setup the open source toolchain easily, download msys2 install executable [here](https://www.msys2.org/), install it, then open the msys2 mingw terminal (search `msys2` in windows start menu)  
```
#pacman -Syu
#pacman -S mingw-w64-x86_64-eda
```
select the yosys, nextpnr, icestorm, icesprog and install, after installed, everything is same as in linux!

# How-to-buy
you can buy iCESugar-nano and PMOD peripherals from our offcial aliexpress shop [Muse Lab Factory Store](https://muselab-tech.aliexpress.com/)

# Reference
### icestorm toolchain
http://www.clifford.at/icestorm/
### riscv gcc toolchain
https://xpack.github.io/riscv-none-embed-gcc/install/
https://www.sifive.com/software
### iCESugar
https://github.com/wuxx/icesugar
### Examples
https://github.com/damdoy/ice40_ultraplus_examples  
https://github.com/icebreaker-fpga/icebreaker-examples
### SpinalHDL
https://spinalhdl.github.io/SpinalDoc-RTD/SpinalHDL/Getting%20Started/index.html
