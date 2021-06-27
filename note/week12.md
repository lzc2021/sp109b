# 第十二周
## linux的行程管理
* 使用fork()分岔出新行程
* 使用execvp(prog,arg_list)將新行程替換為另一個程式
#### code
* fork1.c
```
#include <stdio.h> 
#include <sys/types.h> 
#include <unistd.h>

int main() { 
    fork(); // 一個行程分叉成父子兩個行程
    fork(); // 兩個行程又分別分叉出兩對父子，所以變成四個行程。
    printf("%-5d : Hello world!\n", getpid());
}

```
>fork() 複製行程 n---->2n <br>
>getpid就是得到該行程的識別碼
* result
```
yucheng@ubuntu:~/sp/08-posix/03-fork/01-hello$ gcc fork1.c -o fork1
yucheng@ubuntu:~/sp/08-posix/03-fork/01-hello$ ./fork1
4120  : Hello world!
4122  : Hello world!
yucheng@ubuntu:~/sp/08-posix/03-fork/01-hello$ 4121  : Hello world!
4123  : Hello world!
```
>fork() 的過程: 
>1. 4120-----> 4120&4121
>2. 4120----->4120&4122 , 4121----->4121&4123
* fork2.c
```
#include <stdio.h> 
#include <sys/types.h> 
#include <unistd.h>

int main() { 
    printf("%-5d : enter\n", getpid());
    fork(); // 一個行程分叉成父子兩個行程
    printf("%-5d : after 1st fork\n", getpid());
    fork(); // 兩個行程又分別分叉出兩對父子，所以變成四個行程。
    printf("%-5d : Hello world!\n", getpid());
}
```
