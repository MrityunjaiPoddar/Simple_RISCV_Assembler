# RISC-V Assembler (Python)

Assembler Code (RISC-V, Python) that converts assembly instructions into binary machine-readable format. The program reads an input file containing RISC-V assembly instructions and generates the corresponding binary machine code output file.

The assembler supports multiple instruction formats including **R-Type, I-Type, S-Type, B-Type, and J-Type** instructions and performs encoding based on the RISC-V instruction set architecture.

---

# Project Overview

This project implements a custom **RISC-V assembler written in Python** that translates human-readable assembly instructions into **32-bit binary machine code** suitable for execution in RISC-V simulators or hardware environments.

The assembler processes an input assembly file, identifies instruction types, handles register encoding, calculates immediate values, resolves labels for branch and jump instructions, and outputs the corresponding binary instructions to an output file.

The program uses **Python classes and modular instruction encoding methods** to maintain a clear and extensible design.

---

# Key Features

- Converts **RISC-V assembly instructions into 32-bit binary machine code**
- Supports multiple instruction formats:
  - R-Type instructions
  - I-Type instructions
  - S-Type instructions
  - B-Type instructions
  - J-Type instructions
- Register encoding for all **32 RISC-V registers**
- Label detection and resolution for **branch and jump instructions**
- Two-pass processing:
  - First pass identifies labels
  - Second pass generates binary code
- Immediate value conversion including **two's complement handling**
- Error handling for invalid instructions or arguments
- Command line interface using **Python sys arguments**
- Automatic output file generation containing machine code
- Modular architecture for easier extension and maintenance

---

# Supported Instructions

### R-Type
- add
- sub
- slt
- srl
- or
- and
- mul

### I-Type
- addi
- lw
- jalr

### S-Type
- sw

### B-Type
- beq
- bne

### J-Type
- jal

### Special Instructions
- rst
- halt

---

# Instruction Encoding

Each instruction is encoded according to the **RISC-V 32-bit instruction format**.

| Format | Fields |
|------|------|
| R-Type | funct7 rs2 rs1 funct3 rd opcode |
| I-Type | imm rs1 funct3 rd opcode |
| S-Type | imm[11:5] rs2 rs1 funct3 imm[4:0] opcode |
| B-Type | imm[12\|10:5] rs2 rs1 funct3 imm[4:1\|11] opcode |
| J-Type | imm[20\|10:1\|11\|19:12] rd opcode |

Immediate values are converted using **two’s complement representation** when required.

---

# How to Run

## Requirements

- Python 3.x

No external libraries are required.

---

## Command

Run the assembler using:

```bash
python Assembler.py <input_file> <output_file>
```

Example:

```bash
python Assembler.py program.asm output.bin
```

---

# Input File Format

The input file should contain **RISC-V assembly instructions**.

Example:

```
add a0,a1,a2
addi t0,t1,10
sw a0,0(sp)
beq a0,a1,label
jal ra,label
```

Labels are supported:

```
loop:
add a0,a1,a2
beq a0,a1,loop
```

---

# Output File

The output file will contain **binary encoded machine instructions**.

Example output:

```
00000000011001011000010100110011
00000000101000110000001010010011
00000000010100010010000000100011
```

---

# System Architecture

The assembler follows a **two-pass architecture**.

### Pass 1 — Label Detection
- Reads the input file
- Stores label names and instruction positions

### Pass 2 — Instruction Encoding
- Parses each instruction
- Identifies instruction format
- Encodes registers, immediates, and opcodes
- Writes binary output

---

# Code Structure

```
Assembler.py
│
├── RISCV Class
│   ├── Opcode mappings
│   ├── Register mappings
│   ├── funct3 / funct7 tables
│   ├── Label detection
│   ├── Instruction encoders
│
├── Instruction Encoding Functions
│   ├── R_Type()
│   ├── I_Type()
│   ├── S_Type()
│   ├── B_Type()
│   ├── J_Type()
│
└── Main Execution
    ├── Read input file
    ├── Resolve labels
    ├── Generate binary output
```

---

# Example Workflow

1. Write an assembly program
2. Run the assembler
3. Binary machine code is generated
4. Output can be used in **RISC-V simulators or hardware**

---

# Contributors

- Mohit Gupta  
- Mrityunjai Poddar
