<div align="center">

# BabySoC Fundamentals & Functional Modelling

</div>

## Introduction to what is BabySoC?
### SoC stands for "System on Chip"
- A System-on-Chip is a single chip that integrates multiple components of a computer or electronic system — like processor (CPU), memory, input/output interfaces, and sometimes even specialized modules like GPU, communication controllers, etc.
Instead of using separate chips for each function, SoC puts them together in one chip, making the system smaller, faster, and more power efficient.
- BabySoC is a simplified, smaller version of a real-world SoC, usually designed for learning and experimentation.It is not as complex as commercial SoCs like those in smartphones or laptops rather it focuses on the basic building blocks like processor core, memory, and simple input-output units.
Think of BabySoC like a "mini lab model" that helps students and engineers understand how a SoC works at a fundamental level.
- Example: A BabySoC may contain:
  
  1. A simple RISC-V or ARM-based CPU core
  
  2. Small RAM and ROM
  
  3. A timer unit
  
  4. UART (for communication with PC)
  
  5. GPIO (to control LEDs or read switches)

## Fundamentals of BabySoC
The basic principles and components that make up BabySoC are:
### (a) Processor Core (CPU)
- The "brain" of the SoC.
- Executes instructions written in assembly/C programming.
- In BabySoC, usually a simple RISC (Reduced Instruction Set Computer) core is used (e.g., RISC-V), because it is easier to learn and implement.
### (b) Memory (RAM & ROM)
- RAM (Random Access Memory): Temporary storage used while programs are running.
- ROM (Read Only Memory): Stores the program code (firmware) permanently.
### (c) Interconnect/Bus
- The communication "road" inside the SoC.
- Connects CPU, memory, and peripherals together.
- Example: AMBA bus, Wishbone bus.
### (d) Input/Output (I/O) Peripherals
- Allow the BabySoC to interact with the outside world.
- Common peripherals are:
  1. GPIO (General Purpose Input Output): Control LEDs, read switches.
  2. UART: Communicate with a PC through serial terminal.
  3. Timer: Generate time delays or periodic signals.
### (e) Power and Clock
- Clock: Synchronizes the entire SoC (like a heartbeat).
- Power management: Ensures circuits run correctly without overheating.
  
## Functional Modelling of BabySoC
### What is Functional Modelling?
- It means creating a high-level representation of the SoC that focuses on what it does (functionality), not on the physical design (transistors, layouts).
- It is often written in Hardware Description Languages (HDL) like Verilog or VHDL, or sometimes in C/C++/SystemC for higher abstraction.
### Purpose of Functional Modelling
- To verify the logic of the system before physically making the chip.
- To simulate how the CPU, memory, and peripherals will behave.
- To debug and test software programs on the model before burning them into hardware.
### Example of Functional Modelling Steps
- Define the CPU : e.g., what instruction set it supports (ADD, SUB, LOAD, STORE).
- Model the memory : a block that stores data and instructions.
- Model peripherals : e.g., GPIO block that can switch an LED on/off.
- Simulate : Run a test program (e.g., blink LED every 1 second) and check if the design works correctly.

## Why Learn BabySoC and Functional Modelling?
- It gives a hands-on understanding of how chips like ARM Cortex or Snapdragon are built at a small scale.
- Bridges the gap between theory (computer architecture) and practical design (hardware implementation).
- Helps you learn both hardware (HDL coding, simulation) and software (programming CPU to control peripherals).
- Essential foundation for VLSI design, embedded systems, and chip design careers.

## Summary
BabySoC is a simplified System-on-Chip that brings together the core building blocks of digital design—CPU, memory, bus, and peripherals—into a single integrated system. It serves as a capstone project that demonstrates the transition from basic modules to a complete working SoC. Through functional modelling and simulation, BabySoC highlights how different components interact, verifies system-level behavior, and provides a strong foundation for understanding real-world SoC design.
 







