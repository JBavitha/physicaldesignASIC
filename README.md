# physicaldesignASIC
# VLSI Physical Design in ASIC's
## Objective
VLSI ASIC (Very Large Scale Integration Application-Specific Integrated Circuit) design is a complex and intricate process focused on creating custom integrated circuits tailored to specific applications.This involves translating the high-level functional representation of the circuit into a physical implementation that meets design constraints, performance targets, and manufacturability requirements.


## Installation
<details>

<summary> Execute run.sh in the below github file </summary>
https://github.com/kunalg123/riscv_workshop_collaterals/blob/master/run.sh

![Screenshot from 2023-08-20 00-57-11](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/70b55c0c-4a49-4812-aa4d-d07acd3b9014)

- If you get as above after running the below command,RISCV GNU toolchain is succesfully installed.
```
riscv64-unknown-elf-gcc --version
```
	### End of installation
 </details>

# TABLE OF CONTENTS
## Day 1

+ [ISA(Instruction Set Architecture)](#Instruction-Set_Architecture)
	- Instruction Set Architecture (ISA) is a crucial component of computer architecture that defines the set of instructions that a computer's central processing unit (CPU) can execute. It serves as an interface between the hardware and software, specifying how programs interact with the CPU and memory.
	- It provides a stable interface for software programmers, allowing them to write code that can run on various CPUs with the same ISA.
	- At the same time, hardware designers have the flexibility to implement the ISA in different ways, optimizing for factors like speed, power efficiency, and cost.
 	

+ [RISC-V(Reduced Instruction Set Computing-Five)](#RISC-V(Reduced-Instruction-Set-Computing-Five)
	- Open Standard: RISC-V is an open standard ISA, which means that its specifications are freely available to the public. This openness encourages collaboration, innovation, and the development of a wide range of processors by various organizations and individuals.
	- Simplicity: RISC-V follows the RISC philosophy of simplicity and orthogonality. It has a relatively small number of instructions with a regular encoding format, making it easier to design and optimize processors.
  
+ From Apps to Hardware
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

```
gcc sum1ton.c
```

To execute the program 

```
./a.out
```

![Screenshot from 2023-08-21 17-44-23](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/ac408668-89fe-468f-a574-e6ef1124f352)

## RISCV GCC Compiler and Dissemble

Now use riscv gcc compiler to compile the c program 

```
riscv64-unknown-elf-gcc -Ofast -mabi=lb64 -march=rv64i -o sum.o sum.c
```

![Screenshot from 2023-08-21 17-50-17](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/4c29c199-e19c-48f9-b85b-d6778dae87c7)

If you find any error as above use follwing three commands to proceed further 

```

export PATH=~/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH
export PATH=~/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH
```
To get dissembled ALP code use following command

```
riscv64-unknown-elf-objdump -d sum.o | less
```

In order to view any instance section type 

```/instance```

Here since we used -Ofast optimisation.

![Screenshot from 2023-08-21 18-04-27](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/71991017-4539-4474-836f-bbf488a258c2)

Here since we used -O1 optimisation.

![Screenshot from 2023-08-21 18-14-47](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/ec75c287-653f-4348-b371-302021390533)

## Spike stimulation and debugging
```spike pk sum1ton.0``` is used check whether the instructions produced are right to give expected output.

![Screenshot from 2023-08-21 17-56-07](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/adb8291e-b655-4174-ad49-31e0992a34bc)

To view the content of the registers 

```
spike -d pk sum1ton.o
```

![Screenshot from 2023-08-21 18-28-20](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/a6715e85-b999-466e-b13d-c84fad3a5b33)

## Integer Number Representation

### Unsigned numbers: 
- Are just like integers but they don't have a + or - sign associated with them. Range: [0, (2^n)-1 ]
### Signed numbers: 
- these are a set of both positive and negative numbers Range : [0, 2^(n-1)-1] to [-1 to 2^(n-1)] To represent negative numbers in binary 2's complement methodology is used.

## Labwork

- Write a C program that shows the maximum and minimum values of "n" bit unsigned numbers Considering(n=64) here

```
#include <stdio.h>
#include <math.h>
int main(){
  
	unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
	unsigned long long int min = (unsigned long long int) (pow(2,64) *(-1));
	printf("Minimum value is %llu\n",min);
	printf("Maximum value is %llu\n",max);
	return 0;
}
```
![Screenshot from 2023-08-21 18-36-34](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/30390269-6a76-4f80-9faa-f8e61ee99117)

Execution 

![Screenshot from 2023-08-21 18-37-47](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/8404c5ee-1143-45fd-a6b1-013407f14dbc)

- Write a C program that shows the maximum and minimum values of "n" bit signed numbers

```
#include <stdio.h>
#include <math.h>

int main(){
	
	long long int max = (long long int) (pow(2,63) -1);
	long long int min = (long long int) (pow(2,63) *(-1));
	printf("Minimum value is %lld\n",min);
	printf("Max value is %lld\n",max);
	return 0;
}
```


![Screenshot from 2023-08-21 18-44-27](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/a7a98b11-b977-4ab0-9647-c332da4f8732)

## Day 2

### Introduction to ABI and Basic Verification flow

- An Application Binary Interface (ABI) is a set of rules and conventions that define how binary programs or object code files interact with each other and with the operating system at runtime.
- ABIs are essential for ensuring compatibility and interoperability between different software components, such as libraries, compilers, and the operating system.

### Memory Allocation for Double Words

- In computer memory and data storage, the term "double words" is often used to refer to a data type that consists of two words of memory, where each word typically represents a fixed number of bits. This concept is more commonly referred to as a "double word" or "dword." The specific size of a double word can vary depending on the computer architecture and the operating system, but it is typically 32 bits (4 bytes) on many modern systems.

# labwork 

- write c code and assemble code in seperate file.

C program

```
#include <stdio.h>

extern int load(int x, int y);

int main()
{
  int result = 0;
  int count = 9;
  result = load(0x0, count+1);
  printf("Sum of numbers from 1 to 9 is %d\n", result);
}
```

Assembly code

```
.section .text
.global load
.type load, @function

load:

add a4, a0, zero
add a2, a0, a1
add a3, a0, zero

loop:

add a4, a3, a4
addi a3, a3, 1
blt a3, a2, loop
add a0, a4, zero
ret
```

Now simulate c program and assembly code using follwing command

```
riscv64-unknown-elf-gcc -O1 -mabi=lb64 -march=rv64i -o custom1to9.o custom1to9.c load.S
```

![Screenshot from 2023-08-21 19-00-52](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/9b1ca4a6-250d-4ed8-b94e-bf1310196552)

Assembly code 

``` 
riscv64-unknown-elf-objdump -d custom1to9.o|less
```

![Screenshot from 2023-08-21 19-02-34](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/51a60e3d-3943-4a50-9f7d-77cdab704da8)

# RTL Design using Verilog with SKY130 Technology

## Introduction to verilog RTL design and synthesis 

- Simulator
  - Simulator is the tool used for checking any design.
    
- Design
  - Design is actual verilog code or set of verilog codes which has intended functionality to meet with the required specifications.
- Testbench
  - This is the setup to apply stimulus (test_vectors) to the design to check its funtionality
### How simulator works?
- Simulator looks for the changes on the input signals
- Upon change to the input the output is evaluated
  - If no change to the input, no change to the output!
- Simulator is looking for change in the values of input!

![Screenshot from 2023-08-27 11-37-02](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/ac08a7ba-66f1-416f-8f99-e7b4e2a56b2a)

### Iverilog based Simulation Flow 

![Screenshot from 2023-08-27 11-38-51](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/32a896ff-fe5e-403b-a979-8bd25da66654)
- output of the simulator is VCD( value change dump) file
- we will use the tool called gtkwave to view the waveform
## Labs using iverilog and gtkwave
### Introduction to Labs 

![Screenshot from 2023-08-27 13-15-34](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/3555dd4a-88ba-4562-87fa-07aa5de1a2f7)


- make directory named vsd
  - ```mkdir vsd```
  - ```cd vsd```
- use the command ```git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git``` which helps in creating a folder ```sky130RTLDesignAndSynthesisWorkshop```
- All library files are stored in ```my_lib```
- verilog_model : contains all the standard cell verilog modules of the standard cells contained in the .lib
- verilog_files : contains all the verilog source files and testbench files which are required for labs

![Screenshot from 2023-08-27 13-17-01](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/44785077-0fee-4527-8660-032d27afcfae)

###  Introduction iVerilog GTKwave Part-1 
- To load source code along with testbench code into iverilog simulator use the command ```iverilog good_mux.v tb_good_mux.v```
- ```a.out``` file gets created to execute that use ```./a.out``` this dumps vcd file.
- load the vcd file into simulator gtkwave ``` gtkwave tb_good_mux.vcd```
![Screenshot from 2023-08-27 13-34-23](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/ca98eac1-deaf-4011-802f-5cc60e110369)
![Screenshot from 2023-08-27 13-37-26](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/e1fa5f0f-4a61-41fc-bab4-4ca41b01047c)

### Introduction iVerilog GTKwave Part-2
- To check the file structure ```gvim tb_good_mux.v -o good_mux.v```
#### good_mux.v 
```
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule

```
#### tb_good_mux.v

```
`timescale 1ns / 1ps
module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule
```
## Introduction to Yosys and Logic Synthesis
### Introduction to Yosys 
- Synthesizer
  - It is a tool used for converting RTL design code to netlist.
  - Yosys is the synthesizer we use in this course.
#### Yosys setup 

![Screenshot from 2023-08-27 14-26-23](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/72a70605-f86d-4e95-ad9d-49db2aee5333)

- Netlist file
  - It is the representation of the design in form of the standard cells in the .lib
- ```read_verilog``` : used to read design
- ```read_liberty``` : used to read .lib
- ```write_verilog``` : used to write out the netlist file
#### verify the synthesis
- Netlist and the tesbench is fed to the iverilog simulator.
- The vcd file is generated and that is fed to the gtkwave simulator.
- The output on the simulator must be same as the output observed during RTL simulation.
- Testbench is same as RTL testbench so there is no need of new testbench.
  










 




















