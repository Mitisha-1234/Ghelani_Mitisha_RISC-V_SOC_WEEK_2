<div align="center">
  
# VSDBabySoC Project Labs

</div>
VSDBabySoC is a simplified System-on-Chip (SoC) design that integrates a RISC-V CPU (RVMyth), a Phase-Locked Loop (PLL), and a Digital-to-Analog Converter (DAC) into a single top-level module. The design demonstrates how digital building blocks (CPU and clock circuits) can be combined with mixed-signal components (DAC) to form a complete SoC.
The goal of this project is to:

- Understand SoC integration of processor, clocking, and analog interfaces.
- Explore digital and mixed-signal simulation using Verilog.
- Provide a platform for verifying RISC-V based processing with peripheral IPs.

## Key Concepts
### 1.  RVMyth (RISC-V CPU)
- Implements a basic RISC-V pipeline capable of executing simple instructions.
- Generates a digital output bus that drives the DAC.
### 2.  PLL (Phase-Locked Loop)
- Used to generate a stable and high-frequency clock for the CPU.
- Demonstrates integration of analog-inspired circuits within an SoC.
### 3.  DAC (Digital-to-Analog Converter)
- Converts the 10-bit digital output from the CPU into an analog signal.
- Useful for mixed-signal verification and showcasing digital-to-analog interfacing.
### 4.  Top-Level SoC (vsdbabysoc.v)
- Integrates CPU, PLL, and DAC into a single design.
- Handles interconnections such as:
  1. PLL clock driving the CPU.
  2. CPU digital bus connected to DAC input.
  3. DAC generating the final analog output.
### 5.  Testbench
- Provides stimulus (reset, clock, reference signals).
- Captures simulation results in .vcd format for waveform analysis.
- Ensures functional correctness of the integrated SoC.

 ## Project Structure
 ```txt
VSDBabySoC/
├── src/
│   ├── include/      # Header files (*.vh)
│   ├── module/       # Verilog + TLV modules
│   │   ├── vsdbabysoc.v   # Top-level module
│   │   ├── rvmyth.v       # CPU
│   │   ├── avsdpll.v      # PLL
│   │   ├── avsddac.v      # DAC
│   │   └── testbench.v    # Testbench
└── output/           # Simulation outputs
```
## Project Setup
First of all we need to clone the following Repository:
```bash
cd ~/VLSI
git clone https://github.com/manili/VSDBabySoC.git
cd VSDBabySoC/
```
As RVMyth is implemented in TL-Verilog (.tlv), it must be converted into standard Verilog before running simulation.To do so run the following commands in the terminal:
```bash
# Install tools
sudo apt update
sudo apt install python3-venv python3-pip

# Create virtual env
python3 -m venv sp_env
source sp_env/bin/activate

# Install SandPiper-SaaS
pip install pyyaml click sandpiper-saas

# Convert TLV → Verilog
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
```
## Pre-Synthesis Simulation
Pre-synthesis simulation verifies the functional correctness of the RTL design before applying synthesis constraints. At this stage, the design is simulated in pure Verilog without considering gate-level delays or physical implementation.For the VSDBabySoC, the pre-synthesis simulation confirms:

- The CPU (RVMyth) executes instructions and drives digital outputs.
- The PLL generates and stabilizes the clock signal.
- The DAC converts CPU’s digital output to an analog-equivalent waveform.
- The integrated top-level SoC (vsdbabysoc.v) operates correctly when tested with the provided testbench.
```bash
mkdir -p output/pre_synth_sim

iverilog -o output/pre_synth_sim/pre_synth_sim.out \
  -DPRE_SYNTH_SIM \
  -I src/include -I src/module \
  src/module/testbench.v

cd output/pre_synth_sim
./pre_synth_sim.out
```
Now for viewing the gtkwave, run the command:
```bash
gtkwave pre_synth_sim.vcd
```
## Pre_synth_sim Waveform

The pre-synthesis simulation of the VSDBabySoC was performed using GTKWave.

<img width="1916" height="1079" alt="Part 2 " src="https://github.com/user-attachments/assets/95355fe1-e88d-48d0-b918-0fe9516601f9" />

The waveform confirms the correct integration of the CPU, DAC, and PLL modules.

- CPU Activity: Instruction fetch and memory transactions are observed through toggling of the CPU_dmem_addr, CPU_dmem_rd_data, and CPU_ld_data signals.
- DAC Operation: The 10-bit digital output from the CPU is successfully converted to an analog-equivalent waveform at the DAC output (OUT, D[9:0]).
- PLL Behavior: The PLL (VCO_IN, period, refpd) demonstrates frequency alignment with the reference clock. Initial fluctuations are seen during the lock-in process, followed by stabilization, indicating proper PLL lock.

This validates that the SoC components are functioning as intended in simulation, with the CPU driving the DAC and the PLL providing a stable clock signal.

## Summary
Through the VSDBabySoC project, I gained hands-on experience in integrating digital and mixed-signal IPs into a single SoC environment. I understood how a CPU core, PLL, and DAC interact within a top-level design and how to validate their functionality through pre-synthesis simulation. I also learned the importance of converting TL-Verilog designs to Verilog for simulation, setting up testbenches for verification, and analyzing results using waveform viewers like GTKWave. This exercise strengthened my understanding of SoC design flow, verification, and system-level integration.
