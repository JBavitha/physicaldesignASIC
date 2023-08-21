# physicaldesignASIC
# VLSI Physical Design in ASIC's
## Objective
VLSI ASIC (Very Large Scale Integration Application-Specific Integrated Circuit) design is a complex and intricate process focused on creating custom integrated circuits tailored to specific applications.This involves translating the high-level functional representation of the circuit into a physical implementation that meets design constraints, performance targets, and manufacturability requirements.


## Installation
- Execute run.sh in the below github file
https://github.com/kunalg123/riscv_workshop_collaterals/blob/master/run.sh

![Screenshot from 2023-08-20 00-57-11](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/70b55c0c-4a49-4812-aa4d-d07acd3b9014)

- If you get as above after running the command,RISCV GNU toolchain is succesfully installed.
```
riscv64-unknown-elf-gcc --version
```
## Day 1
## Introduction to RISC-V ISA and GNU Compiler Chain
### ISA(Instruction Set Architecture)
- Instruction Set Architecture (ISA) is a crucial component of computer architecture that defines the set of instructions that a computer's central processing unit (CPU) can execute. It serves as an interface between the hardware and software, specifying how programs interact with the CPU and memory.
- It provides a stable interface for software programmers, allowing them to write code that can run on various CPUs with the same ISA.
- At the same time, hardware designers have the flexibility to implement the ISA in different ways, optimizing for factors like speed, power efficiency, and cost.
### RISC-V(Reduced Instruction Set Computing -Five)
- Open Standard: RISC-V is an open standard ISA, which means that its specifications are freely available to the public. This openness encourages collaboration, innovation, and the development of a wide range of processors by various organizations and individuals.
- Simplicity: RISC-V follows the RISC philosophy of simplicity and orthogonality. It has a relatively small number of instructions with a regular encoding format, making it easier to design and optimize processors.
