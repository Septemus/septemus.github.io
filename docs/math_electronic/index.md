# 数字电子技术理论笔记

{{< admonition type=warning title="" open=false >}}
此笔记由我个人整理，因此相比教材可能有出入，如果您发现有错误，欢迎和我联系！
{{< /admonition >}}
{{< admonition type=note title="" open=false >}}
此笔记针对西南交通大学2022-2023学年上半学期开设的数电理论课。
{{< /admonition >}}

> # 1 数字逻辑概论

> ## 1.1 数字信号和数字电路

> ### 1.1.1 模拟信号和数字信号

> #### 1.1.1.1 模拟信号

模拟信号是时间和数值均连续变化的电信号，如正弦波、三角波等

> #### 1.1.1.2 数字信号

数字信号是在时间上和数值上均是离散的信号。

> #### 1.1.1.3 模拟信号转换为数字信号

处理过程包括：采样、量化、编码。

> ### 1.1.2 数字信号的描述方法

周期 (T) ---- 表示两个相邻脉冲之间的时间间隔

脉冲宽度 ($t_{w}$)---- 脉冲幅值的50%的两个时间所跨越的时间

占空比 Q ----- 表示脉冲宽度占整个周期的百分比

上升时间$t_{r}$ 和下降时间$t_{f}$ ----从脉冲幅值的10%到90% 上升

![wave1](/images/Mathematical_Electronic/wave1.jpg)

> ## 1.2 数制

> ### 1.2.1 二进制数和十进制数转换

> #### 1.2.1.1 辗转相除法

将十进制数连续不断地除以2 , 直至商为零，所得余数由低位到高位排列，即为所求二进制数。

> #### 1.2.1.2 从高到低比较大小

![eg2](/images/Mathematical_Electronic/eg2.jpg)


> #### 1.2.1.3 小数的转换

对于二进制的小数部分可写成
$$N_{D} = b_{-1} \times 2^{-1} + b_{-2} \times 2^{-2} + \cdots + b_{-(n-1)} \times 2^{-(n-1)} + b_{-n} \times 2^{-n} \tag{1} $$

将上式两边分别乘以2，得

$$2 \times N_{D} = b_{-1} \times 2^{0} + b_{-2} \times 2^{-1} + \cdots + b_{-(n-1)} \times 2^{-(n-2)} + b_{-n} \times 2^{-(n-1)} \tag{2} $$

由此可见，将十进制小数乘以2，所得乘积的整数即为 $b_1$,不难推知，将十进制小数每次减掉上次所得积中的整数再乘以2，直到满足误差要求进行“四舍五入"为止，就可完成由十进制小数转换成二进制小数。

![eg1](/images/Mathematical_Electronic/eg1.jpg)

{{< admonition type=info title="" open=false >}}
对于八进制和十六进制小数，转换时，由小数点开始，整数部分自右向左，小数部分自左向右，三/四位一组，不够三/四位的添零补齐，则每三/四位二进制数表示一位八/十六进制数
{{< /admonition >}}

> ## 1.3 算数运算

> ### 1.3.1 原码、反码、补码

> #### 1.3.1.1 原码

原码表示办法：正数符号位是0，负数符号位是1，数值用其绝对值的二进制数表示。例如
$$ +5 = \boxed{0}101 \tag{1}$$
$$ -5 = \boxed{1}101 \tag{2}$$

> #### 1.3.1.2 反码

反码又称为“1的补码”，正数的反码与正码相同。求二进制负数的反码的简单办法是，符号位不变，将原码的数值逐位求反得到。

> #### 1.3.1.3 补码

补码即为反码的最低位加1所得的数

> ## 1.4 二进制代码

编码:以一定的规则编制代码来区分和表示不同的数值、字母、符号等信息的过程。

二进制代码的位数(n),与需要编码的事件（或信息）的个数(N)之间应满足以下关系： $$2^{n-1}≤N≤2^{n}$$

> ### 1.4.1 BCD码

从4 位二进制数16种代码中,选择10种来表示0~9个数码的方案有很多种。每种方案产生一种BCD码。

|BCD码十进制数码| 8421码| 2421 码| 5421 码| 余3码| 余3循环码|格雷码|
|- |-----|-----|-----|-----|-----|---------------------------------|
|0 | 0000| 0000| 0000| 0011| 0010|0000|
|1 | 0001| 0001| 0001| 0100| 0110|0001|
|2 | 0010| 0010| 0010| 0101| 0111|0011|
|3 | 0011| 0011| 0011| 0110| 0101|0010|
|4 | 0100| 0100| 0100| 0111| 0100|0110|
|5 | 0101| 1011| 1000| 1000| 1100|0111|
|6 | 0110| 1100| 1001| 1001| 1101|0101|
|7 | 0111| 1101| 1010| 1010| 1111|0100|
|8 | 1000| 1110| 1011| 1011| 1110|1100|
|9 | 1001| 1111| 1100| 1100| 1010|1101|
|10| \   | \   | \   | \   | \   |1111|
|11| \   | \   | \   | \   | \   |1110|
|12| \   | \   | \   | \   | \   |1010|
|13| \   | \   | \   | \   | \   |1011|
|14| \   | \   | \   | \   | \   |1001|
|15| \   | \   | \   | \   | \   |1000|

> #### 1.4.1.1 各编码特点

- 有权码：编码的每一位有固定的权值

- 无权码：编码没有固定的权值

    - 余3码的特点:当两个十进制的和是10时，相应的二进制和正
    好是16，于是可自动产生进位信号,而不需修正.1和9, 2和8,…..6和
    4的余3码。便于求10的补码。（本质上一个数的余3码就是这个数加上3的8421码）
    - 格雷码：任何两个相邻代码之间仅有一位不同。
    - 余3码循环码：相邻的两个代码之间仅一位的状态不同。按余3
    码循环码组成计数器时，每次转换过程只有一个触发器翻转，译
    码时不会发生竞争－冒险现象。（本质上一个数的余3循环码就是这个数加上3的格雷码）

> #### 1.4.1.2 用BCD码表示十进制数
对于一个多位的十进制数，需要有与十进制位数相同的几组BCD代码来表示。例如：

![eg3](/images/Mathematical_Electronic/eg3.jpg)

> #### 1.4.1.3 二进制码与格雷码的转换
1. 二进制码$\rightarrow$格雷码
    - 格雷码的最高位（最左边）与二进制码的最高位相同。
    - 从左到右，逐一将二进制码相邻的两位相加（舍去进位），作为格雷码的下一位。

        ![eg4](/images/Mathematical_Electronic/eg4.jpg)

2. 格雷码$\rightarrow$二进制码
    - 二进制码的最高位（最左边）与格雷码的最高位相同。
    - 将产生的每一位二进制码，与下一位相邻的格雷码相加（舍去进位），作为二进制码的下一位。

        ![eg5](/images/Mathematical_Electronic/eg5.jpg)

> ## 1.5 二值逻辑变量与基本逻辑运算

逻辑运算的描述方式:逻辑代数表达式、真值表、逻辑图、卡诺图、波形图和硬件描述语言（HDL) 等。

> ### 1.5.1 各逻辑门

![ld1](/images/Mathematical_Electronic/logicdoor1.webp)
![ld2](/images/Mathematical_Electronic/logicdoor2.webp)
![ld3](/images/Mathematical_Electronic/logicdoor3.webp)

> ## 1.6 逻辑函数

描述输入变量和输出变量之间的因果关系称为逻辑函数

> ### 1.6.1 表示办法

> #### 1.6.1.1 真值表

> #### 1.6.1.2 表达式
逻辑表达式是用与、或、非等运算组合起来，表示逻辑函数与逻辑变量之间关系的逻辑代数式。
1. 只写使输出变量为1的项
2. 每项之中，变量之间是与的关系
3. 变量为1的用原变量，变量为0的用反变量
4. 项与项之间是或的关系

> #### 1.6.1.3 逻辑图
用与、或、非等逻辑符号表示逻辑函数中各变量之间的逻辑关系所得到的图形称为逻辑图

思路：将逻辑函数式中所有的与、或、非运算符号用相应的逻辑符号代替，并按照逻辑运算的先后次序将这些逻辑符号连接起来，就得到图电路所对应的逻辑图

![eg6](/images/Mathematical_Electronic/eg6.jpg)

> #### 1.6.1.4 波形图

用输入端在不同逻辑信号作用下所对应的输出信号的波形图，表示电路的逻辑关系

![eg7](/images/Mathematical_Electronic/eg7.jpg)

> ### 1.6.2 转换

> #### 1.6.2.1 真值表$\rightarrow$逻辑图

1. 根据真值表写出逻辑表达式
2. 化简逻辑表达式
3. 根据表达式画出逻辑图


> #### 1.6.2.1 逻辑图$\rightarrow$真值表

1. 根据逻辑图逐级写出表达式
2. 化简变换求最简与或式
3. 将输入变量的所有取值逐一代入表达式得真值表

> # 2 逻辑代数与硬件描述语言

> ## 2.1 逻辑代数的基本定理和恒等式

> ### 2.1.1 逻辑代数的基本定律和恒等式

![rules](/images/Mathematical_Electronic/logic_algebra_rules.jpg)

> ### 2.1.2 逻辑代数的基本规则

{{< admonition type=info title="" open=false >}}
对偶和反演的区别在于对偶不会把原变量换成反变量
{{< /admonition >}}

> #### 2.1.2.1 对偶规则
对于任何逻辑函数式，若将其中的与（•）换成或（+），或（+）换成与（•）；并将1换成0，0换成1；那么，所得的新的函数式就是L的对偶式，记作$L'$。

![eg8](/images/Mathematical_Electronic/eg8.jpg)

当某个逻辑恒等式成立时，则该恒等式两侧的对偶式也相等。这就是对偶规则。利用对偶规则，可从已知公式中得到更多的运算公式.

> #### 2.1.2.2 反演规则
对于任意一个逻辑表达式L，若将其中所有的与（•）换成或（+），或（+）换成与（•）；原变量换为反变量，反变量换为原变量；将1换成0，0换成1；则得到的结果就是原函数的反函数。

![eg_re](/images/Mathematical_Electronic/eg_re.jpg)

> ## 2.2 逻辑函数表达式的形式

> ### 2.2.1 基本形式

> #### 2.2.1.1 与-或表达式
若干与项进行或逻辑运算构成的表达式。由与运算符和或运算符连接起来。如：
$$ L = A \cdot C + \bar{C} \cdot D $$

> #### 2.2.1.2 或-与表达式
若干或项进行与逻辑运算构成的表达式。由或运算符和与运算符连接起来。如：
$$ L = ( A + C ) \cdot ( B + \bar{C} ) \cdot D $$

> #### 2.2.1.3 其他表达式

> ### 2.2.2 最小项与最小项表达式

> #### 2.2.2.1 最小项的定义

n个变量$X_{1}, X_{2}, …, X_{n}$的最小项是n个因子的乘积，乘积中包含了全部n个变量，每个变量都以它的原变量或非变量的形式在乘积项中出现，且仅出现一次。一般n个变量的最小项应有$2^{n}$个

> #### 2.2.2.2 最小项的性质

- 对于任意一个最小项，只有一组变量取值使得它的值为1
- 任意两个最小项的乘积为0
- 全体最小项之和为1
- 使最小项为1的一组二进制数所对应的十进制数即为最小项的编号值。
- 若干个最小项的和等于其余最小项和的反。
- 两个最小式表达式的与的结果是他们的公共项的并。

> #### 2.2.2.3 最小项的表示

通常用$m_i$表示最小项，m 表示最小项,下标i为最小项编号。

> ### 2.2.3 最大项与最大项表达式

> #### 2.2.3.1 最大项的定义

n个变量$X_1, X_2, …, X_n$的最大项是n个因子或项，每个变量都以它的原变量或非变量的形式在或项中出现，且仅出现一次。一般n个变量的最大项应有$2^n$个

> #### 2.2.3.2 最大项的性质

- 对于任意一个最大项，只有一组变量取值使得它的值为0
- 任意两个最大项的之和为1
- 全体最大项之积为0

> #### 2.2.3.3 最大项的表示

通常用$M_i$表示最大项，M 表示最大项,下标i为最大项号。

> ### 2.2.4 最小项和最大项的关系

两者之间为互补关系：$m_i = \overline{M_i} ，或者M_i = \overline{m_i}$

> ## 2.3 逻辑函数的代数化简法

> ### 2.3.1 逻辑函数的最简形式

逻辑函数有不同形式，将其中包含的与项数最少，且每个与项中变量数最少的与-或表达式称为最简与-或表达式

> ### 2.3.2 代数化简法

运用逻辑代数的基本定律和恒等式进行化简的方法

> #### 2.3.2.1 并项

$$ A + \bar{A} = 1 $$
$$ L = \bar{A} \bar{B} C + \bar{A} \bar{B} \bar{C} = \bar{A} \bar{B} ( C + \bar{C} ) = \bar{A} \bar{B} $$

> #### 2.3.2.2 吸收

$$ A + AB = A $$
$$ L = \bar{A} B + \bar{A} BCD ( E + F ) = AB $$

> #### 2.3.2.3 消去

$$ A + \bar{A} B = A + B $$
$$ L = AB + \bar{A}C + \bar{B}C = AB + ( \bar{A} + \bar{B} ) C = AB + \overline{AB} C = AB + C $$

> #### 2.3.3 形式变化

通常在一片集成电路芯片中只有一种门电路，为了减少门电路的种类，需要对逻辑函数表达式进行变换。一般通过两次取反可变化。

> ## 2.4 逻辑函数的卡诺图化简法

> ### 2.4.1 用卡诺图表示逻辑函数

> #### 2.4.1.1 引出原理

- 逻辑函数可以表达为若干最小项相“或”的形式；
- 逻辑相邻的最小项：如果两个最小项只有一个变量互为反变量，那么，就称这两个最小项在逻辑上相邻;

> #### 2.4.1.2 形式

卡诺图：将n变量的全部最小项都填在小方格阵中，并使具有逻辑相邻的最小项在几何位置上也相邻地排列起来，这样,所得到的图形叫n变量的卡诺图。

![karnaugh](/images/Mathematical_Electronic/karnaugh.jpg)

各小方格对应于各变量不同的组合，而且上下左右在几何上相邻的方格内只有一个因子有差别，这个重要特点成为卡诺图化简逻辑函数的主要依据。

> #### 2.4.1.3 画法

当逻辑函数为最小项表达式时，在卡诺图中找出和表达式中最小项对应的小方格填上1，其余的小方格填上0（有时也可用空格表示），就可以得到相应的卡诺图。任何逻辑函数都等于其卡诺图中为1的方格所对应的最小项之和。

![eg9](/images/Mathematical_Electronic/eg9.jpg)

> ### 2.4.2 化简

> #### 2.4.2.1 步骤

1. 将逻辑函数写成最小项表达式
2. 按最小项表达式填卡诺图，凡式中包含了的最小项，其对应方格填1，其余方格填0，如果是无关项填d或x。
3. 合并最小项，即将相邻的1方格圈成一组(包围圈)，每一组含$2^n$个方格，对应每个包围圈写成一个新的乘积项。
4. 将所有包围圈对应的乘积项相加。

![eg10](/images/Mathematical_Electronic/eg10.jpg)

> #### 2.4.2.2 原则

1. 包围圈内的方格数一定是$2^n$个，且包围圈必须呈矩形。
2. 循环相邻特性包括上下底相邻，左右边相邻和四角相邻。
3. 同一方格可以被不同的包围圈重复包围多次，但新增的包围圈中一定要有原有包围圈未曾包围的方格。
4. 一个包围圈的方格数要尽可能多,包围圈的数目要可能少
5. 当卡诺图中1的个数明显多于0的个数时，可以采取圈0的方式化简，得到原逻辑函数L的反函数，然后再求反，得到L。

> ### 2.4.3 无关项

在真值表内对应于变量的某些取值下，
函数的值可以是任意的，或者这些变量的取值根本不会出现，这些变量取值所对应的最小项称为无关项。
{{< admonition type=info title="" open=false >}}
在含有无关项逻辑函数的卡诺图化简中，它的值可以取0或取1，具体取什么值，可以根据使函数尽量得到简化而定。
{{< /admonition >}}

> ## 2.5 硬件描述语言Verilog HDL基础

> ### 2.5.1 基本语法规则

> #### 2.5.1.1 间隔符

Verilog 的间隔符主要起分隔文本的作用，可以使文本错落有致，便于阅读与修改。间隔符包括空格符（\b）、TAB 键（\t）、换行符（\n）及换页符。

> #### 2.5.1.2 注释符

注释只是为了改善程序的可读性,在编译时不起作用。多行注释符(用于写多行注释): /* --- */；单行注释符 :以//开始到行尾结束为注释文字

> #### 2.5.1.3 标识符

给对象（如模块名、电路的输入与输出端口、变量等）取名所用的字符串。以英文字母或下划线开始如，clk、counter8、_net、bus_A 。

> #### 2.5.1.4 关键字

是Verilog语言本身规定的特殊字符串，用来定义语言的结构。例如，module、endmodule、input、output、wire、reg、and等都是关键词。关键词都是小写，关键词不能作为标识符使用 。

> #### 2.5.1.5 逻辑值集合

为了表示数字逻辑电路的逻辑状态，Verilog语言规定了4种基本的逻辑值。
|val|含义|
|---|--------------|
| 0 | 逻辑0、逻辑假|
| 1 | 逻辑1、逻辑真|
| x/X | 不确定|
| z/Z | 高阻态|


> #### 2.5.1.6 常量
{{< mermaid >}}
    graph LR
	常量--> A(整数型)
	A-->十进制数的形式的表示方法:表示有符号常量例如:30,-2
    A-->带基数的形式的表示方法:表示常量格式为:+/-_二进制位宽'基数符号_数值,例如:3'b101,5'o37,8'he3,8'b1001_0011
	常量--> 实数型
	实数型-->十进制记数法如:0.1,2.0,5.67
    实数型-->科学记数法如:23_5.1e2,5E-4,23510.0,0.0005
{{< /mermaid >}}

Verilog允许用参数定义语句定义一个标识符来代表一个常量，称为符号常量。定义的格式为：parameter 参数名1＝常量表达式1，参数名2＝常量表达式2，……；如 parameter BIT=1, BYTE=8, PI=3.14;

> #### 2.5.1.7 变量的数据类型

1. 线网类型:是指输出始终根据输入的变化而更新其值的变量,它一般指的是硬件电路中的各种物理连接,常用的网络类型由关键词wire定义wire型变量的定义格式如下：wire [n-1:0] 变量名1，变量名2，…，变量名n； 
例:

```Verilog
wire L; //将上述电路的输出信号L声明为网络型变量   
wire [7:0] data bus; //声明一个8-bit宽的网络型总线变量 
```

![eg11](/images/Mathematical_Electronic/eg11.PNG)

{{< admonition type=info title="" open=false >}}
wire型变量未赋值的话缺省值为高阻态Z。
{{< /admonition >}}

2. 寄存器类型:寄存器型变量对应的是具有状态保持作用的电等路元件,如触发器寄存器。寄存器型变量只能在initial或always内部被赋值

|寄存器类型(不对应具体硬件)| 功能说明|
|--------|--------|
|reg     |常用的寄存器型变量|
|integer |32位带符号的整数型变量|
|real |64位带符号的实数型变量|
|time |64位无符号的时间变量|

例:
```verilog
reg clock;//定义一个1位寄存器变量
reg [3:0] counter; //定义一个4位寄存器变量
```

> ### 2.5.3 运算符及优先级

![eg11](/images/Mathematical_Electronic/eg12.PNG)

> ### 2.5.4 门级元件

|元件符号| 功能说明| 元件符号| 功能说明|
|--------|--------|---------|----------|
|and| 多输入端的与门| nand| 多输入端的与非门|
|or| 多输入端的或门| nor| 多输入端的或非门|
|xor| 多输入端的异或门| xnor| 多输入端的异或非门|
|buf| 多输出端的缓冲器| not| 多输出端的反相器|
|bufif1| 控制信号高电平有效的三态缓冲器| notif1| 控制信号高电平有效的三态反相器|
|bufif0| 控制信号低电平有效的三态缓冲器| notif0| 控制信号低电平有效的三态反相器|

> ### 2.5.5 程序的基本结构
模块是Verilog描述电路的基本单元。对数字电路建模时，用一个或多个模块。不同模块之间通过端口进行连接。
1. 每个模块以关键词module开始，以endmodule结束。
2. 每个模块先要进行端口的定义，并说明输入（input)和输出（output),然后对模块功能进行描述。
3. 除了endmodule语句外，每个语句后必须有分号。
4. 可以用/* --- */和//…..对程序的任何部分做注释。
5. 逻辑功能的描述方式有三种不同风格：结构描述方式（门级描述方式,元件列表）、数据流描述方式(assign)，行为描述方式(always)

> #### 2.5.5.1 电路模块定义的一般结构

```Verilog
module 模块名（端口名1, 端口名2, 端口名3,…）； 
    端口类型说明(input, output, inout)； 
    参数定义(可选)； 
    数据类型定义(wire, reg等)； 
    
    实例化低层模块和基本门级元件； 
    连续赋值语句（assign）； 
    过程块结构（initial和always） 
    行为描述语句； 
endmodule
```
> #### 2.5.5.2 描述风格

![eg13](/images/Mathematical_Electronic/eg13.jpg)

![eg14](/images/Mathematical_Electronic/eg14.jpg)

![eg15](/images/Mathematical_Electronic/eg15.jpg)


> # 4 组合逻辑电路

> ## 4.1 组合逻辑电路的分析

> ### 4.1.1 定义
其输出状态在任何时刻只取决于同一时刻的输入状态，而与电路原来的状态无关的逻辑电路。

> ### 4.1.2 结构特征
1. 输出、输入之间没有反馈延迟通路，
2. 不含记忆单元

> ### 4.1.3 分析步骤

1. 由逻辑图写出各输出端的逻辑表达式；
2. 化简和变换逻辑表达式；
3. 列出真值表；
4. 根据真值表或逻辑表达式，经分析最后确定其功能。

> ## 4.2 组合逻辑电路的设计
> ### 4.2.1 步骤
1. 逻辑抽象：根据实际逻辑问题的因果关系确定输入、输出变量，并定义逻辑状态的含义；
2. 根据逻辑描述列出真值表；
3. 由真值表写出逻辑表达式;
4. 简化和变换逻辑表达式，画出逻辑图。


> ## 4.3 组合逻辑电路中的竞争和冒险

> ### 4.3.1 原因
![reason_cp](/images/Mathematical_Electronic/reason_cp.jpg)

> ### 4.3.2 检查方法

> #### 4.3.2.1 代数法
对具备竞争条件的某变量，将除该变量外其他变量取0或1，若原函数可化成 A+$\bar{A}$或A$\cdot \bar{A}$的形式,则A存在冒险。
> #### 4.3.2.2 卡诺图
画出卡诺图，若存在两个相切的卡诺圈，且这个相切的部分没有被另外的卡诺圈包围，则必定存在冒险。

![eg16](/images/Mathematical_Electronic/eg16.jpg)

> ### 4.3.3 消除办法
> #### 4.3.3.1 发现并消除互补变量

![eg17](/images/Mathematical_Electronic/eg17.jpg)

> #### 4.3.3.2 增加乘积项

![eg18](/images/Mathematical_Electronic/eg18.jpg)

> #### 4.3.3.3 输出端并联电容器

如果逻辑电路在较慢速度下工作，为了消去竞争冒险，可以在输出端并联一电容器，致使输出波形上升沿和下降沿变化比较缓慢，可对于很窄的负跳变脉冲起到平波的作用。

> #### 4.3.3.4 引入选通/封锁脉冲

加封锁脉冲/选通脉冲。在输入信号产生竞争冒险的时间内，1在输出端引入一个逻辑封锁/选通门和控制信号，对脉冲将1可能产生的尖峰干扰脉冲进行屏蔽。1控制信号可由one shot电路产生。

> #### 4.3.3.5 接入滤波电路


> ## 4.4 若干典型的组合逻辑电路
> ### 4.4.1 编码器
能将每一个编码输入信号变换为不同的二进制的代码输出。
{{< admonition type=warning title="" open=false >}}
普通编码器不能有两个或以上有效输入。
{{< /admonition >}}
> #### 4.4.1.1 分类
- 普通编码器：任何时候只允许输入一个有效信号，否则输出就会发生混乱。
- 优先编码器：允许同时输入两个以上的有效编码信号。当同时输入几个有效编码信号时，优先编码器能按预先设定的优先级别，只对其中优先权最高的一个进行编码。

> #### 4.4.1.2 典型
{{< figure src="/images/Mathematical_Electronic/4-2coder.jpg" title="4线─2线普通二进制编码器" >}}
{{< figure src="/images/Mathematical_Electronic/keyborad1.jpg" title="键盘电路图" >}}
{{< figure src="/images/Mathematical_Electronic/keyborad2.jpg" title="键盘真值表" >}}
{{< figure src="/images/Mathematical_Electronic/cd4532_1.jpg" title="cd4532优先编码器示意图" >}}
{{< figure src="/images/Mathematical_Electronic/cd4532_2.jpg" title="cd4532优先编码器真值表" >}}
{{< figure src="/images/Mathematical_Electronic/16-4coder.jpg" title="用二片CD4532构成16线-4线优先编码器" >}}
{{< figure src="/images/Mathematical_Electronic/74HC147.jpg" title="74HC147真值表" >}}




> ### 4.4.2 译码器/数据分配器
译码：译码是编码的逆过程，它能将二进制码翻译成代表某一特定含义的信号.(高低电平信号)

译码器：具有译码功能的逻辑电路称为译码器。

![bi_trans](/images/Mathematical_Electronic/bi_trans.jpg)
> #### 4.4.2.1 2线-4线译码器（74HC139）
![2_4_anal](/images/Mathematical_Electronic/2_4trans_anal.jpg)

> #### 4.4.2.2 3线-8线译码器（74HC138)
![3_8_1](/images/Mathematical_Electronic/3_8_1.jpg)
![3_8_2](/images/Mathematical_Electronic/3_8_2.jpg)

> #### 4.4.2.3 应用
![eg19](/images/Mathematical_Electronic/eg19.jpg)
![eg20](/images/Mathematical_Electronic/eg20.jpg)
{{< admonition type=info title="" open=false >}}
$D_i$是$A_i$和$B_i+C_{i-1}$的差关于2的模。  
$C_i$是借位标志。
{{< /admonition >}}
![eg21](/images/Mathematical_Electronic/eg21.jpg)

> #### 4.4.2.4 七段显示译码器(74HC4511)
![eg22](/images/Mathematical_Electronic/eg22.jpg)
![eg23](/images/Mathematical_Electronic/eg23.jpg)



> ### 4.4.3 数据选择器
数据选择器：能实现数据选择功能的逻辑电路。它的作用相当于多个输入的单刀多掷开关，又称“多路开关” 。  

数据选择的功能：在通道选择信号的作用下，将多个通道的数据分时传送到公共的数据通道上去的。

> #### 4.4.3.1 2选1数据选择器

![eg24](/images/Mathematical_Electronic/eg24.jpg)

> #### 4.4.3.2 4选1数据选择器

![eg25](/images/Mathematical_Electronic/eg25.jpg)
![eg26](/images/Mathematical_Electronic/eg26.jpg)
![eg27](/images/Mathematical_Electronic/eg27.jpg)
![eg28](/images/Mathematical_Electronic/eg28.jpg)

> #### 4.4.3.3 8选1数据选择器(74HC151)

![74hc151](/images/Mathematical_Electronic/74hc151.jpg)
![74hc151_g](/images/Mathematical_Electronic/74hc151_graph.jpg)
{{< admonition type=info title="" open=false >}}
L是低电平。  
H是高电平。
{{< /admonition >}}
![eg30](/images/Mathematical_Electronic/eg30.jpg)

> #### 4.4.3.4 数据选择器构成查找表LUT

![lut1](/images/Mathematical_Electronic/lut1.jpg)
![lut2](/images/Mathematical_Electronic/lut2.jpg)

> #### 4.4.3.5 利用数据选择器实现函数的一般步骤:（变量数=选通端数）
1. 将函数变换成最小项表达式
2. 选择输入信号S2、S1、S0作为函数的输入变量
3. 处理数据输入D0~D7信号电平。逻辑表达式中有$m_i$ ,则相应$D_i$ =1，其他的数据输入端均为0。当变量数>选通端数，考虑如何将某些变量接入数据端。
![eg29](/images/Mathematical_Electronic/eg29.jpg)


> ### 4.4.4 数值比较器

> #### 4.4.4.1 一位数值比较器

> ##### 4.4.4.1.1 真值表

|A| B| $F_{A>B}$| $F_{A=B}$| $F_{A<B}$|
|-| -| ----| ----| ----|
|0| 0| 0   | 0   | 1|
|0| 1| 0   | 1   | 0|
|1| 0| 1   | 0   | 0|
|1| 1| 0   | 0   | 1|

> ##### 4.4.4.1.2 表达式

$$
F_{A>B}=A\overline{B}
$$

$$
F_{A<B}=\overline{A}B
$$

$$
F_{A=B}=A\odot B
$$

> ##### 4.4.4.1.3 逻辑图

![1dcomp](/images/Mathematical_Electronic/1dcomp.png)

> #### 4.4.4.2 两位数值比较器

> ##### 4.4.4.2.1 真值表

A1      B1   |   A0     B0  |   $F_{A>B}$ |$F_{A<B}$| $F_{A=B}$|
-----|-|----|-----|------|
A1>B1        |   X          |    1   | 0  |  0|
A1<B1        |   X          |    0   | 1  |  0|
A1=B1        |   A0>B0      |    1   | 0  |  0|
A1=B1        |   A0=B0      |    0   | 0  |  1|
A1=B1        |   A0<B0      |    0   | 1  |  0|


> ##### 4.4.4.2.2 表达式

$$
F_{A>B}=F_{A1>B1}+F_{A1=B1} \cdot  F_{A0>B0}
$$

$$
F_{A<B}=F_{A1<B1}+F_{A1=B1} \cdot  F_{A0<B0}
$$

$$
F_{A=B}=F_{A1=B1} \cdot  F_{A0=B0}
$$

> ##### 4.4.4.2.3 逻辑图

![2dcomp](/images/Mathematical_Electronic/2dcomp.webp)

> #### 4.4.4.3 四位数据比较器

原理和二位比较器相同，从最高位到最低位一次比较。

![74hc85](/images/Mathematical_Electronic/74hc85.gif)

74HC85还有3个拓展输入端:$ I_{A>B},I_{A<B},I_{A=B}  $,可以与低位输出连接组成位数更多的比较器。

> ### 4.4.4.4 拓展

> ##### 4.4.4.4.1 串联

1. 有I端

![series](/images/Mathematical_Electronic/series.png)

先对低位进行比较，将比较结果输给高位的I端。再在高位进行比较。

2. 无I端

![series1](/images/Mathematical_Electronic/series1.jpeg)

> ##### 4.4.4.4.2 并联

![parallel](/images/Mathematical_Electronic/parallel.webp)

> ### 4.4.5 算术运算电路

> #### 4.4.5.1 半加器

只考虑了两个加数本身，而没有考虑低位进位的加法运算叫做半加。

> ##### 4.4.5.1.1 真值表

|A| B| C| S|
|-|--|--|--|
|0| 0| 0| 0|
|0| 1| 0| 1|
|1| 0| 0| 1|
|1| 1| 1| 0|

> ##### 4.4.5.1.2 表达式

$$
    S=A\oplus B
$$

$$
    C=AB
$$

> ##### 4.4.5.1.3 逻辑图


![half_adder](/images/Mathematical_Electronic/half_adder.jpg)

> #### 4.4.5.2 全加器

> ##### 4.4.5.2.1 真值表

|A| B| $C_i$| S| $C_O$|
|-|--|---|--|---|
|0| 0| 0 | 0| 0 |
|0| 0| 1 | 1| 0|
|0| 1| 0 | 1| 0|
|0| 1| 1 | 0| 1|
|1| 0| 0 | 1| 0|
|1| 0| 1 | 0| 1|
|1| 1| 0 | 0| 1|
|1| 1| 1 | 1| 1|

> ##### 4.4.5.2.2 表达式

$$
    S=A\oplus B \oplus C_i
$$

$$
    C_o=AB+(A\oplus B)C_i
$$

> ##### 4.4.5.2.3 逻辑图

![full_adder](/images/Mathematical_Electronic/full_adder.jpg)

> #### 4.4.5.3 串行进位多位加法器


![series_add](/images/Mathematical_Electronic/series_add.webp)

> #### 4.4.5.4 减法器

![substracter](/images/Mathematical_Electronic/substracter.jpg)

> ## 4.6 组合逻辑电路的行为级建模

> ### 4.6.1 if-else语句

![if_eg](/images/Mathematical_Electronic/if_eg.jpg)
```
module chooser_4(S,D,Y);
    input [1:0]S;
    input [3:0]D;
    output reg Y;
    always@(D,S)
        begin
            if(S==2'b00) Y=D[0];
            else if(S==2'b01) Y=D[1];
            else if(S==2'b10) Y=D[2];
            else Y=D[3];
        end
endmodule
```
{{< admonition type=warning title="" open=false >}}
注意，过程赋值语句只能给寄存器型变量赋值，因此，输出变量Y的数据类型定义为reg。
{{< /admonition >}}

> ### 4.6.2 case语句
{{< admonition type=info title="" open=false >}}
用关键词casex和casez表示含有无关项x和高阻z的情况。
{{< /admonition >}}
{{< admonition type=warning title="" open=false >}}
当分支项中的语句是多条语句，必须在最前面写上关键词begin，在最后写上关键词end，成为顺序语句块。
{{< /admonition >}}
> #### 4.6.2.1
对具有使能端$E_n$的4选1数据选择器行为进行Verilog描述。当$E_n$=0时，数据选择器工作，$E_n$=1时，禁止工作，输出为0。
```
module choose_4(S,D,Y,E);
    input [1:0] S;
    input [3:0] D;
    output reg Y;
    input E;
    always@(S,D,E)
    begin
        if(E==1'b1)
        begin
            case(S)
                2'b00:Y<=D[0];
                2'b01:Y<=D[1];
                2'b10:Y<=D[2];
                2'b11:Y<=D[3];
            endcase
        end
        else Y<=1'b0
    end
endmodule
```
> #### 4.6.2.2

对基本的4线-2线优先编码器的行为进行Verilog描述。
```
module coder_4_2(I,Y);
    input [3:0]I;
    output reg[1:0]Y;
    always@(I)
    begin
        casex(I)
            4'b1xxx:Y<=2'b11;
            4'b01xx:Y<=2'b10;
            4'b001x:Y<=2'b01;
            4'b0001:Y<=2'b00;
            default:Y<=2'bx;
        endcase
    end
endmodule
```

> ### 4.6.3 for语句
试用Verilog语言描述具有高电平使能的3线-8线译码器.
```
module trans_3_8(I,Y,E);
    input [2:0]I;
    input E;
    output reg[7:0]Y;
    integar k;
    always@(I,E)
    begin
        Y=8'b1111_1111;
        for(k=0;k<8;k=k+1)
        begin
            if(k==I&&E) Y[k]=0;
            else Y[k]=1;
        end
    end
endmodule
```

> ### 4.6.4 条件运算符
例：用条件运算符描述了一个2选1的数据选择器
```
module chooser_2_1(
    input [1:0]D;
    input sel;
    output reg Y;
);
    always@(D,sel)
    begin
        Y<=sel?D[1]:D[0];
    end
endmodule
```
```
module choose_2_1(
    input [1:0]D;
    input sel;
    output Y;
);
    assign Y<=sel?D[1]:D[0];
endmodule
```

> ### 4.6.5 模块化设计方法
分层次的电路设计:在电路设计中，将两个或多个模块组合起来描述电路逻辑功能的设计方法。

设计方法：自顶向下和自底向上两种常用的设计方法。

> #### 4.6.5.1 四位全加器
![eg31](/images/Mathematical_Electronic/eg31.jpg)

> ##### 4.6.5.1.1 半加器

![half_adder](/images/Mathematical_Electronic/half_adder.jpg)

```
module half_adder(A,B,S,C);
    input A,B;
    output reg S,C;
    always@(A,B)
    begin
        S<=A^B;
        C<=A&B;
    end
endmodule
```

> ##### 4.6.5.1.2 全加器

![full_adder](/images/Mathematical_Electronic/full_adder.jpg)

```
module full_adder(A,B,Ci,S,C0);
    input A,B,Ci;
    output S,C0;
    wire S1,D1,D2;
    half_adder HA1(A,B,S1,D1);
    half_adder HA2(S1,Ci,S,D2);
    or(C0,D1,D2);
endmodule
```

> ##### 4.6.5.1.3 四位全加器
![4badd](/images/Mathematical_Electronic/4badd.jpg)

```
module adder_4_dig(
    input [3:0]A,B;
    input CI;
    output [3:0]S,
    output CO
)
    wire [2:0]C;
    full_adder fa0(A[0],B[0],CI,S[0],C[0]);
    full_adder fa1(A[1],B[1],C[0],S[1],C[1]);
    full_adder fa2(A[2],B[2],C[1],S[2],C[2]);
    full_adder fa3(A[3],B[3],C[2],S[3],CO);
endmodule
```

> # 5 锁存器和触发器

> ## 5.1 双稳态电路

> ### 5.1.1 基本的双稳态电路
双稳态电路是锁存器和触发器的结构组成、功能实现的基础.

![bi_stable](/images/Mathematical_Electronic/bi_stable.jpg)



> ## 5.2 SR锁存器

> ### 5.2.1 基本SR锁存器

![sr1](/images/Mathematical_Electronic/sr1.jpg)

> #### 5.2.1.1 工作原理
1. 
![sr2](/images/Mathematical_Electronic/sr2.jpg)

1. 
![sr3](/images/Mathematical_Electronic/sr3.jpg)

1. 
![sr4](/images/Mathematical_Electronic/sr4.jpg)

1. 
![sr5](/images/Mathematical_Electronic/sr5.jpg)

> #### 5.2.1.2 真值表
![sr6](/images/Mathematical_Electronic/sr6.jpg)

> #### 5.2.1.3 变种
![sr7](/images/Mathematical_Electronic/sr7.jpg)

> #### 5.2.1.4 规律
![sr8](/images/Mathematical_Electronic/sr8.jpg)

> #### 5.2.1.5 运用
运用基本SR锁存器消除机械开关触点抖动引起的脉冲输出。
![sr9](/images/Mathematical_Electronic/sr9.jpg)

> ### 5.2.2 门控SR锁存器
![ensr](/images/Mathematical_Electronic/ensr.jpg)


> ## 5.3 D锁存器
> ### 5.3.1 电路结构
![D1](/images/Mathematical_Electronic/D1.jpg)
{{< admonition type=info title="" open=false >}}
没有圆圈的一侧是高电平的时候TG就是通路。
{{< /admonition >}}
> ### 5.3.2 逻辑功能
![d_func](/images/Mathematical_Electronic/d_func.jpg)


> ## 5.4 触发器的电路结构和工作原理

{{< admonition type=tip title="" open=false >}}
在逻辑图中触发器的时钟信号接口处有三角
{{< /admonition >}}

共同点：

具有0 和1两个稳定状态，一旦状态被确定，就能自行保持。一个锁存器或触发器能存储一位二进制码。

不同点：

锁存器---对脉冲电平敏感的存储电路，在特定输入脉冲电平作用下改变状态。

触发器---对脉冲边沿敏感的存储电路，在时钟脉冲的上升沿或下降沿的变化瞬间改变状态

![triggers](/images/Mathematical_Electronic/triggers.jpg)

> ### 5.4.1 D触发器

> #### 5.4.1.1 电路结构

两个D锁存器级联构成一个主从D触发器

主锁存器与从锁存器结构相同(但使能信号相反)

TG1和TG4的工作状态相同

TG2和TG3的工作状态相同

![locker1](/images/Mathematical_Electronic/locker1.jpg)

> #### 5.4.1.2 D触发器工作原理



1. CP=0时：

    TG1导通，TG2断开——输入信号D 送入主锁存器。

    Q'跟随D端的状态变化，使Q'=D

    TG3断开，TG4导通——从锁存器维持在原来的状态不变。

2. CP=1时：

    TG1断开，TG2导通——输入信号D 不能送入主锁存器。主锁存器维持原态不变。

    TG3导通，TG4断开——主锁存器Q'的信号送从锁存器Q端。使Q=D。

    触发器的状态仅仅取决于CP信号上升沿到达前瞬间的D信号！

> ##### 5.4.1.2.1 特性表

|D |$Q_n$| $Q_{n+1}$|
|--|-|-----|
|0 |0 |0|
|0 |1 |0|
|1 |0 |1|
|1 |1 |1|

> ##### 5.4.1.2.2 特性方程
$$ Q^{n+1} = D $$

> ##### 5.4.1.2.3 状态图

![d_pic](/images/Mathematical_Electronic/d_pic.jpg)

> ### 5.4.2 JK触发器

![jk_trigger](/images/Mathematical_Electronic/jk_trigger.jpg)

{{< admonition type=tip title="" open=false >}}
本质上JK触发器就是升级版的SR触发器，多了个翻转功能。
{{< /admonition >}}

> #### 5.4.2.1 工作原理

> ##### 5.4.2.1.1 特性表

|J |K |$Q_n$ |$Q_{n+1}$ |说明|
|--|--|---|-----|----|
|0 |0 |0  |0    |保持|
|0 |0 |1  |1    |保持|
|0 |1 |0  |0    |置0|
|0 |1 |1  |0    |置0|
|1 |0 |0  |1    |置1|
|1 |0 |1  |1    |置1|
|1 |1 |0  |1    |翻转|
|1 |1 |1  |0    |翻转|

> ##### 5.4.2.1.2 特性方程

$$ Q_{n+1} = J\overline{ Q_{n} } + \overline{K}Q_{n} $$

> ##### 5.4.2.1.2 状态转移图

![jk_pic](/images/Mathematical_Electronic/jk_pic.jpg)

> ### 5.4.3 T触发器

![T_trigger](/images/Mathematical_Electronic/T_trigger.jpg)

> #### 5.4.3.1 工作原理

> ##### 5.4.3.1.1 特性表

|T |Qn |Qn+1|
|--|---|----|
|0 |0  |0|
|0 |1  |1|
|1 |0  |1|
|1 |1  |0|

> ##### 5.4.3.1.2 特性方程

$$ Q_{n+1} = T\overline{ Q_{n} } + \overline{T}Q_{n} $$

> ##### 5.4.3.1.3 状态转移图

![t_pic](/images/Mathematical_Electronic/t_pic.jpg)

> ### 5.4.4 SR触发器

![sr_trigger](/images/Mathematical_Electronic/sr_trigger.jpg)

> #### 5.4.4.1 特性表

|Qn |S |R |Qn+1|
|---|--|--|----|
|0  |0 |0 |   0|
|1  |0 |0 |   1|
|0  |0 |1 |   0|
|1  |0 |1 |   0|
|0  |1 |0 |   1|
|1  |1 |0 |   1|
|0  |1 |1 |   x|
|1  |1 |1 |   x|

> #### 5.4.4.2 特性方程


$$Q_{n+1} = S + R\overline{ Q_{n} }$$
$$ SR = 0 $$

> #### 5.4.4.3 状态转移图

![sr_pic](/images/Mathematical_Electronic/sr_pic.jpg)

> ## 5.5 D触发器转换

> ### 5.5.1 D触发器构成JK触发器

![d2jk](/images/Mathematical_Electronic/d2jk.jpg)

> ### 5.5.2 D触发器构成T触发器

![d2t](/images/Mathematical_Electronic/d2t.jpg)

> # 6 时序逻辑电路

时序逻辑电路的工作特点是任意时刻的输出状态不仅与该当前的输入信号有关，而且与此前电路的状态有关。

> ## 6.1 时序逻辑电路的基本概念

> ### 6.1.1 时序逻辑电路的模型与分类

> #### 6.1.1.1 时序电路的基本结构

![time_circuit](/images/Mathematical_Electronic/time_circuit.jpg)

> #### 6.1.1.2 时序逻辑电路的分类

按状态变化分类：
1. 同步时序电路:电路状态的变化在同一时钟脉冲作用下发生，即存储电路里所有触发器有一个统一的时钟源，它们的状态在同一时刻更新。
2. 异步时序电路:没有统一的时钟脉冲或没有时钟脉冲，电路的状态更新不是同时发生的。
   
![classfication2](/images/Mathematical_Electronic/classfication2.jpg)

按输出信号分类：
1. 米利（Mealy）型时序电路:电路的输出是输入变量及触发器输出Q1、Q0 的函数，这类时序电路亦称为米利型电路
2. 穆尔（ Moore）型时序电路:电路输出仅仅取决于各触发器的状态，而不受电路当时的输入信号影响或没有输入变量，这类电路称为穆尔型电路

![classfication1](/images/Mathematical_Electronic/classfication1.jpg)
> ## 6.2 同步 时序逻辑电路的分析


> ### 6.2.1 逻辑方程组

输出方程: $O＝f_1(I,S)$

表达输出信号与输入信号、状态变量的关系式

激励方程: $E＝f_2(I,S)$ 

表达了激励信号与输入信号、状态变量的关系式

状态方程: $S^{n+1}＝f_3(E,S^n)$

表达存储电路从现态到次态的转换关系式

{{< admonition type=note title="" open=false >}}
状态方程是由激励方程和所用的触发器的类型决定的
{{< /admonition >}}

> #### 6.2.2 表达过程

1. 列出逻辑方程组
2. 根据方程组列出状态转换真值表
3. 将状态转换真值表化为转换表
4. 根据转换表得状态表
5. 根据状态表画状态转移图

> #### 6.2.2.1 例

![eg32](/images/Mathematical_Electronic/eg32.jpg)

1. 列出逻辑方程组：
   
   - 输出方程：$$X = Q_0\overline{ Q_1 }$$
                $$Y = \overline{A} ( Q_0 + Q_1 ) $$
   - 激励方程：$$ D_0 = A ( Q_0 + Q_1 ) $$
                $$ D_1 = A \overline{Q_0} $$
   - 状态方程：
        $$ 
        Q^{n+1}_{0} = A ( Q^{n}_0 + Q^{n}_1 ) 
        $$

        $$ 
        Q_{1}^{n+1} = A \overline{ Q_{0}^{n} } 
        $$
2. 根据方程组列出状态转换真值表:

|A| $Q_0^n$| $Q_1^n$| $Q_0^{n+1}$| $Q_1^{n+1}$| X| Y|
|-|----|----|------|------|--|--|
|0| 0  | 0  | 0    | 0    | 0| 0|
|0| 0  | 1  | 0    | 0    | 0| 1|
|0| 1  | 0  | 0    | 0    | 1| 1|
|0| 1  | 1  | 0    | 0    | 0| 1|
|1| 0  | 0  | 0    | 1    | 0| 0|
|1| 0  | 1  | 1    | 1    | 0| 0|
|1| 1  | 0  | 1    | 0    | 1| 0|
|1| 1  | 1  | 1    | 0    | 0| 0|


3. 将状态转换真值表化为转换表
   
![eg33](/images/Mathematical_Electronic/eg33.jpg)

4. 根据转换表得状态表

令$S^n$为$Q_0^nQ_1^n$，$S^{n+1}$为$Q_0^{n+1}Q_0^{n+1}$，4个状态为00=a，01=b，10=c，11=d，得：

![eg34](/images/Mathematical_Electronic/eg34.jpg)

5. 根据状态表画状态转移图
   
![eg35](/images/Mathematical_Electronic/eg35.jpg)


> ## 6.3 同步 时序逻辑电路的设计
{{< admonition type=note title="" open=false >}}
同步时序逻辑电路的设计是分析的逆过程,其任务是根据实际逻辑问题的要求，设计出能实现给定逻辑功能的电路。
{{< /admonition >}}
> ### 6.3.1 设计同步时序逻辑电路的一般步骤

> #### 6.3.1.1 根据给定的逻辑功能建立原始状态图和原始状态表

1. 明确电路的输入条件和相应的输出要求，分别确定输入变量和输出变量的数目和符号。
2. 找出所有可能的状态和状态转换之间的关系。
3. 根据原始状态图建立原始状态表。

> #### 6.3.1.2 状态化简-----求出最简状态图
合并等价状态，消去多余状态的过程称为状态化简

{{< admonition type=info title="" open=false >}}
等价状态：在相同的输入下有相同的输出，并转换到同一个次态去的两个状态称为等价状态。
{{< /admonition >}}

> #### 6.3.1.3 状态编码（状态分配）

给每个状态赋以二进制代码的过程。

$2^{n-1}$ < M $\leq 2^n$ （M:状态数;n:触发器的个数）

{{< admonition type=info title="" open=false >}}
状态编码的位数即为触发器的个数
{{< /admonition >}}


> #### 6.3.1.4 选择触发器的类型
> 
> #### 6.3.1.5 求出电路的激励方程和输出方程

> #### 6.3.1.6 画出逻辑图并检查自启动能力


> ## 6.5 若干典型的时序逻辑电路

> ### 6.5.1 寄存器和移位寄存器
在数字电路系统中，把需要处理的二进制数据或代码暂时存储起来，以便在需要的时候随时取用，这样的操作叫做寄存

> #### 6.5.1.1 8位CMOS寄存器74HC374

![74HC374](/images/Mathematical_Electronic/74HC374.jpg)

> #### 6.5.1.2 移位寄存器

移位寄存器是既能寄存数码，又能在时钟脉冲的作用下使数码在高低位之间移动的逻辑功能部件。

![reg_classfication](/images/Mathematical_Electronic/reg_classfication.jpg)

> ##### 6.5.1.2.1 基本移位寄存器

![move_reg](/images/Mathematical_Electronic/move_reg.jpg)

> ##### 6.5.1.2.2 多功能双向移位寄存器

![74hc194](/images/Mathematical_Electronic/74HC194.jpg)

![74hc194_tab](/images/Mathematical_Electronic/74hc194_tab.jpg)

> ### 6.5.2 计数器

计数器的基本功能是对输入时钟脉冲进行计数。它也可用于分频、定时、产生节拍脉冲和脉冲序列及进行数字运算等等。

> #### 6.5.2.1 二进制计数器

![bi_cnt](/images/Mathematical_Electronic/binary_counter.jpg)

{{< admonition type=note title="" open=false >}}
$Q_0$在每个CP都翻转一次，$FF_0$可采用T=1的T触发器。  
$Q_1$仅在$Q_0$=1后的下一个CP到来时翻转，$FF_1$可采用T= $Q_0$的T触发器。  
$Q_2$仅在$Q_0$=$Q_1$=1后的下一个CP到来时翻转。$FF_2$可采用T= $Q_0Q_1$的T触发器。  
$Q_3$仅在$Q_0$=$Q_1$=$Q_2$=1后的下一个CP到来时翻转。$FF_3$可采用T= $Q_0Q_1Q_2$的T触发器。
{{< /admonition >}}

![4d_bi_cnt](/images/Mathematical_Electronic/4d_bi_cnt.jpg)

> ##### 6.5.2.1.1 74LVC161

{{< admonition type=info title="" open=false >}}
一个变量与0异或等于本身，与1异或等于它的取反。
{{< /admonition >}}

![4d_bi_cnt1](/images/Mathematical_Electronic/4d_bi_cnt1.jpg)

![74LVC161](/images/Mathematical_Electronic/74LVC161.PNG)

用74LVC161构成九进制加计数器:

1. 反馈清零法：利用异步置零输入端，在M进制计数器的计数过程中，跳过M-N个状态，得到N进制计数器的方法。
   
   ![9D74LVC161](/images/Mathematical_Electronic/9D74LVC161.PNG)

2. 反馈置数法:利用同步置数端，在M进制计数器的计数过程中，跳过M-N个状态，得到N进制计数器的方法。

    ![9D74LVC161_1](/images/Mathematical_Electronic/9D74LVC161_1.PNG)
    
用74VC161组成256进制计数器:

1. 并行进位：低位片的进位作为高位片的使能
   
   ![256cnt1](/images/Mathematical_Electronic/256cnt1.PNG)

2. 串行进位：低位片的进位作为高位片的时钟

   ![256cnt2](/images/Mathematical_Electronic/256cnt2.PNG)

{{< admonition type=info title="" open=false >}}
如果不加反相器，00001110的下个状态不再是00001111而是00011111。加了反相器使得00001110的下个状态时00001111，然后00001111的下个状态是00010000。
{{< /admonition >}}


> ## 6.7 用Verilog HDL描述时序逻辑电路

> ### 6.7.1 移位寄存器

用行为级描述always描述一个４位双向移位寄存器，有异步清零、同步置数、左移、右移和保持。功能同74HC194。

```
module reg4(clk,clr,S,data,left0,right0,en,Q);

    input clk,clr,left0,right0,en;
    input [1:0] S;
    input [3:0] data;
    output reg [3:0] Q;
    always@(posedge clk or posedge clr)
    begin
        if(clr) Q<=4'b0000;
        else if(en)
        begin
            case(S)
            2'b00: Q<=Q;
            2'b01: Q<={Q[2:0],right0};
            2'b10: Q<={left0,Q[3:1]};
            2'b11: Q<=data;     
            endcase
        end
    end
endmodule
```

> ### 6.7.2 计数器

用Verilog描述带使能端和同步置数端的可逆4位二进制计数器

```
module counter(clk,en,set,data,Q,flag);
    input en,set,flag;
    input [3:0] data;
    output reg [3:0] Q;
    always@(posedge clk)
    begin
        if(!en) Q<=Q;
        else if(set) Q<=data;
        else if(flag==1) Q<=Q+1;
        else Q<=Q-1;
    end
endmodule

```

> ### 6.7.3 状态转换图

![eg36](/images/Mathematical_Electronic/eg36.jpg)

```
module loop(A,Y,clk,clr);
    parameter S0=2'b00,S1=2'b01,S2=2'b11;
    input A,clk;
    reg [1:0] cur,next;
    output reg Y;
    always@(posedge clk,negedge clr)
    begin
        if(clr) cur<=S0;
        else if(clk) cur<=next;
    end
    always@(posedge clk)
    begin
        Y<=0;
        case(cur)
            S0: next<=A?S1:S2;
            S1: next<=A?S0:S2;
            S2: if(A) next<=S2;
                else begin next<=S0;Y<=1;
            default: next<=S0;
        endcase
    end
endmodule

```

> # 7 半导体存储器


> ## 7.1 只读存储器 (ROM）

ROM是一种永久性数据存储器，其中的数据一般由专用的装置写入，数据一旦写入，不能随意改写，在切断电源之后，数据也不会消失。

ROM主要由地址译码器、存储矩阵和输出控制电路三部分组成。

![rom_struct](/images/Mathematical_Electronic/rom_struct.jpg)

> ### 7.1.1 基本概念

1. 存储容量（M)：存储单元的数目。
2. 字：存储器中作为一个整体被存取传送处理的一组数据 。
3. 字长：一个字所含的位数称为字长。
4. 字数：字的总量。
5. 地址线个数/地址码位数n：字数=$2^n$
6. 数据位数=位数。

例：容量为64K ×1的存储系统有多少个存储单元？其地址码需要几位？数据位是几位？

存储单元数=字数×位数=64K×1=64K个=$2^{16}$个

地址线数：

因为字数为64K=$2^{16}$个，即n=16，所以地址线数为16位而数据线数等于位数，故数据线为1位

{{< admonition type=info title="" open=false >}}
1K=1024=$2^{10}$  
1M=1024K=$2^{20}$  
1G=1024M=$2^{30}$
{{< /admonition >}}

> ## 7.2 随机存取存储器 (RAM)

在正常工作状态只能读出信息。断电后信息不会丢失，常用于存放固定信息(如程序、常数等)。

> ### 7.2.1 静态随机存取存储器(SRAM)

![sram](/images/Mathematical_Electronic/sram.jpg)

![sram_workmode](/images/Mathematical_Electronic/sram_workmode.jpg)

> ### 7.2.3 动态随机存取存储器(DRAM)

![dram](/images/Mathematical_Electronic/dram.jpg)

> #### 7.2.3.1 写操作

X=1 $\overline{WE}$=0  T导通，电容器C与位线B连通。

输入缓冲器被选通，数据$D_I$经缓冲器和位线写入存储单元如果$D_I$为1，则向电容器充电，C存1;反之电容器放电,C存0 。

> #### 7.2.3.2 读操作

X=1 $\overline{WE}$=1

T导通，电容器C与位线B连通

输出缓冲器/灵敏放大器被选通，C中存储的数据通过位线和缓冲器由D0输出

每次读出后，必须及时对读出单元刷新，即此时刷新控制R也为高电平，则读出的数据又经刷新缓冲器和位线对电容器C进行刷新。





