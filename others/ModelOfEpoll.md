# epoll IO多路复用模型

对于IO多路复用模型，有3种，分别是select poll与epoll。
对于select模型，select函数的原型为:
```cython
int select(int numfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds，struct timeval *timeout)
```
readfds参数表示监控的准备好的可读描述符集合，writefds表示准备好的可写描述符集合，exceptfds表示准备好的错误文件描述符集合，timeout表示select调用的超时时间。

select调用返回时，readfds会指向真正可读的描述符集合，writefds指向真正可写的描述符集合，exceptfds同理。select返回值为真正发生事件的文件描述符的总数。
select并不会直接告诉进程发生IO事件的描述符，仅仅只是通知进程有IO事件发生或本次监听已超时，每次select调用完成，需要进程轮询所有的描述符来获取实际发生IO事件的描述符。

select的缺点：select需要将监听的描述符从用户态拷贝到内核态，因此如果监听大量的文件描述符时，会占用过多内存空间，同时进程需要轮询描述符，会导致效率极低。select中监听文件描述符的集合通过位图来表示，默认监听的最大文件描述符为1024.

对于poll模型，poll和select非常相似，本质的区别在于存放fd集合的数据结构不同。poll通过链表来维护描述符集合，因此突破了select监听文件描述符数量的限制。但是select和poll都有一个问题，它们是通过轮询的方式来检查文件描述符可读或可写，造成了资源浪费。

epoll模型是前两者的加强。
有关于epoll原理的理解，参考[这篇文章](https://www.zhihu.com/search?type=content&q=epoll)。

