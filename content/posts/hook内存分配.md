---
title: 内存泄漏检测
date: 2024-12-26T21:40:58+08:00
lastmod: 2024-12-26T21:40:58+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 编程
tags:
  - 内存泄漏
  - hook
# nolastmod: true
draft: false
---

内存泄漏检测
```cpp
#define _GNU_SOURCE
#include <dlfcn.h>
#include <stdlib.h>
#include <stdio.h>
#include <map>

// 用于存储内存块信息
std::map<void*, size_t> allocated_memory;

void* malloc(size_t size) {
    // 获取原始的 malloc 函数
    static void* (*original_malloc)(size_t) = nullptr;
    if (!original_malloc) {
        original_malloc = (void* (*)(size_t))dlsym(RTLD_NEXT, "malloc");
    }

    // 分配内存
    void* ptr = original_malloc(size);

    // 记录分配的内存块
    allocated_memory[ptr] = size;

    printf("malloc: %p, size: %zu\n", ptr, size);
    return ptr;
}

void free(void* ptr) {
    // 获取原始的 free 函数
    static void (*original_free)(void*) = nullptr;
    if (!original_free) {
        original_free = (void (*)(void*))dlsym(RTLD_NEXT, "free");
    }

    // 释放内存前检查是否存在泄漏
    if (allocated_memory.find(ptr) != allocated_memory.end()) {
        allocated_memory.erase(ptr);  // 删除记录
        printf("free: %p\n", ptr);
    } else {
        printf("Warning: Freeing unallocated memory: %p\n", ptr);
    }

    // 调用原始的 free 函数
    original_free(ptr);
}

// 内存泄漏检查函数
void check_memory_leaks() {
    if (!allocated_memory.empty()) {
        printf("Memory leaks detected:\n");
        for (const auto& entry : allocated_memory) {
            printf("Leaked memory: %p, size: %zu\n", entry.first, entry.second);
        }
    } else {
        printf("No memory leaks detected.\n");
    }
}

// 注册函数，在程序退出时自动调用 check_memory_leaks
void __attribute__((constructor)) register_leak_check() {
    atexit(check_memory_leaks);
}
```
