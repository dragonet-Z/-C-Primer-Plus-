[Toc]  
开始做做笔记，加油！
注：所有笔记基于书内容和我的理解，就挑一些重点记下来，如果大家发现不对的地方欢迎指出嗷~
# 第一章 初识C语言
## 1 使用C语言的7个步骤
### 1.1 定义程序目标
其实就是先要做好整个项目的大纲，作用就如同创业的计划书一般重要
>我通常是分为三步：这个项目要达到什么功能、功能如何实现、维护代码，没想到书居然写的那么详细
### 1.2 设计程序（功能实现）
知道程序要完成的任务之后，就要考虑如何通过程序去实现它
### 1.3 编写代码
就是按图索骥的将第二步的那些功能用代码表达出来
### 1.4 编译
编译源代码，编译器将源代码转换成可执行代码（可执行代码指用计算机的机器代码表示的代码）
### 1.5 运行程序
可执行文件就是可运行的程序，在windows上是exe程序（命令提示符模式）
### 1.6 测试和调试程序
程序错误称为bug，查找并修复程序错误的过程和调试
### 1.7 维护和修改代码
拓展程序的功能或者用一个更好的解决方案，这时候就需要维护和修改你的代码
>第一步和第二步其实是很重要的，代码永远不是目的，不要为了写代码而写代码哦！
## 2 windows下集成开发环境
>暂时只用windows系统，我相信就人机交互和易用程度来说，windows还是可圈可点的  

Windows IDE选择的是Microsoft Visual Studio 2015
通常来说都是用【Win32 控制台应用程序】
尝试运行个Hello.c
```C
#include <stdio.h>

int main()
{
    printf ("Hello,World!");
    return 0;
}
```
在这个程序编译和运行都没有问题，但是程序都是一闪而过
这个时候，你可以用两种方法来解决这个问题
1. ```system ("pause")```，作用是暂停程序
    这个方法需要添加头文件stdlib.h，然后将这个语句加在return语句前
    搞定之后程序代码是这样的
    ```C
    #include <stdio.h>
    #include <stdlib.h>

    int main()
    {
        printf ("Hello,World!");
        system("pause");
        return 0;
    }
   ```
   运行结果
   ![]()
2. ```getchar()```，作用是击键等待
    这个方法不需要添加头文件
    通常来说一个getchar()已经足够，实际运行的时候则需要根据程序需要来多一个
    改定之后程序代码是这样的
    ```C
    #include <stdio.h>

    int main()
    {
        printf("Hello,World!");
        getchar();
        return 0;
    }
    ```
    运行结果
    ![]()
    在回车后程序就会直接消失~  

# 第二章 C语言概述
## 1 示例程序1
```C
#include <stdio.h>

int main (void)
{
    int num;
    num = 9;

    printf ("I have %d apple.\n",num);

    return 0;
}
```
### 1.1 程序讲解

![]()

#### 1.1.1 头文件
相当于将stdio.h的文件内所有内容都“黏贴”到该行的位置
```#include```是C语言的预处理器指令
所有的C编译器都会提供```stdio.h```，std代表的是“标准”,io代表的是输入/输出，.h后缀代表它是个头文件，这个文件的含义就是**标准输入/输出头文件**

#### 1.1.2 main函数
如流程图所示，main函数**总是第一个被调用的函数**，每个工程都需要有一个main函数，C程序一定是从main函数开始执行！
int表示了main函数的返回数类型是整型，通常来说，函数名后的圆括号内会包含一些传入函数的参数，该程序中没有传递参数，则加个void在括号内
你可能在VC++6.0之类的编译器可能看过这样子的main函数```void main()```，注意哦，C标准中**从未定义**过void main，不建议大家来搞这种作死的行为😂

#### 1.1.3 注释
```C
    /*这是个简简单单的注释*/
    /*
    这是个简简单单的注释
    */
```
注释可以说是非常方便的功能了，好的注释可以让你和其他人来更好地理解你的代码和逻辑
C99增加了一种新的注释方法，普遍用于C++和java
```C
//这是另一种新的注释，只适用于单行
int nb;
int a; //也可以用在这里
```

#### 1.1.4 花括号、声明
一般来说，所有C函数都会使用花括号{}来标记函数的开始和结束，且只有花括号有这种功能
声明：```int num;```这行代码叫声明，它表达了两个意思，定义了一个名为num的变量、定义了num的数据类型为int整型
int 是C语言的一个关键字（后续会讲解关键字）
num 是一个标识符，通过声明，我们可以把特定的标识符和计算机内存中的特定位置联系起来
C99和C11遵循C++的管理，可以把声明放在块中的任意位置
```C
int a;
a = 1;
…………
…………
int b;
b = 999;
```
标识符的命名规则
可以用小写字母、大写字母、数字、下划线(_)来命名，且名称的第一个字符必须是字母或者下划线，示例如下  
| 有效的名称 | 无效的名称 |
| :--------: | :--------: |
|  wiggles   |   $z]**    |
|    cat2    |    2cat    |
|  Hot_Tub   |  Hot-Tub   |
|  taxRate   |  tax rate  |
|   _kcab    |   don't    |

#### 1.1.5 赋值、printf函数、return语句
```num = 1;```赋值是C语言的基本操作之一，这行代码的意思是将1这个值赋给num变量
printf函数是C语言的一个标准函数，```printf ("I have an apple");```如这一句，冒号中的内容就是**参数**，而且是**实际参数（实参）**，形参则是函数中来储存值的变量
```printf ("apple is great\n");```在这句的输出中并不会看见```\n```，\n代表换行符，作用和键盘按下Enter键一样。换行符是*转义序列*的一种，转义序列常用于无法直接输入或难以表达的字符，如\t代表Tab键，\b代表Backspace键，转义字符都从反斜杠开始(\)
```printf ("He have %d apple",a);```在这句中的输出中我们会看到%d的位置上出现了a的值，这是因为%d可以将变量作为十进制整数打印
return语句：所有有返回值的C函数都要有return语句，如果遗漏了main函数的return函数，程序在运行至}的时候会自动返回0，希望大家养成有返回值函数后面就有return语句的好习惯。

---
## 2 示例程序2 
```C
#include <stdio.h>
int sixtimes(int times);
int main(void)
{
    int feet,fathoms;
    fathoms = 2;
    feet = sixtimes(fathoms);
    printf ("There are %d feet in %d fathoms\n",feet,fathoms);
    printf ("Yes,I said %d feet",6*fathoms);
}

int sixtimes(int times)
{
    return 6*times;
}
```

### 2.1 程序讲解

#### 2.1.1 多条声明
```int feet,fathoms;```函数在一行代码中声明了两个函数，这种声明等价于
```C
int feet;
int fathoms;
```

#### 2.1.2 多个函数
我们可以看见```sixtime()```函数出现了三次，分别是声明、调用和定义
*函数声明*:我们直接复制函数头部，加个分号即可
*函数的调用*：跟之前说的printf函数类似，fathoms作为实参，times作为形参，feet得到sixtimes的返回值
*函数定义*：形式与main函数相似，都是函数名、花括号之类的。注：何时执行sixtimes函数取决于它在main函数中调用的位置，而非他在文件中的位置

## 3 关键字和保留标识符
<center>ISO C关键字</center>  

|   auto    |  extern  |    short     |        while         |
| :-------: | :------: | :----------: | :------------------: |
|   break   |  float   |  **signed**  |    ***_Alignas***    |
|   case    |   for    |    sizeof    |    ***_Alignof***    |
|   char    |   goto   |    static    |    ***_Atomic***     |
| **const** |    if    |    struct    |     ***_Bool***      |
| continue  | *inline* |    switch    |    ***_Complex***    |
|  defalut  |   int    |   typedef    |    ***_Generic***    |
|    do     |   long   |    union     |   ***_Imaginary***   |
|  double   | register |   unsigned   |   ***_Noreturn***    |
|   else    | restrict |   **void**   | ***_Static_assert*** |
| **enum**  |  return  | **volatile** | ***_Thread_local***  |
粗斜体的关键字（最右边的整列）是在C11标准中提出的
斜体的关键字是在C99标准中提出的
粗体的关键字是在C90标准中提出的
>注：关键字不可以用来做标识符哦
---
# 第三章 数据与C

## 1 示例程序
```C
/* platinum.c  -- your weight in platinum */
#include <stdio.h>
int main(void)
{
    float weight;    /* 你的体重             */
    float value;     /* 相等重量的白金价值     */
    
    printf("Are you worth your weight in platinum?\n");
    printf("Let's check it out.\n");
    printf("Please enter your weight in pounds: ");
    
    /* 获取用户输入                     */
    scanf("%f", &weight);
    /* 假设白金的价格是每盎司$1700          */
    /* 14.5833用于将英镑常衡盎司换成金衡盎司 */
    value = 1700.0 * weight * 14.5833;
    printf("Your weight in platinum is worth $%.2f.\n", value);
    printf("You are easily worth that! If platinum prices drop,\n");
    printf("eat more to maintain your value.\n");
    
    getchar();
    getchar();
    return 0;
}
```

### 1.1 程序讲解
1. ```float weight;```建立了新的浮点数类型的变量，已处理更大范围的数据，可以带小数的数字
2. 为了打印float类型的变量，printf函数采用%f来处理浮点数。%.2f之类的可以精准控制输出的位数
3. scanf()用于读取键盘的输入。通过%f可以读取到用户输入的浮点数，&weight告诉scanf()将输入值赋给名为weight的变量，scanf()通过&符号找到weight变量的地址

位、字节、字
位(bit)是最小的储存单元，可以储存0和1，位是计算机内存的基本构建块
字节(byte)是常用的计算机储存单位，字节的标准定义是1字节为8位
字(word)是设计计算机时给定的自然储存单位

## 2 C语言基本数据类型

### 2.1 int类型

#### 2.1.1 声明
第二章已经讲解过int声明整型变量，就是int后面加个变量名和分号，如果有多个变量声明的话，可以在同一条声明中声明这些变量，如```int hogs,cows,goat;```等

#### 2.1.2 初始化
所谓初始化其实就是赋给变量一个初始值，C语言中，初始化和声明可以放在一起，如```int a = 999;```等

#### 2.1.3 打印
可以用printf函数打印int类型的值，在第二章中介绍过，%d指明了打印整数的位置，%d称为*转换说明*，在实际使用时，应注意%d和变量个数要相同，编译器可能不会捕获这种错误

#### 2.1.4 整数溢出
ISO C规定的int 取值范围最小为-32768~32767(即大小为2^16)
16位unsigned int 的取值范围时0~65535

```C
/* toobig.c-exceeds maximum int size on our system */
#include <stdio.h>
int main(void)
{
    int i = 2147483647;
    unsigned int j = 4294967295;
    
    printf("%d %d %d\n", i, i+1, i+2);
    printf("%u %u %u\n", j, j+1, j+2);
    // %u代表这是unsigned int 类型的值
    getchar();
    return 0;
}
```
程序的输出效果如图：
![]()
这个程序里面，i和j变量都超过了规定的最大值，当他们达到能表示的最大值时，会重新从起始点开始

### 2.2 char类型

#### 2.2.1 声明

声明方式与int的类似，声明的示例：

```C
char response;
char itable, latan;
```
#### 2.2.2 字符常量和初始化

如果想将一个字符常量初始化为字母A，则可以用```char grade =  'A';```做到
在C语言中，单引号(')括起来的单个字符称为*字符常量*
```C
char a;
a = 'T';   //此时的T是一个字符常量
a = T;    //此时的T是一个变量
a = "T";    //此时的T是一个字符串（后续章节会讲）
```

#### 2.2.3 非打印字符
浏览ASCⅡ码可知，有一些字符是打印不出来的，例如一些代表行为的字符（换行、退格、蜂鸣等）
使用特殊符号序列表示一些特殊的字符，这种符号序列称为转义序列，下面列出一些转义序列
<center>转义序列</center>

|   转义序列   |                             含义                              |
| :----------: | :-----------------------------------------------------------: |
|      \a      |                        警报（ANSI C）                         |
|      \b      |                             退格                              |
|      \f      |                             换页                              |
|      \n      |                             换行                              |
|      \r      |                             回车                              |
|      \t      |                          水平制表符                           |
|      \v      |                          垂直制表符                           |
| \\|反斜杠(\) |
|      \'      |                            单引号                             |
|      \"      |                            双引号                             |
|      \?      |                             问号                              |
|     \0oo     | 八进制值 (hh必须是有效的2十六进制数，即每可表示0~f中的一个数) |
|     \xhh     | 十六进制数 (oo必须是有效的八进制数，即每个o可表示0~7中的一个) |




#### 2.2.4 打印字符

```C
#include <stdio.h>
int main (void)
{
    char ch;

    printf ("Please enter a character.\n");
    scanf ("%c",&ch);
    printf ("The code for %c is %d.\n", ch, ch);

    getchar();
    getchar();
    return 0;
}
```

该程序输出结果是
Please enter a character
A
The code for A is 65.

由此可见，%c可以打印一个字符，而%d可以打印字符对应的ASCⅡ码
有符号char范围是-128~127，无符号char范围是0~255

### 2.3 float、double、long double类型
C语言中的浮点数类型有float、double和long double类型，浮点数的表示方法有科学计数法、指数计数法等等，下面列出一些示例











































