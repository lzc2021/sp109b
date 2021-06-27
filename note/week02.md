# 第二周

## 系统程式重点
* 编译器(Complier)
* 组译器(Assembler)
* 虚拟机(Virtual Machine)
* 作业系统(Operating System)

## 编译器执行步骤:
* 先进行文法处理(Syntax)
* 词彙解析(Lexer)，将字符序列转换为标记序列的过程
* 语法剖析器(Parser)，进行语法检查、并构建由输入的单词组成的资料结构(语法树)
* 再来进行语意处理(Semantics Analysis)产生语意树
* 最佳化并产生Code Generation(IR档 → ASM档 → OBJ档)

#### Compiler编译器所需要的阶段
Syntax 语法上的处理 分两个lexer、parser（最核心的关键）  这是语法的部分
semantic 语义的部分 形态检测  不同语言不一样 eg：c语言需要比较严格的检测 而javaScript不需要
Code Generation 程式码生成   IR中间码   ASM组合语言  OBJ目的档




## Paser理论基础
Grammar 语法
Grammar语法  在自然语言中没有非常严格的规定 

举例S表示一个句子 一个句子由名词短语NP和动词短语VP组成

而名词短语由形容词adj和名词n组成 动词短语由动词v和名词n组成

* 深层语法 Noam Chomsky  
没有办法严格规定 所以需要深度学习来做机器翻译
* BNF(Backus Normal Form)  
是一种用于表示上下文无关文法的语言，上下文无关文法描述了一类形式语言

#### Code
```
#include <stdio.h>
#include <assert.h>
#include <string.h>
#include <ctype.h>

int tokenIdx = 0;
char *tokens;

int E();
int F();

void error(char *msg) {
  printf("%s", msg);
  assert(0);
}

// 取得目前字元
char ch() {
  char c = tokens[tokenIdx];
  return c;
}

// 取得目前字元，同時進到下一格
char next() {
  char c = ch();
  tokenIdx++;
  return c;
}

// ex: isNext("+-") 用來判斷下一個字元是不是 + 或 -
int isNext(char *set) {
  char c = ch();
  return (c!='\0' && strchr(set, c)!=NULL);
}

// 產生下一個臨時變數的代號， ex: 3 代表 t3。
int nextTemp() {
  static int tempIdx = 0;
  return tempIdx++;
}

// F =  Number | '(' E ')'
int F() {
  int f;
  char c = ch();
  if (isdigit(c)) {
    next(); // skip c
    f = nextTemp();
    printf("t%d=%c\n", f, c);
  } else if (c=='(') { // '(' E ')'
    next();
    f = E();
    assert(ch()==')');
    next();
  } else {
    error("F = (E) | Number fail!");
  }
  return f; 
}

// E = F ([+-] F)*
int E() {
  int i1 = F();
  while (isNext("+-")) {
    char op=next();
    int i2 = F();
    int i = nextTemp();
    printf("t%d=t%d%ct%d\n", i, i1, op, i2);
    i1 = i;
  }
  return i1;
}

void parse(char *str) {
  tokens = str;
  E();
}

int main(int argc, char * argv[]) {
  printf("argv[0]=%s argv[1]=%s\n", argv[0], argv[1]);
  printf("=== EBNF Grammar =====\n");
  printf("E=F ([+-] F)*\n");
  printf("F=Number | '(' E ')'\n");
  printf("==== parse:%s ========\n", argv[1]);
  parse(argv[1]);
}

```

#### 执行历史

```
PS F:\1文件\演算法\xtcs\sp\03-compiler\00-gen> gcc genExp.c rlib.c -o genExp
PS F:\1文件\演算法\xtcs\sp\03-compiler\00-gen> ./genExp
4/8
2
(1)/2
0*(5/0)-((4*6)*9)/((9/9)*6)
5*9
7*1
7*2+4*1
7
PS F:\1文件\演算法\xtcs\sp\03-compiler\00-gen> gcc genEnglish.c rlib.c -o genEnglish
PS F:\1文件\演算法\xtcs\sp\03-compiler\00-gen> ./genEnglish
the cat chase the dog
PS F:\1文件\演算法\xtcs\sp\03-compiler\01-exp0> gcc exp0.c -o exp0
PS F:\1文件\演算法\xtcs\sp\03-compiler\01-exp0> ./exp0 '3+5'
argv[0]=F:\1文件\演算法\xtcs\sp\03-compiler\01-exp0\exp0.exe argv[1]=3+5
=== EBNF Grammar =====
E=F ([+-] F)*
F=Number | '(' E ')'
==== parse:3+5 ========
t0=3
t1=5
t2=t0+t1
PS F:\1文件\演算法\xtcs\sp\03-compiler\01-exp0> ./exp0 '3+(5-4)'
argv[0]=F:\1文件\演算法\xtcs\sp\03-compiler\01-exp0\exp0.exe argv[1]=3+(5-4)
=== EBNF Grammar =====
E=F ([+-] F)*
F=Number | '(' E ')'
==== parse:3+(5-4) ========
t0=3
t1=5
t2=4
t3=t1-t2
t4=t0+t3
```
