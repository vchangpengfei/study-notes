#相关链接
官网
https://man7.org/tlpi/index.html
错误解决
https://man7.org/tlpi/code/faq.html#sys-capability.h-missing
代码下载
https://github.com/bradfa/tlpi-dist

需要对一些基本概念有所了解 如下

# c语言基础

宏：类似一个模板，c语言代码在编译前预处理做替换，并且可以通过传入参数，来做不同的代码预处理

## 指针

指针声明：int * p;
指针初始化：&变量名称，如 &a
指针访问及修改：*p
空指针：没有初始化的变量默认赋值指针的位置为0，这个地址是不允许访问的
野指针：访问不是自己申请的内存地址
指针指向可以修改，指针的值不可以修改 常量指针 指针常量
sizeof
指针遍历数组 p++

## typedef

一种数据起的别名

```
//定义
#define	EXIT_SUCCESS	0
//使用
exit(EXIT_SUCCESS);
```

# makefile

