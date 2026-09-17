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

That's actually a good starting point. With 3 Windows 10 PCs + 100 sq ft + 1 student, you can create a useful virtual + physical embedded lab without buying expensive equipment immediately.

Suggested 3-PC arrangement

┌─────────────────────┐
                 │   Small LAN/Switch  │
                 └──────┬──────┬───────┘
                        │      │
                 ┌──────┘      └──────┐
                 ▼                     ▼
             PC-1                   PC-2
          Development              Simulation
          STM32CubeIDE             Wokwi/Renode
          GCC/GDB                  Proteus
          Git                      QEMU
                 │
                 │
                 ▼
                PC-3
          Testing / Networking
          Serial terminals
          Wireshark
          MQTT broker
          Git server

What each PC can do

🖥️ PC-1 — Firmware Development

Install:

STM32CubeIDE

STM32CubeMX

STM32CubeProgrammer

ARM GCC

GDB

Git

VS Code


Connect your STM32 Nucleo to this PC.

This becomes the student's primary development machine.


---

🖥️ PC-2 — Virtual Embedded Lab

Install:

Wokwi

Renode

QEMU

Proteus (if you decide to purchase a license)


Students can develop and test firmware virtually before touching the physical board.

This is particularly useful for your situation because one physical STM32 board can be shared between the student and the virtual environment.


---

🖥️ PC-3 — Networking / Testing

This can become your embedded networking machine.

Install:

Wireshark

Python

MQTT broker

Mosquitto

Git

VS Code

Serial terminal software


You can build projects such as:

STM32 / ESP32
                    │
                    │ Wi-Fi / Ethernet
                    ▼
                 PC-3
                    │
             ┌──────┴──────┐
             ▼             ▼
           MQTT          Python
          Broker         Server
             │             │
             └──────┬──────┘
                    ▼
                Database

That gives your student exposure to embedded + networking + IoT, which is a valuable combination.


---

You can even create a virtual LAN

Your 3 PCs can be connected through a small 5-port Gigabit Ethernet switch.

Then:

Gigabit Switch
             /      |      \
            /       |       \
          PC-1     PC-2     PC-3
           │         │        │
       Firmware   Simulator  Server

You can teach:

IP addressing

DHCP

DNS basics

TCP/IP

UDP

TCP sockets

HTTP

MQTT

Client/server architecture

Wireshark packet analysis

Embedded networking


And later connect an ESP32/STM32 Ethernet board to the same network.


---

An even better idea: Virtual machines

Your existing PCs can also run virtual machines.

For example:

Windows 10 Host
       │
       ├── Linux VM
       │      ├── GCC
       │      ├── Git
       │      ├── MQTT
       │      └── Python
       │
       └── Windows Software
              ├── STM32CubeIDE
              ├── Proteus
              └── Wireshark

However, this depends heavily on the RAM and CPU of your three PCs.

If they have only 4 GB RAM, I would avoid running several VMs. If they have 8–16 GB RAM, the setup becomes much more flexible.


---

What you actually need to buy now

Because you already have 3 PCs, I would start very small:

Item	Approx. budget

5-port Gigabit switch	₹700–₹1,200
Ethernet cables	₹300–₹500
STM32 Nucleo	₹2,500–₹4,000
ESP32	₹400–₹700
Breadboard/components	₹1,000–₹1,500
Sensors/display modules	₹1,500–₹2,000
Multimeter	₹700–₹1,000
USB logic analyzer	₹1,000–₹2,000
Initial investment	~₹8,100–₹12,900


You can postpone the oscilloscope, bench power supply and CAN analyzer until the course progresses.

This is the approach I'd recommend for your lab:

3 existing PCs + ₹10–15K hardware + free simulation software = a functional starter embedded lab.

And importantly, the student can spend most of the first few weeks on C, Embedded C, ARM, STM32, debugging and protocols before you need expensive instrumentation.