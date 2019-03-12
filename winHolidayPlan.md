# 系统调用-寒假规划

## 背景

别问，问就是没有背景瞎操作。

## 环境及工具

- `Debian9.7 - 32位`
- `python3`

## 技术储备

| 技术 | 储备 |
|---|---|
| linux简单操作 | :-) |
| gdb | `$ man gdb` |
| python | 就菜鸡玖不会 :-( |
| python gdb库 | [Python-GDB-API](https://sourceware.org/gdb/onlinedocs/gdb/Python-API.html) |
| strace 命令 | [Linux strace命令](https://www.cnblogs.com/ggjucheng/archive/2012/01/08/2316692.html) 或 `$ man starce` |
| 系统调用函数 | [syscalls - Linux system calls](http://www.man7.org/linux/man-pages/man2/syscalls.2.html#top_of_page) 或 `$ man syscalls` |
| 计算机组成原理 | [MOOC计算机系统基础(一)](https://www.icourse163.org/course/NJU-1001625001) 和 [MOOC计算机系统基础(三)](https://www.icourse163.org/course/NJU-1002532004) |

大神博客分享：

- [Linux/Unix笔记本](https://www.cnblogs.com/ggjucheng/archive/2012/08/18/2645321.html)
- [gdb跟踪分析系统调用system_call的处理过程](https://blog.csdn.net/bshcc/article/details/50950604)
- [Python 拓展 GDB](http://python.jobbole.com/85415/)

## 短期目标

由于具体指导方案没有给出，前期只好先技术储备，并在秦师傅的带领下完成一些小目标：

1. 用`python`代码实现`gdb`的几个简单功能
2. 探索如何用`gdb`跟踪系统调用

尽量在开学前完成（打字人已心虚