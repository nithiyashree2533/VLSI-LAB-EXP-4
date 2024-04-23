# VLSI-LAB-EXP-4
SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS



AIM: 



 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.



APPARATUS REQUIRED:



Xilinx 14.7
Spartan6 FPGA



**LOGIC DIAGRAM**



SR FLIPFLOP



![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)



Verilog Code:



```
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
```



output:



![srff](https://github.com/nithiyashree2533/VLSI-LAB-EXP-4/assets/161813688/542d669a-3a5f-4a3f-a952-5cc6c6f1565a)



logic diagram



JK FLIPFLOP



![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)



Verilog Code:



```
module jkff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({j,k})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=~q;
endcase
end
end
endmodule
```



output:



![jkff](https://github.com/nithiyashree2533/VLSI-LAB-EXP-4/assets/161813688/e76e95b7-95a5-46a8-bbb9-57c28184e22b)



logic diagram



T FLIPFLOP



![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)



verilog code:



```
module tff(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
```



output:



![tff](https://github.com/nithiyashree2533/VLSI-LAB-EXP-4/assets/161813688/04f65b8b-38ed-4927-9a39-35b74a12b2a7)



D FLIPFLOP



![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)



verilog code:



```
module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
```



output:



![dff](https://github.com/nithiyashree2533/VLSI-LAB-EXP-4/assets/161813688/5d2e84e0-5e18-4b36-b055-24b64d539e6f)



COUNTER



![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)

Updown Counter:



Logic Diagram:



![image](https://github.com/nithiyashree2533/VLSI-LAB-EXP-4/assets/161813688/c09d0ebd-f66e-49b7-adf5-e9d3008cc541)




Verilog Code:


```
module udc(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```


output:


![udc](https://github.com/nithiyashree2533/VLSI-LAB-EXP-4/assets/161813688/cc4c3051-e1b7-48ec-8a14-030e5dd278eb)


Mod-10 Counter:



Logic Diagram:


![image](https://github.com/nithiyashree2533/VLSI-LAB-EXP-4/assets/161813688/2db8ef96-2f77-4665-8898-b93e4f0ed921)


verilogcode
```


module mod10(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
```



output:



![mtc](https://github.com/nithiyashree2533/VLSI-LAB-EXP-4/assets/161813688/54015a4c-0697-4f4e-904e-8e7efe52d0bd)



Ripple Carry Counter:



Logic Diagram:



![image](https://github.com/nithiyashree2533/VLSI-LAB-EXP-4/assets/161813688/beb65972-078d-4146-b890-5b4d23d048a8)



![image](https://github.com/nithiyashree2533/VLSI-LAB-EXP-4/assets/161813688/ec5599ef-ef41-4d72-92c6-805d51731246)




Verilog Code:



```
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule

module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule

module rcc(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf1(q[0],clk,rst);
tff tf2(q[1],q[0],rst);
tff tf3(q[2],q[1],rst);
tff tf4(q[3],q[2],rst);
endmodule
```


output:



![Rca](https://github.com/nithiyashree2533/VLSI-LAB-EXP-4/assets/161813688/fb66fd29-dca1-4694-b195-fd0130ac790a)



PROCEDURE:



STEP:1  Start  the Xilinx navigator, Select and Name the New project.



STEP:2  Select the device family, device, package and speed. 



STEP:3  Select new source in the New Project and select Verilog Module as the Source type. 



STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.



STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax. 



STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.   



STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.



STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained.



STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.



STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.



STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.


 

RESULT



Hence SR, JK, T, D - FLIPFLOP, COUNTER DESIGN are simulated and synthesised using Xilinx ISE.


