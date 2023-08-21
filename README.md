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
  
### From Apps to Hardware
Application software ---> System software ---> Hardware

This Application Software enters into a block called as System Software and this system software intern converts application program into  binary language.
- Major components of system sofware are:
  1. OS(Operating System)
  2. Compiler
  3. Assembler
![Screenshot from 2023-08-21 17-19-03](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/c61ccc96-f3ad-4a8d-842c-0c0d5186eb4d)

### Type of Instructions
- Pseudo Instructions
- Base Integer Instructions(RV64I)
- Multiply Extension(RV64M)
- Single and Double precision floating point Extension(RV64F and RV64D)

## Labwork
Write a program to calculate the sum of numbers from 1 to n

we write program in leafpad as sum1ton.c

```
#include<stdio.h>
int main()
{
int i,sum=0,n=5;
for(i=1;i<=n;i++)
{
sum=sum+i;
}
printf("sum of numbers from 1 to %d is %d \n",n,sum);
return 0;
}
```
![Screenshot from 2023-08-21 17-36-51](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/c0f6639b-05b4-4d1e-996c-d68d4581c782)

Compile the code using following command 

```gcc sum1ton.c```

To execute the program 

```./a.out```

![Screenshot from 2023-08-21 17-44-23](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/ac408668-89fe-468f-a574-e6ef1124f352)

## RISCV GCC Compiler and Dissemble

Now use riscv gcc compiler to compile the c program 

```riscv64-unknown-elf-gcc -Ofast -mabi=lb64 -march=rv64i -o sum.o sum.c```

![Screenshot from 2023-08-21 17-50-17](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/4c29c199-e19c-48f9-b85b-d6778dae87c7)

If you find any error as above use follwing three commands to proceed further 

```
vim ~/.bashrc
export PATH=~/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH
export PATH=~/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH
```
To get dissembled ALP code use following command

```riscv64-unknown-elf-objdump -d sum.o | less```

In order to view main section type 

```/main```

Here since we used -Ofast optimisation.

![Screenshot from 2023-08-21 18-04-27](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/71991017-4539-4474-836f-bbf488a258c2)

Here since we used -O1 optimisation.

![Screenshot from 2023-08-21 18-14-47](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/ec75c287-653f-4348-b371-302021390533)

## Spike stimulation and debugging
```spike pk sum1ton.0``` is used check whether the instructions produced are right to give expected output.

![Screenshot from 2023-08-21 17-56-07](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/adb8291e-b655-4174-ad49-31e0992a34bc)

To view the content of the registers 

```spike -d pk sum1ton.o```

![Screenshot from 2023-08-21 18-28-20](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/a6715e85-b999-466e-b13d-c84fad3a5b33)

## Integer Number Representation

### Unsigned numbers: 
- Are just like integers but they don't have a + or - sign associated with them. Range: [0, (2^n)-1 ]
### Signed numbers: 
- these are a set of both positive and negative numbers Range : [0, 2^(n-1)-1] to [-1 to 2^(n-1)] To represent negative numbers in binary 2's complement methodology is used.










