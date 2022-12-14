# 线程特有数据
```c
    pthread_key_create(pthread_key_t *key,void(*destructor)(void *))
```
数据结构
- 一个全局（进程范围）数组，存放线程特有数据的键信息。
- 每个线程包含一个数组，存有为每个线程分配的线程特有数据块的指针（通过调用 pthread_setspecific()来存储指针）。
- 线程数组中每个元素 有两个字段组成 
    1. 该元素是否在使用（即已由之前对 pthread_key_create()的调用分配）。
    2. 用于存放针对此键、线程特有数据块的解构函数指针（是函数 pthread_key_crate()中参数 destructor 的一份拷贝）。


# 线程局部存储
__thread 关键字表示每一个线程有一份独立的实体，每一个线程都不会干扰。
```
static __thread char buf[MAX_ERROR_LEN];
```
