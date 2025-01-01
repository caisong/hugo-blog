---
title: Ffsbpython解析输出excel
date: 2021-09-03T21:40:48+08:00
lastmod: 2021-09-03T21:40:48+08:00
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
# ffsb python解析输出excel
```python
#!/bin/python
# --*--coding: utf-8 --*--

import re
import sys


excel_file = 'benchmark_test.xlsx'

opNames = ["create", "readall", "append", "stat",
           "delete", "writeall", "writeall_fsync", "open_close",
           "create_fsync", "append_fsync"]

sumNames = ["open", "read", "write", "unlink", "close", "stat"]

opValue = ["Transactions", "TPS", "TPercent", "OpWeight"]
sumValue = ["Min", "Avg", "Max"]

benchmark_op = dict()
avg_benchmark_op = dict()
benchmark_sum = dict()
avg_benchmark_sum = dict()
benchmark_read = list()
benchmark_write = list()

for p in opNames:
    benchmark_op[p] = dict()
    for k in opValue:
        benchmark_op[p][k] = list()

for s in sumNames:
    benchmark_sum[s] = dict()
    for k in sumValue:
        benchmark_sum[s][k] = list()

reg_op = '''^\s+\w+\s\:(\s+\d+(\.?\d+\%?)?){4}'''
reg_sum = '''\[(\s*\w+)\](\s+\d+(\.\d+)?){4}'''
reg_read_th = '''Read Throughput: (\d+\.?\d+?[M|K])B\/sec'''
reg_write_th = '''Write Throughput: (\d+\.?\d+?[M|K])B\/sec'''

unit_map = {'Transactions': 'Trans', 'TPS': 'Trans/sec',
            'TPercent': '%', 'OpWeight': '%'}


def process_data(filename):
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
                pass


def print_output():
    for op in opNames:
        for k in opValue:
            try:
                value = benchmark_op[op][k]
                if value:
                    print('Main.%s.%s %s' %
                          (op, k, ' '.join(str(x) for x in benchmark_op[op][k])))
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


def process_benchmark(data):
    if len(data) == 0:
        return None
    avg = sum(data) / len(data)
    cirtion_1 = min(data) / avg
    cirtion_2 = max(data) / avg
    return avg, cirtion_1, cirtion_2


def print_benchmark():
    for op in opNames:
        for k in opValue:
            try:
                value = process_benchmark(benchmark_op[op][k])
                if value:
                    print('Main.%s.%s %.3f %s %.2f %.2f' %
                          (op, k, value[0], unit_map[k], value[1], value[2]))
            except Exception as e:
                pass

    value = process_benchmark(benchmark_read)
    print('Throughput.Read %.3f KB/S %.2f %.2f' %
          (value[0], value[1], value[2]))
    value = process_benchmark(benchmark_write)
    print('Throughput.Write %.3f KB/S %.2f %.2f' %
          (value[0], value[1], value[2]))

    for s in sumNames:
        for k in sumValue:
            try:
                value = process_benchmark(benchmark_sum[s][k])
                if value:
                    print('Syscall_latency.%s.%s %.3f milliseconds %.2f %.2f' %
                          (s, k, value[0], unit_map[k], value[1], value[2]))
            except Exception as e:
                pass


def print_benchmark_to_excel():
    import xlsxwriter
    workbook = xlsxwriter.Workbook(excel_file)
    worksheet = workbook.add_worksheet()
    worksheet.write(0, 0, 'Benchmark.ffsb')
    worksheet.write(0, 1, 'Average')
    worksheet.write(0, 2, 'Unit')
    merge_format = workbook.add_format({
        'align': 'center',
        'valign': 'vcenter'})
    worksheet.merge_range('D1:E1', 'Range', merge_format)
    row = 1
    col = 0
    for op in opNames:
        for k in opValue:
            try:
                value = process_benchmark(benchmark_op[op][k])
                if value:
                    worksheet.write(row, col, 'Main.{}.{}'.format(op, k))
                    worksheet.write(row, col + 1, value[0])
                    worksheet.write(row, col + 2, unit_map[k])
                    worksheet.write(row, col + 3, value[1])
                    worksheet.write(row, col + 4, value[2])
                    row += 1
            except Exception as e:
                pass

    value = process_benchmark(benchmark_read)
    worksheet.write(row, col, 'Throughput.Read')
    worksheet.write(row, col + 1, value[0])
    worksheet.write(row, col + 2, 'KB/S')
    worksheet.write(row, col + 3, value[1])
    worksheet.write(row, col + 4, value[2])
    row += 1

    value = process_benchmark(benchmark_write)
    worksheet.write(row, col, 'Throughput.Write')
    worksheet.write(row, col + 1, value[0])
    worksheet.write(row, col + 2, 'KB/S')
    worksheet.write(row, col + 3, value[1])
    worksheet.write(row, col + 4, value[2])
    row += 1

    for s in sumNames:
        for k in sumValue:
            try:
                value = process_benchmark(benchmark_sum[s][k])
                if value:
                    worksheet.write(
                        row, col, 'Syscall_latency.{}.{}'.format(s, k))
                    worksheet.write(row, col + 1, value[0])
                    worksheet.write(row, col + 2, 'milliseconds')
                    worksheet.write(row, col + 3, value[1])
                    worksheet.write(row, col + 4, value[2])
                    row += 1
            except Exception as e:
                pass
    workbook.close()


def append_data_to_excel():
    import xlsxwriter
    import xlrd
    wbRD = xlrd.open_workbook(excel_file)
    sheets = wbRD.sheets()
    wb = xlsxwriter.Workbook(excel_file)

    r_sheet = w_sheet = None
    for sheet in sheets:  # write data from old file
        newSheet = wb.add_worksheet(sheet.name)
        if sheet.name == '' or True:
            r_sheet = sheet
            w_sheet = newSheet

        for row in range(sheet.nrows):
            for col in range(sheet.ncols):
                newSheet.write(row, col, sheet.cell(row, col).value)

    # D2~E2

    red_format = wb.add_format({'bg_color': 'red'})

    begin_col = r_sheet.ncols
    for row in range(1, r_sheet.nrows):
        average_value = r_sheet.cell(row, 1).value
        range_min = r_sheet.cell(row, 3).value
        range_max = r_sheet.cell(row, 4).value
        index = r_sheet.cell(row, 0).value.split('.')
        data = None
        if 2 == len(index):
            data = benchmark_read if index[1] == 'Read' else benchmark_write
        elif 'Main' == index[0]:
            data = benchmark_op[index[1]][index[2]]
        elif 'Syscall_latency' == index[0]:
            data = benchmark_sum[index[1]][index[2]]
        else:
            print(index)
            raise ValueError
        i = 0
        for value in data:
            if value < range_min * average_value or value > range_max * average_value:
                w_sheet.write(row, begin_col + i, 'FAIL', red_format)
            else:
                w_sheet.write(row, begin_col + i, 'PASS')
            i += 1
            w_sheet.write(row, begin_col + i, value)
            i += 1
        for col in range(begin_col, begin_col+len(data), 2):
            w.worksheet(r_sheet.nrows, col, '=SUMIF('%s%d:%s%d', )
    wb.close()


if __name__ == '__main__':
    filename = sys.argv[1]
    process_data(filename)
    # print_benchmark_to_excel()
    #print_output()
    #print_benchmark()
    append_data_to_excel()


```

Tags:
  ffsb