---
title: Ffsbdataprocess
date: 2021-09-03T21:40:47+08:00
lastmod: 2021-09-03T21:40:47+08:00
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
# ffsb data process
```python
#!/bin/python
# --*--coding: utf-8 --*--

import re
import sys

filename = sys.argv[1]

opNames = ["create", "readall", "append", "stat", "delete", "writeall",
           "writeall_fsync", "open_close", "create_fsync", "append_fsync"]

sumNames = ["open", "read", "write", "unlink", "close", "stat"]

opValue = ["Transactions", "TPS", "TPercent", "OpWeight"]
sumValue = ["Min", "Avg", "Max"]

reg_op = '''^\s+\w+\s\:(\s+\d+(\.?\d+\%?)?){4}'''
reg_sum = '''\[(\s*\w+)\](\s+\d+(\.\d+)?){4}'''
reg_read_th = '''Read Throughput: (\d+\.?\d+?[M|K])B\/sec'''
reg_write_th = '''Write Throughput: (\d+\.?\d+?[M|K])B\/sec'''

unit_map = {'Transactions': 'Trans', 'TPS': 'Trans/sec',
            'TPercent': '%', 'OpWeight': '%'}

benchmark_op = dict()
benchmark_sum = dict()
benchmark_read = list()
benchmark_write = list()


def process_data():
    for p in opNames:
        benchmark_op[p] = dict()
        for k in opValue:
            benchmark_op[p][k] = list()

    for s in sumNames:
        benchmark_sum[s] = dict()
        for k in sumValue:
            benchmark_sum[s][k] = list()

    pattern_op = re.compile(reg_op, re.I)
    pattern_sum = re.compile(reg_sum, re.I)
    with open(filename) as ffsb:
        for line in ffsb:
            m = pattern_op.match(line)
            try:
                if m:
                    lineStr = m.group(0)
                    array = lineStr.strip().split()
                    for x in range(len(opValue)):
                        benchmark_op[array[0]][opValue[x]].append(
                            float(array[2 + x].strip('% KMB/sec')))
                else:
                    m = pattern_sum.match(line)
                    if m:
                        array = line.strip(' []').split()
                        for x in range(len(sumValue)):
                            benchmark_sum[array[0].strip('[]')][
                                sumValue[x]].append(float(array[1 + x].strip()))
                    else:
                        m = re.match(reg_read_th, line)
                        if m:
                            value = m.group(1)
                            if value[-1] == 'M':
                                benchmark_read.append(float(value[:-1]) * 1024)
                            else:
                                benchmark_read.append(float(value[:-1]))
                        else:
                            m = re.match(reg_write_th, line)
                            if m:
                                value = m.group(1)
                                if value[-1] == 'M':
                                    benchmark_write.append(
                                        float(value[:-1]) * 1024)
                                else:
                                    benchmark_write.append(float(value[:-1]))

            except Exception as e:
                raise e


def print_data():
    for op in opNames:
        for k in opValue:
            try:
                value = benchmark_op[op][k]
                if value:
                    print('Main.%s.%s %s' % (op, k, " ".join(str(x)
                                                             for x in benchmark_op[op][k])))
            except Exception as e:
                pass

    print('Throughput.Read %s' % " ".join(str(x) for x in benchmark_read))
    print('Throughput.Write %s' % " ".join(str(x) for x in benchmark_write))

    for s in sumNames:
        for k in sumValue:
            try:
                value = benchmark_sum[s][k]
                if value:
                    print('Syscall_latency.%s.%s %s' %
                          (s, k, " ".join(str(x) for x in benchmark_sum[s][k])))
            except Exception as e:
                pass


avg_benchmark_op = dict()
avg_benchmark_sum = dict()


def process_benchmark():
    for op in opNames:
        avg_benchmark_op[op] = dict()
        for k in opValue:
            length = len(benchmark_op[op][k])
            if length:
                avg_benchmark_op[op][k] = (float('%.3f' % (sum(benchmark_op[op][k]) / length)),
                                           min(benchmark_op[op][k]),
                                           max(benchmark_op[op][k]))

    for s in sumNames:
        avg_benchmark_sum[s] = dict()
        for k in sumValue:
            length = len(benchmark_sum[s][k])
            if length:
                avg_benchmark_sum[s][k] = (float('%.3f' % (sum(benchmark_sum[s][k]) / length)),
                                           min(benchmark_sum[s][k]),
                                           max(benchmark_sum[s][k]))


def print_benchmark():
    for op in opNames:
        for k in opValue:
            try:
                value = avg_benchmark_op[op][k]
                if value:
                    print('Main.%s.%s %.3f %s %.3f %.3f' %
                          (op, k, value[0],
                           unit_map[k], value[1] / value[0], value[2] / value[0]))
            except Exception as e:
                pass

    read_avg = sum(benchmark_read) / len(benchmark_read)
    write_avg = sum(benchmark_write) / len(benchmark_write)
    print('Throughput.Read %.3f KB/sec %.3f %.3f' %
          (read_avg, min(benchmark_read) / read_avg,
           max(benchmark_read) / read_avg))
    print('Throughput.Write %.3f KB/sec %.3f %.3f' %
          (write_avg, min(benchmark_write) / write_avg,
           max(benchmark_write) / write_avg))

    for s in sumNames:
        for k in sumValue:
            try:
                value = avg_benchmark_sum[s][k]
                if value:
                    print('Syscall_latency.%s.%s %.3f milliseconds %.3f %.3f' %
                          (s, k, value[0], value[1] / value[0], value[2] / value[0]))
            except Exception as e:
                pass

xlsx_filename = 'benchmark_1.xlsx'


def process_excel():
    from openpyxl import Workbook
    wb = Workbook()
    ben = wb.active
    ben.append()


def process_excel_head():
    pass


def process_excel_data():
    pass
```

Tags:
  ffsb