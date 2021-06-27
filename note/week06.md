# 第六周

## 编译流程

![image](https://github.com/lzc2021/sp109b/blob/main/image/01.png)

```
直接編譯連結，產生執行檔
$ gcc main.c sum.c -o run    //-o:指定輸出檔
$ gcc main.c sum.c           //輸出檔檔名為a.exe(Windows)、a.out(Mac)

產生組合語言(-S)
$ gcc -S main.c -o main.s

組譯後連結,產生執行檔
$ gcc main.c sum.s -o run

產生目的檔(-c)
$ gcc -c sum.c -o sum.o

連結目的檔,產生執行檔
$ gcc main.o sum.o -o run
```

![image](https://github.com/lzc2021/sp109b/blob/main/image/02.png)

![image](https://github.com/lzc2021/sp109b/blob/main/image/03.png)
