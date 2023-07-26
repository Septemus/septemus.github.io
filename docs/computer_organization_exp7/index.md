# 西南交通大学计组实验7-指令存储器与取指令部分的设计


{{< admonition type=note title="" open=false >}}
此笔记针对西南交通大学2023-2024学年上半学期开设的计组实验课。
{{< /admonition >}}

{{< admonition type=success title="" open=false >}}
代码和输出已通过助教验收。
{{< /admonition >}}

{{< admonition type=warning title="Frequency" open=false >}}
使用时必须将clk频率设置成100k
{{< /admonition >}}


{{< admonition type=tip title="Special thanks👍🏿" open=false >}}
感谢何同学提供的参考代码和实验要求！
{{< /admonition >}}


> # 1 实验内容

利用quartus提供的IP Core和FPGA内部存储器，完成指令存储器与取指部分设计。

> # 2 代码/原理图

> ## 2.1 顶层文件

<img src="/images/exp7_block.png" width="80%">

> ## 2.2 PC寄存器

```Verilog
module pc_function(input clk,input pc_clr,input [7:0]DATA_INPUT,input [1:0]M,output reg[7:0]PC
);
wire [31:0] second_counter;
count_second cs (clk,second_counter);
always@(negedge clk or negedge pc_clr)
	begin
		if(!pc_clr)
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
						PC<=PC;
					end
				2'b11:
					begin 
						PC<=DATA_INPUT;
					end
			endcase		
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
		//if(second_counter==32'd1)
		second_counter <= 0;
		else 
		second_counter<=second_counter+1;
	end
endmodule
```

> ## 2.4 数码管
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

> ## 2.5 矩阵键盘
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

> ## 2.6 ROM的内容

| addr | +0  | +1  | +2  | +3  | +4  | +5  | +6  | +7  |
|------|-----|-----|-----|-----|-----|-----|-----|-----|
| 0    | 0002| 0017| 002C| 0041| 0056| 006B| 0080| 0095|
| 8    | 00AA| 00BF| 00D4| 00E9| 00FE| 0113| 0128| 013D|
| 16   | 0152| 0167| 017C| 0191| 01A6| 01BB| 01D0| 01E5|
| 24   | 01FA| 020F| 0224| 0239| 024E| 0263| 0278| 028D|
| 32   | 02A2| 02B7| 02CC| 02E1| 02F6| 030B| 0320| 0335|
| 40   | 034A| 035F| 0374| 0389| 039E| 03B3| 03C8| 03DD|
| 48   | 03F2| 0407| 041C| 0431| 0446| 045B| 0470| 0485|
| 56   | 049A| 04AF| 04C4| 04D9| 04EE| 0503| 0518| 052D|
| 64   | 0542| 0557| 056C| 0581| 0596| 05AB| 05C0| 05D5|
| 72   | 05EA| 05FF| 0614| 0629| 063E| 0653| 0668| 067D|
| 80   | 0692| 06A7| 06BC| 06D1| 06E6| 06FB| 0710| 0725|
| 88   | 073A| 074F| 0764| 0779| 078E| 07A3| 07B8| 07CD|
| 96   | 07E2| 07F7| 080C| 0821| 0836| 084B| 0860| 0875|
| 104  | 088A| 089F| 08B4| 08C9| 08DE| 08F3| 0908| 091D|
| 112  | 0932| 0947| 095C| 0971| 0986| 099B| 09B0| 09C5|
| 120  | 09DA| 09EF| 0A04| 0A19| 0A2E| 0A43| 0A58| 0A6D|
| 128  | 0A82| 0A97| 0AAC| 0AC1| 0AD6| 0AEB| 0B00| 0B15|
| 136  | 0B2A| 0B3F| 0B54| 0B69| 0B7E| 0B93| 0BA8| 0BBD|
| 144  | 0BD2| 0BE7| 0BFC| 0C11| 0C26| 0C3B| 0C50| 0C65|
| 152  | 0C7A| 0C8F| 0CA4| 0CB9| 0CCE| 0CE3| 0CF8| 0D0D|
| 160  | 0D22| 0D37| 0D4C| 0D61| 0D76| 0D8B| 0DA0| 0DB5|
| 168  | 0DCA| 0DDF| 0DF4| 0E09| 0E1E| 0E33| 0E48| 0E5D|
| 176  | 0E72| 0E87| 0E9C| 0EB1| 0EC6| 0EDB| 0EF0| 0F05|
| 184  | 0F1A| 0F2F| 0F44| 0F59| 0F6E| 0F83| 0F98| 0FAD|
| 192  | 0FC2| 0FD7| 0FEC| 1001| 1016| 102B| 1040| 1055|
| 200  | 106A| 107F| 1094| 10A9| 10BE| 10D3| 10E8| 10FD|
| 208  | 1112| 1127| 113C| 1151| 1166| 117B| 1190| 11A5|
| 216  | 11BA| 11CF| 11E4| 11F9| 120E| 1223| 1238| 124D|
| 224  | 1262| 1277| 128C| 12A1| 12B6| 12CB| 12E0| 12F5|
| 232  | 130A| 131F| 1334| 1349| 135E| 1373| 1388| 139D|
| 240  | 13B2| 13C7| 13DC| 13F1| 1406| 141B| 1430| 1445|
| 248  | 145A| 146F| 1484| 1499| 14AE| 14C3| 14D8| 14ED|


> # 3 引脚分配

<img src="/images/pin7.png" width="80%">

> # 4 仿真波形

<img src="/images/wvf7.png" width="80%">

> # 5 源码已上传github


github仓库：
{{< person url="https://github.com/Septemus/swjtu_computer_organization_exp7_cmd_reader.git" name="swjtu_computer_organization_exp7_cmd_reader" text="github库" picture="/images/github.jpg" >}}

> # 6 上机操作视频

{{< admonition type=tip title="Special thanks👍🏿" open=false >}}
感谢何同学拍摄了以下这段操作视频！🤗
{{< /admonition >}}


{{< bilibili BV1vM4y1e7sa >}}
