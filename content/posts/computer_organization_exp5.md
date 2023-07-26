---
title: "西南交通大学计组实验5-CPU寄存器组设计"
date: 2023-05-04T10:44:58+08:00
draft: false
categories: ["college"]
featuredImagePreview: "/images/intel-fpga.png"
featuredImage: "/images/intel-fpga.png"
---

{{< admonition type=note title="" open=false >}}
此笔记针对西南交通大学2023-2024学年上半学期开设的计组实验课。
{{< /admonition >}}

{{< admonition type=success title="" open=false >}}
代码和输出已通过助教验收。
{{< /admonition >}}

{{< admonition type=warning title="Frequency" open=false >}}
使用时必须将clk频率设置成100k
{{< /admonition >}}

> # 1 实验内容

CPU寄存器组设计

> # 2 代码/原理图

> ## 2.1 顶层文件

```Verilog
module exp5(
	input clk,
	input [1:0]RA,
	input wr,
	input rd,
	input [1:0]M,
	input clr,
	input [3:0] KEY_R,
	input key_clr,
	output [3:0] KEY_C = 4'b0111,
	output [7:0] R0,
	output [7:0] R1,
	output [7:0] R2,
	output [7:0] R3,
	output [7:0] PC,
	output [2:0] sel,
	output [31:0] N,
	output [7:0]codeout
);
	wire [7:0] DATA_INPUT;
	wire [7:0] key_out;
	keymodule km(.clk(clk),.KEY_R(KEY_R),.KEY_C(KEY_C),.out(key_out),.clr(key_clr));
	segment_displays sd(.clk(clk),.N(N),.seg(codeout),.sel(sel));
	assign DATA_INPUT=key_out;
	wire [31:0]second_counter;
	wire [7:0] X,Y;
	assign N={X,16'h0000,Y};
	count_second cs(clk,second_counter);
	pc_function pf(clk,clr,second_counter,DATA_INPUT,M,PC,Y);
	reg_function rf(clk,wr,rd,RA,DATA_INPUT,R0,R1,R2,R3,X);
endmodule



```

> ## 2.2 根据键盘获取输入

```Verilog
module keymodule(
	input clk,
	input [3:0] KEY_R,
	output reg[3:0] KEY_C = 4'b0111,
	output reg[7:0] out= 8'hxx,
	input clr
//	output reg[2:0] press_times=3'b000
);
	reg [1:0] cnt = 2'b0;
	reg[4:0] num=5'd16;
	reg[31:0] count_num=32'b1;
//根据按钮的列扫描信号和行输入信号判断按钮是否被按下
always  @(posedge clk)
begin
//		if(S==3'b000)
//		begin
//			out<=16'h0000;
//		end
//		else
		if(clr)
		begin
			out<=16'h0000;
		end
		else
		begin
			cnt = cnt + 1'b1;
			case (cnt)
				2'b00:	KEY_C <= 4'b1110;
				2'b01:	KEY_C <= 4'b1101;
				2'b10:	KEY_C <= 4'b1011;
				2'b11:	KEY_C <= 4'b0111;         
			endcase
			if(KEY_R==4'b1111)
			begin
				num=5'd16;
			end
			else 
			begin 
				  case ({KEY_C, KEY_R})
					 
					 8'b1011_1110: num = 5'd0;
					 8'b0111_0111: num = 5'd1;
					 8'b1011_0111: num = 5'd2;
					 8'b1101_0111: num = 5'd3;
					 
					 8'b0111_1011: num = 5'd4;
					 8'b1011_1011: num = 5'd5;
					 8'b1101_1011: num = 5'd6;
					 8'b0111_1101: num = 5'd7;  
					 
					 8'b1011_1101: num = 5'd8;
					 8'b1101_1101: num = 5'd9;
					 8'b1110_0111: num = 5'd10;
					 8'b1110_1011: num = 5'd11;  
					 
					 8'b1110_1101: num = 5'd12;
					 8'b1110_1110: num = 5'd13;
					 8'b0111_1110: num = 5'd14;
					 8'b1101_1110: num = 5'd15;  
				  endcase
			end
			begin
				if(num == 5'b1_0000)
					begin
						if(count_num == 32'b0)begin
							count_num = 32'd100001;end
						count_num = count_num + 1'b1;
					end
				else if(count_num > 32'd100000)
					begin
						count_num = 32'b1;
					
						//移位
						begin
						out=out<<4;
						out[3:0] = num[3:0];
						end
					end
			end
			end
		
end
endmodule   
```

> ## 2.3 计时器

```Verilog
module count_second(input clk,output reg[31:0] second_counter=32'h0000_0000);
always@(negedge clk)
	begin
		if(second_counter==32'd100000)
		second_counter <= 0;
		else 
		second_counter<=second_counter+1;
	end
endmodule
	
```

> ## 2.4 8位7段数码管

```Verilog
module segment_displays(clk,N,seg,sel);
	input clk;
	input [31:0] N;
	output reg [7:0] seg;
	output reg [2:0] sel;
	reg [3:0]num;
	always@(posedge clk)
	begin
		sel<=sel+1;
		
			case(sel)
				3'b110:num<=N[3:0];
				3'b101:num<=N[7:4];
				3'b100:num<=N[11:8];
				3'b011:num<=N[15:12];
				3'b010:num<=N[19:16];
				3'b001:num<=N[23:20];
				3'b000:num<=N[27:24];
				3'b111:num<=N[31:28];
			endcase
	end
	always@(num)
	begin
		case(num)
			4'b0000:seg<=8'b00111111;	//"0"
			4'b0001:seg<=8'b00000110;	//"1"
			4'b0010:seg<=8'b01011011;	//"2"
			4'b0011:seg<=8'b01001111;	//"3”
			4'b0100:seg<=8'b01100110;	//"4"
			4'b0101:seg<=8'b01101101;	//"5"
			4'b0110:seg<=8'b01111101;	//"6"
			4'b0111:seg<=8'b00000111;	//"8"
			4'b1000:seg<=8'b01111111;	//"8"
			4'b1001:seg<=8'b01101111;	//"9"
			4'b1010:seg<=8'b01110111;	//"A"
			4'b1011:seg<=8'b01111100;	//"b"
			4'b1100:seg<=8'b00111001;	//"c"
			4'b1101:seg<=8'b01011110;	//"d"
			4'b1110:seg<=8'b01111001;	//"E"
			4'b1111:seg<=8'b01110001;	//"F"
			default:seg<=8'b00000000;	//"dark"
		endcase
	end
endmodule


```

> ## 2.5 PC功能

```Verilog
module pc_function(input clk,input clr,input [31:0]second_counter,input [7:0]DATA_INPUT,input [1:0]M,output reg[7:0]PC,output reg[7:0] Y);
always@(negedge clk or posedge clr)
	begin
		if(clr)
		begin
			PC<=8'h00;
		end
		else if(!clk)
		begin
			case(M)
				2'b00:
				begin 
					if(!second_counter) PC<=PC+1;
				end
				2'b01:
				begin 
					if(!second_counter) PC<=PC-1;
				end
				2'b10:
					begin
						PC<=DATA_INPUT;
					end
				default:
				begin 
					if(!second_counter) PC<=PC+1;
				end
			endcase
			Y<=PC;		
		end
	end
endmodule

```

> ## 2.6 寄存器功能

```Verilog

module reg_function(
	input clk,
	input wr,
	input rd,
	input [1:0] RA,
	input [7:0] DATA_INPUT,
	output reg[7:0]R0,
	output reg[7:0]R1,
	output reg[7:0]R2,
	output reg[7:0]R3,
	output reg[7:0]X
);
always@(negedge clk)
	begin
		case(RA)
				2'b00:
				begin
					X<=R0;
					if(wr==0&&rd==1)
					begin
						R0<=DATA_INPUT;
					end
				end
				2'b01:
				begin
					X<=R1;
					if(wr==0&&rd==1)
					begin
						R1<=DATA_INPUT;
					end
				end
				2'b10:
				begin
					X<=R2;
					if(wr==0&&rd==1)
					begin
						R2<=DATA_INPUT;
					end
				end
				2'b11:
				begin
					X<=R3;
					if(wr==0&&rd==1)
					begin
						R3<=DATA_INPUT;
					end
				end
			endcase
	end
	endmodule
```
> ## 2.7 仿真用顶层文件

```Verilog
module exp5(
	input clk,
	input [1:0]RA,
	input wr,
	input rd,
	input [1:0]M,
	input clr,
	input [3:0] KEY_R,
	input key_clr,
	output [3:0] KEY_C = 4'b0111,
	output [7:0] R0,
	output [7:0] R1,
	output [7:0] R2,
	output [7:0] R3,
	output [7:0] PC,
	output [2:0] sel,
	output [31:0] N,
	output [7:0]codeout
);
	wire [7:0] DATA_INPUT;
	wire [7:0] key_out;
	keymodule km(.clk(clk),.KEY_R(KEY_R),.KEY_C(KEY_C),.out(key_out),.clr(key_clr));
	segment_displays sd(.clk(clk),.N(N),.seg(codeout),.sel(sel));
	assign DATA_INPUT=key_out;
//	wire [31:0]second_counter;
	wire [7:0] X,Y;
	assign N={X,16'h0000,Y};
//	count_second cs(clk,second_counter);
	pc_function pf(clk,clr,DATA_INPUT,M,PC,Y);
	reg_function rf(clk,wr,rd,RA,DATA_INPUT,R0,R1,R2,R3,X);
endmodule
```

> ## 2.8 仿真用key_module

```Verilog
module keymodule(
	input clk,
	input [3:0] KEY_R,
	output reg[3:0] KEY_C = 4'b0111,
	output reg[7:0] out= 8'hxx,
	input clr
//	output reg[2:0] press_times=3'b000
);
	reg [1:0] cnt = 2'b0;
	reg[4:0] num=5'd16;
	reg[31:0] count_num=32'b1;
//根据按钮的列扫描信号和行输入信号判断按钮是否被按下
always  @(posedge clk)
begin
//		if(S==3'b000)
//		begin
//			out<=16'h0000;
//		end
//		else
		if(clr)
		begin
			out<=16'h0000;
		end
		else
		begin
			cnt = cnt + 1'b1;
			case (cnt)
				2'b00:	KEY_C <= 4'b1110;
				2'b01:	KEY_C <= 4'b1101;
				2'b10:	KEY_C <= 4'b1011;
				2'b11:	KEY_C <= 4'b0111;         
			endcase
			if(KEY_R==4'b1111)
			begin
				num=5'd16;
			end
			else 
			begin 
				  case ({KEY_C, KEY_R})
					 
					 8'b1011_1110: num = 5'd0;
					 8'b0111_0111: num = 5'd1;
					 8'b1011_0111: num = 5'd2;
					 8'b1101_0111: num = 5'd3;
					 
					 8'b0111_1011: num = 5'd4;
					 8'b1011_1011: num = 5'd5;
					 8'b1101_1011: num = 5'd6;
					 8'b0111_1101: num = 5'd7;  
					 
					 8'b1011_1101: num = 5'd8;
					 8'b1101_1101: num = 5'd9;
					 8'b1110_0111: num = 5'd10;
					 8'b1110_1011: num = 5'd11;  
					 
					 8'b1110_1101: num = 5'd12;
					 8'b1110_1110: num = 5'd13;
					 8'b0111_1110: num = 5'd14;
					 8'b1101_1110: num = 5'd15;  
				  endcase
				  out=out<<4;
				  out[3:0] = num[3:0];
			end
//			begin
//				if(num == 5'b1_0000)
//					begin
//						if(count_num == 32'b0)begin
//							count_num = 32'd100001;end
//						count_num = count_num + 1'b1;
//					end
//				else if(count_num > 32'd100000)
//					begin
//						count_num = 32'b1;
//					
//						//移位
//						begin
//						out=out<<4;
//						out[3:0] = num[3:0];
//						end
//					end
//			end
			end
		
end
endmodule   
```

> ## 2.9 仿真用pc_function

```Verilog

module pc_function(input clk,input clr,input [7:0]DATA_INPUT,input [1:0]M,output reg[7:0]PC,output reg[7:0] Y);
always@(negedge clk or posedge clr)
	begin
		if(clr)
		begin
			PC<=8'h00;
		end
		else if(!clk)
		begin
			case(M)
				2'b00:
				begin 
					PC<=PC+1;
				end
				2'b01:
				begin 
					PC<=PC-1;
				end
				2'b10:
					begin
						PC<=DATA_INPUT;
					end
				default:
				begin 
					PC<=PC+1;
				end
			endcase
			Y<=PC;		
		end
	end
endmodule


```

> # 3 引脚分配

<img src="/images/pin5.png" width="80%">

> # 4 仿真波形

<img src="/images/wvf5.png" width="80%">


> # 5 源码已上传github


github仓库：
{{< person url="https://github.com/Septemus/swjtu_computer_organization_exp5_cpureg.git" name="swjtu_computer_organization_exp5_cpureg" text="github库" picture="/images/github.jpg" >}}

