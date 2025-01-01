---
title: CELF
date: 2024-12-24T21:40:31+08:00
lastmod: 2024-12-24T21:40:31+08:00
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
# C ELF

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/mman.h>
#include <libelf.h>
#include <gelf.h>
#include <string.h>
#include <err.h>

int main(int argc, char **argv)
{
    int fd;
    Elf *e;
    Elf_Kind ek;
    size_t shstrndx;

    if (argc != 2)
    {
        errx(EXIT_FAILURE, "Usage: %s <elf_file>\n", argv[0]);
    }

    if (elf_version(EV_CURRENT) == EV_NONE)
    {
        errx(EXIT_FAILURE, "Failed to initialize the libelf library\n");
    }

    if ((fd = open(argv[1], O_RDONLY, 0)) < 0)
    {
        err(EXIT_FAILURE, "open");
    }

    if ((e = elf_begin(fd, ELF_C_READ, NULL)) == NULL)
    {
        errx(EXIT_FAILURE, "elf_begin() failed: %s\n", elf_errmsg(-1));
    }

    if (elf_kind(e) != ELF_K_ELF)
    {
        errx(EXIT_FAILURE, "%s is not an ELF object\n", argv[1]);
    }

    if (elf_getshdrstrndx(e, &shstrndx) != 0)
    {
        errx(EXIT_FAILURE, "elf_getshdrstrndx() failed: %s\n", elf_errmsg(-1));
    }
    size_t phnum;
    if (elf_getphdrnum(e, &phnum) != 0)
    {
        elf_end(e);
        close(fd);
        errx(EXIT_FAILURE, "elf_getphdrnum() failed: %s\n", elf_errmsg(-1));
    }

    // 遍历所有的程序头
    for (size_t i = 0; i < phnum; i++)
    {
        GElf_Phdr phdr;
        if (gelf_getphdr(e, i, &phdr) != &phdr)
        {
            elf_end(e);
            close(fd);
            errx(EXIT_FAILURE, "elf_getphdrnum() failed: %s\n", elf_errmsg(-1));
        }

        // 检查是否是PT_LOAD类型的segment
        if (phdr.p_type == PT_LOAD)
        {
            printf("Found LOAD segment at offset 0x%lx with size 0x%lx\n", (long)phdr.p_offset, (long)phdr.p_filesz);

            off_t aligned_offset = phdr.p_offset & ~(phdr.p_align - 1);
            size_t offset_diff = phdr.p_offset - aligned_offset;
            size_t map_size = phdr.p_filesz + offset_diff;

            int prot = 0;
            if (phdr.p_flags & PF_R) prot |= PROT_READ;
            if (phdr.p_flags & PF_W) prot |= PROT_WRITE;
            if (phdr.p_flags & PF_X) prot |= PROT_EXEC;

            // 使用mmap将该段映射到内存
            void *map_addr = mmap(NULL, map_size, prot, MAP_PRIVATE | MAP_FIXED, fd, aligned_offset);

            // 调整到正确的内存位置
            void *segment_addr = (char *)map_addr + offset_diff;
            size_t phy_offset = phdr.p_paddr - aligned_offset;
            if (!(prot & PROT_WRITE) && (map_size > phdr.p_filesz)){
                void *zero_start = (char *)segment_addr + phy_offset + phdr.p_filesz;
                size_t zero_size = map_size - phdr.p_filesz;
                memset(zero_start, 0, zero_size);
            }

            printf("align segment at address %p ~ %p\n", segment_addr, segment_addr+map_size);

            // // 解除内存映射
            // if (munmap(map_addr, phdr.p_memsz) < 0)
            // {
            //     perror("munmap");
            //     elf_end(e);
            //     close(fd);
            //     exit(1);
            // }
        }
    }

    elf_end(e);
    close(fd);

    return 0;
}
```

Tags:
  elf