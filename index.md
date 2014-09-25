---
title: Oldland CPU
layout: default
---

Introduction
------------

Oldland is a 32-bit RISC CPU designed primarily to learn more about Verilog
and FPGA's.  At the moment this consists of the CPU core itself (Oldland), and
a SoC implementation (Keynsham) that includes the CPU core, on-chip bootrom,
internal SRAM, an SDRAM controller, SPI master and UART.

Included is an instruction set simulator, tools for debugging in gtkwave, a
bootloader (and associated bootrom code), lua based debugger, JTAG for
hardware.  There is a GCC retarget for oldland-elf.

The FPGA target is for a DE0 nano and runs at 50MHz, though it should
synthesize at &gt;80MHz at the moment.

Documentation
-------------

- [Instruction set](instructions.html)
- [Keynsham SoC configuration](keynsham.html)
- [Architecture](docs/design.html)
- [JTAG protocol](docs/jtag.html)
- [How to simulate](docs/simulating.html)
- [Memory busses](docs/memory.html)
- [SPI master](docs/spimaster.html)

Testing
-------

   1. Download
      [binutils-oldland](https://github.com/jamieiles/binutils-oldland") and
      build with:  
```
./configure --target=oldland-elf`  
make all`  
make install`
```

   2. Download
      [gcc-oldland](https://github.com/jamieiles/gcc-oldland) and build with:
```
./configure --target=oldland-elf --disable-libquadmath --disable-libssp --enable-languages=c
make all
make install
```

   3. Make sure that the `oldland-elf-*` tools are in your path and build the CPU
      + tools with:  
```
mkdir BUILD
cd BUILD
cmake -DCMAKE_ISNTALL_PREFIX:PATH=INSTALL_PREFIX ..
make all install
```

   4. Add `${INSTALL_PREFIX}/bin` to your path.

   5. Run `oldland-test` to run the self-tests.

Running On Hardware
-------------------

Build the FPGA image in Quartus and load it onto the device.  Run
oldland-jtagd on the development machine, oldland-debug can then connect to
the CPU over the virtual JTAG.

Licensing
---------

This project is currently licensed under GPLv2 except for oldland-jtagd which
is under the Apache License v2.0.
