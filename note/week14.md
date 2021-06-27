# 第十四周

## socket通訊

* 是一種作業系統提供的行程間通訊機制
* Socket 就是一個網路上的通訊端點，使用者或應用程式只要連接到 Socket 便可以和網路上任何一個通訊端點連線，Socket 之間通訊就如同作業系統內程序（Process）之間通訊一樣
* 系統內部介面（內部網路），介面描述符（抽象介面描述符）和介面位址之間的差別其實很細微，日常編程用的時候幾乎不做區別

## HTTP協定格式
![image](https://user-images.githubusercontent.com/62127656/122156214-20c58380-ce9b-11eb-9094-2f21959f5960.png)
![image](https://user-images.githubusercontent.com/62127656/122156237-2e7b0900-ce9b-11eb-8b9c-c01e1b9231ff.png)
![image](https://user-images.githubusercontent.com/62127656/122156275-418dd900-ce9b-11eb-8f58-a2b8b0ef7d01.png)

#### code
* helloWebServer.c
```
#include "../net.h"
 
char response[] = "HTTP/1.1 200 OK\r\n"
"Content-Type: text/plain; charset=UTF-8\r\n"
"Content-Length: 14\r\n\r\n"
"Hello World!\r\n";

int main(int argc, char *argv[]) {
  int port = (argc >= 2) ? atoi(argv[1]) : PORT;
	net_t net;
	net_init(&net, TCP, SERVER, port, NULL);
	net_bind(&net);
	net_listen(&net);
  printf("Server started at port: %d\n", net.port);
  int count=0;
  while (1) {
		int client_fd = net_accept(&net);
    printf("%d:got connection, client_fd=%d\n", count++, client_fd);
    int n = write(client_fd, response, strlen(response));
    fsync(client_fd);
    assert(n > 0);
    sleep(1);
    close(client_fd);
  }
}
```
