# Microcontrollers

- [Microcontroller](#microcontroller)
- [Embedded design](#embedded-design)
  - [Interrupts](#interrupts)
  - [Programs](#programs)
  - [Other microcontroller features](#other-microcontroller-features)
- [Basic elements of microcontrollers](#basic-elements-of-microcontrollers)
- [Memory Types](#memory-types)
- [Interaction with analog and digital signals](#interaction-with-analog-and-digital-signals)
- [Aliasing](#aliasing)
- [Nyquistův–Shannonův vzorkovací teorém](#Nyquistův-Shannonův-vzorkovací-teorém)
- [ESP IDF](#esp-idf) 
- [ESP memory management](#ESP-memory-management)
- [ARM](#arm)
- [System on chip](#system-on-chip)




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
- bridging the gap between the real world (analog) and the digital realm of computing and data processing.

- **Analog-to-Digital Conversion (ADC)**
  - Analog signals are continuous and can take any value within a range, while digital signals are discrete, consisting of binary values (0s and 1s).
  - **Converting analog signals to digital involves several steps:**
    - **Sampling: - vzorkování** The analog signal is **sampled - vzorkovany at regular intervals.** The **sampling rate must be at least twice the highest frequency component of the analog signal (Nyquist theorem)** to avoid aliasing.
    - **Quantization- Kvantování:** Each sampled value is mapped to the nearest value within a **range of discrete levels.**
    - **Encoding:** The **quantized values are then converted into binary format** for processing by digital systems.  

- **Digital-to-Analog Conversion (DAC)**
  - **Pulse Width Modulation (PWM):**
    - Principle: A digital signal **switches between on and off states at a high frequency**. The **ratio of the time the signal is on (duty cycle)** to the total period determines the **average voltage.**
  - **R-2R Ladder DAC**:
    Principle: Utilizes a network of resistors arranged in a ladder configuration. Each bit of the digital input controls a switch that either connects the resistor to a reference voltage or ground, creating a corresponding analog output.
     
- **Communication Between Analog and Digital Systems**
  - **Mixed-Signal Circuits:** These integrate both analog and digital components on a single chip, facilitating direct interaction. Examples include microcontrollers with built-in ADC and DAC.
    **Interfaces and Protocols:** **Standards like I2C, SPI, and UART facilitate communication between analog sensors and digital processors**. **Signal conditioning circuits (e.g., amplifiers, filters)** are often used to prepare analog signals for ADC.
    Signal Integrity and Noise: Proper design practices (e.g., shielding, grounding) are crucial to minimize noise and ensure accurate conversion and communication.

## Aliasing
- je jev, ke kterému může dojít při **převodu spojitého signálu na signál diskrétní čili nespojitý**. Takový převod se nazývá **vzorkování - sampling.**
- Aby při vzorkování nedocházelo k aliasingu, musí být podle **Nyquistova–Shannonova vzorkovacího teorému** vzorkovací frekvence **větší než dvojnásobek nejvyšší frekvence harmonických složek obsažených ve vzorkovaném signálu.** Pokud tuto podmínku nesplňuje, dochází k **překrytí frekvenčních spekter vzorkovaného signálu**, a tedy ke ztrátě informace. **Harmonické složky jsou sinusové nebo kosinusové komponenty signálu, které jsou celočíselnými násobky základní frekvence.** 
- **antialiasingový filtr**, který má za úkol **odfiltrovat frekvence vyšší, než odpovídají Nyquistovu–Shannonovu teorému.**
- Je to dolní propust realizovaná v případě běžných A/D převodníků jako **analogový frekvenční filtr.**  

## Nyquistův–Shannonův vzorkovací teorém
- je fyzikální tvrzení o tom, **že „přesná rekonstrukce spojitého, frekvenčně omezeného signálu z jeho vzorků je možná tehdy, pokud byla vzorkovací frekvence vyšší než dvojnásobek nejvyšší harmonické složky vzorkovaného signálu.**
- Dle Shannonova teorému je pak ideální frekvence pro vzorkování **rovna dvojnásobku maximální frekvence vyskytující se ve funkci f**. Při vzorkování s krokem menším, než **je polovina maximální frekvence, vzorkuji zbytečně moc**. Při kroku větším než polovina maximální frekvence se Fourierovy obrazy protnou a vzniká aliasing.


## ESP IDF
- ESP-IDF stands for Espressif IoT Development Framework.
- **Key Features of ESP-IDF:**
  - **Comprehensive SDK**: ESP-IDF provides a comprehensive Software Development Kit (SDK) with various **components, libraries, and tools needed for developing applications for ESP32-based devices.**
  - **FreeRTOS-based**: ESP-IDF uses FreeRTOS, an open-source **real-time operating system (RTOS), as its core**. This allows developers to create **multi-tasking applications efficiently.**
  - **Peripheral Drivers**: ESP-IDF comes with a wide range of peripheral drivers, including **GPIO, SPI, I2C, UART, PWM, ADC, DAC, and many others**, allowing developers to interface with a variety of sensors and actuators.
  - **Networking**: ESP-IDF supports multiple networking protocols and stacks, **such as TCP/IP, HTTP/HTTPS, MQTT, and others, enabling seamless connectivity and communication in IoT applications.**
  - **OTA (Over-the-Air) Updates**: ESP-IDF provides built-in support for OTA updates, **allowing devices to be updated with new firmware remotely.**
  - **Security**: ESP-IDF includes features for securing IoT applications, **such as secure boot, flash encryption, and encrypted communication protocols.**

## ESP memory management
- ESP32 chip has multiple memory types and flexible **memory mapping features**. This section describes how ESP-IDF uses these features by default.
- ESP-IDF distinguishes between **instruction memory bus (IRAM, IROM, RTC FAST memory)** and **data memory bus (DRAM, DROM).**
  -  **IRAM - Instruction memory bus - SRAM**
     - Is used to **access memory regions where the CPU fetches its instructions (code) from.**
     - Faster access memory dedicated to holding instructions for quick execution.
     - Usage:
       - storing instructions (code) that need to be **executed rapidly by the CPU**.
       - This includes **performance-critical code**, **interrupt service routines, and real-time processing tasks.**
       - Some timing critical code may be placed into IRAM to reduce the penalty **associated with loading the code from flash.**
       - In some cases, **placing a function into IRAM may reduce delays** caused by a cache miss and significantly improve that function's performance.
     - Typically smaller in size compared to other memory types like IROM, **but optimized for speed.**
  - **IROM (Code Executed from flash)**
    - If a function is not explicitly placed into IRAM (Instruction RAM) or RTC memory, **it is placed into flash**. As IRAM is limited, **most of an application's binary code must be placed into IROM instead.**
    - During Application Startup Flow, **the bootloader (which runs from IRAM)** configures the MMU flash cache to **map the app's instruction code region to the instruction space**. Flash accessed via the **MMU is cached using some internal SRAM** and **accessing cached flash data is as fast as accessing other types of internal memory.**
  - **DROM - data stored in flash**
    - By default, **constant data is placed by the linker into a region mapped to the MMU flash cache**. This is the same as the IROM (Code Executed from flash) section, **but is for read-only data not executable code.**
    - The **only constant data not placed into this memory type by default are literal constants** which are embedded by the compiler into application code. These are placed as the **surrounding function's executable instructions.**
    - Used for storing read-only data such as **constant arrays, lookup tables, and fixed configuration data.**
    - The DRAM_ATTR attribute can be used to force constants from **DROM into the DRAM**
  - **DRAM (Data RAM)**
    - **Non-constant static data (.data) and zero-initialized data (.bss) is placed by the linker into Internal SRAM as data memory**. The remaining space in this region is used for the **runtime heap**.
    - **Due to some memory fragmentation issues caused by ROM**, it is also not possible to **use all available DRAM for static allocations** - however the remaining DRAM is still available as heap at runtime.
    - Constant data may also be placed into DRAM, for example if it is used in an non-flash-safe ISR
  - **RTC memory**
    - **Global and static variables used by code which runs from RTC memory** must be placed into RTC Slow memory.
    - For example **deep sleep variables** can be placed here instead of RTC FAST memory.
    
    - The same region of RTC FAST memory can be accessed as **both instruction and data memory**. Code which has to run **after wake-up from deep sleep mode has to be placed into RTC memory.**   









