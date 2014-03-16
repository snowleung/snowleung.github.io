---
layout: post
title: "fileIO_index"
date: 2014-03-16 17:07
comments: true
categories: [unix,Reading]
---

3.2 文件描述符 @ <unistd.h>

>POSIX
>0. STDIN_FILENO
>1. STDOUT_FILENO
>2. STDERR_FILENO

3.3 open @ <fcntl.h>

>int open(const char *pathname, int oflag, ...)
>oflag: 
>>O_RDONLY
>>O_WRONLY
>>O_RDWR
>>其他可用oflag有:O_APPEND,O_CREAT ...
>pathname,有 NAME_MAX 限制

3.4 creat @ <fcntl.h>

>int creat(const char *pathname, mode_t mode)
>the same whit this function: 
>open(pathname, O_WRONLY|O_CREAT|O_TRUNC, mode) 

3.5 close @ <unistd.h>

>int close(int filedes)

3.6 lseek @ <unistd.h>

>off_t lseek(int filedes, off_t offset, int whence) 

3.7 read @ <unistd.h>

>ssize_t read(int filedes, void *buf, size_t nbytes)

3.8 write @ <unistd.h>

>ssize_t write(int filedes, const void *buf, size_t nbytes)

3.9 I/O 效率

>

3.10 文件共享

>v node

3.11 原子操作

>ssize_t pread(int filedes, void *buf, size_t bytes, off_t offset)
>ssize_t pwrite(int filedes, void *buf, size_t bytes, off_t offset)

3.12 dup和dup2

>int dup(int filedes)
>int dup(int filedes, int filedes2)
>dup 返回新文件描述符一定是当前可用文件描述符中的最小数值。

3.13 sync, fsync, fdatasync

>int fsync(int filedes), 只对filedes写入磁盘后返回，适用数据库操作
>int fdatasync(int filedes), 只影响文件数据部分，fsync还会更新文件属性
>void sync(void),将缓冲排入写队列后返回（未必写入磁盘）

3.14 fcntl @ fcntl,h

>int fcntl(int filedes, int cmd, .../*int arg*/)
>改变已打开的文件的性质。
>fcntl的返回值与命令有关。
>复制一个现有的描述符 cmd = F_DUPFD
>获得/设置文件描述符标记 F_GETFD 或 F_SETFD

3.15 ioctl

>int ioctl(int filedes, int request, ...)

3.16 /dev/fd

>打开文件/dev/fd/n 等于有效复制描述符n (假定描述符n是打开的)







