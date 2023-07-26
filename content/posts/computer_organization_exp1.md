---
title: "西南交通大学计组实验1-四位全加器设计"
date: 2023-04-11T15:45:34+08:00
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

> # 1 实验内容

设计四位加法器

> # 2 代码/原理图

> ## 2.1 顶层文件

<img src="/images/exp1block.png" width="70%">

> ## 2.2 全加器

```Verilog
module full_adder(a,b,c0,s,c1);
	input a,b,c0;
	output wire s,c1;
	wire tmp1,tmp2,tmp3;
	half_adder ha1(a,b,tmp1,tmp2);
	half_adder ha2(tmp1,c0,s,tmp3);
	assign c1=tmp2|tmp3;
endmodule
```

> ## 2.3 半加器

```Verilog
module half_adder(a,b,s,c);
	input a,b;
	output wire s,c;
	assign s=a^b;
	assign c=a&b;
endmodule
```

> ## 2.4 7段数码管译码器

```Verilog
module segment_displays(num,seg);
	input [3:0] num;
	output reg [7:0] seg;
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
			default:seg<=8'b00111111;	//"0"
		endcase
	end
endmodule
```
> # 3 引脚分配

<img src="/images/pin1.png" width="80%">

> # 4 仿真波形

<img src="/images/wvf1.png" width="80%">

> # 5 源码已上传github

github仓库：
{{< person url="https://github.com/Septemus/swjtu_computer_organization_exp_1_4digit_adder" name="swjtu_computer_organization_exp_1_4digit_adder " text="github库" picture="/images/github.jpg" >}}
