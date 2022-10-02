# ebpf相关的笔记

https://zhuanlan.zhihu.com/p/533747093

ebpf入门与实战指南

https://blog.csdn.net/bigwhite20xx/article/details/125631057

一文搞懂如何从头开发一个Hello World级的eBPF程序

## 1. trace + ebpf

## 2. ebpf入门用例介绍

基于sample编写hello world

从openEuler官网获取linux内核源码

比较下来应该是使用libbpf-bootstrap框架，进行hello world程序编写入手更快一点。

## 2. 写一段代码利用ebpf从内核中导出CPU利用率信息