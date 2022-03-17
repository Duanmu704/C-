# goto

goto语句在C语言中可以实现无条件跳转，通过和if语句的有效组合也可以实现循环结构。

## 1、goto语句的标准形式

#### goto语句由关键字goto和一个代码中存在的标号名组成。标准形式如下所示：goto标号名;

#### 其执行逻辑为：当程序执行这一句后，将无条件跳转到标号名所在位置，然后执行该位置后的代码。

#### 标号的命名规则与变量名的命名规则相同，都必须由字母、数字和下画线组成，且第一个字符必须为字母或下画线；而且标号名必须是唯一的，不得与其他标识符相同。同时，goto语句中的标号名必须在程序中存在，否则，编译器会报错。使用goto语句可以改变语句的执行顺序。

【例1】使用goto语句实现的死循环。



```c++
#include <stdio.h>
int main(void) 
{
infinite_loop:           //标号
	printf("死循环!!!\n");
	goto infinite_loop;  //跳转至指定标号
}


```

【运行结果】程序运行后，进入死循环，反复打印一行字符串。使用【Ctrl+C】快捷键终止执行。
【代码解析】本程序是goto语句改变程序语句执行顺序的经典范例。第4行，为一个标号语句，在程序中并不执行任何功能，只是对语句做标识的作用。第6行，这是一个goto语句，该语句执行后程序将无条件地跳转到程序标号“infinite_loop”后执行代码。由于程序执行到第6行并跳转到第4行，一直重复执行打印语句，陷入死循环。

2、搭配使用goto语句于if语句
2.1选择结构
使用goto语句改写if-else语句，形式如下：

```c++
if ( 表达式 ) {
            操作1;
            goto else_end;
        }
        else_start:
            操作2;
        else_end:
            后续操作;
```



2.2循环结构1
使用goto语句实现for语句，形式如下：

```c++
  表达式1;                       /* 即初始化表达式 */
        for_start:
            if ( 表达式2 ) {               /* 即判断表达式 */
                操作;
                表达式3;                   /* 即变量控制表达式 */
                goto for_start;
            }
```


2.3循环结构2
使用goto语句实现while语句，形式如下：

```c++
    while_start:
        if ( 表达式 ) {
            操作;
            goto while_start;
        }
```

2.4循环结构3
使用goto语句实现do-while语句，形式如下：

```c++
    do_while_start:
        操作;
        if ( 表达式 )
            goto do_while_start;
```

但是，上面这些代码的展示，只是告诉读者goto语句使用的灵活性，但不鼓励使用以上的代码形式。

3、慎用goto语句
由于goto语句的跳转过于灵活，容易破坏程序流程，同时，goto语句的大部分功能都可以用其他语句来更好地实现，所以大多数人都有意识地限制goto语句的使用，甚至有人把goto语句视为逻辑混乱的毒瘤。但是，在一些特殊的场合还是可以看到goto语句的独特作用的。
3.1从循环中跳出
虽然在C语言中，for语句与while语句可以使用continue语句和break语句结束循环，但是对于多层循环则无能为力。这时，便需要使用goto语句。
【例2】使用goto语句结束多层循环

```c++
#include <stdio.h>
int main(void) {
	int i, j;
	int data;
	int sum = 0;
	const int m = 3;                                    /* 行数 */
	const int n = 3;                                    /* 列数 */
	printf("Please input a %d*%d matrix:\n", m, n);     /* 提示输入矩阵规模 */
	for (i = 0; i < m; ++i) {
		for (j = 0; j < n; ++j) {
			printf("matrix[%d][%d](>0) = ", i, j);  /* 提示要输入的矩阵元素 */
			scanf_s("%d", &data);                   /* 输入元素值 */
			/* 输入非法，则退出内部循环 */
			if (data <= 0) {
				printf("Error: wrong data!!! Exit loop\n");
				goto ERROR_DATA;                   /* 跳转到指定标号处 */
			}
			sum += data;                            /* 求和 */
		}
	}
	printf("The sum of numbers in this matrix is %d.\n", sum);
	/* 输出总和 */
ERROR_DATA:                                          /* 指定的标号 */
	return 0;
}
```




【代码解析】本程序使用goto语句改写了范例2的break语句。当输入一个小于0的数值时，第14行的if判断表达式为真，则进入if体，输出错误信息后执行goto语句。由于ERROR_DATA设置return语句前，因此，goto语句将程序跳转至return语句处，跳出了二层for循环，直接执行return语句结束程序。
提示：第19行输出矩阵元素和时，也不需要判断数据输入是否正常，因为如果输入有错误，该printf语句会被跳过。

3.2增强代码的可读性
当程序对多种情况的处理方式完全相同时，便可以使用goto语句。这不仅可以加强代码可读性，还可以较少代码量。

3.3减少return语句使用
————————————————
版权声明：本文为CSDN博主「梦想程序菜鸡」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_46166537/article/details/105074824



