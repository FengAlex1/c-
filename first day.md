# first day

## 1.1hello world

```c
#include <stdio.h>// #include的意思是“包含”，包含stdio.h的文件
                  //stdio -standard input output标准输入输出 （std-standard）（i-input）（o-output）。

//int就是整型的意思；main前面的int表示main函数调用以后返回一个整型值。
int main()//主函数-main，是程序的入口，main函数有且有一个；
{
	printf("hello,cccc\n");//等于print function--打印函数, "\n" 表示输出后换行
	//printf是库函数，是C语言本身提供给我们使用的函数。所以要调用 #include <stdio>
	return 0;//return就是返回的意思，返回整数0。
}

```

## 1.2数据类型

```c
char         //字符数据类型
short        //短整型 
int          //整型
long         //长整型
long long    //更长整型
float        //单精度浮点数
double       //双精度浮点数
 
  //%c--打印字符
  //%d--打印整型
  //%f--打印浮点数字
  //%p--以地址的形式打印
  //%x--打印16进制数字
    
 //char-字符类型
 int main()
{
    char ch ='A';//内存
    printf("%c\n",ch);// %c--打印字符格式的数据,打印结果为：A
    return 0;
}

//int--整型
int main()
{
    int age=20;
    printf("%d\n",age);//  %d--打印整型十进制数据，打印结果为:20
    return 0;
}

//short int--短整型

//long--长整型
int mian()
{
    long num=100;
    printf("%d\n",num);打印结果也是：100
    return 0;
}

//float--单精度浮点类型
int main()
{
    float f = 2.0;
    printf("%f\n", f);//打印结果为：5.00000。float类型能包含五个小数点。
    return 0;
}

//double--双精度浮点类型
int main()
{
    double f = 3.14;
    printf("%f\n", f);//这里的打印可以用 %f，但是最好还是使用 %lf，表示使用双精度打印。
    return 0;
}

//计算各个类型占用空间
int main()
{
    printf("%d\n", sizeof(char));//1
    printf("%d\n", sizeof(int));//4
    printf("%d\n", sizeof(long));//4，long可以是4 or 8.
    printf("%d\n", sizeof(short));//2
    printf("%d\n", sizeof(long long));//8
    printf("%d\n", sizeof(float));//4
    printf("%d\n", sizeof(double));//8
    short int age=20//short对应两个字节，也就是16个bit位。2^16-1=65535。
        //如果数据不是很大推荐使用小整型，bit位越少，越能节省空间。
}//打印出来的这些数字就是“byte--字节”

#include <stdio.h>
int main()
{
    //    年龄 20
    short age = 20;//向内存申请2个字节=16bit位，用来存放20
    float weight = 95.6f;//可能系统会报错，把95.6当作双精度浮点归到double类型；在95.6后面加一个“f”，说明为单精度浮点即可解决。
                         //向系统申请4个字节，存放小数。据C语言标准 sizeof(long) >= sizeof(int),根据平台不同，long可能是4或8.
    return 0;
}
```

计算机中的单位
bit-比特位 < byte-字节 < kb < mb < gb < tb < pb 

一个bit（比特位）只能存放一个 0或1。

1byte=8bit

1kb=1024byte

1mb=1024kb

1tb=1024mb

1pb=1024mb



## 1.3 变量、常量

生活中有些值是不会变的（圆周率，身份证号，血型，性别等等）

有些值是可以变的（年龄，体重，薪资等）



### 1.3.1 定义变量的办法

类型  + 变量名 + 赋值

```c
int age=150
float weight=45.5f
char ch='w'
```



### 1.3.2 变量的分类

- 局部变量
- 全局变量

```c
#include <stdio.h>
int num2=20;//全局变量--定义在“代码块（{}）”之外的变量
int main()
{
    int num1=10;//局部变量--定义在“代码块（{}）之内的变量”
    return 0;
}

int a = 20;
int main()
{
    int a = 10;
    printf("%d\n", a);//打印结果为：10
    return 0;
}//局部变量名和全局变量名相同时，不会有冲突，但是局部变量优先。
//建议全局变量和局部变量的名字不要相同，容易产生bug。
//局部变量只能在自属局部的代码块{}中使用。

int main()
{
    //计算两个数的和
    int num1 = 1;
    int num2 = 2;
    int sum =0;

    //输入数据--使用输入函数scanf
    scanf_s("%d%d", &num1, &num2);//取地址符号“&”，vs2019不能使用scanf，而要使用scanf_s
    //int sum = 0;//这里是错误的，C语言语法规定，变量要定义在当前代码块最前面。
    sum = num1 + num2;
    printf("sum=%d", sum);
    return 0;
}

```



### 1.3.3 变量的作用域和生命周期

#### **作用域:**

**限定这个名字的可用性的代码范围就是这个名字的作用域。**

- 局部变量的作用域是变量所在的局部范围
- 全局变量的作用域就是整个工程

```c
#include <stdio.h>
int main()
{
    int go=20;//局部变量的作用域是变量所在的局部范围
    printf("go+%d",go);
    return 0;
}


int go=20;//全局变量的作用域就是整个工程
int main()
{
    printf("go+%d",go);
    return 0;
}

int main()
{
    //extern函数是声明外部文件符号的
    extern int g_val;// g_val是其他文件的全局变量
    printf("g_val=%d\n",g_val);
    return 0;
}
```

#### 生命周期

**变量的生命周期值的是变量的创建到变量的销毁之间的一个时间段。**

1. 局部变量的声明周期是：进入作用域  生命周期开始，出作用域 生命周期结束。
2. 全局变量的生命周期是：整个程序的生命周期。

```c
#include <stdio.h>
int main()
    int golang = 110l;//全局变量的生命周期就是整个程序的生命周期
{
    int go=20;//局部变量的生命中周期就是它的作用域
    printf("go+%d",go);
    return 0;
}
```

