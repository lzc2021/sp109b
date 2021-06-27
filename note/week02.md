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

## Paser理论基础
Grammar 语法
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
