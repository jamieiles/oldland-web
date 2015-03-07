---
title: Oldland CPU
layout: default
---

Introduction
------------

Oldland is a 32-bit RISC CPU targeted at FPGAs.  The main features are:

  - 5 stage load/store pipeline.
  - 16 general purpose registers.
  - N-way set-associative blocking instruction/data caches
  - Software managed instruction/data TLBs with 4KB page size.
  - JTAG debug controller for execution control and state
  modification/inspection.
  - Exception table for interrupts, data/instruction aborts, illegal
  instruction and software interrupts along with separate ITLB/DTLB miss
  handlers.
  - User and supervisor modes.

Keynsham is a SoC using Oldland as the core and has a number of peripherals:

 - 32MB SDR SDRAM controller.
 - SPI master with configurable number of chip selects.
 - On-chip bootrom.
 - On-chip memory.
 - Programmable timers.
 - Interrupt controller.
 - UART.
 - SPI master.

There is a C model along with Icarus and Verilator RTL simulations.  The
Keynsham SoC can be synthesized to run on a Terasic DE0 Nano.  There are ports
of binutils, gcc and u-boot available.

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
- [TLBs](docs/tlb.html)
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
