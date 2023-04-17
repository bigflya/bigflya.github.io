---
title: linux学习经验
categories: 编程
tags: 学习经验
abbrlink: 82b691dd
date: 2023-02-28 11:57:44
---
<!-- <h1 align = "center"> linux修炼手册</h1> -->




## C语言基础



### linux编程预科：

#### ***编译器*：** 

gcc，make

------

#### **c编译过程编译过程**:

 **流程：**源文件--1预处理--3编译--4汇编--5链接--可执行文件（.c -->  .out）

1. 
   预处理:  gcc -E hello.c

2. 保存预处理文件  gcc -E hello.c > hello.i

3. 编译：   gcc -S hello.i

4. 汇编：  gcc -c hello.s

5. 链接并指定生成文件为hello： gcc hello.o -o hell

   ------

   **对上面过程进行包装**：  gcc hello.c  即可在当前目录生成可执行文件,也可以用make 进行编译  make hello (make操作不用带后缀)

**测试编译后的文件** ：  ./hello

------

#### **vim 编辑器的使用技巧：**

运行 vim  /etc/vimrc    对vim编辑器进行修改
建议  cp /etc/vimrc ~/.vimrc   复制一份在自己的家目录，这样 这个vim只对当前用户有效，而不会修改所有用户的vim

 想查看 函数原型 直接在vim 中光标放在函数上 按shift+k

------

#### **gcc编译器的使用技巧**：

gcc hello.c -Wall 编译并打印所有警告

echo $? 打印上一行命令的输出状态

------

#### **shell的使用技巧**：

ls -l  可以用  ll  代替



#### 编程的基本要求：

1. 头文件要正确包含
2. 以函数为单位进行程序的编写
3. 声明部分+实现部分
4. return 0;
5. 空格、注释、对齐的中要求
6. 算法：解决问题的方法（用流程图、ns图、有限状态机FSM进行算法逻辑设计）

### c语言：（TYPE NAME =VALUE）

#### c语言注释技巧：

直接在 通过预编译跳过的形式注释：

```c
#if 0
func()
{
    
    
    
}
#endif
```



代码块注释：

```c
/*
 *
 *
 * 这样也可以
*/
```

#### 基本数据类型：

记住整型int 是占一个机器字长就可以，在32位机器上int 是32位的，其余的 双精度 单精度 的字长都是以int 为基础进行放缩的，例如 在32位机器上double 占64位、float 占32位、short 是16、char占8位。

不能抛开是多少位机器，谈论 不同数据类型所占 位数长度，

有符号和无符号只是 表示的数值范围不同，二者所占的字节数是一样的。

#### 变量的类型及生命周期和作用范围：

auto  默认，会随机给初值 （分配空间），自动收回空间

register   （建议型）寄存器类型，只能定义局部变量

static   静态型 禁止函数的外部拓展，初值位0，或空

extern  说明性，不能改变被说明的变量的值或类型

#### 逻辑运算符:

这部分比较简单随用随查

#### 输入输出（I/O）:

1. 格式化输入输出函数： scanf 、printf

   int printf(const char *format, ...)

   format: "%[修饰符] 格式字符"，动态实参

   变参 、和定参的区分方法

   小知识：printf也是有返回值的

    

   ```c
   printf("[%s:%d]before while().\n",__FUNCTION__,__LINE__);//可以打印此句话所在的函数和行号
   function()
   printf("[%s:%d]after while().\n",__FUNCTION__,__LINE__);//可以打印此句话所在的函数和行号
   ```

   format: 抑制符 * 

   %s 的使用是比较危险的，因为不知道存储空间的大小 

   scanf 放在循环结构中要注意能否接收到正常的有效内容

   

2. 字符输入输出函数：getchar、putchar

3. 字符串输入输出函数：gets(!)、puts

​	  gets 是十分危险的函数，可以用 fgets 或者getline来代替

#### 流程控制（三大结构 --顺序、选择、循环）：

选择： if-else switch-case

  小知识：   else 只与离他最近的if相嵌套

​                     case 中只能放常量或常量表达式 

​					 

循环： while    do-while for  if-goto

​        while 和do while 的区别，要了解到do -while 可以多执行一次 

​		if-goto(慎用，goto实现的是无条件跳转，且不能跨越函数跳转)

辅助控制： continue       break  

  break 跳出本层循环 ，continue 跳出本次循环

#### 数组

数组的特点 ：在内存中连续存放

数组名本身就是表示地址的常量 所以调用数组的时候不用在 数组名前面写取地址符号。

一维数组：

 初始化 ： 部分初始化  全部初始化  不初始化  static  

数组名：  是表示地址的常量，也是数组的起始位置，

数组越界：只能靠程序员的经验来检查，IED不会报错，因为越界是通过指针偏移来找对应的内存地址的，即使那一块不属于数组的范围，但内存中只要存在 就不会报错。

排序方法： 冒泡法 、选择法、快速排序法

删除法求质数

二维数组：

二维数组行号可以省略

字符数组：

  数组是不能直接复制的 ，用strcpy()来 赋值，还可以用strncpy()来拷贝给字符数组相应的值，可以防止越界现象。

string.h的头文件里面还有好多函数可以可以设置类似的strncat  strcat   strcmp  strncmp等  ，其中strcmp比较的是相应位置的ascii码

sizeof(str)算末尾的/0  ，strlen(str)不算末尾的/0

printf("%s--->%d\n"，__ FUNCTION__ ,sizeof(a)) 这句话中 __ FUNCTION__会打印当前行所在函数名。

#### 指针

已知：  int  *p=a              （其中a为一维数组）  可以推出下面的两行结论

a[i]=*(a+i)= * (p+i)=p[i]

&a[i]=a+i  =p+i=&p[i]                                   注意数组名存放的是数组的起始地址(见解：我个人理解数组本身也是一个指针)



指针可以节省传参的资源开销

一个指针变量在内存中占4个字节（32位机器），若是64位机器则占8个字节。

变量与地址： 

指针与指针变量：  

直接访问与间接访问：

空指针与野指针：  

空类型：void  ，不太确定指针的类型的时候就用void 类型

指针运算：  *   &   比较地址

指针与数组：  涉及到指针与数组的一些相关知识，

**const与指针：**

------

   常量指针：  

​             定义： 又叫 常指针，通俗理解 就是这是个指针但是这个指针指向常量。这个常量是指指针的值（地址），而不是地址指向的值。  形式 int const* p  ; const int* p

​            关键点：常量指针指向的对象不能通过这个指针来修改，但仍然可以通过原来的定义来修改。（错误示范  *p =10），函数传入参数如果不希望被误改 可以指定传入参数为常量指针

​                          常量指针可以被赋值为变量的地址，之所以叫常量指针，是为了限制通过这个指针修改变量。

​                         指针还可以指向别处，因为指针本身是个变量，可以指向任意地址

------

  指针常量：

​                定义 ： 本质是个常量，而用指针修饰它。指针常量的值是指针，因为这个值是常量，所以不能被赋值。 形式  int const* p; const int* p;

​           关键点：

​                      指针常量是  一个   常量

​                     指针所保存的地址可以改变，然而指针所指的值却不可以改变

​                     指针本身是常量，指向的地址不可以改变即p 不能改变。但是指向的地址所对应的内容可以变化。即 *P可以发生改变。（错误示范  p =&t）



------

指针数组与数组指针：

```c
// 指针数组 ：
#include <stdio.h>
#include <stdlib.h>

void print_arr(int p[],int n)
{
        int i;
        printf("%s:%d\n",__FUNCTION__,sizeof(p));
        for(i = 0; i<n; i++)
                printf("%d",*(p+i));
        printf("\n");


}


int main()
{
        int a[] = {1,3,5,7,9};
        printf("%s:%d\n",__FUNCTION__,sizeof(a));
        print_arr(a,sizeof(a)/sizeof(*a));


}

```

​               int  * arr[3]

​	数组指针：

​          int(*p)[3]

多级指针：



#### 函数

```c
#include<stdio.h>
#include<stdlib.h>
//定义一个函数
int main(int argc,char *argv[])
{
    int i;
    printf("argc = %d\n",argc);
    for(i =0;i<argc; i++)
        puts(argv[i]);
    return 0;


}

```

函数传参:

```c
#include <stdio.h>
#include <stdlib.h>

void swap(int *p, int *q)
{
    
    int tmp;
    tmp = *p;
    *p = *q;
    *q = tmp;
    
}

int main()
{
	int i = 3,j = 5;
    int tmp;
    swap(&i,&j);
    printf("i=%d\nj = %d\n",i,j);
    
    
}
```

值传递：

地址传递：  比较重要 ，核心理解 点就是  ，指针的内涵

全局变量：



函数的调用（递归和嵌套）：

递归是嵌套的一个特例 

```c
#include <stdio.h>
#include <stdlib.h>
int max(int a,int b,int c)
{
    int tmp;
    tmp = a>b?a:b;
    return tmp>c?tmp:c;
    
    
}
int min(int a,int b,int c)
{
    int tmp;
    tmp = a<b?a:b;
    return tmp<c?tmp:c;
    
}
int dist(int a,int b,int c)
{
    
    return max(a,b,c)-min(a,b,c);
}
int main()
{
    int a = 3,b = 5,c = 10;
    int res;
    res = dist(a,b,c);
    printf("res = %d\n",res);
    return 0;
    
    
}
```



函数与一维数组：



```c
#include <stdio.h>
#include <stdlib.h>
//以前的做法
int main()
{	
    int i;
    int a[] = {1,3,5,7,9};
    for(i=0;i<sizeof(a)/sizeof(*a);i++)
        printf("%d\n",a[i]);
    exit(0);
    
    
}

```

------

***小知识：***不同位数操作系统下不同的变量类型所占字节数如下，指针是随操作系统位数变的，而int 还有其他类型基本不咋变化。

| c类型         | 32   | 64   |
| ------------- | ---- | ---- |
| char          | 1    | 1    |
| short int     | 2    | 2    |
| int           | 4    | 4    |
| long int      | 4    | 8    |
| long long int | 8    | 8    |
| char*         | 4    | 8    |
| float         | 4    | 4    |
| double        | 8    | 8    |

------



```c
#include <stdio.h>
#include <stdlib.h>
//现在的做法
int print_arr(int *a)//这里并不知道指针a 的大小，即不知道指针能访问的空间大小，要想精确访问需要再传进来一个参数  int n ,然后利用 for 循环来准确访问a中所有的值 ，也可以将 int *a写成 int p[], 在形参中一个[]相当于 一个*  例如  char **argv   就等价于char *argv[]
{
    int i;
    i = sizeof(a);
    printf("%d",i);//形参a 作为一个指针 占8个字节，因为系统是64位所以是8若是32位则是4

}
int main()
{

    int a[] = {1,3,5,7,9};//32位系统一个int占4个字节
    printf("%ld\n",sizeof(a));//4x5 =20

    print_arr(a);

    exit(0);


}
//运行结果  
// 20 8
```



```text
一维数组，传参时的实参与形参对应表

实参: a	*a	a[0]	&a[3]	p[i]	p	*p	p+1


形参：int*	int	int		int*	int		int*	int		int*
```



函数与二维数组：

```c
#include <stdio.h>
#include <stdlib.h>
#define M 3
#define N 4
void print_arr(int *p,int n)//这种方法相当于把二维数组当成一维数组来处理注意第一个形参类型，思考为什么可以这样
{		
    	int i;
	    for(i = 0;i<n;i++)
        {
            printf("%d",p[i]);
            
        }
    
    	printf("\n");
}
int main()
{
	int a[M][N]={1,2,3,4,5,6,7,8,9,10,11,12};
	print_arr(&a[0][0],M*N); // *a  a[0]  *(a+0)  这几种是等价的都是相当于把行指针转换为列指针
    
	exit(0);
}
```

```c
/*
//上面代码的第二种实现方式

*/
#include <stdio.h>
#include <stdlib.h>
#define M 3
#define N 4
void print_arr1(int (*p)[N],int m ,int n)//第一个形参的本质其实是一个数组指针所以可以这样写  也可以写成 int p[][N]
{		
    	int i,j;
	    for(i = 0;i<m;i++)
        {
            for(j=0;j<n;j++)
                printf("%4d",p[i][j]);//或者*(*(p+i)+j)
            printf("\n");
            
            
        }
    
    	
}
int main()
{
	int a[M][N]={1,2,3,4,5,6,7,8,9,10,11,12};
	print_arr1(a,M,N);
    
	exit(0);
}
```



```
二维数组，传参时的实参与形参对应表,核心就是判断是不是行指针 或者列指针
/*p[i]相当于一级指针中的某个元素，p是指向一行的，相当于一个一维数组p[i]就是一维数组里面的元素*/
int a[M][N]={......};
int *p=*a;
int (*q)[N]=a;

实参: a[i][j]		*(a+i)+j	a[i]+j	p[i]	*p	
     q[i][j]	  *q			q	  p+3	 q+1


形参：int	 		int *		int *	int		int	
     int	   int*  	int (*)[N]    int *		int(*)[N]



```



二维数组名相当于是一个行指针

二维数组相当于 一个 数组指针   int (*p)[N]  ，在写小函数形参的时候要写成这样

 





指针函数： 返回值 如 int * fun(int)

```c
#include <stdio.h>
#include <stdlib.h>

#define M 3
#define N 4

int *find_num(int (*p)[N] ,int num)
{
    if(num>M-1)
        return NULL;
    
    return *(p+num);
}
int main()
{
    int i,j;
    int a[M][N]={1,2,3,4,5,6,7,8,9,10,11,12};
    int *res;
    int num =0;
    res = find_num(a,num);
    if(res !=NULL)
    {
        for(i=0;i<N;i++)
            printf("%d",res[i]);
        printf("\n");
    }
    else
    {
         printf("error! can not find\n");
    }


}

```

函数指针：  类型 如  int(*p)(int);

```c
#include <stdio.h>
#include <stdlib.h>
int add(int a ,int b)
{
    
    return a+b;
}
int main()
{
    int a=3,b=4;
    int ret;
    int (*p)(int,int);
    p= add;
    ret = p(a,b);
    printf("%d\n",ret);
    
}
```

函数指针数组：

 			类型 如  int (*arr[N])(int);



```c
#include <stdio.h>
#include <stdlib.h>
int add(int a ,int b)
{
    
    return a+b;
}
int main()
{
    int a=3,b=4,i;
    int ret;
    int (*funcp[2])(int,int);
    funcp[0] = add;
    //funcp[1] = sub?
    for(i= 0;i<1;i++)
    {
        ret=funcp[i](a,b);
         printf("%d\n",ret);
    }
    
   
    
}
```



指向指针函数的函数指针数组：

​	形式  int *(*funcp[N])(int)

------



#### 构造类型：

##### ***结构体***

- 产生及意义：把不同类型的数据，存放在连续的空间

- 描述：   struct  结构体名

  ​				{

  ​						数据类型	成员1；

  ​						数据类型	成员2；

  ​						............

  ​				};

- 嵌套定义:

  ​		

  ```
  嵌套的结构体可以直接完整的嵌入内部，也可以在外面单独定义这个嵌套的小结构体，但要注意嵌套在内部要在结构体后面写上成员，嵌在里面的小结构体只是相当于一个 数据类型 。
  ```

  

- 定义变量（变量、数组、指针），初始化及成员引用

  ​			

  ```c
  #include <stdio.h>
  #include <stdlib.h>
  #define NAMESIZE	32
  struct simp_st
  {
      int i;
      float f;
      char ch;
  };
  int main()
  {
      //TYPE NAME = VALUE
      struct simp_st a={123,456.789,'w'};//结构体初始化。  TYPE 是struct simp_st
      //对指定成员赋值 struct simp_st a={.i=147,.ch='s'};
      //指定成员赋值方法2 struct simp_st *p = &a;  //引用方法 p->i  ,p->ch 等
      //指定成员赋值方法3  struct simp_st arr[2]{{123,123.123,'c'},{456,456.456,'b'}}   //使用方法p =&arr[0];   for(;;i++,p++)注意p是结构体所以p++每次跳一个结构体大小，若p是整形p++一次跳4个字节，p是double则p跳 diuble类型所占字节数
      a.i=2358784886;
      printf("%d--%f--%c",a.i,a.f,a.ch);
      exit(0);
      
  }
  ```

  

- 结构体的对齐原则[参考资料](https://cloud.tencent.com/developer/article/1703257)：从存储原理的角度来看这就是牺牲空间的原则来减少时间的消耗，具体就是跳过了其中一些空间来减少时间的消耗，结构体的总大小为其成员中所含最大类型的整数倍。 在一些网络传输过程中，要注意 对齐方式可能不一样。这时候就需要设置不对齐方法如下。

  ```c
  struct a
  {
      int i;
      char ch;
      float f;
  }__attribute__((packed));
  ```

  

- 函数传参： 方式（值，地址）  。值传参是临时深拷贝，开销非常大。通常会使用指针传参 开销比较小，只有一个指针大小的开销，比如32位操作系统开销是4个字节，64位操作系统是8个字节

- 无头结构体：只能在声明的时候把变量定义好。

  ​				

- 微型学生管理系统：

  ​		

  ```c
  #include <stdio.h>
  #include <stdlib.h>
  #include<string.h>
  #include <unistd.h>
  #define NAMESIZE	32
  struct student_st
  {
      int id;
      char name[NAMESIZE];
      int math;
      int chinese;
  };
  
  void stu_set(struct student_st *p,const struct student_st *q)
  {
      //可以 p->id = q->id;
      *p = *q;
  }
  void stu_show(struct student_st *p)
  {
      printf("%d %s %d %d\n",p->id,p->name,p->math,p->chinese);
      
  }
  void stu_changename(struct student_st *p,const char *newname)
  {
      //错误示范    p->name = newname   ,左边是常量。指针是变量但是指针所指的内容是常量，是不能直接这样赋值的。
      strcpy(p->name,newname);
      
  }
  void menu(void)
  {
      printf("\n1 set\n2 change name\n3 show\n");
      printf("Please enter the num of you want to choice(q for quit):\n");
  }
  int main()
  {
      struct student_st stu,tmp;
      char newname[NAMESIZE];
      int choice;
      int ret;
      do{
          menu();
          ret = scanf("%d",&choice);//按理来说每个scanf和printf都有可能出错，要进行校验，要设置出错推出选项
          if(ret !=1)
              break;
          switch(choice)
              {
                  case 1:
                      printf("Please enter for the stu[id name math math chinese]:\n");
                      scanf("%d%s%d%d",&tmp.id,tmp.name,&tmp.math,&tmp.chinese);
                      stu_set(&stu,&tmp);
                      break;
                  case 2:
                      printf("Please enter the new name: ");
                      scanf("%s",newname);
                      stu_changename(&stu,newname);
                      break;
                  case 3:
                      stu_show(&stu);
                  	break;
                  default:
                      exit(1);
  
              }
          	sleep(1);//#include <unistd.h>
          
          
          
      	}while(1);
      
  
      exit(0);
  }
  
  ```

  


##### ***共用体：***

  - 产生及意义：相当于结构体中的成员有多个，但同时只能一种情况存在。多个成员公用一块空间，当在使用其中一个成员时，其他成员是不生效的。这点可以从内存占用反应出来。

  - 类型描述：

    ​	 

    ```c
    union 共用体名
    {
        数据类型 成员名1；
        数据类型 成员名2；
            .......
    };
    ```

    

  - 嵌套定义： 与结构体差不多，且共用体可以嵌套结构体，结构体也能嵌套共用体

  - 定义变量（变量、指针、数组），初始化及成员引用：

    - 成员引用：   第一种  变量名.成员名      第二种   指针名->成员名

  - 占用内存大小：  公用体的大小是根据它里面最大的那个成员 来分配的。

  - 函数传参（值、地址）：  记住一点 地址传参开销小。

    - 实现高四位加上低四位的例子:

    ```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <stdint.h>
    
    //方法一：传统方法依靠位运算
    int main()
    {
    	uint32_t i = 0x11223344;
    	printf("%x\n",(i>>16)+i&0xFFFF);
    }
    
    /*
    //方法二：共用体和结构体嵌套
    union
    {
    	struct
    	{
    		uint16_t i;//占两个字节
    		uint16_t j;//占两个字节
    	}x;//占四个字节
    	uint32_t y;//占四个字节
    }a;//占四个字节
    
    int main()
    {
    a.y = 0x11223344;
    printf("%x\n",a.x.i+a.x.j);
    
    }
    */
    
    ```

  - 位域： 没有实际开发使用的意义 ，但也是一个知识点。存放变量不是以字节为单位而是以位为单位。

    ​				

    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    union
    {
    	struct
    	{
    		char a:1;//占一个位
    		char b:2;
    		char c:1;
    	}x;//总共占4位
    	char y;//8位
    }w;//总共占8位
    
    int main()
    {
    	
    
    }
    ```

    - 大端和小端的概念：大端指数据存储时，数据的高位保存在低地址中，数据的低位保存在高地址中。  常用的x86体系结构，多数都是小端  。c51是非常典型的大端。很多arm  和dsp都是小端结构。

    ​	

##### ***枚举：***

  - 相对比较简单，这里用一个例子说明,把枚举当宏来使用，方便查错，预处理之后报错 报的是名，而不是宏的值： 1 2 3。但是它不能当成函数传参来使用，而宏可以。

    ``` c
      #include<stdio.h>
      #include<stdlib.h>
      
      enum
      {
          STATE_RUNNING = 1,
          STATE_CANCELED,//默认是2
          STATE_OVER //最后一句不需要逗号，这里默认是3
          
      }；
      struct job_st
      {
          int id;
          int state;
          time_t start ,end;
      };
      int main()
      {
          struct job_st job1;
          /*获取任务状态*/
          switch(job1.state)
          {
              case STATE_OVER:
                  break;	
              case STATE_CANCELED:
                  break;
              case STATE_OVER:
                  break;
              default:
                  abort();
          }
          
      }
    ```

#### 动态内存管理：

- 几个相关函数：

  -  malloc     void *malloc(size_t size);  申请指定大小的内存空间
  - calloc          
  - realloc(已经用了一部分内存，想再申请一部分，若用掉的部分内存后面的位置被占用了，则找一大块相应的连续内存 将此任务已经用掉的部分内存内容剪切过去，相当于重新分配了一块连续的大内存)
  -  free  void free(void *ptr)  释放内存  ，free之后把指针设置为空指针 ，这样可以避免野指针的出现

- 原则：谁申请谁释放

  重构学生管理系统的例子：(主要对名字的最大占用空间做了改变)

  ```c
  #include <stdio.h>
  #include <stdlib.h>
  #include<string.h>
  #include <unistd.h>
  #define NAMEMAX	1024
  struct student_st
  {
      int id;
      char *name;
      int math;
      int chinese;
  };
  
  void stu_set(struct student_st *p,const struct student_st *q)
  {
      p->id = q->id;
      p->name = malloc(strlen(q->name)+1);//加1是预留一个尾0
      if(p->name ==NULL)
          exit(1);
      strcpy(p->name, q->name);
      p->math = q->math;
      p->chinese = q->chinese;
  }
  void stu_show(struct student_st *p)
  {
      printf("%d %s %d %d\n",p->id,p->name,p->math,p->chinese);
      
  }
  void stu_changename(struct student_st *p,const char *newname)
  {
      free(p->name);
      p->name = malloc(strlen(newname)+1);
      strcpy(p->name,newname);
      
  }
  void menu(void)
  {
      printf("\n1 set\n2 change name\n3 show\n");
      printf("Please enter the num of you want to choice(q for quit):\n");
  }
  int main()
  {
      struct student_st stu,tmp;
      char newname[NAMEMAX];
      int choice;
      int ret;
      do{
          menu();
          ret = scanf("%d",&choice);//按理来说每个scanf和printf都有可能出错，要进行校验，要设置出错推出选项
          if(ret !=1)
              break;
          switch(choice)
              {
                  case 1:
                  	tmp.name = malloc(NAMEMAX);
                      printf("Please enter for the stu[id name math math chinese]:\n");
                      scanf("%d%s%d%d",&tmp.id,tmp.name,&tmp.math,&tmp.chinese);
                      stu_set(&stu,&tmp);
                  	free(tmp.name);//释放掉临时名存放的空间，做到谁申请谁释放
                      break;
                  case 2:
                      printf("Please enter the new name: ");
                      scanf("%s",newname);
                      stu_changename(&stu,newname);
                      break;
                  case 3:
                      stu_show(&stu);
                  	break;
                  default:
                      exit(1);
  
              }
          	sleep(1);//#include <unistd.h>
          
          
          
      	}while(1);
      
  
      exit(0);
  }
  
  ```

  

------



#### 补充知识：

- 一个典型的typedef:

  - 类型：   typedef  已有的数据类型  新名字：

  - 作用：1、为已有的数据类型改名，  2、对数据类型做重定义 这样就可以在程序从32位机器 转到64位机器上运行时可以快速对数据类型进行修改

    ```text
    #define IP int *
    IP p,q;-----> int *p,q;
    
    typedef int *IP;
    IP p,q;------>int *p,*q;
    
    typedefy int ARR[6];  //本质是 int [6]->ARR
    ARR a;------>int a[6]
    
    struct node_st
    {
    	int i;
    	float f;
    
    };
    typedef struct node_st  NODE;
    NODE a;--------> struct node_st a;
    
    
    typedef struct node_st *NODEP;
    NODEP p;---->struct node_st *p;
    
    
    //还可以简单点
    
    typedef struct
    {
    	int i;
    	float f;
    }NODE,*NODEP; //直接对无名的结构体改名 既可改成NODE ,也可改成 *NODEP
    
    
    typedef int FUNC(int);
    FUNC f;---->int f(int);
    
    //  int *(*p)(int); 指向函数指针的指针函数
    ```

    

- makefile工程文件

  - make定义：  make是一个集成的工程管理器，

  - makefile定义：  make执行的一个脚本，程序员一般写一个大写的MAKEFILE 在里面对编译过程进行说明，

  - .h文件不参与编译 ，makefile中写的是依赖关系 

    

    

## 数据结构

​    

