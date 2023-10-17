**LOGIC GATES**
 A logic gate is a device that acts as a building block for digital circuits.
 ![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/c343bc34-7cf0-4642-8f2a-ca721902df29)
 
**boolean operators**
 ![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/095e7826-b2a2-4493-914a-c5524bc82154)

 **combinational circuit**
 Combinational circuits are made up of logic gates. The output of each logic gate is determined by its logic function.
 ![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/e1381d52-b006-4bf0-8d79-ffd3057967e7)

 **makerchip**

**pythogorean example**
![pyyy](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/802f162d-b9d1-4a96-bbbd-d94d6403f296)



**inverter**
![inverter1](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/ab9ac5e6-fa1e-4ad0-814a-4afdcd518a39)


**and gate**
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/727724ac-5573-4275-be9e-1f43aba4aa7c)

**vectors**

![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/63205ccc-fa16-4a8c-9945-24206728e9a6)

**mux**
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/64806b51-9fe7-49ab-924a-d377addcbc43)

![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/2f302444-4c52-44b4-8ac5-b5cffc0a1daf)

**SEQUENTIAL LOGIC**
sequential Logic is sequenced by a clock signal
D-flipflop
Q Output: This is the main output of the flip-flop and represents the state of the D input at the last clock edge. It reflects the data stored in the flip-flop.
Q' (Q-bar) Output: This is the complement of the Q output. If Q is 1, then Q' is 0, and vice versa.
The D flip-flop also has a Reset input that can be used to reset the flip-flop to a specific state.

**Fibonacci Series**
1,1,2,3,5,8,13,....

$val[15:0] = $reset ? 1 : >>1$val + >>2$val 
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/a9a2695c-1dbc-4b41-83e2-1c04f23e5827)
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/b6ce3c06-655f-4f42-aa52-378537d01a11)

**Free running counter
**


![VV](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/6835cb85-2752-4b6f-834b-896106c47888)


**PIPELINING**
**Pipelined pythagoras's theorem**


 logic to calculate the length c below, given a and b, using Pythagora’s Theorem.


c = sqrt(a2 + b2)
 Pythagoras’s Theorem
 ![PY](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/7637d9f8-0121-4d27-bb79-4fe0bfd3f135)

 
 
This logic can be implemented in a circuit as:


Pythagorean Theorem Logic

L
@1
      $aa_sq[31:0] = $aa * $aa;
      $bb_sq[31:0] = $bb * $bb;
   @2
      $cc_sq[31:0] = $aa_sq + $bb_sq;
   @3
      $cc[31:0] = sqrt($cc_sq);



![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/d1030fd1-072b-46ba-80ea-2a82813a0ea3)

```
  |calc
      
      @0
         $aa_sq[7:0] = $aa[3:0] ** 2;
         $bb_sq[7:0] = $bb[3:0] ** 2;
      @2
         $cc_sq[8:0] = $aa_sq + $bb_sq;
      @4
         $cc[4:0] = sqrt($cc_sq);
        
```
**PIPELINED CALCULATOR**
        

**VALIDITY**
     Validity makes the code easier to debug, with cleaner design, better error checking and automated clock gating.

Clock gating is a power saving feature as it avoids toggling clock signals.

**Distance calculator**
```
|calc
      @1
         $reset = *reset;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] ** 2;
            $bb_sq[31:0] = $bb[3:0] ** 2;
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
      @4
         $tot_dist[63:0] = 
                   $reset ? '0 :
                   $valid ? >>1$tot_dist + $cc :
                            >>1$tot_dist;
```

                                               
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/bdff2d47-48ed-4fbc-8321-a9203f0711ed)

**2-Cycle Calculator with Validity**
calc
      @0
         $reset = *reset;
      @1
         $valid = $reset ? 1'b0 : >>1$valid + 1'b1;
         $val2[31:0] = $rand2[3:0];
         $val1[31:0] = >>2$out;
         $reset_or_valid = $valid || $reset;
      ?$reset_or_valid
         @1
            $sum[31:0] = $val1[31:0] + $val2[31:0];
            $diff[31:0] = $val1[31:0] - $val2[31:0];
            $prod[31:0] = $val1[31:0] * $val2[31:0];
            $quot[31:0] = $val1[31:0] / $val2[31:0];
         @2 
            $out[31:0] = $reset ? 32'b0 : 
                        ($op[1:0] == 2'b00) ? $sum :
                        ($op[1:0] == 2'b01) ? $diff :
                        ($op[1:0] == 2'b10) ? $prod : $quot;

![ver](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/8c1ebda9-deed-47a4-9f1e-46f2ee850dd4)
**Calculator with Single-Value Memory**

   ```|calc
      @0
         $reset = *reset;
      @1
         $valid = $reset ? 1'b0 : >>1$valid + 1'b1;
         $val2[31:0] = $rand2[3:0];
         $val1[31:0] = >>2$out;
         $reset_or_valid = $valid || $reset;
      ?$reset_or_valid
         @1
            $sum[31:0] = $val1[31:0] + $val2[31:0];
            $diff[31:0] = $val1[31:0] - $val2[31:0];
            $prod[31:0] = $val1[31:0] * $val2[31:0];
            $quot[31:0] = $val1[31:0] / $val2[31:0];
         @2 
            $mem[31:0] = $reset ? 32'b0 : 
                         ($op[2:0] == 3'b101) ? $val1 :
                                              >>2$mem;
            $out[31:0] = $reset ? 32'b0 : 
                        ($op[2:0] == 3'b000) ? $sum :
                        ($op[2:0] == 3'b001) ? $diff :
                        ($op[2:0] == 3'b010) ? $prod : 
                        ($op[2:0] == 3'b011) ? $quot : 
                        ($op[2:0] == 3'b100) ? >>2$mem : >>2$out;
```

![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/818afd66-b3ee-49ff-b547-0775e33b5971)

**Basic RISC-V CPU Microarchitecture**


**Introduction to simple RISC-V micro-architectureI**
1.Fetch and Decode
2.RISC-V Control Logic
**Introduction to simple RISC-V micro-architecture**
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/f258610b-3c9b-4c4a-a5bc-1fcb6b849d90)
A single-cycle RISC-V CPU is a simplified implementation of a RISC-V (Reduced Instruction Set Computing) processor where each instruction is executed in a single clock cycle.
**Instruction Fetch (IF)**: In the first stage, the CPU fetches the instruction from memory using the program counter (PC) and increments the PC to point to the next instruction. The instruction is loaded into the instruction register (IR).

**Instruction Decode (ID)**: During this stage, the CPU decodes the instruction in the IR. It identifies the operation to be performed, the source registers, and the destination register. It also performs register file reads.

**Execute (EX)**: In this stage, the actual execution of the instruction occurs. For ALU (Arithmetic Logic Unit) operations, this is where the ALU performs the calculations. For memory operations, such as loads and stores, the memory access is performed.

**Memory Access (MEM):** In this stage, the CPU interacts with memory. If the instruction is a load or store, data is read from or written to memory. If the instruction does not involve memory access, this stage becomes a pass-through stage.

**Write-Back (WB):** The final stage is where the results of the instruction are written back to the register file. The result of an ALU operation or data loaded from memory is written to the destination register.

**FETCH AND DECODE**
Implementation Plan
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/6d1f7934-3daf-47b3-8d7a-a81a5387c72a)

LABS
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/1f89c4a3-daea-4e64-9fd1-ad62abfe13ce)



**fetch logic **
code**
  ```|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required


```

![Screenshot from 2023-10-17 21-10-35](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/d217f52f-7622-4453-b720-d4f8349532c8)
![OO](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/d7828685-67d1-49e7-b545-c16c8e7c009b)
Lab for Instruction Decode
```|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1[4:0] = $instr[19:15];
         $rs2[4:0] = $instr[24:20];
         $rd[4:0] = $instr[11:7];
         $opcode[6:0] = $instr[6:0];
         $funct7[6:0] = $instr[31:25];
         $funct3[2:0] = $instr[14:12];
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required


```
![PPP](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/de29c5dd-fba8-4720-bf69-6b21dd31bbd2)
Lab to Decode Individual Instruction

```|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];         
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
```
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/4026d2a2-f971-4749-bf09-ce75da34041b)
**RISC-V Control Logic**
Lab for Register File
```|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = 1'b0;
         $rf_wr_index[4:0] = 5'b0;
         $rf_wr_data[31:0] = 32'b0;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/b37c4239-6672-400e-971f-62c7ab3e1262)

Lab for ALU Operations (add/addi)
```|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = 1'b0;
         $rf_wr_index[4:0] = 5'b0;
         $rf_wr_data[31:0] = 32'b0;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation

```
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/857a81a0-f731-40ad-aeb6-e6a3d434491f)

**Lab for Register File Write**
```|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = $rd_valid && $rd != 5'b0;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation

```
![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/cdf215e7-f0d1-4f41-9a20-b6736cbe748e)

**Lab for Branch Instructions**
```|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>1$taken_br ? >>1$br_tgt_pc :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = $rd_valid && $rd != 5'b0;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $br_tgt_pc[31:0] = $pc + $imm;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation

```

![image](https://github.com/poornima-chetty/Poornima_riscv/assets/142583396/9c3bf4c6-ef22-465c-9be0-7fe09f4b38c8)

