# 2022年西南交通大学计算机与人工智能学院转专业机考试题



{{< admonition type=note title="Attention" open=false >}}
由于2022年考核形式特殊，不具备普适性，本文对试卷原题略有修改，使其与一般情况下OJ模式吻合。
{{< /admonition >}}
{{< admonition type=warning title="Warning1" open=false >}}
本人能力有限，代码可能有错误。若读者发现欢迎联系我指出！
{{< /admonition >}}
{{< admonition type=warning title="Warning2" open=false >}}
机考和ACM、蓝桥杯之类的编程比赛有差别，不是通过了测试点就得分。改卷老师会参考代码的具体书写情况。极不推荐考生使用qsort、bsearch等库函数图方便！
{{< /admonition >}}
> ## 1.序列生成
> ### 题目要求


写程序,在屏奉上打印出如下序列的前100项。(20 分)

1. 序列的第一、二项分别为2和3:

2. 序列后继项如下生成:

- 若序列的最后两项的乘积为一位数,则该一位数即为后续项:
- 若序列的最后两项的乘积为两位数,则该两位数的十位数字和个位数字分别为后续项的连续两项。
  
要求输出格式为"%2d",每行输出 10 个数,共10 行

解决思路：建立一个一位数组，从第三个元素开始遍历，每个元素的值都取决于前两个元素的乘积。

测试输入：
```
无
```
测试输出：
```
 2 3 6 1 8 8 6 4 2 4
 8 3 2 6 1 2 2 4 8 3
 2 6 1 2 2 4 8 3 2 6
 1 2 2 4 8 3 2 6 1 2
 2 4 8 3 2 6 1 2 2 4
 8 3 2 6 1 2 2 4 8 3
 2 6 1 2 2 4 8 3 2 6
 1 2 2 4 8 3 2 6 1 2
 2 4 8 3 2 6 1 2 2 4
 8 3 2 6 1 2 2 4 8 3
```

Source Code:
```c
#include<stdio.h>
#include<stdlib.h>
#pragma warning(disable:4996)
#define _for(a,b,c) for(a=b;a<c;++a)
int main(void)
{
	int arr[105] = { 2,3 },i,t;
	_for(i, 2, 100) {
		t = arr[i - 1] * arr[i - 2];
		if (t < 10) arr[i] = t;
		else arr[i] = t / 10,arr[++i]=t%10;
	}
	_for(i, 1, 101) {
		printf("%2d", arr[i - 1]);
		if ( !(i % 10)) putchar('\n');
	}
	return 0;
}
```

> ## 2.字符串除重
> ### 题目要求

从键盘输入一个字符串(长度不超过80个字符),将串中连续相同的字符只保留一个并生成新的字符串,最后输出生成的新字符串,要求定义函数 void cvt(char* s,char* t)实现操作输入输出格式 %s”。(20 分)

测试输入: 
```
aabbcccstbbbba
```
测试输出:
```
abcstba
```
解决思路：定义前置字符ch=s[0],从i=1开始遍历，若s[i]!=ch则t的最后一项=s[i]同时ch=s[i]，否则略过

Source Code:
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#pragma warning(disable:4996)
#define _for(a,b,c) for(a=b;a<c;++a)
#define MAXN 85
void cvt(char* s, char* t);
int main(void)
{
	//freopen("d:\\test.txt", "r", stdin);
	char str[2][MAXN] = { 0 };
	scanf("%s", str[0]);
	cvt(str[0], str[1]);
	printf("%s", str[1]);
	return 0;
}
void cvt(char* s, char* t)
{
	char ch =*(t++) =*(s++);
	while (*s)
	{
		if (ch != *s)
		{
			ch = *s;
			*(t++) = ch;
		}
		++s;
	}
}
```

> ## 3.矩阵排序
> ### 题目要求

给定m行n列整数矩阵,编写函数,以该矩阵作为参数(假定m,n 己用define 定义为整型常量),实现如下要求:(20 分) 
    
1. 每行元素按由小到大顺序存储;  
1. 各行以第1列元素为关键字,按该关键字由小到大次序存储各行； 
1. 要求只写出函数(不要求实现矩阵的输入与输出),可以定义其它辅助函数。 
   示例矩阵:3-5 12 -7 函数处理后矩阵:19 0 5 5 8 2 10 6
153 12 49 550
2 68 10

测试输入: 
```
无
```
测试输出:
```
-9   0   5   5
-7  -5   3  12
-2   6   8  10
```
解决思路：先单独对数组的每一行排序，再根据每行首元素大小对行排序（通过交换两行中每个相同位置的元素实现行的交换）。

裁判程序:
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#pragma warning(disable:4996)
#define _for(a,b,c) for(a=b;a<c;++a)
#define m 3
#define n 4
void reshape(int matrix[m][n]);
void prtma(int matrix[m][n])
{
	int i, j; _for(i, 0, m) {
		_for(j, 0, n) {
			printf("%2d", matrix[i][j]);
			if (j < n - 1) putchar('  ');
			else putchar('\n');
		}
	}
}
int main(void)
{
	//freopen("d:\\test.txt", "r", stdin);
	int matrix[m][n] = { 3,-5,12,-7,8,-2,10,6,-9,5,5,0 };
	reshape(matrix);
	prtma(matrix);
	return 0;
}

//your source code here:

```

Source Code:
```c
void reshape(int matrix[][n])
{
	int i,j,k; _for(k, 0, m) {
		_for(i, 1, n) {
			int t = matrix[k][i];
			for (j = i - 1; j >= 0; --j) {
				if (matrix[k][j] > t) matrix[k][j + 1] = matrix[k][j];
				else break;
			}
			matrix[k][j + 1] = t;
		}
	}
	_for(i, 1, m) {
		int t = matrix[i][0];
		for (j = i - 1; j >= 0; --j) {
			if (matrix[j][0] > t) {
				int t1;
				_for(k, 0, n) {
					t1 = matrix[j][k];
					matrix[j][k] = matrix[j + 1][k];
					matrix[j + 1][k] = t1;
				}
			}
			else break;
		}
	}
}
```

> ## 4.递归计算
> ### 题目要求

给定自然数n,函数f(n)定义如下：

f(0)=0,

f(1)=1,

f(2n)=f(n)

f(2n+1)=f(n)+f(2n-1)

1. 定义递归函数，计算f(n).(10分)
1. 定义非递归函数，计算f(n).(10分)

测试输入：
```
1984
```
测试输出：
```
69
```
解决思路：

递归函数按照题目要求即可，非递归函数可建立一个数组从i=2开始递推。

裁判程序：
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#pragma warning(disable:4996)
#define _for(a,b,c) for(a=b;a<c;++a)
long long func(int n);
int main(void)
{
	//freopen("d:\\test.txt", "r", stdin);
	int n; scanf("%d", &n);
	printf("%lld", func(n));
	return 0;
}

//your source code here:
```

1. Source Code:
```c
long long func(int n)
{
	if(n<2) return n;
	if (n % 2) return func(n / 2) + func(n - 2);
	else return func(n / 2);
}
```
2. Source Code:
```c
long long func(int n)
{
	static long long dp[10005] = { 0,1 };
	if (n < 2) return n;
	else {
		int i; _for(i, 2, n + 1) {
			if (i % 2) dp[i] = dp[i / 2] + dp[i - 2];
			else dp[i] = dp[i / 2];
		}
		return dp[n];
	}
}
```

> ## 5.处理学生成绩文件
> ### 题目要求
通过文件"a.txt"输入若干行学号、姓名、成绩，将每个学生信息存储于单向链表结点，要求节点连接次序为成绩由大到小次序。将结点按连接次序输出到文件"b.txt"。

测试输入文件"a.txt"（数据的分隔符为空格和换行）：
```
1001 张三     72
1002 王晓华   80
1003 Alice   55
1004 欧阳文修 95
```
测试输出文件"b.txt":
```
1004 欧阳文修 95
1002 王晓华 80
1001 张三 72
1003 Alice 55
```

解题思路：输入完一个结点，就把这个结点插入到链表的正确位置，这样输入完后链表就是有序的，就可以直接输出到b文件。

{{< admonition type=failure title="Wrong answer" open=false >}}
据改卷老师说法，此题不能采用先把结点排好序再连成链表，或者先连成链表再在链表上排序的做法。
{{< /admonition >}}

Source Code:
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#pragma warning(disable:4996)
#define _for(a,b,c) for(a=b;a<c;++a)
typedef struct node {
	int id, grd;
	char name[25];
	struct node* next, * last;
}node;
typedef struct list { node* head; }list;
list* crtl();
node* crtn(int id, int grd, char* n);
void clear(list* l);
int main(void)
{
	FILE* fp = fopen("d:\\a.txt", "r");
	list* L = crtl(); int id, grd; char tn[25]; node* p;
	while (fscanf(fp, "%d %s %d", &id, tn, &grd) != EOF)
	{
		node* newn = crtn(id, grd, tn);
		for (p = L->head; p->next && p->next->grd > grd; p = p->next);
		newn->next = p->next;
		p->next = newn;
	}
	fclose(fp);fp = fopen("d:\\b.txt", "w");
	p = L->head->next;
	while (p) {
		fprintf(fp, "%d %s %d\n", p->id, p->name, p->grd);
		p = p->next;
	}
	fclose(fp);clear(L);
	return 0;
}
list* crtl()
{
	list* L = (list*)malloc(sizeof(list)); L->head = crtn(0, 0, "H");
	return L;
}
node* crtn(int id, int grd, char* n)
{
	node* ret = (node*)malloc(sizeof(node));
	ret->id = id, ret->grd = grd;
	strcpy(ret->name, n);
	ret->next = ret->last = NULL;
	return ret;
}
void clear(list* l)
{
	node* p = l->head, * t;
	while (p) {
		t = p; p = p->next;
		free(t);
	}
	free(l);
}
```
