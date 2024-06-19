# Microcontrollers

- [Microcontroller](#microcontroller)
- [Embedded design](#embedded-design)
  - [Interrupts](#interrupts)
  - [Programs](#programs)
  - [Other microcontroller features](#other-microcontroller-features)
- [Basic elements of microcontrollers](#basic-elements-of-microcontrollers)
- [Memory Types](#memory-types)
- [Interaction with analog and digital signals](#interaction-with-analog-and-digital-signals)



## Microcontroller
- microcontroller unit (MCU)
- is a small computer on a **single integrated circuit.** A microcontroller contains **one or more CPUs (processor cores)** along with memory and programmable **input/output peripherals.**
- program memory in the form of **NOR flash, OTP ROM, or ferroelectric RAM** is also often included on the chip, as well as a small amount of RAM.
- microcontrollers are designed for **embedded applications**, in contrast to the microprocessors used in personal computers

- In modern terminology, a microcontroller is similar to, **but less sophisticated than, a system on a chip (SoC).**
- A **SoC** may include a microcontroller as one of its components but usually integrates it with advanced peripherals **like a graphics processing unit (GPU), a Wi-Fi module, or one or more coprocessors.**

- Mixed-signal microcontrollers are common, integrating analog components needed to control non-digital electronic systems.
- In the context of the Internet of Things, **microcontrollers are an economical and popular means of data collection**, sensing and actuating the physical world as **edge devices**. 



## Embedded design
- A microcontroller can be considered a self-contained system with a processor, memory and peripherals and can be used as an **embedded system**.
- Embedded systems often use **event-driven architecture (EDA) to handle interactions and processes efficiently.**
- Embedded systems often use **interrupt-driven programming as a core part of their event-driven architecture.**
- EDA implementation in Embedded Systems:
  - **Interrupts**
  - **Interrupt Service Routines (ISRs)**
  - **Event Queues**:
    - Some embedded systems use event queues to manage multiple events, ensuring they are processed in a **prioritized and orderly fashion**.  

 ### Interrupts
 - Microcontrollers must provide **real-time (predictable, though not necessarily fast) response to events** in the embedded system they are controlling.
 - When certain events occur, an interrupt system can signal the processor **to suspend processing the current instruction sequence and to begin an interrupt service routine (ISR, or "interrupt handler")** which will perform any processing required based on the source of the interrupt, before returning to the original instruction sequence.
 - Possible interrupt sources are **device-dependent** and often include events such as an **internal timer overflow, completing an analog-to-digital conversion, a logic-level change on an input**
 - Interrupts may also **wake a microcontroller from a low-power sleep state** where the processor is halted until required to do something by a **peripheral event.**

### Programs
- Typically microcontroller programs must fit in the **available on-chip memory**, since it would be costly to provide a system with external, expandable memory.
- Compilers and assemblers are used to convert both **high-level and assembly language code into a compact machine code** for storage in the microcontroller's memory.


### Other microcontroller features
- Microcontrollers usually contain from several to dozens of **general purpose input/output pins (GPIO)**.
- **GPIO pins are software configurable** to either an input or an output state.
- A less common feature on some microcontrollers is a **digital-to-analog converter (DAC)** that allows the processor to output **analog signals or voltage levels.**
- A dedicated **pulse-width modulation (PWM) block** makes it possible for the CPU to control power converters, resistive loads, motors, etc., **without using many CPU resources in tight timer loops.**
- A **universal asynchronous receiver/transmitter (UART) block)**  makes it possible to **receive and transmit data over a serial line with very little load on the CPU.**
- Dedicated **on-chip hardware** also often includes capabilities to communicate with other devices (chips) in digital formats such as **Inter-Integrated Circuit (I²C)**, **Serial Peripheral Interface (SPI), Universal Serial Bus (USB), and Ethernet.**


## Basic elements of microcontrollers
- Microcontrollers may not implement an external address or data bus as they integrate RAM and non-volatile memory on the same chip as the CPU.
- **A microcontroller is a single integrated circuit**, commonly with the following features:
  - central processing unit – ranging from small and simple 4-bit processors to complex 32-bit or 64-bit processors
  - volatile memory (RAM) for data storage
  - ROM, EPROM, EEPROM or Flash memory for program and operating parameter storage
  - serial input/output such as serial ports (UARTs)
  - other serial communications interfaces like I²C, Serial Peripheral Interface and Controller Area Network for system interconnect
  - peripherals such as timers, event counters, PWM generators, and watchdog
  - clock generator – often an oscillator for a quartz timing crystal, resonator or RC circuit

## Memory Types
- Two different kinds of memory are commonly used with microcontrollers, **a non-volatile memory for storing firmware** and a **read-write memory for temporary data.**
- **Non-volatile memory**
  -  (NVM) or non-volatile storage is a type of computer memory that **can retain stored information even after power is removed.**
  -  **EPROM, EEPROM, FLASH memory, Solid-state drive (SSD)**
- **Volatile memory**
  - is computer memory that requires power to maintain the stored information
  - it retains its contents while powered on but when the power is interrupted, the stored data is quickly lost.
  - In addition to usually **being faster than forms of mass storage** such as a hard disk drive
  - There are two kinds of volatile RAM: **dynamic and static.**
    - **SRAM**
      - **Uses bistable latching circuitry** made up of **six transistors per bit to store data**. It does not need to be refreshed as long as power is supplied.
      - SPEED: **Faster than DRAM because it does not need to be refreshed** and can be accessed more quickly.
      - DENSITY: **Lower density because it requires more transistors per bit**, making it less efficient in terms of space.
      - POWER CONSUMPTION: **Generally consumes less power in idle mode** but more power during active use compared to DRAM.
      - USAGE: Typically used for **cache memory (e.g., CPU cache) where speed is critical, RAM, CACHE MEMORY L1, L2, L3, VRAM - video RAM from graphics processing**
    - **DRAM**
      - **Uses a capacitor and a transistor per bit to store data.** **The capacitor leaks charge** and therefore needs to be **refreshed periodically** to maintain the data.  
      - SPEED: Slower than SRAM due to the need **for periodic refresh cycles.**
      - DENSITY: **Higher density** because it uses fewer components per bit
      - POWER CONSUMPTION: Consumes more power overall due to the need for **periodic refreshing.**
      - USAGE: Commonly used for main memory.
  

## Interaction with analog and digital signals


