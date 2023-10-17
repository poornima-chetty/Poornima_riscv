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
