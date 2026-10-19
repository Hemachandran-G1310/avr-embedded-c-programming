# 🛠️ AVR-GCC Installation on Linux

This guide explains how to install and configure the **AVR-GCC toolchain** for developing Embedded C programs for the **ATmega328P** on Debian/Ubuntu-based Linux systems.

---

## 📋 Requirements

- Linux / Ubuntu
- Internet connection
- Terminal
- ATmega328P (for hardware programming)

---

## 1️⃣ Update the Package List

First, update the local package repository:

```bash
sudo apt update

2️⃣ Install AVR-GCC and Required Tools
Install the AVR compiler, libraries, binary utilities, and programming tool:

sudo apt install -y gcc-avr binutils-avr avr-libc avrdude

🐛 Optional: Install GDB for Debugging

sudo apt install -y gdb-avr

📦 Installed Tools
Tool	Purpose
gcc-avr	AVR C compiler
binutils-avr	AVR assembler, linker, and binary utilities
avr-libc	C library for AVR microcontrollers
avrdude	Used to program/flash AVR microcontrollers
gdb-avr	Debugging support for AVR


3️⃣ Verify AVR-GCC Installation
Check whether AVR-GCC is installed correctly:

avr-gcc --version

If installed successfully, the terminal will display the installed AVR-GCC version.
4️⃣ Verify AVRDUDE Installation

Check AVRDUDE:
avrdude -?

This displays the available AVRDUDE options and commands.
5️⃣ Check AVR-LibC
Check whether the AVR C library is available:

avr-gcc -print-file-name=avr/io.h

The command should return the location of the avr/io.h header file.
