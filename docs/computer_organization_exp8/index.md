# 西南交通大学计组实验8-指令分析与执行


{{< admonition type=note title="" open=false >}}
此笔记针对西南交通大学2023-2024学年上半学期开设的计组实验课。
{{< /admonition >}}

{{< admonition type=success title="" open=false >}}
代码和输出已经过助教验收。
{{< /admonition >}}

{{< admonition type=warning title="Frequency" open=false >}}
使用时必须将clk频率设置成100k
{{< /admonition >}}


{{< admonition type=tip title="Special thanks👍🏿" open=false >}}
感谢何同学提供的参考代码和实验要求！
{{< /admonition >}}

> # 0 完结撒花🏵️

🎉恭喜你已完成所有的计组实验，很有幸被你发现我的博客，我在校的时间里会一直维护计组实验的相关内容并进行答疑。也欢迎大家提出更好的改进建议！

⭐如果你喜欢我的设计的话，可以在github上follow我并对我的仓库点star，这会让它们被更多的校友发现，你的支持是我最大的动力！

🧠我在学习过程中也会发布其他技术相关的文章，如果你感兴趣欢迎关注！

👩🏿‍🎓最后祝各位同学学习顺利，前程似锦！

> # 1 实验内容

利用quartus提供的IP Core和FPGA内部存储器，完成指令存储器与取指部分设计。

> # 2 代码/原理图

> ## 2.1 顶层文件

<img src="/images/exp8_block.png" width="80%">

> ## 2.2 PC寄存器

{{< admonition type=info title="此处防抖参考了咕咕与瓜的博客：" open=false >}}
https://blog.csdn.net/yck1716/article/details/124656502
{{< /admonition >}}

```Verilog
module pc_function(input clk,input pc_clr,input manual_plus,output reg[7:0]PC
);
parameter   S1 = 2'b00,		//松开稳定时
            S2 = 2'b01,		//按下毛刺时
            S3 = 2'b10,		//按下稳定时
            S4 = 2'b11;		//松开毛刺时
				
 
 
/*===============================================================20ms计数器=============================================================*/
reg en_counter;	//计数使能
reg [19:0] cnt;	//计数
reg cnt_full;
 
//只有当计数使能为高电平的时候，计数器才会计数
always@(posedge clk or negedge pc_clr)
	begin
		if(!pc_clr)
			cnt <= 0;
		else if(en_counter)
			cnt <= cnt + 1'b1;
		else 
			cnt <= 0;
	end
	
//计数满信号（数数到1000000计数满时间到。1000000是1M，当基于clk信号频率进行计数时，cnt_full走过(1/50M)s*1M的时间，即20ms）
always@(posedge clk or negedge pc_clr)	//当clk接50MHz的信号时，相当于clk在1s内进行了50M次计数，相邻上升沿相间(1/50M)s
begin
	if(!pc_clr)
		cnt_full <= 1'b0;
	else if(cnt == 20'd10000)	
		cnt_full <= 1'b1;
	else 
		cnt_full <= 1'b0;
end
 
 
 
/*==============================================================判断边沿模块=============================================================*/
reg key_tmp0,key_tmp1;
 
always@(posedge clk or negedge pc_clr)
	begin
		if(!pc_clr)
			begin
				key_tmp0 <= 1'b1;
				key_tmp1 <= 1'b1;
			end
			
		else
			begin
				key_tmp0 <= manual_plus;		//manual_plus按键输入
				key_tmp1 <= key_tmp0;	
			end
			
	end
 
wire pedge,nedge;
assign nedge = (!key_tmp0) & key_tmp1;        //下降沿（下一clk时为0，上一clk时为1）
assign pedge = key_tmp0 & (!key_tmp1);        //上升沿（下一clk时为1，上一clk时为0）
 
 
 
/*=============================================================状态机模块================================================================*/
reg [1:0] state;
reg key_flag;		//经消抖后可确认的按下动作
reg key_state;		//按键状态，高电平为未按下，低电平为按下状态
 
always@(posedge clk or negedge pc_clr)
	begin
		
		if(!pc_clr)
			begin
				state      <= S1; 
				en_counter <= 1'b0;	//计数器归零
				key_state  <= 1'b1;	//按键未按下
				key_flag   <= 1'b0;
			end
		
		else 
			begin
				case(state)
					
					S1:	//高电平（松开稳定）
						begin
							key_flag   <= 1'b0;	//按键未按下，不计
							key_state  <= 1'b1;	//按键松开状态
							en_counter <= 1'b0;	//计数器归零
							
							if(nedge)	//检测到下降沿，进入下一个状态同时打开计数器
								begin
									state      <= S2;
									en_counter <= 1'b1;	//计数器使能
								end
							
							else 
								state <= state;	//保持目前状态    
						end
					
					S2:	//下降沿抖动（按下毛刺）
						if(cnt_full)	//计数满，说明达到稳定状态，关闭计数器，进入下一个状态
							begin
								state      <= S3;
								en_counter <= 1'b0;	//计数器归零
								key_flag   <= 1'b1;	//按键可确认已按下
								key_state  <= 1'b0;	//按键按下状态
							end
						
						else if(pedge)	//检测到上升沿（毛刺），跳回S1状态同时关闭计数器
							begin
								en_counter <= 1'b0;	//计数器归零
								state      <= S1;
							end
						
						else 
							state <= state;	//保持目前状态
							
					S3:	//低电平（按下稳定）
						begin
							key_flag <= 1'b0;	//一个按键周期测到一次就行，现在可清零了（后面代码编写只在意其posedge）
							
							if(pedge)	//检测到上升沿，进入下一个状态同时打开计数器
								begin
									state      <= S4;
									en_counter <= 1'b1;	//计数器使能
								end
							
							else 
								state <= state;	//保持目前状态
						end
					
					S4:	//上升沿抖动（松开毛刺）
						if(cnt_full)
							begin
								state     <= S1;
								key_state <= 1'b1;
							end
						
						else 
							if(nedge)
								begin
									en_counter <= 1'b0;	//计数器归零
									state      <= S3;					 		
								end 
							else 
								state <= state;	//保持目前状态
					
					default:
						state <= S1;
						
					endcase
	
			end
	
	end
always@(posedge key_flag,negedge pc_clr)
	//key_flag：经消抖后可确认的按下动作
	begin
	if(!pc_clr)
		PC <= 0;
	else
		PC<=PC+1;
	end

endmodule


```

> ## 2.3 数码管
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

> ## 2.4 矩阵键盘
```Verilog
module keymodule(
	input clk,
	input [3:0] KEY_R,
	output reg[3:0] KEY_C = 4'b0111,
	output reg[7:0] out= 8'hxx,
	input key_clr
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
		if(!key_clr)
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

> ## 2.5 ROM的内容


| addr | +0   | +1   | +2   | +3   | +4   | +5   | +6   | +7   |
|------|------|------|------|------|------|------|------|------|
| 0    | 7600 | 8300 | 7340 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 8    | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 16   | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 24   | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 32   | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 40   | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 48   | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 56   | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 64   | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 72   | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 80   | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 88   | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 96   | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 104  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 112  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 120  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 128  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 136  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 144  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 152  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 160  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 168  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 176  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 184  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 192  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 200  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 208  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 216  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 224  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 232  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 240  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 248  | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |

> ## 2.6 选择ALU的操作数

```Verilog
module choose_opts(
input clk,
	input [7:0]R0,
	input [7:0]R1,
	input [7:0]R2,
	input [7:0]R3,
	input [3:0]choose_reg,
	output [15:0] res
);
	reg [7:0]opt1,opt2;
	initial
	begin
		opt1<=8'b0000_0000;
		opt2<=8'b0000_0000;
	end
	always@(posedge clk)
	begin
			case(choose_reg[3:2])
				2'b00:opt1<=R0;
				2'b01:opt1<=R1;
				2'b10:opt1<=R2;
				2'b11:opt1<=R3;
			endcase
			case(choose_reg[1:0])
				2'b00:opt2<=R0;
				2'b01:opt2<=R1;
				2'b10:opt2<=R2;
				2'b11:opt2<=R3;
			endcase
	end
	assign res={opt1,opt2};
endmodule

```

> ## 2.7 寄存器组
```Verilog
module exp5(
	input clk,
	input [1:0]RA,
	input wr,
	input rd,
	input [1:0]M,
	input clr,
	input manual_plus,
	input [7:0] key_out,
	input [7:0] res_alu,
	input [1:0] res_dest,
	input enact,
	output [7:0] R0,
	output [7:0] R1,
	output [7:0] R2,
	output [7:0] R3,
	output [7:0] PC
);
	wire [7:0] DATA_INPUT;
	assign DATA_INPUT=key_out;
	pc_function pf  (clk,clr,manual_plus,PC);
	reg_function rf (clk,wr,rd,RA,DATA_INPUT,R0,R1,R2,R3,res_alu,res_dest,enact);
endmodule

```

> ## 2.8 通用寄存器

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
	input [7:0] res_alu,
	input [1:0] res_dest,
	input enact
);
always@(negedge clk)
	begin
		if(res_dest==2'b00&&!enact)
					begin
						R0<=res_alu;
					end
		else if(res_dest==2'b01&&!enact)
					begin
						R1<=res_alu;
					end
		else if(res_dest==2'b10&&!enact)
					begin
						R2<=res_alu;
					end
		else if(res_dest==2'b11&&!enact)
					begin
						R3<=res_alu;
					end
		else 
		begin
			case(RA)
					2'b00:
					begin
						if(wr==0&&rd==1)
						begin
							R0<=DATA_INPUT;
						end
						else if(wr==1&&rd==1)
						begin
							R0<=res_alu;
						end
					end
					2'b01:
					begin
						if(wr==0&&rd==1)
						begin
							R1<=DATA_INPUT;
						end
						else if(wr==1&&rd==1)
						begin
							R1<=res_alu;
						end
					end
					2'b10:
					begin
						if(wr==0&&rd==1)
						begin
							R2<=DATA_INPUT;
						end
						else if(wr==1&&rd==1)
						begin
							R2<=res_alu;
						end
					end
					2'b11:
					begin
						if(wr==0&&rd==1)
						begin
							R3<=DATA_INPUT;
						end
						else if(wr==1&&rd==1)
						begin
							R3<=res_alu;
						end
					end
				endcase
			end
	end
	endmodule
	 
```

> ## 2.9 运算器

```Verilog
module exp4(
	input clk,
	input [2:0]S,
	input cin,
	input [15:0] operators,
	output exceed,
	output [15:0] ans,
	output [7:0] X,
	output [7:0] Y,
	output [7:0] alu_res
);
midware mw(operators,X,Y,clk);
assign alu_res=ans[7:0];
manipulate man(clk,S,X,Y,cin,ans,exceed);
endmodule

```

> ## 2.10 运算器的计算功能
```Verilog
module manipulate(

	input clk,
	input [2:0]S,
	input [7:0]X,
	input [7:0]Y,
	input cin,
	output reg[15:0]ans,
	output reg exceed
	);
	initial
	begin
		ans<=8'h00;
	end
	always@(posedge clk)
	begin
			case(S)
				3'b000:ans<=16'b0000_0000_0000_0000;
				3'b001:ans<={8'b0000_0000,X&Y};
				3'b010:ans<={8'b0000_0000,X|Y};
				3'b011:ans<={8'b0000_0000,X^Y};
				3'b100:
				begin 
					ans<=X+Y+(cin?1'b0:1'b1);
				end
				3'b101:ans<={8'b0000_0000,X[6:0],1'b0};
				3'b110:ans<={8'b0000_0000,1'b0,X[7:1]};
				3'b111:ans<={8'b0000_0000,((X>>7)&1)?1:0,X[7:1]};
			endcase
	end
	always@(posedge clk)
	begin
		if(S==3'b100)
		begin
			if( ans[8]^ans[7] ) exceed<=1;
			else exceed<=0;
		end
		else exceed<=0;
	end
endmodule

```

> ## 2.11 运算器的中间件
```Verilog
module midware(
	input [15:0]key_out,
	output reg [7:0] X,
	output reg [7:0] Y,
	input clk
);
	always@(posedge clk)
	begin
		X<=key_out[15:8];
		Y<=key_out[7:0];
	end
endmodule

```

> ## 2.12 取指令并向各模块发送信号
```Verilog
module execute(
	input clk,
	input [15:0] order,
	input manual_plus,
	output reg[3:0] choose_reg,
	output reg[2:0] S,
	output reg[1:0] res_dest
);
	always@(posedge clk)
	begin
		case(order[15:12])
			4'b0111:
			begin
				S<=3'b011;
				choose_reg<=order[11:8];
				res_dest<=order[7:6];
			end
			4'b1000:
			begin
				S<=3'b110;
				choose_reg<={order[11:10],2'b00};
				res_dest<=order[9:8];
			end
			default:
			begin
				S<=S;
				choose_reg<=choose_reg;
				res_dest<=res_dest;
			end
		endcase
		
	end
endmodule

```

> ## 2.14 页面切换

```Verilog
module page_switch(
	input clk,
	input [2:0]switch_buttons,
	input [7:0]R0,
	input [7:0]R1,
	input [7:0]R2,
	input [7:0]R3,
	input [7:0]pc,
	input [15:0] order,
	input [31:0]alu_N,
	output reg[31:0] N,
	output reg[1:0] status
);
	//reg status[1:0]=2'b00;
	initial
	begin
		status<=2'b00;
	end
	always@(posedge clk)
	begin
		//N<={R0,R1,R2,R3};
		casex(switch_buttons)
			3'bxx0: status<=2'b00;
			3'bx01: status<=2'b01;
			3'b011: status<=2'b10;
			default: status<=status;
		endcase
		case(status)
			2'b00:N<={R0,R1,R2,R3};
			2'b01:N<={order,8'h00,pc};
			2'b10:N<=alu_N;
		endcase
	end
endmodule

```

> # 3 引脚分配

<img src="/images/pin8.png" width="80%">

> # 4 仿真波形

<img src="/images/wvf8.png" width="80%">

> # 5 源码已上传github


github仓库：
{{< person url="https://github.com/Septemus/swjtu_computer_organization_exp8_cmd_rdexec.git" name="swjtu_computer_organization_exp8_cmd_rdexec" text="github库" picture="/images/github.jpg" >}}


> # 6 上机操作视频


{{< bilibili BV1Kh411F7dW >}}

