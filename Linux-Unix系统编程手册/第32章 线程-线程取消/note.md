# 取消状态及类型
可以修改线程的取消状态
```
int pthread_setcancelstate(int state,int *oldstate)
int pthread_setcanceltype(int type,int *oldtype)
```

# 线程取消
```
//取消线程
int pthread_cancel(pthread_t thread) 
//在线程中检测当前线程是否取消，如果是 就终止
void pthread_testcancel();
```

# 线程清理
比如线程中在一个互斥量中间取消，会导致取消的线程没有释放锁，而导致死锁，所以需要线程清理
用来将共享变量以及pthread对象的不一致状态做处理
```
pthread_cleanup_pop()
pthread_cleanup_push()
```