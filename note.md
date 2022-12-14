# 概述

介绍posix线程，即pthreads

一个进程可以包含多个线程。

同一程序的所有线程独立执行相同的程序，且共享同一份内存区域，其中包括

- 初始化数据段（initialized data）
- 未初始化数据段（uninitialized data）
- 堆内存段

以上是进程的数据组成，可以回顾下老的知识点

多处理器环境下，同一进程中多个线程可以并发执行

线程优于进程，网络服务器举例：服务器进程（父进程）在接受客户端的连接后，会调用fork创建一个单独的子进程，处理客户端的请求。
采用这种设计，服务器能同时为多个客户端提供服务。但某些情况下的确存在一些限制

- 进程间信息难以共享，进程间通信得依靠ipc的方式
- 调用fork创建进程的代价较高，cow技术仍需复制诸如内存页表（page table)和文件描述符（fd)之类的多种进程属性
  线程解决了上述两个问题
- 线程间可以方便快速的共享信息。只需要将数据复制到共享（全局或堆）变量中即可。
- 创建线程比创建进程通常要快10倍甚至更多。快的主要原因是避免了cow时的数据复制
  **除了全局内存外，线程还共享其他的属性，包括如下内容**
- 进程id和父进程id
- 进程组id和会话id
- 控制终端
- 进程凭证
- 打开的文件描述符
- 由fcntl创建的记录锁
- 信号处置
- 文件系统的相关信息：文件权限掩码、当前工作目录和根目录
- 定时器
- 信号量
- 资源限制
- cpu时间消耗
- 资源消耗
- nice值（setpriority 和 nice设置）
  **线程独有的属性**
- 线程id
- 信号掩码
- 线程特有数据
- 备选信号栈
- errno变量
- 浮点型环境
- 实时调度策略和优先级
- cpu亲和力
- 能力
- 栈，本地变量和函数的调用链接信息

# pthreads api

pthreads data type结构如下


| 数据类型        | 描述             | 备注 |
| ----------------- | ------------------ | ------ |
| pthread_t       | 线程id           |      |
| pthread_mutex_t | 互斥对象（Mutex) |      |
|                 |                  |      |
|                 |                  |      |
|                 |                  |      |
|                 |                  |      |
|                 |                  |      |
|                 |                  |      |

在多线程的程序中，每个线程都有属于自己的errno

pthread函数均以返回0表示成功，返回正值表示失败，这个值和errno的值含义相同。

创建线程函数

```
int pthread_create(pthread_t *thread,const pthread_attr_t *attr,void *(*start)(void *),void *arg);
Return 0 on success,or a positive error number on error
```

线程的终止

void pthread_exit(void *retval)

获取线程id

pthread_t pthread_self(void);

join线程

pthread_join(pthread_t thread,void **retval) 可以通过retval获取线程的返回值

线程分离

pthread_detach(pthread_t thread) 分离状态的线程，不能被join,也就不能获取返回值

线程属性

pthread_create 方法签名第二个参数，是pthread_attr_t ,可以指定线程的属性

# 线程VS进程


线程有点有：

- 数据共享简单。
- 创建快速是进程的十倍
- 线程间的上下文切换比进程一般都要短

缺点有：

- 编程时要确保函数线程安全
- 某个线程的bug可能导致整个进程不可用
- 每个线程都在争用宿主进程有限的虚拟地址空间（虚拟地址空间大小受 外存容量和CPU地址表示的范围的限制）
