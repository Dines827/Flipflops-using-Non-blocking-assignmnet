# EXPERIMENT 3B: Simulation of All Flip-Flops using Non Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **Non blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **Non blocking assignment (`<=`)** inside the `always` block.  
Non Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Non Blocking)
```verilog
`timescale 1ns / 1ps
module SR_FF(S,R,clk,rst,Q);
 input  S,R,clk,rst;
 output reg Q;
 always @(posedge clk) 
begin
 if (rst==1)
 Q <= 0;  
else if(S==0 && R==0)
 Q <= Q;
 else if(S==0 && R==1)
 Q <= 1'b0;
 else if(S==0 && R==0)
 Q <= 1'b1;
 else
 Q <= 1'bx;
 end
 endmodule
 
```
### SR Flip-Flop Test bench 
```verilog
module SR_FF_tb;
 reg s,r,clk,rst;
 wire q;
 SR_FF uut(s,r,clk,rst,q);
 always #5clk=~clk;
 initial 
begin
 clk=0;s=0;r=0;rst=1;
 #10 rst=0;
 #10 s=1;r=0;
 #10 s=0;r=0;
 #10 s=0;r=1;
 #10 s=1;r=1;
 #10 s=0;r=0;
 #20;
 $finish;
 end
 endmodule
```
#### SIMULATION OUTPUT

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/9643d8c3-29d1-4f8e-ad36-d9923346a56a" />


### JK Flip-Flop (Non Blocking)
```verilog
`timescale 1ns / 1ps
 module JK_ff (J,K,clk,rst,Q);
 input  J,K,clk,rst;
 output reg Q;
 always @(posedge clk) 
begin
 if (rst==1)
 Q <= 0;  
else if(J==0 && K==0)
 Q <= Q;
 else if(J==0 && K==1)
 Q <= 1'b0;
 else if(J==0 && K==0)
 Q <= 1'b1;
 else
 Q <= 1'bx;
 end
 endmodule
```
### JK Flip-Flop Test bench 
```verilog
module JK_tb;
 reg j,k,clk,rst;
 wire q;
 JK_ff uut(j,k,clk,rst,q);
 always #5clk=~clk;
 initial 
begin
 clk=0;j=0;k=0;rst=1;
 #10 rst=0;
 #10 j=1;k=0;
 #10 j=0;k=0;
 #10 j=0;k=1;
 #10 j=1;k=1;
 #10 j=0;k=0;
 #20;
 $finish;
 end
 endmodule

```
#### SIMULATION OUTPUT

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/fab6a989-f2f5-4fad-bd36-91a2d02fffae" />

### D Flip-Flop (Non Blocking)
```verilog
`timescale 1ns / 1ps
 module DFF(clk,rst,D,Q);
 input clk,rst,D;
 output reg Q;
 always @ (posedge clk)
 begin
 if (rst==1)
 Q<=0;
 else
 Q<=D;
 end
 endmodule
```
### D Flip-Flop Test bench 
```verilog
module DFF_tb;
 reg clk,rst,D;
 wire Q;
 DFF uut(clk,rst,D,Q);
 always #5 clk=~clk;
 initial
 begin
 clk=0;
 D=0;
 rst=1;#10;
 rst=0;
 D=0; #10;
 D=1;
 end
 endmodule
```

#### SIMULATION OUTPUT

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/0d05c7c6-563a-4d89-9db2-95dfca5fb82f" />

### T Flip-Flop (Non Blocking)
```verilog
`timescale 1ns / 1ps
 module TFF(clk,rst,T,Q);
 input clk,rst,T;
 output reg Q;
 always @ (posedge clk)
 begin
 if (rst==1)
 Q<=0;
 else
 Q<=T;
 end
 endmodule
```
### T Flip-Flop Test bench 
```verilog
module tb_TFF;
 reg clk,rst,T;
 wire Q;
 TFF uut(clk,rst,T,Q);
 always #5 clk=~clk;
 initial
 begin
 clk=0;
 T=0;
 rst=1;#10;
 rst=0;
 T=0; #10;
 T=1;
 end
 endmodule
```

#### SIMULATION OUTPUT
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/d8303388-3645-4ba5-9dea-de2585f1c3c7" />


### RESULT
All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL. The outputs matched the expected truth table values, demonstrating correct sequential behavior.

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
