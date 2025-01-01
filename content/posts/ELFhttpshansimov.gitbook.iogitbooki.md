---
title: ELFhttpshansimov.gitbook.iogitbooki
date: 2024-06-05T21:40:26+08:00
lastmod: 2024-06-05T21:40:26+08:00
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
![ELF](https://hansimov.gitbook.io/~gitbook/image?url=https%3A%2F%2F4154149387-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-legacy-files%2Fo%2Fassets%252F-MHt_spaxGgCbp2POnfq%252F-MI8p7rbEV-s_nV5Ru6X%252F-MI8pJh5IxzFL80HMTY3%252F07-03%2520%25E5%2585%25B8%25E5%259E%258B%25E7%259A%2584ELF%25E5%258F%25AF%25E9%2587%258D%25E5%25AE%259A%25E4%25BD%258D%25E7%259B%25AE%25E6%25A0%2587%25E6%2596%2587%25E4%25BB%25B6.png%3Falt%3Dmedia%26token%3Dd9d57c1c-24ef-401a-bf91-04bdf60fad68&width=400&dpr=3&quality=100&sign=5497b0ac1cb3f1a79b9438c992a2cd70c2c1a7c4fce58b010b191fad44aaec12)

.symtab：一个符号表，它存放在程序中定义和引用的函数和全局变量的信息。一些程序员错误地认为必须通过 -g 选项来编译一个程序，才能得到符号表信息。实际上，每个可重定位目标文件在 .symtab 中都有一张符号表（除非程序员特意用 STRIP 命令去掉它）。然而，和编译器中的符号表不同，.symtab 符号表不包含局部变量的条目。

.rel.text：一个 .text 节中位置的列表，当链接器把这个目标文件和其他文件组合时，需要修改这些位置。一般而言，任何调用外部函数或者引用全局变量的指令都需要修改。另一方面，调用本地函数的指令则不需要修改。注意，可执行目标文件中并不需要重定位信息，因此通常省略，除非用户显式地指示链接器包含这些信息。

.rel.data：被模块引用或定义的所有全局变量的重定位信息。一般而言，任何已初始化的全局变量，如果它的初始值是一个全局变量地址或者外部定义函数的地址，都需要被修改。

[重定位](https://hansimov.gitbook.io/csapp/part2/ch07-linking/7.7-relocation)

重定位节和符号定义。在这一步中，链接器将所有相同类型的节合并为同一类型的新的聚合节。例如，来自所有输入模块的. data 节被全部合并成一个节，这个节成为输出的可执行目标文件的. data 节。然后，链接器将运行时内存地址赋给新的聚合节，赋给输入模块定义的每个节，以及赋给输入模块定义的每个符号。当这一步完成时，程序中的每条指令和全局变量都有唯一的运行时内存地址了。

重定位节中的符号引用。在这一步中，链接器修改代码节和数据节中对每个符号的引用，使得它们指向正确的运行时地址。要执行这一步，链接器依赖于可重定位目标模块中称为重定位条目（relocation entry）的数据结构，我们接下来将会描述这种数据结构。

```c
typedef struct {
/*
    offset 是需要被修改的引用的节偏移。
    symbol 标识被修改引用应该指向的符号。
    type 告知链接器如何修改新的引用。
    addend 是一个有符号常数，一些类型的重定位要使用它对被修改引用的值做偏移调整
  */
    long offset;    /* Offset of the reference to relocate */
    long type:32,   /* Relocation type */
         symbol:32; /* Symbol table index */
    long addend;    /* Constant part of relocation expression */
} Elf64_Rela;
```

链接器的重定位算法的伪代码。第 1 行和第 2 行在每个节 s 以及与每个节相关联的重定位条目 r 上迭代执行。为了使描述具体化，假设每个节 s 是一个字节数组，每个重定位条目 r 是一个类型为 Elf64_Rela 的结构。另外，还假设当算法运行时，链接器已经为每个节（用 ADDR(s) 表示）和每个符号都选择了运行时地址（用 ADDR(r.symbol) 表示）。第 3 行计算的是需要被重定位的 4 字节引用的数组 s 中的地址。如果这个引用使用的是 PC 相对寻址，那么它就用第 5 ~ 9 行来重定位。如果该引用使用的是绝对寻址，它就通过第 11 ~ 13 行来重定位。

```c
foreach section s {
    foreach relocation entry r {
        refptr = s + r.offset;  /* ptr to reference to be relocated */
    
        /* Relocate a PC-relative reference */
        if (r.type == R_X86_64_PC32){
            refaddr = ADDR(s) + r.offset; /* ref's run-time address */
            *refptr = (unsigned) (ADDR(r.symbol) + r.addend - refaddr);
        }

        /* Relocate an absolute reference */
        if (r.type ==R_X86_64_32)
            *refptr = (unsigned) (ADDR(r.symbol) + r.addend);
    }
}
```

![ELF2](https://hansimov.gitbook.io/~gitbook/image?url=https%3A%2F%2F4154149387-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-legacy-files%2Fo%2Fassets%252F-MHt_spaxGgCbp2POnfq%252F-MI8pquOBkqRu_B1qWTy%252F-MI8q7GVbCgZ3tgNwsW_%252F07-13%2520%25E5%2585%25B8%25E5%259E%258B%25E7%259A%2584ELF%25E5%258F%25AF%25E6%2589%25A7%25E8%25A1%258C%25E7%259B%25AE%25E6%25A0%2587%25E6%2596%2587%25E4%25BB%25B6.png%3Falt%3Dmedia%26token%3Dee867860-bd62-4fa9-9505-e67f606b06f9&width=400&dpr=3&quality=100&sign=1f425dc9cb46ecff2c705d71d4d24e9553b7ba095d9b8c822ca9a891473192a0)

对于任何段 s，链接器必须选择一个起始地址 vaddr，使得

vaddr mod align = off mod align

这里，off 是目标文件中段的第一个节的偏移量，align 是程序头部中指定的对齐（ 221221 = 0x200000）。例如，图 7-14 中的数据段中

vaddr mod align = 0x600df8 mod 0x200000 = 0xdf8

以及

off mod align = 0xdf8 mod 0x200000 = 0xdf8


[打桩](https://hansimov.gitbook.io/csapp/part2/ch07-linking/7.13-library-interpositioning)


