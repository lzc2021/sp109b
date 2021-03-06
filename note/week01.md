# 第一周

## 评分方式 
* 期中成绩(=笔记) 40%
* 期末成绩(=专案) 40%
* 上课问问题 20%

### 系统程式(System programming)
* 系统程式设计，是针对电脑系统软体开发而进行的编程活动
* 系统程式设计，主要是为电脑硬体提供相对应的软体服务
* 系统程式通常与其执行机器的架构是有密切的关係:组译器, 编译器,作业系统

#### 概念表达
系统程序 其实可以有三个典型 数据库系统 高级语言程序 操作系统 LZ这里的系统是指操作系统吧 操作系统按计算机系结构的分类 是直接面向机器 也就是我们说的裸机（只为用户提供了基本的基本指令系统）那么操作系统是在硬件指令上的再次扩充 向数据库系统 高级语言程序 提供更完善的指令系统（基于这一点它提供了API和DLL供高层系统调用）此外操作系统还对硬件资源进行管理和用户作业的调度（基于这一点就有硬件的驱动程序和操作系统用于调度管理的内核程序）另外操 作系统还要提供用户界面（那么就要提供命令或者图形界面的程序）另外还有对文件的管理（管理文件的程序） 还要提供系统安全等（安全相关程序） 等等

### 系统软体(System Software)
* 设计给程式设计师使用的软体称为系统软体，设计给一班大众使用的则称为影用软体
* 常见的系统软体包含：作业系统 (operating system)、编译器 (compiler)、直译器 (interpreter)、连结器 (linker)、载入器 (loader)、组译器 (assembly)、除错器 (debugger)、硬体驱动程式 (driver)、公用程式

#### 概念表达
系统软件是指控制和协调计算机及外部设备,支持应用软件开发和运行的系统，是无需用户干预的各种程序的集合，主要功能是调度，监控和维护计算机系统；负责管理计算机系统中各种独立的硬件，使得它们可以协调工作。系统软件使得计算机使用者和其他软件将计算机当作一个整体而不需要顾及到底层每个硬件是如何工作的。

## 什么是GCC

* gcc是"GNU Compiler Collection"的缩写，从字面意思可以知道它是一个编译器集。gcc不止可以编译器c语言，还能用于c++，java，object-C等语言程序。但是在这裡，我们的嵌入式学习中，目前只去关注gcc在C语言方面的编译功能

#### 概念表达
GCC（GNU Compiler Collection，GNU编译器套件）是由GNU开发的编程语言译器。GNU编译器套件包括C、C++、 Objective-C、 Fortran、Java、Ada和Go语言前端，也包括了这些语言的库（如libstdc++，libgcj等。） 
GCC的初衷是为GNU操作系统专门编写的一款编译器。GNU系统是彻底的自由软件。此处，“自由”的含义是它尊重用户的自由。

#### 定义
GCC是以GPL许可证所发行的自由软件，也是GNU计划的关键部分。GCC的初衷是为GNU操作系统专门编写一款编译器，现已被大多数类Unix操作系统（如Linux、BSD、MacOS X等）采纳为标准的编译器，甚至在微软的Windows上也可以使用GCC。GCC支持多种计算机体系结构芯片，如x86、ARM、MIPS等，并已被移植到其他多种硬件平台 。
GCC原名为GNU C语言编译器（GNU C Compiler），只能处理C语言。但其很快扩展，变得可处理C++，后来又扩展为能够支持更多编程语言，如Fortran、Pascal、Objective -C、Java、Ada、Go以及各类处理器架构上的汇编语言等，所以改名GNU编译器套件（GNU Compiler Collection）。

#### makefile
``` $ make ```

```
CC := gcc
AR := ar
CFLAGS = -std=c99 -O0
TARGET = run
LIB = libstat.a

all: $(TARGET)

$(TARGET): $(LIB) main.o
	$(CC) $(CFLAGS) $^ -L ./ -lstat -o $@
#gcc函式库前面需加lib
$(LIB): sum.o
	$(AR) -r $@ $^
#gcc底下的函式库压缩程式
%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f *.o *.a
```

#### Makefile 特殊符号

```
$@ : 该规则的目标文件 (Target file)
$* : 代表 targets 所指定的档案，但不包含副档名
$< : 依赖文件列表中的第一个依赖文件 (Dependencies file)
$^ : 依赖文件列表中的所有依赖文件
$? : 依赖文件列表中新于目标文件的文件列表
$* : 代表 targets 所指定的档案，但不包含副档名

?= 语法 : 若变数未定义，则替它指定新的值。
:= 语法 : make 会将整个 Makefile 展开后，再决定变数的值。
```

> 参考资料：百度百科
