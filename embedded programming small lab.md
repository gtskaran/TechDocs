With only 1 student initially and 100 sq ft, I would not invest ₹3 lakh in a full lab. Start with a compact personal embedded workstation that can support one student now and expand later.

Recommended initial setup: ₹25,000–₹40,000

The student can bring the laptop; you provide the lab hardware.

Equipment	Qty	Approx. ₹

STM32 Nucleo board	1	3,000
ESP32 board	1	500
Breadboard + components	1 set	1,500
Sensors/display/modules	1 set	2,000
Digital multimeter	1	800
Logic analyzer	1	1,500–3,000
2-channel oscilloscope	1	8,000–12,000
Bench power supply	1	5,000–7,000
Soldering station	1	2,000–3,000
USB cables/adapters	1 set	1,000
Jumper wires/connectors	1 set	500
CAN modules	2	1,000–2,000
Storage/boxes/misc.	—	1,500–2,000
Estimated total		₹28,800–₹39,300


I would initially target around ₹30,000–₹35,000, rather than buying everything at once.

What I would buy first

Stage 1 — Start teaching immediately

Spend roughly ₹10,000–₹15,000:

STM32 Nucleo

ESP32

Breadboard

Components

Sensors

OLED

Multimeter

USB cables

Jumper wires


This is enough for:

Embedded C → GPIO → timers → interrupts → ADC → PWM → UART → I²C → SPI

Stage 2 — Add debugging equipment

Once the student reaches peripheral/debugging work:

Logic analyzer

Oscilloscope

Bench power supply


This brings you toward ₹25,000–₹35,000.

Stage 3 — Add CAN

When you reach automotive/industrial topics:

2 CAN transceivers

CAN bus termination

USB-CAN interface


No need to buy these on day one.


---

100 sq ft layout

You really don't need much space for one student.

A 6 × 10 ft room can comfortably work.

┌──────────────────────────┐
│                          │
│   STORAGE / COMPONENTS   │
│                          │
│ ┌──────────────────────┐ │
│ │  4–5 ft WORKBENCH    │ │
│ │                      │ │
│ │ Laptop  STM32  DMM   │ │
│ │ Breadboard  Scope    │ │
│ └──────────────────────┘ │
│                          │
│       Student Chair      │
│                          │
│  Whiteboard / TV/Monitor │
│                          │
└─────────── DOOR ─────────┘

A 4–5 ft × 2 ft workbench is enough.

I'd put the oscilloscope and power supply at the back of the bench, with the breadboard and STM32 in the student's working area.


---

Student should bring

For the first student, I would make this very simple:

Student provides

Laptop

Laptop charger

USB mouse (optional)

Notebook

Personal pen drive (optional)


You provide

STM32

ESP32

Electronics components

Breadboard

Multimeter

Oscilloscope

Logic analyzer

Power supply

Sensors

Displays

CAN equipment


This means the student doesn't have to spend heavily before joining.


---

Laptop specification

Don't require an expensive laptop.

Minimum

8 GB RAM + 256 GB SSD

Recommended

16 GB RAM + 512 GB SSD

Windows 10/11 is perfectly adequate for the STM32 development environment.

Linux can be introduced later.


---

Software — ₹0

Your teaching PC/student laptop can use:

STM32CubeIDE

STM32CubeMX

STM32CubeProgrammer

ARM GCC

Git

VS Code

GDB

Python

FreeRTOS


So there is essentially no software licensing cost for the core curriculum.


---

⚠️ One thing I would NOT buy yet

Don't buy:

10 STM32 boards

10 ESP32 boards

expensive professional oscilloscopes

expensive programmers

large component inventory

expensive soldering/rework equipment

Raspberry Pi cluster

expensive CAN analyzers


With one student, these will mostly sit unused.

Instead, make the lab modular.

₹12K Start
     ↓
First student
     ↓
₹10K–₹15K instrumentation
     ↓
2–3 students
     ↓
Add second STM32
     ↓
Add second workstation
     ↓
5 students
     ↓
Expand equipment

My recommendation for your situation

Since you currently have 1 enquiry + 100 sq ft, I'd start with a ₹30,000 maximum lab, but purchase it in two stages.

The most important investment isn't the number of boards. It's having one good STM32 setup + proper debugging instruments + a structured project-based curriculum.

If you want, I can make you a ₹15,000 "minimum viable embedded lab" shopping list in India, followed by a ₹30,000 upgraded version, with specific STM32 board, oscilloscope, logic analyzer, power supply, sensors and component choices.