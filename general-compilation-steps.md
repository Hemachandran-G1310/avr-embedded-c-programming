# ⚙️ General AVR Compilation and Programming Steps

This guide explains the basic workflow for compiling and programming a **bare-metal Embedded C program** for the **ATmega328P** using AVR-GCC and AVRDUDE.

---

## 1️⃣ Write the Source Code

Create and write your bare-metal C program, for example `blink.c`, using any text editor.

```bash
nano blink.c
```

You can also use other editors such as VS Code or Vim.

---

## 2️⃣ Compile the C Program to an ELF File

Use **`avr-gcc`** to compile the C source code into an **ELF (Executable and Linkable Format)** file.

The `-mmcu=atmega328p` option specifies the target microcontroller, while `-Os` optimizes the program for smaller code size.

```bash
avr-gcc -mmcu=atmega328p -Os -o blink.elf blink.c
```

### 🔍 Command Breakdown

| Option | Purpose |
|---|---|
| `avr-gcc` | AVR C compiler |
| `-mmcu=atmega328p` | Specifies the target MCU |
| `-Os` | Optimizes for smaller code size |
| `-o blink.elf` | Specifies the output file |
| `blink.c` | Input C source file |

📄 **Output:**

```text
blink.elf
```

---

## 3️⃣ Convert ELF to Intel HEX

AVR programmers commonly use **Intel HEX** files for programming Flash memory.

Use **`avr-objcopy`** to convert the ELF file into a HEX file.

```bash
avr-objcopy -O ihex -R .eeprom blink.elf blink.hex
```

### 🔍 Command Breakdown

| Option | Purpose |
|---|---|
| `avr-objcopy` | Converts the file into another format |
| `-O ihex` | Specifies Intel HEX as the output format |
| `-R .eeprom` | Excludes the EEPROM section |
| `blink.elf` | Input ELF file |
| `blink.hex` | Output HEX file |

📄 **Output:**

```text
blink.hex
```

---

## 4️⃣ Check Program Memory Usage

Use **`avr-size`** to check how much Flash and SRAM your program uses.

```bash
avr-size --format=avr --mcu=atmega328p blink.elf
```

The ATmega328P provides:

- 💾 **32 KB Flash memory**
- 🧠 **2 KB SRAM**
- 🗃️ **1 KB EEPROM**

This step helps verify that your program fits within the available memory.

---

## 5️⃣ Detect the Serial Port

Connect the development board to your computer using USB.

On Linux, the board may appear as:

```text
/dev/ttyACM0
```

or:

```text
/dev/ttyUSB0
```

To identify the available serial ports:

```bash
ls /dev/ttyACM* /dev/ttyUSB*
```

💡 **Tip:** If the command does not show anything, check the USB connection and make sure the board is properly detected by Linux.

---

## 6️⃣ Flash the HEX File to the ATmega328P

Use **`avrdude`** to upload the HEX file to the ATmega328P through the board's bootloader.

```bash
avrdude -p m328p -c arduino -P /dev/ttyACM0 -b 115200 -U flash:w:blink.hex:i
```

### 🔍 Command Breakdown

| Option | Purpose |
|---|---|
| `avrdude` | AVR programming utility |
| `-p m328p` | Specifies the ATmega328P |
| `-c arduino` | Uses the Arduino bootloader protocol |
| `-P /dev/ttyACM0` | Specifies the serial port |
| `-b 115200` | Specifies the baud rate |
| `-U` | Performs a memory operation |
| `flash` | Selects Flash memory |
| `w` | Write operation |
| `blink.hex` | HEX file to upload |
| `i` | Intel HEX format |

🚀 After successful programming, the ATmega328P will execute the uploaded program.

---

## 🔄 Complete Compilation Workflow

```text
       📝 blink.c
           │
           │ avr-gcc
           ▼
       📦 blink.elf
           │
           │ avr-objcopy
           ▼
       📄 blink.hex
           │
           │ avrdude
           ▼
    🔧 ATmega328P Flash
           │
           ▼
      ⚡ Program Runs
```

---

## 🧰 Tools Used

| Tool | Function |
|---|---|
| `avr-gcc` | 🛠️ Compiles Embedded C code |
| `avr-objcopy` | 🔄 Converts ELF to HEX |
| `avr-size` | 📊 Checks memory usage |
| `avrdude` | 🚀 Programs the ATmega328P |

---

> 💡 **Note:** The serial port, programmer type, and baud rate depend on the board and programming method being used. The example above assumes an **ATmega328P board using an Arduino-style bootloader**.
