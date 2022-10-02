# 在openEuler-22.03-LTS上使用bcc学习ebpf

BCC 是一个开源的 Linux 动态跟踪工具。无第三方模块依赖，该工具继承 BPF 这个强大的内核中虚拟机的功能，可对程序进行高效而且安全的跟踪

https://github.com/iovisor/bcc/blob/master/docs/tutorial_bcc_python_developer.md

官方入门参考文档

## 1. 在openEuler-22.03-LTS上下载bcc

openEuler-22.03-LTS本身有bcc的安装包，直接通过下面的命令下载即可

```
yum install bcc
```

但是需要注意一点，在使用python编写bcc脚本时需要使用

```
from bpfcc import BPF
```

## 2. github下载bcc的源码

```
git clone https://github.com/iovisor/bcc.git
```

跳转到bcc/example目录下，直接执行hello_world.py

注意要将

```
from bcc import BPF
```

替换为

```
from bpfcc import BPF
```

如果有报错，显示没有kernel_headers

![无kernel_headers报错](.\bcc_image\无kernel_headers报错.JPG)

可以执行命令

```
yum install kernel-devel kernel-headers
```

最终是要在当前内核版本对应的/lib/module/$(uname -r)目录下找到build文件和source文件，如果安装的是不同版本的kernel-headers，只要创建软链接即可

```shell
/lib/modules/5.10.0-60.18.0.13.oe2203.raspi.aarch64
[root@openEuler 5.10.0-60.18.0.13.oe2203.raspi.aarch64]# ll
total 2.4M
lrwxrwxrwx  1 root root   41 Sep 22 22:24 build -> ../5.10.0-60.56.0.84.oe2203.aarch64/build
drwxr-xr-x 11 root root 4.0K Mar 27 08:00 kernel
-rw-r--r--  1 root root 580K Mar 27 08:00 modules.alias
-rw-r--r--  1 root root 603K Mar 27 08:00 modules.alias.bin
-rw-r--r--  1 root root  15K Mar 27 08:00 modules.builtin
-rw-r--r--  1 root root  28K Mar 27 08:00 modules.builtin.alias.bin
-rw-r--r--  1 root root  16K Mar 27 08:00 modules.builtin.bin
-rw-r--r--  1 root root  82K Mar 27 08:00 modules.builtin.modinfo
-rw-r--r--  1 root root 197K Mar 27 08:00 modules.dep
-rw-r--r--  1 root root 272K Mar 27 08:00 modules.dep.bin
-rw-r--r--  1 root root  384 Mar 27 08:00 modules.devname
-rw-r--r--  1 root root  65K Mar 27 08:00 modules.order
-rw-r--r--  1 root root  407 Mar 27 08:00 modules.softdep
-rw-r--r--  1 root root 258K Mar 27 08:00 modules.symbols
-rw-r--r--  1 root root 314K Mar 27 08:00 modules.symbols.bin
lrwxrwxrwx  1 root root   42 Sep 22 22:25 source -> ../5.10.0-60.56.0.84.oe2203.aarch64/source
[root@openEuler 5.10.0-60.18.0.13.oe2203.raspi.aarch64]# uname -a
Linux openEuler 5.10.0-60.18.0.13.oe2203.raspi.aarch64 #1 SMP PREEMPT Wed Mar 30 05:01:23 UTC 2022 aarch64 aarch64 aarch64 GNU/Linux
[root@openEuler 5.10.0-60.18.0.13.oe2203.raspi.aarch64]#
```

## 3. 执行文件

```shell
./hello_world.py
```

这个文件的作用是在clone一个新的线程时，打印hello world。此时需要在另一个终端上敲入一些命令。在内核中创建一些线程，就可以看到下面的hello world的打印，amazing!!!

```shell
[root@openEuler examples]# ./hello_world.py
b'           <...>-744     [003] d..3  2062.536327: bpf_trace_printk: Hello, World!'
b''
b'            bash-744     [003] d..3  2068.001262: bpf_trace_printk: Hello, World!'
b''
```

Ctrl^C 可以停止执行

```python
from bpfcc import BPF

# This may not work for 4.17 on x64, you need replace kprobe__sys_clone with kprobe____x64_sys_clone
BPF(text='int kprobe__sys_clone(void *ctx) { bpf_trace_printk("Hello, World!\\n"); return 0; }').trace_print()
```

