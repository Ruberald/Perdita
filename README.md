# Perdita

[![Build](https://github.com/durangoretro/Perdita/actions/workflows/c-cpp.yml/badge.svg)](https://github.com/durangoretro/Perdita/actions/workflows/c-cpp.yml)

![imagen](https://github.com/durangoretro/Perdita/assets/6067824/a1064e48-e111-43a2-a4b9-5e70fd253bd7)


Perdita is a Durango Emulator that can run any ROM created for Durango. Perdita is based on the **65C02** instruction set and the **Durango-X** architecture, but currently does **not** support the _Rockwell **R**65C02_ extensions. However, the _WDC_ `WAI` and `STP` opcodes are emulated, the former as a **breakpoint**.

With Perdita you can test your developments, and use the internal development tools, like memory dump or gamepad emulation. **Emulation is complete** and, on a reasonably powered computer, _cycle-accurate_. The only current caveats are:

* **Sound** is emulated, but some _distortion_ may be heard.
* _Real-time **video mode** switching_ won't display properly on the emulated screen.


## Build and use perdita

Perdita uses the **SDL2 framework** to display the screen contents, so you need to install it on your system (Linux only).

```bash
apt install sdl2-dev
```

You can use Makefile to generate the perdita executable.

```bash
make
```

### Build For Windows

To Build for windows, you need to install _MinGW_. Later, use the next command.

```bash
make perdita.zip
```

### Use

To run Perdita, you can use the following instructions

```bash
./perdita [options] <path to romfile>
```

The options included are:

* ```-a```: load ROM at supplied address, example ```0x8000```.
* ```-f```: fast mode.
* ```-s```: safe mode (will stop on warnings and BRK).
* ```-p```: start in STEP mode
* ```-l```: enable error LED(s)
* ```-k```: keep GUI open after program end
* ```-h```: headless -- no graphics!
* ```-v```: verbose (warnings/interrupts/jumps/events/all)
* ```-r```: do NOT randomize memory at startup
* ```-g```: emulate controllers (Gamepads); you can use usb gamepads with durango emulator.
* ```-m```: do NOT emulate Minstrel-type keyboard

Also, you can execute some commands using functions keys:

* ```F1```: Stop emulation and quit.
* ```F2```: NMI Button (Non-Maskable Interrupt).
* ```F3```: IRQ (Interrupt ReQuest).
* ```F4```: Reset.
* ```F5```: Pause and display status.
* ```F6```: Dump memory (and register) contents.
* ```F7```: Single-Step execution (while paused).
* ```F8```: Resume normal execution (from pause).
* ```F9```: Load dump file (`dump.bin`).
* ```F10```: Load keystrokes file (`keystrokes.txt`), emulating each keystroke _every 25 interrupts_ (1/10 second), or 50 interrupts in case of the `ENTER` key.

## Virtual Serial Port (VSP)

As a valuable debugging tool, a _Virtual Serial Port_ is provided. It allows communication with the host environment thru a predefined I/O device occupying two addresses: `$DF93` for data exchange and `$DF94` for [configuration](vsp.md).

## Keyboard emulation

_Perdita_ includes two kind of keyboards: an "intelligent" PASK-like device (ASCII character received at `$DF9A`) and the Minstrel-like 40-key keyboard provided as standard (at `$DF9B`). _The latter can be disabled with the `-m` option for debugging purposes_.

## Gamepad emulation

Two _NES-type_ gamepads are emulated into the standard I/O addresses `$DF9C` and `$DF9D`, using the standard protocol. If no physical gamepads are available, they can be emulated by host keystrokes via the `-g` option.
