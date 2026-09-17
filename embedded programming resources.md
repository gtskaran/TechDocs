For a job-oriented Embedded Programming course, I would not give the student a huge reading list. With your 3-PC lab, I would build the course around 4–5 core books + free official documentation + hands-on online resources.

📚 Books I recommend

1. C Programming — start here

The C Programming Language — Kernighan & Ritchie

Best for learning the fundamentals and developing proper C thinking.

Focus on:

pointers

arrays

structures

functions

memory

bitwise operations


For a job-oriented embedded course, I would supplement it with Effective C — Robert C. Seacord, particularly for writing safer, more professional C.


---

2. Embedded C

Embedded C — Michael J. Pont

Good bridge between normal C and embedded programming.

The student should learn:

C
 ↓
Embedded C
 ↓
Hardware registers
 ↓
Microcontroller
 ↓
Firmware


---

3. Embedded Systems — excellent reference

Making Embedded Systems — Elecia White

This is one I particularly like for students because it focuses on how embedded engineers actually think about systems, rather than only teaching syntax.

Topics include:

architecture

debugging

testing

real-time considerations

hardware/software interaction

design decisions



---

4. ARM Cortex-M

For your STM32-based course, this becomes important.

Embedded Systems: Introduction to ARM Cortex-M Microcontrollers — Jonathan Valvano

Very useful for understanding:

ARM architecture

GPIO

interrupts

timers

ADC

UART

SPI

I²C

real-time programming


This is particularly suitable for turning the course from an Arduino-style hobby course into an MCU/firmware course.


---

5. RTOS / FreeRTOS

Mastering the FreeRTOS Real Time Kernel — Richard Barry

This is especially useful once the student understands bare-metal STM32.

And an important advantage:

FreeRTOS provides the official book/documentation online, so you don't necessarily need to purchase a physical copy.


---

🌐 Online resources

1. STMicroelectronics — essential

STMicroelectronics

For your course, the official STM32 documentation should be the student's primary technical reference.

[STMicroelectronics STM32 resources](https://www.st.com/en/microcontrollers-microprocessors/stm32-32-bit-arm-cortex-mcus.html?utm_source=chatgpt.com)

Students should learn to read:

Datasheets

Reference manuals

Programming manuals

Application notes

Errata sheets


This skill is extremely important for employment.

Don't let students depend entirely on YouTube tutorials.


---

2. STM32CubeIDE / CubeMX

[STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html?utm_source=chatgpt.com)

[STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html?utm_source=chatgpt.com)

Use these for:

project creation

clock configuration

GPIO

peripherals

code generation

debugging



---

3. ARM Developer

Arm

[Arm Developer Documentation](https://developer.arm.com/documentation?utm_source=chatgpt.com)

This should be your student's reference for:

Cortex-M

ARM architecture

CMSIS

interrupts

processor fundamentals



---

4. FreeRTOS

[FreeRTOS Documentation](https://www.freertos.org/Documentation/00-Overview?utm_source=chatgpt.com)

Use this for:

Tasks

Queues

Semaphores

Mutexes

Timers

Scheduling

Interrupt interaction



---

5. Wokwi

Wokwi

[Wokwi](https://wokwi.com/?utm_source=chatgpt.com)

This is particularly relevant to your small lab.

Students can experiment virtually before using your physical hardware.

For example:

Student writes code
       ↓
Wokwi simulation
       ↓
Debug
       ↓
Understand circuit
       ↓
Flash real STM32/ESP32
       ↓
Test hardware


---

6. Renode

[Renode Documentation](https://renode.readthedocs.io/?utm_source=chatgpt.com)

I'd introduce this later.

It is useful for teaching:

embedded systems

MCU simulation

networking

firmware testing

automated testing


It is more advanced than Wokwi.


---

7. Zephyr RTOS

Once the student becomes comfortable with FreeRTOS, introduce:

Zephyr

[Zephyr Project](https://www.zephyrproject.org/?utm_source=chatgpt.com)

Zephyr is worth knowing because modern embedded development increasingly involves RTOS-based, portable embedded platforms.

Don't start with Zephyr, though.

STM32 bare metal → FreeRTOS → Zephyr is a more sensible progression.


---

8. Git

[Git Documentation](https://git-scm.com/doc?utm_source=chatgpt.com)

Make Git mandatory from the beginning.

Every student's project should look something like:

stm32-temperature-monitor/
│
├── Core/
├── Drivers/
├── Inc/
├── Src/
├── Docs/
├── Tests/
├── README.md
└── .gitignore

And the student should maintain commits such as:

Initial STM32 project
Add GPIO driver
Add temperature sensor
Add I2C communication
Add UART diagnostics
Fix sensor timeout
Add error handling

That's much closer to professional development.


---

9. Linux

For the Embedded Linux portion:

[Linux Kernel Documentation](https://docs.kernel.org/?utm_source=chatgpt.com)

[Bootlin Training Materials](https://bootlin.com/training/?utm_source=chatgpt.com)

Bootlin's free training material is particularly valuable for:

Embedded Linux

Linux kernel

device drivers

Yocto

Buildroot

boot process



---

10. Networking

For the networking/IoT component of your course:

[Wireshark Documentation](https://www.wireshark.org/docs/?utm_source=chatgpt.com)

[MQTT Official Site](https://mqtt.org/?utm_source=chatgpt.com)

Students can use your three Windows 10 PCs to create a miniature network:

PC 1
   Development
       │
       │
   ┌───┴────┐
   │ Switch │
   └───┬────┘
       │
 ┌─────┴─────┐
 ▼           ▼
PC 2        PC 3
Simulator   MQTT/Server

Then connect ESP32 to the same network.


---

🎓 My recommended student curriculum

I would actually give your student this resource sequence, rather than asking them to read everything simultaneously:

Month 1

Book: K&R / Effective C

Online:

C exercises

GCC

Git

VS Code


Projects:

20–30 C programs

pointer exercises

bit manipulation

state machine



---

Month 2

Book: Embedded C / Valvano

Online:

ARM documentation

STM32 documentation

STM32CubeIDE


Projects:

GPIO
LED
Button
Timer
Interrupt
PWM
ADC
UART


---

Month 3

STM32 reference manuals + datasheets

Projects:

I²C sensor
SPI display
EEPROM
RTC
DMA
Watchdog

Introduce:

Logic Analyzer + Oscilloscope


---

Month 4

FreeRTOS official book/documentation

Projects:

Task
Queue
Semaphore
Mutex
Timer
Interrupt → Task

Then build one complete RTOS project.


---

Month 5

CAN + IoT

STM32
 ↓
CAN
 ↓
ESP32
 ↓
Wi-Fi
 ↓
MQTT
 ↓
PC

Use Wireshark for network analysis.


---

Month 6

Embedded Linux

Use your PC-2/PC-3 as Linux virtual machines if their hardware is adequate.

Topics:

Linux
 ↓
C
 ↓
Processes
 ↓
Threads
 ↓
Sockets
 ↓
GPIO
 ↓
Device drivers
 ↓
Buildroot / Yocto


---

⭐ If you want to keep the student's book cost low

I would make only three books mandatory:

1. K&R — The C Programming Language


2. Making Embedded Systems — Elecia White


3. Embedded Systems: Introduction to ARM Cortex-M — Valvano



Then use official online documentation as the primary reference for STM32, ARM, FreeRTOS, Linux, CAN and networking.

That keeps the course affordable while teaching an important professional habit:

> An embedded engineer must know how to find the answer in a datasheet/reference manual—not just remember code from a tutorial.



For your one-student/100 sq ft lab, this resource strategy also works very well because you can make the 3 PCs into Development + Simulation + Networking/Debugging stations, and use the physical STM32/ESP32 hardware only when the lesson requires real hardware.