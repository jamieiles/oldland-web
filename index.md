---
title: Oldland CPU
layout: default
---

Introduction
------------

Oldland is a 32-bit RISC CPU designed primarily to learn more about Verilog
and FPGA's.  The project consists of the CPU core itself (Oldland), and
a SoC implementation (Keynsham) that includes the CPU core, on-chip bootrom,
internal SRAM, an SDRAM controller, SPI master and UART.

Included is an instruction set simulator, tools for debugging in gtkwave, a
bootloader (and associated bootrom code), lua based debugger, JTAG for
hardware.  There is a GCC+binutils retarget for oldland-elf and a u-boot port
that runs in both simulation and on the FPGA.

The Terasic DE0-nano board using an Altera Cyclone IV is the supported board
running at ~75MHz on slow silicon @85°C.

Documentation
-------------

- [Instruction set](instructions.html)
- [Keynsham SoC configuration](keynsham.html)
- [Architecture](docs/design.html)
- [JTAG protocol](docs/jtag.html)
- [How to simulate](docs/simulating.html)
- [Memory busses](docs/memory.html)
- [SPI master](docs/spimaster.html)
- [Boot process](docs/booting.html)

Testing
-------

   - Download [binutils-gdb-oldland](https://github.com/jamieiles/binutils-gdb-oldland") and build with:  
{% highlight bash %}
./configure --target=oldland-elf`  
make all`  
make install`
{% endhighlight %}

   - Download [gcc-oldland](https://github.com/jamieiles/gcc-oldland) and build with:
{% highlight bash %}
./configure --target=oldland-elf --disable-libquadmath --disable-libssp --enable-languages=c
make all
make install
{% endhighlight %}

   - Make sure that the `oldland-elf-*` tools are in your path and build the CPU + tools with:  
{% highlight bash %}
mkdir BUILD
cd BUILD
cmake -DCMAKE_ISNTALL_PREFIX:PATH=INSTALL_PREFIX ..
make all install
{% endhighlight %}

   - Add `${INSTALL_PREFIX}/bin` to your path.

   - Run `oldland-test` to run the self-tests.

Running On Hardware
-------------------

Build the FPGA image in Quartus and load it onto the device.  Run
oldland-jtagd on the development machine, oldland-debug can then connect to
the CPU over the virtual JTAG.

Licensing
---------

This project is currently licensed under GPLv2 except for oldland-jtagd which
is under the Apache License v2.0.
