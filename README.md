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
	
</details>

## Day 1

<details>

<summary> ISA(Instruction Set Architecture)</summary>

- Instruction Set Architecture (ISA) is a crucial component of computer architecture that defines the set of instructions that a computer's central processing unit (CPU) can execute. It serves as an interface between the hardware and software, specifying how programs interact with the CPU and memory.
- It provides a stable interface for software programmers, allowing them to write code that can run on various CPUs with the same ISA.
- At the same time, hardware designers have the flexibility to implement the ISA in different ways, optimizing for factors like speed, power efficiency, and cost.

</details>

<details>

<summary> RISC-V(Reduced Instruction Set Computing-Five) </summary>

- Open Standard: RISC-V is an open standard ISA, which means that its specifications are freely available to the public. This openness encourages collaboration, innovation, and the development of a wide range of processors by various organizations and individuals.
- Simplicity: RISC-V follows the RISC philosophy of simplicity and orthogonality. It has a relatively small number of instructions with a regular encoding format, making it easier to design and optimize processors.

</details>

<details>

<summary> From Apps to Hardware </summary> 

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
</details>

<details>

<summary> Labwork </summary> 

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
</details>
<details>

<summary> RISCV GCC Compiler and Dissemble </summary> 


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
</details>
<details>

<summary> Spike stimulation and debugging </summary> 

```spike pk sum1ton.0``` is used check whether the instructions produced are right to give expected output.

![Screenshot from 2023-08-21 17-56-07](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/adb8291e-b655-4174-ad49-31e0992a34bc)

To view the content of the registers 

```
spike -d pk sum1ton.o
```

![Screenshot from 2023-08-21 18-28-20](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/a6715e85-b999-466e-b13d-c84fad3a5b33)
</details>
<details>

<summary> Integer Number Representation </summary>


### Unsigned numbers: 
- Are just like integers but they don't have a + or - sign associated with them. Range: [0, (2^n)-1 ]
### Signed numbers: 
- these are a set of both positive and negative numbers Range : [0, 2^(n-1)-1] to [-1 to 2^(n-1)] To represent negative numbers in binary 2's complement methodology is used.
</details>
<details>

<summary> Labwork </summary>


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
</details>

## Day 2

<details>
<summary> Introduction to ABI and Basic Verification flow </summary>


- An Application Binary Interface (ABI) is a set of rules and conventions that define how binary programs or object code files interact with each other and with the operating system at runtime.
- ABIs are essential for ensuring compatibility and interoperability between different software components, such as libraries, compilers, and the operating system.
</details>
<details>
<summary> Memory Allocation for Double Words </summary>


- In computer memory and data storage, the term "double words" is often used to refer to a data type that consists of two words of memory, where each word typically represents a fixed number of bits. This concept is more commonly referred to as a "double word" or "dword." The specific size of a double word can vary depending on the computer architecture and the operating system, but it is typically 32 bits (4 bytes) on many modern systems.
</details>

<details>
<summary> Labwork </summary>


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
</details>

# RTL Design using Verilog with SKY130 Technology
## DAY3 - Introduction to Verilog RTL design and synthesis

### Introduction to Open-Source Simulator iVerilog

<details>
<summary> Introduction to iVerilog Design Testbench </summary>
	
 
- Simulator
	- Simulator is the tool used for checking any design.
    
- Design
  - Design is actual verilog code or set of verilog codes which has intended functionality to meet with the required specifications.
- Testbench
  - This is the setup to apply stimulus (test_vectors) to the design to check its funtionality
#### How simulator works?
- Simulator looks for the changes on the input signals
- Upon change to the input the output is evaluated
  - If no change to the input, no change to the output!
- Simulator is looking for change in the values of input!

![Screenshot from 2023-08-27 11-37-02](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/ac08a7ba-66f1-416f-8f99-e7b4e2a56b2a)

#### Iverilog based Simulation Flow 

![Screenshot from 2023-08-27 11-38-51](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/32a896ff-fe5e-403b-a979-8bd25da66654)
- output of the simulator is VCD( value change dump) file
- we will use the tool called gtkwave to view the waveform

</details>

### Labs using iverilog and gtkwave
<details>
<summary> Introduction to Labs  </summary>


![Screenshot from 2023-08-27 13-15-34](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/3555dd4a-88ba-4562-87fa-07aa5de1a2f7)


- make directory named vsd
  - ```mkdir vsd```
  - ```cd vsd```
- use the command ```git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git``` which helps in creating a folder ```sky130RTLDesignAndSynthesisWorkshop```
- All library files are stored in ```my_lib```
- verilog_model : contains all the standard cell verilog modules of the standard cells contained in the .lib
- verilog_files : contains all the verilog source files and testbench files which are required for labs

![Screenshot from 2023-08-27 13-17-01](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/44785077-0fee-4527-8660-032d27afcfae)
</details>

<details>
<summary> Introduction iVerilog GTKwave Part-1   </summary>

- To load source code along with testbench code into iverilog simulator use the command ```iverilog good_mux.v tb_good_mux.v```
- ```a.out``` file gets created to execute that use ```./a.out``` this dumps vcd file.
- load the vcd file into simulator gtkwave ``` gtkwave tb_good_mux.vcd```
![Screenshot from 2023-08-27 13-34-23](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/ca98eac1-deaf-4011-802f-5cc60e110369)
![Screenshot from 2023-08-27 13-37-26](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/e1fa5f0f-4a61-41fc-bab4-4ca41b01047c)
</details>

<details>
<summary> Introduction iVerilog GTKwave Part-2   </summary>


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
</details>

### Introduction to Yosys and Logic Synthesis

<details>
<summary> Introduction to yosys  </summary>

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
</details> 

<details>
<summary> Introduction to logic synthesis part-1  </summary>
	
- RTL Design
  - Behavioral representation of the required specification
- Synthesis
  - RTL to Gate level translation.
  - The design is converted into gates and the connections are made between the gates.
  - This is given out as a file called netlist.

![Screenshot from 2023-08-27 20-25-03](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/af88a5ce-fdc3-4d7a-ac7d-7c660e0e7599)

- .lib
  - Collection of logical modules.
  - Includes basic logic gates like And, Or, Not, etc
  - It contains Different flavors of same gate.
    - 2 input And gate
      - Slow version.
      - Medium version.
      - Fast version.
    - 3 input And gate
      - slow version.
      - Medium version.
      - Fast version.
    - 4 input And gate

  - It contains all standard cells to implement any Boolean logic functionalities.

- Why different flavours of gate??
  - Combinational logic determines the maximum speed of operation of the digital logic circuit.
  - T_clock > T_pd + T_cq + T_setup
  - To achieve maximum clock frequency(better performance) T_clock should me minimum that means all the delays(T_pd + T_cq + T_setup) must be minimum.
  - To ensure that there are no "HOLD" issues at DFF_B, we need cells that work slowly.
  - Hence we need cells that work fast to meet the required performance and we need cells that work slow to meet HOLD.
</details> 
<details>
<summary> Introduction to logic synthesis part-2  </summary>

#### Fast cell v/s Slow cells

- Fast Cells
  - Fast cells use wider transistors to enable higher current carrying capacity.
  - This allows for quicker charging and discharging of capacitive loads, resulting in faster signal transitions.
  - Wider transistors generally consume more power compared to narrower ones due to the increased current flow and larger gate capacitance.
  - While faster cells offer improved performance, they might have larger silicon area requirements due to the increased number of transistors. Additionally, they might be more susceptible to issues like noise and power consumption.

    
- Slow Cells
  - Slow cells use narrower transistors to reduce power consumption and minimize power dissipation.
  - Narrower transistors consume less power due to their lower current carrying capacity and reduced gate capacitance.
  - While slower cells consume less power, they might operate at lower clock frequencies and have longer signal propagation delays.
  - This can impact their ability to process data quickly.





#### Selection of the Cells
  - We have to guide the Synthesizer to choose the flavour of cells that is optimum for implementation of logic circuit.
  - More use of faster cells leads to bad circuit in terms of power and area and also hold time violations.
  - More use of slower cells leads to sluggish circuits amd may not meet the performance needs.
  - Hence the guidance is offered to the synthesiser in the form of constraints.

</details> 

### Labs using Yosys and Sky130 PDKs


<details>
<summary> Yosys lab  </summary>

### Yosys installation
```
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make
sudo apt-get update
sudo apt-get install build-essential clang bison flex  libreadline-dev gawk tcl-dev libffi-dev git  graphviz xdot pkg-config python3 libboost-system-dev libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make
sudo make install

```
- To invoke yosys
``` cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files ```
Type yosys
![Screenshot from 2023-08-28 23-24-00](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/f07fcfc7-f1e6-4c9a-8012-22a875097845)


- To read the library

``` read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib ```

- To read the design

``` read_verilog good_mux.v```



![Screenshot from 2023-08-28 23-56-04](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/3a177cf7-d83b-4fff-a597-d3e959085eba)

- To syntheis the module

 ``` synth -top good_mux ```

![Screenshot from 2023-08-28 23-58-39](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/b5fc27f3-553d-4267-a16a-fe36a1c8f796)

- For realizing the logic in the verilog file 
``` abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib```
![Screenshot from 2023-08-29 00-00-24](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/48f6790c-0fbb-45cb-9a48-064b7e2f7939)
- For logic realization ``` show ```
  - The mux is completely realised in the form of sky130 library cells. 
![Screenshot from 2023-08-29 00-04-24](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/d86a9f86-82fd-488c-9a02-452a6b4185f3)

- To write netlist
```
write_verilog good_mux_netlist.v
!gvim good_mux_netlist.v
```
![Screenshot from 2023-08-29 00-09-16](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/600ef5ba-e540-43aa-9a46-31f2ba8cddbb)
![Screenshot from 2023-08-29 00-07-45](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/8c8cbcf2-3442-463b-becd-b22648ffc8ef)
- To view simplified code
```
write_verilog -noattr good_mux_netlist.v
!gvim good_mux_netlist.v
```
![Screenshot from 2023-08-29 00-14-27](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/74121b14-fbc7-433a-b963-9cb6391283fd)

![Screenshot from 2023-08-29 00-12-39](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/83d6e53a-2e01-42d9-9c70-7ee853ef23c9)

</details> 

## DAY4 - Timing libs, Hierarchial and flat synthesis, and efficient flop coding styles.
### Introduction to timing .libs

<details>
<summary> Introduction to Dot Lib </summary>

- To view the contents in the .lib
 ``` gvim ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib ```


![Screenshot from 2023-08-29 00-47-33](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/66811173-1c83-404f-ab0c-7f29e3e87db5)

- First line ```library ("sky130_fd_sc_hd__tt_025C_1v80") ``` tells the name of the library.
- tt indicates typical type
- 025C indicates the temperature
- Process, Voltage ,Temperature are the three important parameters for design to work and it tells how my silicon work.
</details>

### Hierarchical vs Flat Synthesis

<details>
<summary> Hierarchical Synthesis Flat Synthesis  </summary>

#### Hierarchical Synthesis

``` 
cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
gvim multiple_modules.v
```

![Screenshot from 2023-08-29 16-34-21](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/6b28aa5f-9a46-4746-b490-1a6367c28c30)


```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show multiple_modules
```

![image](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/5869bb16-ac9f-4b2e-ac40-0af8aa1b8ef4)

![Screenshot from 2023-08-29 19-08-39](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/acd9060f-a507-4c11-a4cd-56d44841ea39)

- To show multiple modules ``` show multiple_modules ```

![Screenshot from 2023-08-29 16-43-08](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/9294542b-5616-4676-b810-3d08090b598e)

- ```
  
    write_verilog -noattr multiple_modules_hier.v
    !gvim multiple_modules_hier.v
  ```
![Screenshot from 2023-08-29 19-15-19](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/daefa8e2-6ff4-4042-b59f-a6f7d50d910a)


#### Flattened Synthesis

- ```
  yosys
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  read_verilog multiple_modules.v
  synth -top multiple_modules
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  flatten
  show
  ```
 
 ![Screenshot from 2023-08-29 19-33-17](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/36c5b451-2266-4f4b-8028-fde1c41cf6bc)
 
- ```
  write_verilog -noattr multiple_modules_flat.v
  !gvim multiple_modules_flat.v
  ```
![Screenshot from 2023-08-29 19-35-33](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/0ad1a0fb-fa96-45af-bff7-4f5c8dda7450)

- In flattened synthesis we can see the complete structure which we cannot in hierarchial synthesis.

</details>

### Various Flop Coding Styles and Optimization

<details>
<summary> Why Flops and Flop Coding Styles  </summary>

#### Glitch
- A glitch is a momentary and unwanted voltage or logic level transition in a digital circuit that occurs outside the expected or specified timing requirements.
- Glitches can occur due to various reasons, including propagation delays, race conditions, improper signal timing, or metastability issues.
- Inorder to avoid glitch we use flops.

#### Flops

- Flip-flops are bistable multivibrators that store a single binary bit (0 or 1).
- They are used to store and synchronize data in digital circuits.
- ```Sequential Logic``` : Flip-flops are commonly used in sequential logic circuits to store the state information. They are the memory elements of a digital system.
- ```Clocking Mechanism``` : Flip-flops are edge-triggered, which means they change their output only on the rising or falling edge of a clock signal. This property ensures synchronization and avoids timing hazards.
- ```Types``` : There are different types of flip-flops, including D flip-flops, JK flip-flops, T flip-flops, and SR flip-flops, each with its unique characteristics and use cases.

#### Flop Coding Styles:

- Synchronous Design: In synchronous digital design, flip-flops are controlled by a clock signal. The design follows a clocking methodology, where all operations occur at specific clock edges, ensuring synchronization and predictability.
- Asynchronous Design: In asynchronous digital design, flip-flops may not rely on a common clock signal. Signals change as their inputs change, making timing analysis more complex and potentially leading to glitches and hazards.
- Coding Conventions: Depending on the coding style, designers may use different coding conventions and techniques for implementing flip-flops in digital circuits. These conventions help ensure proper functionality and timing.

#### D Flip-Flop with Asynchronous Reset

- Why asynchronous is because it does not look for any clock.
- When a clock edge occurs (as determined by the clock signal), the D input is latched into the flip-flop, and its output Q takes on the value of D.
- However, if the asynchronous reset signal (R) is asserted (set to 1), it overrides the clocked behavior and immediately sets Q to 0, irrespective of the D input or clock edge.

```gvim dff_asyncres.v```

![Screenshot from 2023-09-01 10-57-36](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/50b6ffa3-0f50-4651-bab3-3f5e6b2cd9fd)


#### D Flip_Flop with Asynchronous Set

- When a clock edge occurs (as determined by the clock signal), the D input is latched into the flip-flop, and its output Q takes on the value of D.
- However, if the asynchronous set signal (S) is asserted (set to 1), it overrides the clocked behavior and immediately sets Q to 1, irrespective of the D input or clock edge.

```gvim dff_async_set.v```
![Screenshot from 2023-09-01 10-34-26](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/7b7a8ef1-bcea-46b5-a2a6-0a1b0e2ee350)

#### D Flip-Flop with Synchronous Reset

- Synchronous reset resets the flip-flop's state only on a specific clock edge.
- When the clock edge occurs (as determined by the CLK signal), the D input is latched into the flip-flop, and its output Q takes on the value of D.
- However, the synchronous reset signal (R) is considered synchronous with the clock, meaning the reset operation occurs on the same clock edge.
- When the reset signal (R) is asserted (set to 1) on the clock edge, it forces the Q output to a known state (usually 0) at that specific clock edge.

```gvim dff_syncres.v```
![Screenshot from 2023-09-01 10-38-50](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/5e361d9b-fa2a-4dcf-9488-153e0a5f0645)

#### D Flip-Flop with Asynchronous Reset and Synchronous Reset
- D Flip-Flop can be designed with both asynchronous and synchronous reset capabilities to provide flexibility in handling reset operations in digital circuits.

``` gvim dff_asyncres_syncres.v```

![Screenshot from 2023-09-01 10-45-56](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/7eda3f7f-6ac7-4f93-b147-cbd99fb657dc)

 </details>
 
<details>
<summary> Lab Flop Synthesis Simulations </summary>

#### D Flip-Flop with Asynchronous Reset

- Simulation
  ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
  iverilog dff_asyncres.v tb_dff_asyncres.v
  ./a.out
  gtkwave tb_dff_asyncres.vcd

  ```
![Screenshot from 2023-09-01 11-20-15](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/6f2dcd88-67e8-4038-91de-892365b77f9d)

#### D Flip_Flop with Asynchronous Set

- Simulation
  ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
  iverilog dff_async_set.v tb_dff_async_set.v
  ./a.out
  gtkwave tb_dff_async_set.vcd

  ```
![Screenshot from 2023-09-01 21-10-24](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/afa07b93-a11b-4fd8-b47c-08a210f58c77)
  
#### D Flip-Flop with Synchronous Reset

- simulation
  ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
  iverilog dff_syncres.v tb_dff_syncres.v
  ./a.out
  gtkwave tb_dff_syncres.vcd

  ```
![Screenshot from 2023-09-01 21-21-30](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/8549d251-db5c-495f-a5f6-241182260288)

#### Synthesis 
- D Flip-Flop with Asynchronous Reset
```
cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

yosys

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

read_verilog dff_asyncres.v

synth -top dff_asyncres

dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

show

```
![Screenshot from 2023-09-01 21-28-46](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/b9dbe24b-4a6a-44cd-b992-10347e5654b8)

- D Flip_Flop with Asynchronous Set
```
cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show

```
![Screenshot from 2023-09-01 21-34-18](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/7371156f-ae27-4d77-bce0-7240da3319c8)

- D Flip-Flop with Synchronous Reset
```
cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_syncres.v
synth -top dff_syncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show

```
![Screenshot from 2023-09-01 22-11-14](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/46be5ce7-a035-4ccc-b9f7-e86449ad56de)

</details>

<details>
<summary> Interesting Optimisations  </summary>

```
cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
gvim mult_2.v
```
![Screenshot from 2023-09-01 22-23-54](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/dcb3e19c-1da3-4b36-991a-57b5e5176b56)


```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mult_2.v
synth -top mul2

```
![Screenshot from 2023-09-01 22-39-32](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/147391a4-52ed-4782-adb1-22cebbe36199)

```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show

```
![Screenshot from 2023-09-01 22-40-48](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/787dc2bd-3eb0-4683-83e0-4462ec7c3f8a)

```

write_verilog -noattr mul2_netlist.v
!gvim mul2_netlist.v

```
![Screenshot from 2023-09-01 22-42-16](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/2f0e77d1-8a54-4b6f-943e-f5ecc1a38cf3)

``` gvim mult_8.v ```

![Screenshot from 2023-09-01 22-47-55](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/a6b371fc-4e56-4ca4-a891-4c61e39c818d)

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog mult_8.v
synth -top mult8
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![Screenshot from 2023-09-01 22-55-18](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/ee4feb63-e16c-4f55-b656-662bcabecc33)

![Screenshot from 2023-09-01 22-55-46](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/27dc1e7f-40f4-4e62-83ed-f29f44f42128)

```
cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
yosys
write_verilog -noattr mult8_netlist.v
!gvim mult8_netlist.v
```
![Screenshot from 2023-09-01 22-59-16](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/f8430cc1-cf17-4c65-b7bb-4d6de1956233)

</details>

## DAY5 - Combinational and Sequential Optimisations

### Introduction to Optimisations

<details>
<summary> Optimisations(Intro)  </summary>

#### Combinational Logic Optimisation

- Squeezing the logic to get the most optimised design
  - Area and Power savings

- Constant Propagation
  - Direct Optimisaton

- Boolean Logic Optimisation
  - K-Map
  - Quine McKluskey

#### Sequential logic Optimisation

- Basic
  - Sequential Constant propagation

- Advanced 
  - State optimisation
  - Retiming
  - Sequential Logic Cloning (Floor Plan Aware Synthesis)

</details>

### Combinational Logic Optimisations
<details>
<summary> Combinational logic optimizations(LABS)  </summary>

<details>
<summary> opt_check  </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim opt_check.v
  ```
  
![Screenshot from 2023-09-02 20-36-29](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/e934da93-6477-4b3e-aa66-13af483c1e6e)


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys
  
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog opt_check.v

  synth -top opt_check

  opt_clean -purge

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
![Screenshot from 2023-09-02 20-11-05](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/71141646-ea11-4cf7-a5b6-b60b5d6aa792)

![Screenshot from 2023-09-02 20-11-51](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/167144f7-7f08-40f9-b63d-562fb75a6acd)


</details>

<details>
<summary> opt_check2  </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim opt_check2.v
  ```

![image](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/aa7d902d-6a3f-42dc-a8d5-a285bcd2d983)


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog opt_check2.v

  synth -top opt_check2

  opt_clean -purge

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```


![Screenshot from 2023-09-02 20-16-53](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/a32d2961-bb18-4a65-a360-89eb7adf3a10)

![Screenshot from 2023-09-02 20-16-25](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/6c9d4359-9700-46a4-809c-8135ff1b3e13)

</details>

<details>
<summary> opt_check3  </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim opt_check3.v
  ```
![Screenshot from 2023-09-02 20-22-24](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/762a6883-0481-41f3-8cdf-beeaa8f2a7bb)

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog opt_check3.v

  synth -top opt_check3

  opt_clean -purge

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
![Screenshot from 2023-09-02 20-25-47](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/1f6af05a-a9f7-4c7c-8517-f27df5e1964c)

![Screenshot from 2023-09-02 20-26-49](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/9fe8bf9f-c4f9-41c0-9fc9-b91fe55f1432)


</details>

<details>
<summary> opt_check4  </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim opt_check4.v
  ```
![Screenshot from 2023-09-02 20-33-17](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/3e339813-f7e3-41ad-bce7-58003542d174)


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog opt_check4.v

  synth -top opt_check4

  opt_clean -purge

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
![Screenshot from 2023-09-02 20-30-54](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/819e3485-03ce-4365-83cc-6242103ca7f4)

![Screenshot from 2023-09-02 20-31-49](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/50caf06e-a64b-4d2c-ad3d-9b82bb3d286e)


</details>

<details>
<summary> multiple_module_opt </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim multiple_module_opt.v
  ```

![Screenshot from 2023-09-02 20-42-45](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/f153dfb9-6a30-451f-ab76-a284ff8195d5)

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog multiple_module_opt.v

  synth -top multiple_module_opt

  flatten

  opt_clean -purge

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
![Screenshot from 2023-09-02 20-44-49](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/e55d67c6-b188-462b-8237-f37c62528e55)

![Screenshot from 2023-09-02 20-55-52](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/d855a707-257d-4e36-ac50-1849c6b06077)

</details>


</details>

### Sequential Logic Optimisations

<details>
<summary> Sequential logic optimizations(LABS) </summary>

<details>
<summary> dff_const1 </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim dff_const1.v
  ```
![Screenshot from 2023-09-02 21-05-46](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/86653ba6-89df-4887-ab78-a2240b825b97)

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  iverilog dff_const1.v tb_dff_const1.v

  ./a.out

  gtkwave tb_dff_const1.vcd

  ```

![Screenshot from 2023-09-02 21-14-48](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/a31b09e5-1267-48ea-82df-393bece706f5)

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog dff_const1.v

  synth -top dff_const1

  opt_clean -purge

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
![Screenshot from 2023-09-02 21-17-54](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/68cce4a0-43a3-45a9-ae83-55eb3e36ccd9)

![Screenshot from 2023-09-02 21-18-41](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/204bfdf2-fa1b-4a10-bb9b-b4a150fa5b8d)

</details>


<details>
<summary> dff_const2 </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim dff_const2.v
  ```
![Screenshot from 2023-09-02 21-29-01](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/aa5c2bef-3bc9-49ac-990d-3213f1450938)


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  iverilog dff_const2.v tb_dff_const2.v

  ./a.out

  gtkwave tb_dff_const2.vcd

  ```

![Screenshot from 2023-09-02 21-41-51](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/e156ee29-1a09-4539-8f81-b820768286fd)


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog dff_const2.v

  synth -top dff_const2

  opt_clean -purge

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
![Screenshot from 2023-09-02 21-43-56](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/1d61883a-2b3c-488c-aafd-6617d31aaa13)


![Screenshot from 2023-09-02 21-44-43](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/06004e2a-ef41-47d1-9bec-0a5e1f33f3c1)


</details>


<details>
<summary> dff_const3 </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim dff_const3.v
  ```
![Screenshot from 2023-09-02 21-31-48](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/c01ba62f-6643-4c34-a252-37a218d8b985)

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  iverilog dff_const3.v tb_dff_const3.v

  ./a.out

  gtkwave tb_dff_const3.vcd

  ```

![Screenshot from 2023-09-02 22-09-32](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/17f770d7-cde1-43bc-9fe7-f52c023244b5)

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog dff_const3.v

  synth -top dff_const3

  opt_clean -purge

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
![Screenshot from 2023-09-02 22-11-33](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/51d8e8f1-4d31-41f7-82c5-a38457817316)


![Screenshot from 2023-09-02 22-12-26](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/f4250d2b-5ad1-43ee-b252-bf4e7eb66a3f)


</details>


<details>
<summary> dff_const4 </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim dff_const4.v
  ```
![Screenshot from 2023-09-02 21-35-55](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/79b6d745-e7f0-409e-b813-2069a00c4858)

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  iverilog dff_const4.v tb_dff_const4.v

  ./a.out

  gtkwave tb_dff_const4.vcd

  ```

![Screenshot from 2023-09-02 22-15-14](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/01982099-1193-4f2e-b2b5-bead630dbcb7)


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog dff_const4.v

  synth -top dff_const4

  opt_clean -purge

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
![Screenshot from 2023-09-02 22-19-27](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/30a215cc-5ade-491b-b678-9158214b3dd5)


![Screenshot from 2023-09-02 22-20-07](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/d9123f3e-14cb-4032-bfcc-f443f83db1ed)

</details>


<details>
<summary> dff_const5 </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim dff_const5.v
  ```
![Screenshot from 2023-09-02 21-37-12](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/7b61db48-f176-4213-9d42-a92c46aa742f)


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  iverilog dff_const5.v tb_dff_const5.v

  ./a.out

  gtkwave tb_dff_const5.vcd

  ```

![Screenshot from 2023-09-02 22-17-49](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/c600e4d0-515d-444e-ad81-739de9229b3a)


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog dff_const5.v

  synth -top dff_const5

  opt_clean -purge

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
![Screenshot from 2023-09-02 22-22-06](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/fb785e97-a58f-4f04-bf93-6d0c4f2dc7a0)

![Screenshot from 2023-09-02 22-23-51](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/586b32f2-4350-40a4-83ec-65deaa4e215c)

</details>


</details>

### Sequential Optimisations for Unused Outputs

<details>
<summary> counter_opt  </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim counter_opt.v
  ```
  
![Screenshot from 2023-09-02 22-37-03](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/b47ae5cc-c456-4da0-996b-027ef546fe03)


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys
  
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog counter_opt.v

  synth -top counter_opt

  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
![Screenshot from 2023-09-02 22-38-38](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/c1f2b24f-ede1-4ab5-baaa-ae293b5bd01a)

![Screenshot from 2023-09-02 22-39-34](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/7ca5e05d-41e3-4b51-8ac8-04a9fa7eaee1)

</details>

<details>
<summary> counter_opt2  </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim counter_opt2.v
  ```
  
![Screenshot from 2023-09-02 22-43-30](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/86c89446-f5ee-4824-9337-961a0d43acf8)



- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys
  
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog counter_opt2.v

  synth -top counter_opt

  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```
![Screenshot from 2023-09-02 23-08-18](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/5fee8986-8675-4668-81d3-b41a9af0ec09)
![Screenshot from 2023-09-02 23-09-17](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/78c2faa3-b2c6-4cee-955e-3d69771a3c7b)

</details>

## DAY6 - GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

### GLS, Synthesis-Simulation mismatch and Blocking/Non-blocking statements

<details>
<summary> GLS Concepts And Flow Using Iverilog   </summary>

- GLS : Gate Level Simulation
- What is GLS?
  - Running the test bench with Netlist as Design Under Test.
  - Netlist is logically same as RTL Code.
    - Same Test Bench will align with the Design.

- Why GLS?

  - Verify the logical correctness of design after synthesis
  - Ensuring the timing of the design is met.
    - For this GLS needs to be run with delay annotation.


![Screenshot from 2023-09-03 09-00-54](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/282aca45-c7d1-4944-b422-db4b17f8c6eb)

- Gate level verilog models
  - Timing aware (validate functionality + timing )
  - Functional (validate funtionality of the design alone.)

</details>

<details>
<summary> Synthesis-Simulation mismatch  </summary>

- Synthesis-simulation mismatch refers to a discrepancy or misalignment between the results of a synthesis process and a subsequent simulation or modeling of the same system or process.This happens due to
  - Missing sensitivity List
  - Blocking vs Non-Blocking Assignments
  - Non Standard Verilog Coding

</details>


<details>
<summary> Blocking And Non-Blocking Statements In Verilog  </summary>

- Blocking Assignment (=):
  - In Verilog, the = operator is used for blocking assignments.
  - When a blocking assignment statement is encountered, it evaluates the right-hand expression and assigns the result to the left-hand variable or register immediately.
  - The next statement waits for the blocking assignment to complete before executing.
  - This means that statements are executed in a sequential manner, one after the other.
  - Blocking assignments are commonly used when you want to model synchronous logic behavior or when you need to ensure specific sequencing of operations in your hardware description. 

- Non-Blocking Assignment (<=):
  - Non-blocking assignments use the <= operator to indicate that the assigned values will be updated simultaneously at the end of the current simulation time step, ensuring that all assignments are scheduled without blocking each other.
  - Non-blocking assignments are commonly used in synchronous digital designs to model behavior where multiple signals need to change simultaneously, such as in flip-flop updates or pipeline stages.
  - They help ensure proper sequencing of operations in hardware description languages like Verilog and VHDL.

</details>

<details>
<summary> Caveats with Blocking Statements  </summary>

- Blocking statements in Verilog are straightforward and easy to use, but they come with some caveats that designers should be aware of to avoid unexpected behavior or simulation mismatches.
- Here are some key caveats and considerations when working with blocking statements in Verilog:
  - Sequential Execution: Blocking statements execute sequentially in the order they appear within a procedural block. This can be both an advantage and a limitation. It's essential to ensure that your code's sequence matches your intended behavior, especially in synchronous designs.

  - Race Conditions: Using only blocking assignments may lead to race conditions in some situations. Race conditions occur when multiple assignments to the same variable occur within the same procedural block, and the order of execution affects the final outcome. To avoid race conditions, you may need to use non-blocking assignments (<=) in specific cases.
  - Behavioral vs. RTL Simulation: Verilog is often used for both behavioral and RTL (Register-Transfer Level) simulations. In behavioral simulations, blocking statements may be sufficient to model the desired behavior. However, in RTL simulations, where hardware details are more critical, you should carefully consider the use of blocking vs. non-blocking assignments to model accurate hardware behavior.
  - Simulation vs. Synthesis: Verilog code is often used for simulation and synthesis. While blocking statements are generally well-suited for simulation, they may not always represent hardware accurately when targeting synthesis for FPGA or ASIC implementation. For synthesis, you may need to follow synthesis-specific coding guidelines.
  
</details>

### Labs on GLS and Synthesis-Simulation Mismatch

<details>
<summary> ternary_operator_mux   </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim ternary_operator_mux.v
  ```
![Screenshot from 2023-09-03 10-24-49](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/de698735-c142-4fba-b08c-b5bfd2e0bf87)

##### Simulation
- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  iverilog ternary_operator_mux.v tb_ternary_operator_mux.v

  ./a.out

  gtkwave tb_ternary_operator_mux.vcd

  ```

![Screenshot from 2023-09-03 10-31-26](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/739ec6f8-5824-4d89-950a-6447293d58fb)

##### Synthesis


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog ternary_operator_mux.v

  synth -top ternary_operator_mux

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```

![Screenshot from 2023-09-03 10-33-19](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/1958b0d8-0ee7-49f8-ac2e-ceccc9656cf4)

![Screenshot from 2023-09-03 10-33-47](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/b3ac58f4-fbf2-4fe3-a82e-8670509e5609)

##### To do GLS 

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v

./a.out

gtkwave tb_ternary_operator_mux.vcd
```
![Screenshot from 2023-09-03 10-52-42](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/0076b875-ba55-4711-aeb0-93ad574ddb82)

</details>

<details>
<summary> bad_mux  </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim bad_mux.v
  ```
![Screenshot from 2023-09-03 10-59-29](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/3f32858c-ab7b-45b6-9d17-c304da10cc5b)


##### Simulation
- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  iverilog bad_mux.v tb_bad_mux.v

  ./a.out

  gtkwave tb_bad_mux.vcd

  ```

![Screenshot from 2023-09-03 11-01-48](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/6a35601f-a430-4121-ab54-891e64be2c04)


##### Synthesis


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog bad_mux.v

  synth -top bad_mux

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```

![Screenshot from 2023-09-03 11-08-21](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/54525af4-2b0b-4d6f-bf12-021d4cee19d1)

![Screenshot from 2023-09-03 11-15-21](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/9326efc1-c5c7-4abf-b261-b9cd58ac48ad)


##### To do GLS 

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v

./a.out

gtkwave tb_bad_mux.vcd
```

![Screenshot from 2023-09-03 11-17-51](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/4af02d35-a990-441d-ac6c-74f5465cf1e3)


</details>


### Labs on Synth-Sim Mismatch for Blocking Statement

<details>
<summary> blocking_caveat  </summary>

- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  gvim blocking_caveat.v
  ```
![Screenshot from 2023-09-03 11-25-32](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/4dbe5f05-42f9-4e73-a438-b8f0fbbf170e)



##### Simulation
- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  iverilog blocking_caveat.v tb_blocking_caveat.v

  ./a.out

  gtkwave tb_blocking_caveat.vcd

  ```

![Screenshot from 2023-09-03 11-27-55](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/a92d8e92-d26e-45dc-8b01-664d944e9115)



##### Synthesis


- ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files

  yosys

  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  read_verilog blocking_caveat.v

  synth -top blocking_caveat

  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

  show
  ```

![Screenshot from 2023-09-03 11-29-33](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/ea6f9d7d-e48e-4b55-8631-dc0625c1d6d0)

![Screenshot from 2023-09-03 11-30-05](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/17851192-014b-43e2-8833-62235ada61a4)



##### To do GLS 

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v

./a.out

gtkwave tb_blocking_caveat.vcd   

```
![Screenshot from 2023-09-03 11-32-01](https://github.com/JBavitha/physicaldesignASIC/assets/142578450/ccc708f8-abae-4fb1-a234-3b5886dd11bd)

</details>




































