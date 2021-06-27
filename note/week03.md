# 第三周

##编译器 
### Compiler
#### BNF/EBNF/生成语法
#### Lexer
#### 运算式编译器
#### Exp/if/While

Fopen()
```
r -- 读取。档案必须存在

w -- 新建档案写入。同名档案若存在则清空，并被视为新档案

a -- 附加。追加的数据在文件末尾。该文件如果不存在会被创建

r+ -- 读、更新。打开档案并写入，档案必须存在

w+ -- 写、更新。创建档案并打开以进行更新或清空同名档案内容

a+ -- 资料附加到旧档案后面(游标指在EOF)，可读取资料

b -- 二进位模式

rw+ -- 可读取可写入，档案若存在就直接写入，不存在就创建新的档案
```

#### 执行历史

```
PS F:\1文件\演算法\xtcs\sp\03-compiler\02-lexer> gcc lexer.c -o lexer
PS F:\1文件\演算法\xtcs\sp\03-compiler\02-lexer> ./lexer sum.c
#include "sum.h"

int main() {
  int t = sum(10);
  printf("sum(10)=%d\n", t);
}
token=#      
token=include
token="sum.h"
token=int    
token=main   
token=(      
token=)      
token={      
token=int    
token=t
token==
token=sum
token=(
token=10
token=)
token=;
token=printf
token=(
token="sum(10)=%d\n"
token=,
token=t
token=)
token=;
token=}
0:#
1:include
2:"sum.h"
3:int
4:main
5:(
6:)
7:{
8:int
9:t
10:=
11:sum
12:(
13:10
14:)
15:;
16:printf
17:(
18:"sum(10)=%d\n"
19:,
20:t
21:)
22:;
23:}
```
