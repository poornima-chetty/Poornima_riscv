RTL synthesis and GLS simulation:
tools used
Go to the following directory and create two ".v" files
**code**
**pes_ser.v**
```module vsdserializer_v1(clk, load, INPUT, OUTPUT);
input clk, load;
input [9:0] INPUT;
output reg OUTPUT;
reg [9:0] tmp;
always @(posedge clk)
begin
  if(load)
  tmp<=INPUT;
  else![pes1](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/fe394f16-01f8-4759-9173-cb5b7ab3ff1b)

  begin
  OUTPUT <= tmp[9];
  tmp <= {tmp[8:0],1'b0};
  end
end
endmodule
```

![pes1](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/fe394f16-01f8-4759-9173-cb5b7ab3ff1b)

**pes_ser_tb.v**
```
`timescale 1ns / 1ps
module vsdserializer_v1_tb();
reg clk,load;
reg[9:0] INPUT;
wire OUTPUT;
vsdserializer_v1 dut (clk, load, INPUT, OUTPUT);
initial begin
 clk = 1;
 INPUT = $urandom;
 load = 1;
 #30 load = 0;
 #120 INPUT = $urandom;
load = 1;
#30 load = 0;
#120 INPUT = $urandom;
load = 1;
#30 load = 0;
end
always #50 clk = ~clk;
initial begin
$dumpfile("vsdserializer_v1.vcd");
$dumpvars(0,vsdserializer_v1_tb);
#900 $finish;
end
endmodule
```
![pes2](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/7b6352ee-e42b-4216-b61c-46d1c3167aad)

running the saved files using following commands
**Simulation**
```cd VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files
iverilog pes_ser.v pes_ser_tb.v
./a.out
gtkwave vsdserializer_v1.vcd

```
![outputfinal](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/97448556-699a-4387-8b2e-aa04354d2dee)
**RTL synthesis**

Go to verilog_files directory and type yosys
![yosys](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/a7ef477b-0829-426a-b7c2-dfc624ab42fb)

type following commands
 ```read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog pes_ser.v
 synth -top vsdserilaizer_v1
```
![abc](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/19be6e40-00d4-4c69-9df8-03efba542132)


**to view the netlist 
use following commands**
To make the given netlist code even more simpler and small give the following commands:

```
write_verilog -noattr pes_ser.v
pes_ser.v
```
![peser](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/b8ebaa88-86da-4222-8d65-d10f25c07277)
**GLS(Gate Level Simulation)**

Gate-level simulation is a technique used in digital design and verification to validate the functionality of a digital circuit at the gate-level implementation.
It involves simulating the circuit using the actual logic gates and flip-flops that make up the design, as opposed to higher-level abstractions like RTL (Register Transfer Level) descriptions.
This type of simulation is typically performed after the logic synthesis process, where a high-level description of the design is transformed into a netlist of gates and flip-flops.
We perform this to verify logical correctness of the design after synthesizing it. Also ensuring the timing of the design is met.
To use the iVerilog, we give the following commands as shown below:
![pre](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/e72b7506-0e65-470a-8923-7036fdc2a6e7)
![vsdser](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/a1956aad-45d2-445f-8137-db33683b1b53)






 
