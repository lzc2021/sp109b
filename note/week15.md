# 第十五周

##  TCP & UDP
UDP 和 TCP 都是常见的网路通讯协定，这两种协定能确保网际网路资料传输的快速和完整性。它们做相同的工作，但运作方式不同，TCP 较可靠，UDP 较快速
###  TCP(传输控制协定)
* 是一种连接导向的、可靠的、基于位元组流的传输层通信协定
* 可以确保讯息的到达顺序，先送先到。会先双方建立安全连线，然后在通讯
#### 概念表达
传输控制协议（TCP，Transmission Control Protocol）是一种面向连接的、可靠的、基于字节流的传输层通信协议，由IETF的RFC 793定义。
TCP旨在适应支持多网络应用的分层协议层次结构。 连接到不同但互连的计算机通信网络的主计算机中的成对进程之间依靠TCP提供可靠的通信服务。TCP假设它可以从较低级别的协议获得简单的，可能不可靠的数据报服务。 原则上，TCP应该能够在从硬线连接到分组交换或电路交换网络的各种通信系统之上操作。
#### 定义
传输控制协议（TCP，Transmission Control Protocol）是为了在不可靠的互联网络上提供可靠的端到端字节流而专门设计的一个传输协议。
互联网络与单个网络有很大的不同，因为互联网络的不同部分可能有截然不同的拓扑结构、带宽、延迟、数据包大小和其他参数。TCP的设计目标是能够动态地适应互联网络的这些特性，而且具备面对各种故障时的健壮性。

###  UDP(使用者资料报协定)
* 属于非连接导向，直接通过socket通讯
* 是一个简单的面向资料报的通信协定，位于OSI模型的传输层
* UDP适用于不需要或在程式中执行错误检查和纠正的应用，它避免了协定栈中此类处理的开销
* 对时间有较高要求的应用程式通常使用UDP，因为丢弃封包比等待或重传导致延迟更可取

#### 概念表达
Internet 协议集支持一个无连接的传输协议，该协议称为用户数据报协议（UDP，User Datagram Protocol）。UDP 为应用程序提供了一种无需建立连接就可以发送封装的 IP 数据包的方法。RFC 768 描述了 UDP。
Internet 的传输层有两个主要协议，互为补充。无连接的是 UDP，它除了给应用程序发送数据包功能并允许它们在所需的层次上架构自己的协议之外，几乎没有做什么特别的事情。面向连接的是 TCP，该协议几乎做了所有的事情。

#### 定义
UDP 是User Datagram Protocol的简称， 中文名是用户数据报协议，是OSI（Open System Interconnection，开放式系统互联） 参考模型中一种无连接的传输层协议，提供面向事务的简单不可靠信息传送服务，IETF RFC 768 是UDP的正式规范。UDP在IP报文的协议号是17。
UDP协议与TCP协议一样用于处理数据包，在OSI模型中，两者都位于传输层，处于IP协议的上一层。UDP有不提供数据包分组、组装和不能对数据包进行排序的缺点，也就是说，当报文发送之后，是无法得知其是否安全完整到达的。UDP用来支持那些需要在计算机之间传输数据的网络应用。包括网络视频会议系统在内的众多的客户/服务器模式的网络应用都需要使用UDP协议。UDP协议从问世至今已经被使用了很多年，虽然其最初的光彩已经被一些类似协议所掩盖，但即使在今天UDP仍然不失为一项非常实用和可行的网络传输层协议。
#### code
* chat.c
```
#include <stdio.h>
#include <string.h>
#include <fcntl.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>

#define SMAX 80

int main(int argc, char *argv[]) {
    int fd;
    char *fifo0 = "/tmp/user0";
    char *fifo1 = "/tmp/user1";
    mkfifo(fifo0, 0666);
    mkfifo(fifo1, 0666);

    char *me, *you;
    if (strcmp(argv[1], "0")) { // me:0 => you:1
        me = fifo0;
        you = fifo1;
    } else { // me:1 => you:0
        me = fifo1;
        you = fifo0;
    }

    char msg[SMAX];
    if (fork() == 0) {
        // child: receive message and print (一直讀對方的訊息，讀到就印出來)
        fd = open(you, O_RDONLY); // 開啟對方管道
        while (1) {
            int n = read(fd, msg, sizeof(msg)); // 讀取對方發來的訊息
            if (n <= 0) break; // 如果管道已經關閉，就離開
            printf("receive: %s", msg); // 印出訊息
        }
        close(fd); // 關閉管道
    } else {
        // parent: readline and send （一直讀鍵盤，然後把訊息送給對方）
        fd = open(me, O_WRONLY); // 開啟我方管道
        while (1) {
            fgets(msg, SMAX, stdin); // 讀一行輸入
            int n = write(fd, msg, strlen(msg)+1); // 將該行輸入訊息送上我方管道
            if (n<=0) break;
        }
        close(fd);
    }
    return 0;
}
```
> 参考资料：百度百科
