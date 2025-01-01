---
title: Rustc交互
date: 2023-04-18T21:41:30+08:00
lastmod: 2023-04-18T21:41:30+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - category1
tags:
  - tag1
  - tag2
# nolastmod: true
draft: false
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
# rust c 交互
## rust 调用 c

* 调用普通`c`函数
```c
int add(int a, int b) {
    return a + b;
}
```

```rust
// main.rs
//指定链接到C 库
#[link(name = "add")]
extern {
    fn add(a: i32, b: i32) -> i32;
}

fn main() {
    let result = unsafe { add(1, 2) };
    println!("1 + 2 = {}", result);
}
```

```bash
# 编译C库
$ gcc -c -fPIC add.c -o add.o
$ gcc add.o -shared -o libadd.so

# rust 链接
$ rustc main.rs -L /path/to/library/folder -l add
$ ./main
1 + 2 = 3
```

* 调用C结构体
```c
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Point;

void print_point(Point* p) {
    printf("Point: (%d, %d)\n", p->x, p->y);
}
```

```rust
// main.rs

#[repr(C)]
struct Point {
    x: i32,
    y: i32,
}

#[link(name = "mylib")]
extern {
    fn print_point(p: *const Point);
}

fn main() {
    let p = Point { x: 10, y: 20 };
    
    // 转换 Point 结构体为 C 的结构体指针类型
    let c_p = &p as *const Point;

    // 调用 C 函数
    unsafe {
        print_point(c_p);
    }
}
```

* 调用C内存分配
```rust
// main.rs

use libc::{malloc, free};
use std::ffi::CString;

#[link(name = "mylib")]
extern {
    fn process_string(s: *const u8);
}

fn main() {
    let s = CString::new("Hello, world!").unwrap();

    // 计算字符串的长度（包括终止符）
    let len = s.as_bytes().len() + 1;

    // 在 C 中分配足够的空间来保存字符串
    let c_str = unsafe { malloc(len) as *mut u8 };

    // 把 Rust 字符串复制到 C 字符串中
    unsafe {
        std::ptr::copy_nonoverlapping(s.as_ptr(), c_str, len);
    }

    // 调用 C 函数并传递指向 C 字符串的指针
    unsafe {
        process_string(c_str);
    }

    // 释放由 C 分配的内存
    unsafe {
        free(c_str as *mut libc::c_void);
    }
}
```

* 调用C自定义内存分配函数
```rust
// main.rs

use std::os::raw::c_void;
use std::alloc::{Layout, alloc, dealloc};

extern "C" {
    fn my_malloc(size: usize) -> *mut c_void;
    fn my_free(ptr: *mut c_void);
}

fn main() {
    let size = 1024;

    // 在 Rust 中分配内存
    let layout = Layout::from_size_align(size, 1).unwrap();
    let ptr = unsafe { my_malloc(size) as *mut u8 };

    // 使用 Rust 操作分配的内存
    for i in 0..size {
        unsafe {
            *ptr.offset(i as isize) = i as u8;
        }
    }

    // 调用自定义的 C 函数释放内存
    unsafe {
        my_free(ptr as *mut c_void);
    }
}
```

## C调用rust

* `rust`代码
```rust
#[no_mangle]
pub extern "C" fn add_numbers(a:i32, b:i32) -> i32 {
    a + b
}
```
* C 使用动态库方式调用rust
```bash
rustc --crate-type=cdylib my_lib.rs
```

```c
#include <stdio.h>
#include <stdint.h>
#include <stdlib.h>
#include <dlfcn.h>

typedef void (*add_fn)(int32_t, int32_t, int32_t*);

int main() {
    void* handle = dlopen("./libmylib.so", RTLD_LAZY | RTLD_GLOBAL);
    if (!handle) {
        printf("Failed to open library: %s\n", dlerror());
        return -1;
    }
    add_fn add = (add_fn)dlsym(handle, "add");
    if (!add) {
        printf("Failed to find symbol: %s\n", dlerror());
        dlclose(handle);
        return -1;
    }
    int32_t a = 1;
    int32_t b = 2;
    int32_t result;
    int32_t *result_ptr = &result;
    add(a, b, result_ptr);
    printf("%d + %d = %d\n", a, b, result);
    dlclose(handle);
    return 0;
}
```



* C 使用静态库方式调用rust
```bash
rustc --crate-type=staticlib my_lib.rs
```

```c
#include <stdio.h>
#include <stdint.h>

extern int32_t add(int32_t, int32_t);

int main() {
    int32_t a = 1;
    int32_t b = 2;
    int32_t result = add(a, b);
    printf("%d + %d = %d\n", a, b, result);
    return 0;
}
```

* C 直接调用rust代码
```c
#include <stdio.h>
#include <stdint.h>

int32_t add(int32_t, int32_t);

int main() {
    int32_t a = 1;
    int32_t b = 2;
    int32_t result = add(a, b);
    printf("%d + %d = %d\n", a, b, result);
    return 0;
}
```