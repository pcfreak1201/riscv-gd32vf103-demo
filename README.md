# Simple demo on how to boot a modern RISC-V chipset

The source of this firmware demo is carefully crafted to be as simple as
possible to get a single threaded system up and running on a modern 32 bit
RISC-V microcontroller such as the feature rich GD32VF103 from GigaDevice.

The author is not happy with the complexity nor abstraction level of the
example code already available from various sources. Why make it hard when you
can keep it simple?

The overall goal of this demo is to minimize the use of assembly language in
favor of C and use as little as possible of it to get things moving. Also, no
details are abstracted away and linked to some silly IDE.

The code is open source under the modified BSD license  - happy hacking!

Authored by martin.lund@keep-it-simple.com

## Demo firmware

The demo firmware blinks the D3 LED and writes hello world to USART0!

It also includes use of the official GD32VF103 driver library from GigaDevice
which includes examples on how to use every peripheral on the chip.

## Hardware

![Polos Logo](https://www.analoglamb.com/wp-content/uploads/2020/01/polos_gd32vf103_alef_board_00.png)

Polos GD32VF103 Alef Board from AnalogLamb:

https://www.analoglamb.com/product/polos-gd32v-alef-board-risc-v-mcu-board

## Toolchain

Use crosstool-ng (see http://crosstool-ng.github.io) to build a modern gcc
toolchain that supports the RISC-V flavor (ilp32,ima) of the GD32VF103.

Simply install latest version of crosstool-ng and build the "riscv32-unknown-elf" sample.

## How to get source

    $ git clone --recurse-submodules https://github.com/lundmar/riscv-gd32vf103-demo.git

## How to build

Use your favorite gcc riscv toolchain like so:

    $ cd riscv-gd32vf103-demo
    $ make CROSS_COMPILE=riscv32-unknown-elf-

## How to flash

Install the modified dfu-utils found here:
https://github.com/riscv-mcu/gd32-dfu-utils

Then simply connect the board via USB and enter boot mode by pressing the boot0
key + reset key, then unpress reset.

To flash the firmware simply do:

    $ dfu-util -a 0 -d 28e9:0189 -s 0x8000000:mass-erase:force -D firmware.bin