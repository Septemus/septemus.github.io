---
title: "西南交通大学计组实验-课程设计"
date: 2023-06-16T15:22:02+08:00
draft: false
categories: ["college"]
featuredImagePreview: "/images/intel-fpga.png"
featuredImage: "/images/intel-fpga.png"
---


> # 1 实验内容

1. 底层用 Verilog HDL 语言实现简单的处理器模块设计。
2. 调用存储器模块设计 64×8 的存储器模块。
3. 顶层用原理图方式将简单的处理器模块和存储器模块连接形成简单的计算机核心
部件组成的系统。
4. 将指令序列存入存储器，然后分析指令执行流程


> # 2 代码/原理图


{{< admonition type=warning title="" open=false >}}
由于本次使用modelsim-altera仿真，仿真时顶层不能用原理图，必须要转换为Verilog文件。
{{< /admonition >}}

> ## 2.1 顶层文件

> ### 2.1.1 设计用原理图

<img src="/images/block9.png" width="80%">

> ### 2.1.2 仿真用Verilog代码

```Verilog
// Copyright (C) 1991-2013 Altera Corporation
// Your use of Altera Corporation's design tools, logic functions 
// and other software and tools, and its AMPP partner logic 
// functions, and any output files from any of the foregoing 
// (including device programming or simulation files), and any 
// associated documentation or information are expressly subject 
// to the terms and conditions of the Altera Program License 
// Subscription Agreement, Altera MegaCore Function License 
// Agreement, or other applicable license agreement, including, 
// without limitation, that your use is for the sole purpose of 
// programming logic devices manufactured by Altera and sold by 
// Altera or its authorized distributors.  Please refer to the 
// applicable agreement for further details.

// PROGRAM		"Quartus II 64-Bit"
// VERSION		"Version 13.1.0 Build 162 10/23/2013 SJ Full Version"
// CREATED		"Fri Jun 09 00:49:29 2023"

module computer(
	reset,
	clk,
	Write_read,
	overflow,
	M_addr,
	M_data_out,
	M_q,
	PC,
	R0,
	R1,
	R2,
	R3,
	state
);


input wire	reset;
input wire	clk;
output wire	Write_read;
output wire	overflow;
output wire	[11:0] M_addr;
output wire	[7:0] M_data_out;
output wire	[7:0] M_q;
output wire	[7:0] PC;
output wire	[7:0] R0;
output wire	[7:0] R1;
output wire	[7:0] R2;
output wire	[7:0] R3;
output wire	[2:0] state;

wire	[11:0] M_addr_ALTERA_SYNTHESIZED;
wire	[7:0] M_data_in;
wire	[7:0] M_data_out_ALTERA_SYNTHESIZED;
wire	we;





cpu	b2v_inst2(
	.clk(clk),
	.reset(reset),
	.M_data_in(M_data_in),
	.Write_read(we),
	.overflow(overflow),
	.M_addr(M_addr_ALTERA_SYNTHESIZED),
	.M_data_out(M_data_out_ALTERA_SYNTHESIZED),
	.PC(PC),
	.R0(R0),
	.R1(R1),
	.R2(R2),
	.R3(R3),
	.state(state));
	defparam	b2v_inst2.Add = 4'b0011;
	defparam	b2v_inst2.And = 4'b0101;
	defparam	b2v_inst2.Idle = 4'b0000;
	defparam	b2v_inst2.Jmp = 4'b1011;
	defparam	b2v_inst2.Jz = 4'b1100;
	defparam	b2v_inst2.Load = 4'b0001;
	defparam	b2v_inst2.Move = 4'b0010;
	defparam	b2v_inst2.Or = 4'b0110;
	defparam	b2v_inst2.Read = 4'b1101;
	defparam	b2v_inst2.Shl = 4'b1001;
	defparam	b2v_inst2.Shr = 4'b1000;
	defparam	b2v_inst2.st_0 = 3'b000;
	defparam	b2v_inst2.st_1 = 3'b001;
	defparam	b2v_inst2.st_2 = 3'b010;
	defparam	b2v_inst2.st_3 = 3'b011;
	defparam	b2v_inst2.st_4 = 3'b100;
	defparam	b2v_inst2.Stop = 4'b1111;
	defparam	b2v_inst2.Sub = 4'b0100;
	defparam	b2v_inst2.Swap = 4'b1010;
	defparam	b2v_inst2.Write = 4'b1110;
	defparam	b2v_inst2.Xor = 4'b0111;


mif2	b2v_inst3(
	.clock(clk),
	.wren(we),
	.address(M_addr_ALTERA_SYNTHESIZED[5:0]),
	.data(M_data_out_ALTERA_SYNTHESIZED),
	.q(M_data_in));

assign	Write_read = we;
assign	M_addr = M_addr_ALTERA_SYNTHESIZED;
assign	M_data_out = M_data_out_ALTERA_SYNTHESIZED;
assign	M_q = M_data_in;

endmodule

```

> ## 2.2 RAM初始化内容（mif2.mem）

| addr | +0 | +1 | +2 | +3 | +4 | +5 | +6 | +7 |
|------|----|----|----|----|----|----|----|----|
| 0    | 00 | 15 | 24 | D0 | 1F | 94 | 31 | E0 |
| 8    | 1E | 41 | A1 | 61 | 84 | 51 | 28 | 2D |
| 16   | 7B | D0 | 1E | C0 | 19 | D0 | 1D | B0 |
| 24   | 13 | F0 | 00 | 00 | 00 | 00 | 00 | 39 |
| 32   | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 40   | 00 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |

> ## 2.3 cpu模块

```Verilog
module cpu(
	clk,
	reset,
	M_data_in,
	Write_read,
	M_addr,
	M_data_out,
	overflow,
	R0,R1,R2,R3,PC,state
);


	//wire [15:0]IR;
	//wire [7:0] A,R0,R1,R2,R3,PC,RX,RY;
	//choose_rx_ry crr(clk,IR,R0,R1,R2,R3,RX,RY);
	//status_machine sm(M_data_in,clk,reset,Write_read,M_addr,M_data_out);
	//assign M_addr=MAR;
	//assign M_data_out=MDR;
parameter Idle =4'b0000;
parameter Load =4'b0001;
parameter Move =4'b0010;
parameter Add  =4'b0011;
parameter Sub  =4'b0100;
parameter And  =4'b0101;
parameter Or   =4'b0110;
parameter Xor  =4'b0111;
parameter Shr  =4'b1000;
parameter Shl  =4'b1001;
parameter Swap =4'b1010;
parameter Jmp  =4'b1011;
parameter Jz   =4'b1100;
parameter Read =4'b1101;
parameter Write=4'b1110;
parameter Stop =4'b1111;
parameter st_0 = 3'b000;
parameter st_1 = 3'b001;
parameter st_2 = 3'b010;
parameter st_3 = 3'b011;
parameter st_4 = 3'b100;
input clk,reset;
input [7:0] M_data_in;
output reg [7:0] R0=8'h00,R1=8'h00,R2=8'h00,R3=8'h00,PC=8'h00;
output reg overflow;
reg [7:0]A=8'h00,RX,RY;
//reg [7:0] MDR;
reg [15:0] IR=8'h00;
//reg[11:0] MAR;
output reg Write_read;
output reg[11:0]M_addr=12'h000;
output reg[7:0]M_data_out=8'h00;
output reg [2:0] state=st_0;
wire [3:0]OP;
reg [2:0] step_counter=3'b000;
reg flag1=1'b1;
assign OP=IR[15:12];
always@(posedge clk or negedge reset)
	begin
		if(!reset)
		begin
			R0<=0;
			R1<=0;
			R2<=0;
			R3<=0;
			RX<=0;
			RY<=0;
			PC<=0;
			M_addr<=0;
			M_data_out<=0;
			A<=0;
			state<=st_0;
			flag1<=1'b1;
		end
		
		else if(clk)
		begin
		//按照步长划分状态，而每个状态又有子状态
		//步长为0时执行取指令操作
			if(step_counter==3'b000)
			begin
					IR<={M_data_in,8'h00};
					Write_read<=0;
					PC<=PC+1;
					flag1<=1'b1;
					step_counter<=step_counter+1;
			end
		//步长为2时执行取操作数和运算
			else if(step_counter==3'b001)
			begin
			case(state)
				//根据寄存器选择RX，RY
				st_0:
				begin
					if(flag1)
					begin
						case(IR[11:10])
						2'b00:begin
							RX<=R0;
						end
						2'b01:begin
							RX<=R1;
						end
						2'b10:begin
							RX<=R2;
						end
						2'b11:begin
							RX<=R3;
						end
					endcase
					case(IR[9:8])
						2'b00:begin
							RY<=R0;
						end
						2'b01:begin
							RY<=R1;
						end
						2'b10:begin
							RY<=R2;
						end
						2'b11:begin
							RY<=R3;
						end
					endcase	
					flag1<=0;
					end
					else 
					begin
						A<=RY;
						M_addr<=PC;
						state<=st_1;
						flag1<=1;
					end
				end
				
				//以下内容参照实验参考书的表3
				st_1:
				
				begin

					if(flag1)
					begin
						Write_read<=0;
						case(OP)
							Load: R0<={4'h0,IR[11:8]};
							Move: RX<=A;
							Shr:	RX<={1'b0,RX[7:1]};
							Shl:  RX<={RX[6:0],1'b0};
							Add:	RX<=RX+A;
							Sub:	RX<=RX-A;
							And:	RX<=RX&A;
							Or:	RX<=RX|A;
							Xor:	RX<=RX^A;
							Swap:	RY<=RX;
						endcase
						flag1<=0;
					end
					else 
					begin
						if(OP==Stop)
						begin
							state<=st_1;
						end
						else if(OP==Swap||OP==Jmp||OP==Jz||OP==Read||OP==Write)
						begin
							state<=st_2;
						end
						else begin
							if(OP==Load) step_counter<=0;
							else step_counter<=step_counter+1;
							state<=st_0;
						end
						flag1<=1;
					end
					
				end
				
				
				
				
				st_2:
				begin
					if(flag1)
					begin
						Write_read<=0;
						
						case(OP)
							Swap:RX<=A;
							Jmp:
							begin
								IR[7:0]<=M_data_in;
							end
							Read:
							begin
								IR[7:0]<=M_data_in;
							end
							Write:
							begin
								IR[7:0]<=M_data_in;
							end
							Jz:
							begin
								if(R0==0)
								begin
									IR[7:0]<=M_data_in;
								end
							end
						endcase
						flag1<=0;
						if(OP!=Swap) PC<=PC+1;
					end
					else 
					begin
						M_data_out<=R0;
						if(OP==Swap) begin
							state<=st_0;
							step_counter<=step_counter+1;
							
						end
						else begin
							if(OP==Jmp||OP==Read||OP==Write) M_addr<=IR[11:0];
							else if(OP==Jz && R0==0) M_addr<=IR[11:0];
							else M_addr<=PC;
							state<=st_3;
							
						end
						flag1<=1;
					end
				end
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
				st_3:
				begin
					if(flag1)
					begin
						if(OP==Jmp) PC<=IR[11:0];
						else if(OP==Jz&&R0==0) PC<=IR[11:0];
						else if(OP==Read) Write_read<=0;
						else if(OP==Write) Write_read<=1;
						flag1<=0;
					end
					else 
					begin
						if(OP==Read||OP==Write) M_addr<=PC;
						if(OP==Jmp||OP==Jz) begin
							state<=st_0;
							step_counter<=step_counter+1;
						end
						else state<=st_4;
						Write_read<=0;
						flag1<=1;
					end
					
				end
				
				
				st_4:
				begin
					if(flag1)
					begin
						if(OP==Read) R0<=M_data_in;
						flag1<=0;
					end
					else 
					begin
						Write_read<=0;
						state<=st_0;
						if(OP==Read) step_counter<=3'b000;
						else step_counter<=step_counter+1;
						flag1<=1;
					end
				end
				
			endcase
			end
			//将RX,RY的值赋值回通用寄存器
			else if(step_counter==3'b010)
			begin
				case(IR[11:10])
						2'b00:begin
							R0<=RX;
						end
						2'b01:begin
							R1<=RX;
						end
						2'b10:begin
							R2<=RX;
						end
						2'b11:begin
							R3<=RX;
						end
					endcase
					case(IR[9:8])
						2'b00:begin
							R0<=RY;
						end
						2'b01:begin
							R1<=RY;
						end
						2'b10:begin
							R2<=RY;
						end
						2'b11:begin
							R3<=RY;
						end
					endcase
					step_counter<=3'b000;
			end
		end
	end
endmodule

```

> # 3 仿真波形

<img src="/images/wvf9_1.png" width="80%">

<img src="/images/wvf9_2.png" width="80%">

> # 4 源码已上传github


github仓库：
{{< person url="https://github.com/Septemus/swjtu_computer_organization_course_design.git" name="swjtu_computer_organization_course_design" text="github库" picture="/images/github.jpg" >}}