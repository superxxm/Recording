# Thread Summary
## 目录
- 1.前言
- 2.线程标识，创建，终止
- 3.线程同步
### 1.前言
>线程（英语：__thread__）是操作系统能够进行运算调度的最小单位。被包含在进程中，是进程中实际运作的单位。一条线程指的是进程中一个单一的顺序控制流，一个进程中可以并发多个线程，每条线程并行执行不同的任务。（出自维基百科）

__线程与进程的区别__：一个程序至少有一个进程，一个进程至少有一个线程，线程的划分尺度要小于进程，所以多线程程序的并发性高。要开启一个进程，操作系统要为其分配内存空间及相应资源，而创建一个线程则不需要，同一进程内的不同线程共享父进程的空间资源。

__下面，以__`POSIX`线程__来介绍线程相关知识。__
### 2.线程标识，创建，终止
#### 2.1 线程标识
线程标识，即线程__ID__，类似进程__ID__,进程__ID__在整个系统中是唯一的，但线程__ID__不同，线程__ID__只有在它所属的进程上下文中才有意义。
线程__ID__是用`pthread_t`数据类型来表示的，实现的时候可以用一个结构来代表`pthread_t`数据类型，所以可移植的操作系统实现不能把它作为整数来处理。必须用一个函数来对两个线程__ID__进行比较。
```
#include <pthread.h>
int pthread_equal(pthread_t tid1, pthread_t tid2);
//返回值：若相等，返回非0数值，否则返回0
```
线程可以通过调用`pthread_self`函数来获得自身的线程__ID__
```
#include <pthread.h>
pthread_t pthread_self(void);
//返回值：调用线程的线程ID
```
#### 2.2线程创建
在__POSIX__线程的情况下，程序开始运行时，是以单线程中的单个控制线程启动的，创建多个控制线程之前，程序的行为与传统的进程并没有什么区别，新增的线程可以通过调用`pthread_create`函数来创建
```
#include <pthread.h>
int pthread_create(pthread_t *restrict tidp,
                   const pthread_attr_t *restrict,
                   void *(*start_rtn)(void *), void *restrict art);
//返回值：若成功，返回0;否则，返回错误编号                   
```
当`pthread_create`成功返回时，新创建的线程的__ID__会被设置成`tidp`指向的内存单元。`attr`参数用于定制不同的线程属性，`NULL`创建一个具有默认属性的线程。
新创建的线程从`start_rtn`函数的地址开始运行，该函数只有一个无类型指针参数`art`如果需要向函数传递的参数超过一个以上，那么需要把这些参数放到一个结构中，然后把这个结构的地址作为`arg`参数传入。
#### 2.3线程终止
单个线程可以通过3种方式退出，因此可以在不终止整个进程的情况下，停止它的控制流。
1. 线程可以简单的从启动例程中返回，返回值是线程的退出码。
2. 线程可以被同一进程中的其他线程取消。
3. 线程调用`pthread_exit`
```
#include <pthread.h>
void pthread_exit(void *rval_ptr);
```
`rval_ptr`参数是一个无类型指针，与传给启动例程的但个参数类似，进程中的其他线程也可以通过调用`pthread_join`函数访问到这个指针。
```
#include <pthread.h>
int pthread_join(pthread_t thread, void **rval_ptr);
//返回值：成功返回0，否则，返回错误编号。
```
调用线程将一直阻塞，直到指定的线程调用`pthread_exit`、从启动例程中返回或者被取消。如果线程简单地从它的启动例程返回，`rval_ptr`就包含返回码。如果线程被取消，由`rval_ptr`指定的内存单元就设置为`PTHREAD_CANCELED`。
可以通过调用`pthread_join`自动把线程设置与分离状态(后面会讨论到)，这样资源就可以恢复，如果线程已处于分离状态，`pthread_join`调用就会失败，返回`EINVAL`，尽管这种行为是与具体实现相关的。
如果对线程返回值并不感兴趣，可以把`rval_ptr`设为`NULL`这种情况下，调用`pthread_join`函数可以等待指定的线程终止，但并不获取线程终止状态。
如何获取已终止的线程的退出码。
```
#include <apue.h>
#include <pthread.h>

void *
thr_fn1(void *arg)
{
    printf("thread 1 returning\n");
    return ((void*)1);
}
void *
thr_fn2(void *arg)
{
    printf("thread 2 exiting\n");
    pthread_exit((void *)2);
}

int
main(void)
{
    int         err;
    pthread_t   tid1,tid2;
    void        *tret;

    err = pthread_create(&tid1, NULL, thr_fn1, NULL);
    if(err != 0)
        err_exit(err, "can`t create thread 1");
    err = pthread_create(&tid2, NULL, thr_fn2, NULL);
    if(err != 0)
        err_exit(err, "can`t create thread 2");
    err = pthread_join(tid1, &tret);
    if(err != 0)
        err_exit(err, "can`t join with thread 1");
    printf("thread 1 exit code %ld\n", (long)tret);
    err = pthread_join(tid2, &tret);
    if(err != 0)
        err_exit(err, "can`t join with thread 2");
    printf("thread 2 exit code %ld\n", (long)tret);
    exit(0);
}
```
### 3.线程同步
多进程程序需要我们考虑进程之间通信(IPC)的问题，而多线程本来就是共享统一进程的内存资源的，所以通信自然不成问题，但是多个线程同时访问一块内存区域就存在__同步__的问题了，下面就看看解决线程同步的一些方法。
#### 4.1互斥量
