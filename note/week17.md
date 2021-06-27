# 第十七周

##  xv6
* xv6是在ANSI C中针对多处理器x86系统的Unix第六版的现代重新实现
* xv6 Makefile的一个特性是能够以可读的格式生成整个原始码清单的PDF文档
#### 定义
Xv6是由麻省理工学院(MIT)为操作系统工程的课程（代号6.828）,开发的一个教学目的的操作系统。Xv6是在x86处理器上(x即指x86)用ANSI标准C重新实现的Unix第六版(Unix V6，通常直接被称为V6)。

#### 历史
MIT的一个操作系统工程的课程，代号6.828最初使用了Unix v6和John Lion的《Unix V6注释和代码》这本书（通常被称为“狮”书，Lion是作者的姓，这里做为一个双关语，这本书使人们可以得到Unix的源代码）； 而在实验环节，学生们主要是在intel x86 的CPU上实现一个称为Jos的“外核”架构(exokernel)的操作系统。
向学生介绍多个系统（V6，Jos）能帮助他们建立更多操作系统设计的观念。但V6从一开始就导致了教学上的麻烦。很多学生怀疑使用V6这样一个30多年前的，使用旧式C语言（比K&R C还要旧）开发的，并且在过时的PDP-11硬件上运行的系统是否合适。而且学生们还要苦于同时学习PDP-11和Intel x86两种不同架构的底层差别。于是在2006年夏天，课程的老师们决定以V6为基础，使用ANSI C写一个新的在Intel x86多处理器计算机上的系统，也就是Xv6，来代替V6。Xv6使用x86 CPU，更适合学生的经验，而且将6.828课程统一到单一的体系结构上。增加多处理器支持需要使用锁和线程来处理并发（单处理器只要简单的开/关中断即可）。重写一个新系统的过程中，也使V6中比较粗糙的一些部分，如调度和文件系统得到了改进。于是MIT在2006年秋季的6.828课程中就开始使用Xv6了。

#### code
```
user@user:~/sp/10-riscv/04-xv6os/xv6$ make qemu
qemu-system-riscv64 -machine virt -bios none -kernel kernel/kernel -m 256M -smp 3 -nographic -drive file=fs.img,if=none,format=raw,id=x0 -device virtio-blk-device,drive=x0,bus=virtio-mmio-bus.0

xv6 kernel is booting

hart 2 starting
hart 1 starting
init: starting sh
$ ls
.              1 1 1024
..             1 1 1024
README         2 2 2058
cat            2 3 23976
echo           2 4 22808
forktest       2 5 13184
grep           2 6 27336
init           2 7 23912
kill           2 8 22784
ln             2 9 22736
ls             2 10 26216
mkdir          2 11 22888
rm             2 12 22872
sh             2 13 41760
stressfs       2 14 23880
usertests      2 15 153560
grind          2 16 38016
wc             2 17 25120
zombie         2 18 22280
console        3 19 0
yc             1 20 48
hello.txt      2 22 8
$ echo 'qemu' > qemu.txt
$ ls
.              1 1 1024
..             1 1 1024
README         2 2 2058
cat            2 3 23976
echo           2 4 22808
forktest       2 5 13184
grep           2 6 27336
init           2 7 23912
kill           2 8 22784
ln             2 9 22736
ls             2 10 26216
mkdir          2 11 22888
rm             2 12 22872
sh             2 13 41760
stressfs       2 14 23880
usertests      2 15 153560
grind          2 16 38016
wc             2 17 25120
zombie         2 18 22280
console        3 19 0
yc             1 20 48
hello.txt      2 22 8
qemu.txt       2 23 7
$ cat qemu.txt
'qemu'
$ QEMU: Terminated
```

> 参考资料：百度百科
