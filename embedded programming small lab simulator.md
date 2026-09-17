Yes. If by “LAN environment” you mean lab equipment/protocols and embedded hardware that you would otherwise need costly physical instruments for, there are several good simulators. For a 1-student, 100 sq ft lab, simulation can reduce your initial hardware investment significantly.

Useful options

Software	Simulates	Cost	Usefulness

Wokwi	Arduino, ESP32, STM32, sensors, displays, UART, I²C, SPI	Free/paid tiers	⭐⭐⭐⭐⭐
Renode	ARM MCUs, embedded Linux, networking, peripherals	Free/open source	⭐⭐⭐⭐⭐
QEMU	ARM systems, embedded Linux, networking	Free/open source	⭐⭐⭐⭐
Proteus	MCU + electronic circuits + instruments	Commercial	⭐⭐⭐⭐⭐
MATLAB/Simulink	Control systems, MCU modeling, simulation	Commercial	⭐⭐⭐
Cisco Packet Tracer	LAN/networking	Free for eligible users	⭐⭐⭐⭐


For your particular lab

I would use a hybrid approach:

STUDENT LAPTOP
                       │
        ┌──────────────┼──────────────┐
        │              │              │
       Wokwi         Renode        Proteus
        │              │              │
     MCU +          Firmware +     Circuit +
    Sensors        Networking     Instruments
        │              │              │
        └──────────────┼──────────────┘
                       │
                 REAL STM32
                       │
              Real-world testing

Wokwi

This is probably the first one I'd introduce to your student.

It lets students experiment with microcontrollers and electronics without immediately connecting physical hardware.

For example:

STM32 / ESP32
     │
 ┌───┼────┐
 │   │    │
LED OLED Sensor
 │
UART/I²C/SPI

Students can write firmware, run it, observe outputs, and debug before moving to the physical board.

Renode

For a more professional embedded course, Renode is particularly interesting.

It is designed for simulating embedded systems and can simulate CPUs, peripherals and networked systems. This makes it useful when teaching firmware and networking concepts without requiring multiple physical boards.

Proteus

Proteus is useful when you want students to see something closer to a virtual electronics laboratory:

Microcontroller
      ↓
Virtual Oscilloscope
      ↓
Virtual Logic Analyzer
      ↓
Virtual Multimeter
      ↓
Virtual Components

It can therefore reduce the need to buy some instruments initially.


---

What I would do with your ₹30K budget

Instead of buying a full physical lab immediately:

Physical

₹12K–₹18K

1 STM32 Nucleo

1 ESP32

Breadboard/components

Sensors

Multimeter

basic USB logic analyzer


Simulation

₹0 initially

Wokwi

Renode

QEMU

VS Code

GCC

Git

FreeRTOS


Then add an oscilloscope and bench power supply only when the student reaches the stage where simulation cannot replace the real instrument.

This gives you a very good "virtual + real embedded lab" for a single student without making a large upfront investment.

If by LAN you specifically mean simulating a complete Ethernet/LAN network (multiple PCs, switches, routers, TCP/IP devices) rather than embedded hardware, tell me—that has a different set of excellent free simulators.