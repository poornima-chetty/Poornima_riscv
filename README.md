**Design and Implementation of a 10-bit Serializer(vsdserializer_v1) in RTL2GDS flow using SKY130 pdks**



The purpose of this project is to produce clean GDS (Graphic Design System) Final Layout with all details that is used to print photomasks used in fabrication of a behavioral RTL (Register-Transfer Level) of a 10-bit Serializer, using SkyWater 130 nm PDK (Process Design Kit)*

**About The Project**
OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhySyn, SPEF-Extractor and custom methodology scripts for design exploration and optimization. It is a tool started for true open source tape-out experience and comes with APACHE version 2.0. The goal of OpenLANE is to produce clean GDSII without any human intervention. OpenLANE is tuned for Skywater 130nm open-source PDK and can be used to produce hard macros and chips
*Pin Configuration*
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/65b9c532-afca-40da-b218-1846dbfb7ff4)

![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/a705832f-bc58-4120-afce-6515213727c0)


**RTL to GDSII Introduction**
From conception to product, the ASIC design flow is an iterative process that is not static for every design. The details of the flow may change depending on ECO’s, IP requirements, DFT insertion, and SDC constraints, however the base concepts still remain. The flow can be broken down into 11 steps:

Architectural Design – A system engineer will provide the VLSI engineer with specifications for the system that are determined through physical constraints. The VLSI engineer will be required to design a circuit that meets these constraints at a microarchitecture modeling level.

RTL Design/Behavioral Modeling – RTL design and behavioral modeling are performed with a hardware description language (HDL). EDA tools will use the HDL to perform mapping of higher-level components to the transistor level needed for physical implementation. HDL modeling is normally performed using either Verilog or VHDL. One of two design methods may be employed while creating the HDL of a microarchitecture:

a. RTL Design – Stands for Register Transfer Level. It provides an abstraction of the digital circuit using:

i. Combinational logic
ii. Registers
iii. Modules (IP’s or Soft Macros)
b. Behavioral Modeling – Allows the microarchitecture modeling to be performed with behavior-based modeling in HDL. This method bridges the gap between C and HDL allowing HDL design to be performed

RTL Verification - Behavioral verification of design

DFT Insertion - Design-for-Test Circuit Insertion

Logic Synthesis – Logic synthesis uses the RTL netlist to perform HDL technology mapping. The synthesis process is normally performed in two major steps:

GTECH Mapping – Consists of mapping the HDL netlist to generic gates what are used to perform logical optimization based on AIGERs and other topologies created from the generic mapped netlist.

Technology Mapping – Consists of mapping the post-optimized GTECH netlist to standard cells described in the PDK

Standard Cells – Standard cells are fixed height and a multiple of unit size width. This width is an integer multiple of the SITE size or the PR boundary. Each standard cell comes with SPICE, HDL, liberty, layout (detailed and abstract) files used by different tools at different stages in the RTL2GDS flow.

Post-Synthesis STA Analysis: Performs setup analysis on different path groups.

Floorplanning – Goal is to plan the silicon area and create a robust power distribution network (PDN) to power each of the individual components of the synthesized netlist. In addition, macro placement and blockages must be defined before placement occurs to ensure a legalized GDS file. In power planning we create the ring which is connected to the pads which brings power around the edges of the chip. We also include power straps to bring power to the middle of the chip using higher metal layers which reduces IR drop and electro-migration problem.

Placement – Place the standard cells on the floorplane rows, aligned with sites defined in the technology lef file. Placement is done in two steps: Global and Detailed. In Global placement tries to find optimal position for all cells but they may be overlapping and not aligned to rows, detailed placement takes the global placement and legalizes all of the placements trying to adhere to what the global placement wants.

CTS – Clock tree synteshsis is used to create the clock distribution network that is used to deliver the clock to all sequential elements. The main goal is to create a network with minimal skew across the chip. H-trees are a common network topology that is used to achieve this goal.

Routing – Implements the interconnect system between standard cells using the remaining available metal layers after CTS and PDN generation. The routing is performed on routing grids to ensure minimal DRC errors.

The Skywater 130nm PDK uses 6 metal layers to perform CTS, PDN generation, and interconnect routing. Shown below is an example of a base RTL to GDS flow in ASIC design:
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/168bdcf8-a356-4f31-8b7a-1e8db5259446)


**what is serializer**


Serialization is the process of converting a data object—a combination of code and data represented within a region of data storage—into a series of bytes that saves the state of the object in an easily transmittable form. In this serialized form, the data can be delivered to another data store (such as an in-memory computing platform), application, or some other destination.
A serializer circuit converts parallel data—in other words, multiple streams of data—into a serial (one bit) stream of data that is transmitted over a high-speed connection, such as LVDS, to a receiver that converts the serial stream back to the original, parallel data. A clock system puts parallel into a serial by taking bits from the multiple streams and alternating them on up and down parts of the signals.
![serialiser](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/e1d3eaee-48a7-43f0-a72e-e4f455addc76)


Here's how a serializer typically works:

**Input Data**: The serializer takes structured data as input. This data can be in the form of complex data structures, objects, or even simple data types like numbers and strings.

**Serialization Process**:

**Data Traversal**: The serializer starts by traversing the input data. It follows a specific algorithm to access each part of the data.
**Data Conversio**n: As it traverses the data, the serializer converts each piece of information into a format that can be represented linearly or in binary form. This may involve mapping complex data structures into a sequence of bytes, for example.
**Encoding Rules**: The serializer often follows encoding rules or schemas to ensure that the serialized data can be correctly reconstructed by a deserializer. These encoding rules may include data type information, length indicators, and other metadata.
**Output**: The serialized data is the output of the serializer. This output can be in the form of a binary stream, text representation (e.g., JSON or XML), or any other format suitable for the intended purpose.

**Storage or Transmission**: The serialized data can be stored in a file, transmitted over a network, or used in any other way that requires the data to be in a linear or binary format.

**Deserialization**: To use the serialized data, a deserializer is required. The deserializer performs the reverse process, converting the serialized data back into its original structured form.





**RTL synthesis and GLS simulation:**

Tools used


**iVerilog**:Icarus Verilog is a valuable tool for digital design, enabling engineers and designers to develop, test, and verify complex digital circuits and systems in a software simulation environment before committing to hardware implementation.

**GTKwave** - GTKWave is a free and open-source waveform viewer. It's used primarily in digital design and verification to display simulation results generated by digital simulation tools like Icarus Verilog (which includes IVERILOG).


** Yosys ** - Yosys is an open-source framework for Verilog RTL synthesis. It's widely used in digital design for converting high-level descriptions of a digital circuit into a gate-level representation. In other words, it helps in transforming a behavioral description (written in a language like Verilog) into a netlist, which is a detailed representation of the digital logic in terms of gates and their interconnections.

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
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/bffdaef6-daef-4d13-919b-1599adf4ef6f)

**RTL synthesis**

Go to verilog_files directory and type yosys
![yosys](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/a7ef477b-0829-426a-b7c2-dfc624ab42fb)

type following commands
 ```read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog pes_ser.v
 synth -top vsdserilaizer_v1
```
![abc](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/19be6e40-00d4-4c69-9df8-03efba542132)

synthesis

![dot](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/67fff066-cd76-4f7a-b33c-cd0ffc03c97e)


**to view the netlist 
use following commands**
To make the given netlist code even more simpler and small give the following commands:

```
write_verilog -noattr pes_ser.v
!gvim pes_ser.v
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


***Installation of ngspice magic and OpenLANE***
**ngspice***
Download the tarball from https://sourceforge.net/projects/ngspice/files/ to a local directory

```
cd $HOME
sudo apt-get install libxaw7-dev
tar -zxvf ngspice-41.tar.gz
cd ngspice-41
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
sudo make
sudo make install

```

**magic**
```
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
sudo make
sudo make install
```
***OpenLANE***
```
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git

sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot 
# After reboot
docker run hello-world (should show you the output under 'Example Output' in https://hub.docker.com/_/hello-world)

- To install the PDKs and Tools
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```

 **OpenLANE Flow**
 
 ![yyy](https://github.com/poornima-chetty/pes_ser/assets/142583396/a81badb1-bb07-4e40-a7ee-ac52e67e464b)
 
 First we create a folder under the name of our design in the 'designs' folder.
 cd pes_ser
 
![json](https://github.com/poornima-chetty/pes_ser/assets/142583396/8a95067a-e341-4799-8aea-410c7899bace)

Here we create a config.json file.
We make a new directory called 'src'.
Do cd src


![ln1](https://github.com/poornima-chetty/pes_ser/assets/142583396/bfeea309-ec7c-4711-a508-4f0b4036c1f4)
We add the following files to this directory.
All these files are found above in the 'pes_ser' folder.



![ln2](https://github.com/poornima-chetty/pes_ser/assets/142583396/9380d807-1e66-4332-bfde-81f642d89c62)

Now in the main 'Openlane' directory type mkdir pdks.

Copy paste the above file in it. Found in the verilog_model folder above.

![ln3](https://github.com/poornima-chetty/pes_ser/assets/142583396/8c6271e3-874e-47e4-992a-5f32d6266031)

Type make mount in the main Openlane folder.
Then type ./flow.tcl -interactive.
To prep the design type

```
prep -design pes_ser
```
**synthesis**

![ln4](https://github.com/poornima-chetty/pes_ser/assets/142583396/796da944-4c12-416c-b6bc-80d801279d0b)

Type
```
run_synthesis
```
Physical Cells
![op1](https://github.com/poornima-chetty/pes_ser/assets/142583396/3c6b71f8-0473-4494-bf9e-c5526aa768de)







***floorplan***
![ln5](https://github.com/poornima-chetty/pes_ser/assets/142583396/6e4e4be5-84ef-4ebf-a8b9-2b274a676591)
 
```
run_floorplan
```
To view the design we type
```
magic -T /home/poornima/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def pes_ser.def &

```

![op3](https://github.com/poornima-chetty/pes_ser/assets/142583396/a14b0288-d323-493b-b1f8-143f21aa36f8)
![op4](https://github.com/poornima-chetty/pes_ser/assets/142583396/049c327b-1f94-457e-928e-b4aa5b1b9e3d)

