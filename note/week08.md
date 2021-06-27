# 第八周
## 作业系统
#### 概念表达
操作系统（operating system，简称OS）是管理计算机硬件与软件资源的计算机程序。操作系统需要处理如管理与配置内存、决定系统资源供需的优先次序、控制输入设备与输出设备、操作网络与管理文件系统等基本事务。操作系统也提供一个让用户与系统交互的操作界面。

![1](https://github.com/lzc2021/sp109b/blob/main/image/04.jpg)

## Unix家族的演变
![1280px-Unix_history-simple svg](https://user-images.githubusercontent.com/62127656/120112671-55ea8a00-c1a9-11eb-8455-493880b82f1f.png)
## glib
* 用链结串列时，已经不需要再自己对指标(Pointer)做许多低阶的处理
* 范例程式 glist.c
```
/* Compile with:
export CFLAGS="`pkg-config --cflags glib-2.0` -g -Wall -std=gnu11 -O3"
export LDLIBS="`pkg-config --libs   glib-2.0`"
make glist
*/
#include <stdio.h>
#include <glib.h>

GList *list;

int main(){
    list = g_list_append(list, "a");
    list = g_list_append(list, "b");
    list = g_list_append(list, "c");
    printf("The list is now %d items long\n", g_list_length(list));

    for ( ; list!= NULL; list=list->next)
        printf("%s\n", (char*)list->data);

    printf("The list is now %d items long\n", g_list_length(list));
}
```
>Glist , g_list_aapend(), glist_lenth()
---
## pkg-config
* pkg-config 是一个在原始码编译时查询已安装的函式库的使用介面的电脑工具软体。
* C/C++编译器需要的输入参数
* 连结器需要的输入参数
* 已安装软体包的版本资讯
## 指令
* ```sudo apt-get install libglib2.0-dev``` 安装glib函式库
* ```-lm``` 连结math.h这个函式库，因为在c语言中math非标准函式库，但c++则是
* ```apt install libsqlite3-dev``` 安装sqlite3函式库
* ```ps``` 查看背景及前景执行的程式
* ```&``` 背景执行
* ```#ifndef``` 如果没定义则做后续
* ```define```定义某物
* ```endif``` 结束if
