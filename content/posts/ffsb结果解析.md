---
title: Ffsb结果解析
date: 2021-09-03T21:40:49+08:00
lastmod: 2021-09-03T21:40:49+08:00
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
# ffsb结果解析
```plain
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 0.06%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 0.06%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 0.06%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 0.06%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 0.06%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 0.06%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 0.06%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 0.06%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 0.06%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 0.06%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 48.97%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
fs setup took 0 secs
Syncing()...6 sec
Starting Actual Benchmark At: Thu Jan 26 00:30:47 2017

Syncing()...1 sec
FFSB benchmark finished   at: Thu Jan 26 00:31:01 2017

Results:
Benchmark took 13.87 sec

Total Results
===============
             Op Name   Transactions	 Trans/sec	% Trans	    % Op Weight	   Throughput
             =======   ============	 =========	=======	    ===========	   ==========
             readall :        11698	    843.15	15.010%		10.380%	   3.29MB/sec
              create :        16440	   1184.94	21.095%		10.791%	   4.63MB/sec
              append :         1010	     72.80	 1.296%		10.380%	    291KB/sec
              delete :           93	      6.70	 0.119%		 9.558%	           NA
                stat :           87	      6.27	 0.112%		 8.941%	           NA
            writeall :        13949	   1005.39	17.899%		10.380%	   3.93MB/sec
      writeall_fsync :        30079	   2167.99	38.596%		 9.147%	   8.47MB/sec
          open_close :           99	      7.14	 0.127%		10.175%	           NA
        create_fsync :         3438	    247.80	 4.411%		 9.558%	    991KB/sec
        append_fsync :         1040	     74.96	 1.334%		10.689%	    300KB/sec
-
5617.14 Transactions per Second

Throughput Results
===================
Read Throughput: 3.29MB/sec
Write Throughput: 18.6MB/sec

System Call Latency statistics in millisecs
=====
		Min		Avg		Max		Total Calls
		========	========	========	============
[   open]	0.013000	0.269726	124.470001	         793
   -
[   read]	0.003000	0.005743	5.221000	       11698
   -
[  write]	0.004000	0.079473	420.509003	       65956
   -
[ unlink]	0.057000	3.104903	139.417007	          93
   -
[  close]	0.002000	0.004115	0.015000	         793
   -
[   stat]	0.012000	0.019023	0.044000	          87
   -



0.5% User   Time
10.8% System Time
11.3% CPU Utilization
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 48.90%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
fs setup took 0 secs
Syncing()...7 sec
Starting Actual Benchmark At: Thu Jan 26 00:31:09 2017

Syncing()...7 sec
FFSB benchmark finished   at: Thu Jan 26 00:31:27 2017

Results:
Benchmark took 17.96 sec

Total Results
===============
             Op Name   Transactions	 Trans/sec	% Trans	    % Op Weight	   Throughput
             =======   ============	 =========	=======	    ===========	   ==========
             readall :         3432	    191.13	 4.840%		 8.575%	    765KB/sec
              create :        38123	   2123.12	53.766%		11.475%	   8.29MB/sec
              append :          770	     42.88	 1.086%		 9.710%	    172KB/sec
              delete :           89	      4.96	 0.126%		11.223%	           NA
                stat :           88	      4.90	 0.124%		11.097%	           NA
            writeall :        21664	   1206.50	30.554%		 9.458%	   4.71MB/sec
      writeall_fsync :         3169	    176.49	 4.469%		 8.701%	    706KB/sec
          open_close :           77	      4.29	 0.109%		 9.710%	           NA
        create_fsync :         2723	    151.65	 3.840%		10.340%	    607KB/sec
        append_fsync :          770	     42.88	 1.086%		 9.710%	    172KB/sec
-
3948.80 Transactions per Second

Throughput Results
===================
Read Throughput: 765KB/sec
Write Throughput: 14.6MB/sec

System Call Latency statistics in millisecs
=====
		Min		Avg		Max		Total Calls
		========	========	========	============
[   open]	0.012000	0.582338	189.878998	         616
   -
[   read]	0.003000	0.012614	26.857000	        3432
   -
[  write]	0.004000	0.293199	664.065979	       67219
   -
[ unlink]	0.058000	1.302730	31.836000	          89
   -
[  close]	0.001000	0.004412	0.079000	         616
   -
[   stat]	0.012000	0.020182	0.045000	          88
   -



0.4% User   Time
6.6% System Time
7.0% CPU Utilization
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 54.25%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
fs setup took 0 secs
Syncing()...6 sec
Starting Actual Benchmark At: Thu Jan 26 00:31:35 2017

Syncing()...4 sec
FFSB benchmark finished   at: Thu Jan 26 00:31:51 2017

Results:
Benchmark took 15.95 sec

Total Results
===============
             Op Name   Transactions	 Trans/sec	% Trans	    % Op Weight	   Throughput
             =======   ============	 =========	=======	    ===========	   ==========
             readall :         5024	    314.95	 6.525%		12.191%	   1.23MB/sec
              create :        29424	   1844.59	38.212%		 8.237%	   7.21MB/sec
              append :          590	     36.99	 0.766%		 9.720%	    148KB/sec
              delete :           62	      3.89	 0.081%		10.214%	           NA
                stat :           69	      4.33	 0.090%		11.367%	           NA
            writeall :         2700	    169.26	 3.506%		 9.885%	    677KB/sec
      writeall_fsync :        13314	    834.65	17.290%		10.214%	   3.26MB/sec
          open_close :           57	      3.57	 0.074%		 9.390%	           NA
        create_fsync :        25282	   1584.92	32.833%		10.873%	   6.19MB/sec
        append_fsync :          480	     30.09	 0.623%		 7.908%	    120KB/sec
-
4827.24 Transactions per Second

Throughput Results
===================
Read Throughput: 1.23MB/sec
Write Throughput: 17.6MB/sec

System Call Latency statistics in millisecs
=====
		Min		Avg		Max		Total Calls
		========	========	========	============
[   open]	0.014000	0.114055	18.941999	         476
   -
[   read]	0.003000	0.008782	10.585000	        5024
   -
[  write]	0.004000	0.113076	481.164001	       71790
   -
[ unlink]	0.058000	2.897145	164.621002	          62
   -
[  close]	0.002000	0.004489	0.084000	         476
   -
[   stat]	0.011000	0.017609	0.057000	          69
   -



0.5% User   Time
10.5% System Time
11.0% CPU Utilization
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 57.41%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
fs setup took 0 secs
Syncing()...6 sec
Starting Actual Benchmark At: Thu Jan 26 00:31:58 2017

Syncing()...4 sec
FFSB benchmark finished   at: Thu Jan 26 00:32:16 2017

Results:
Benchmark took 17.60 sec

Total Results
===============
             Op Name   Transactions	 Trans/sec	% Trans	    % Op Weight	   Throughput
             =======   ============	 =========	=======	    ===========	   ==========
             readall :        27154	   1543.12	29.818%		10.382%	   6.03MB/sec
              create :        16028	    910.85	17.600%		 9.406%	   3.56MB/sec
              append :         1240	     70.47	 1.362%		11.003%	    282KB/sec
              delete :          115	      6.54	 0.126%		10.204%	           NA
                stat :          129	      7.33	 0.142%		11.446%	           NA
            writeall :        18100	   1028.59	19.876%		 9.317%	   4.02MB/sec
      writeall_fsync :        13076	    743.09	14.359%		10.382%	    2.9MB/sec
          open_close :          102	      5.80	 0.112%		 9.051%	           NA
        create_fsync :        14082	    800.26	15.464%		 9.583%	   3.13MB/sec
        append_fsync :         1040	     59.10	 1.142%		 9.228%	    236KB/sec
-
5175.14 Transactions per Second

Throughput Results
===================
Read Throughput: 6.03MB/sec
Write Throughput: 14.1MB/sec

System Call Latency statistics in millisecs
=====
		Min		Avg		Max		Total Calls
		========	========	========	============
[   open]	0.013000	0.287392	139.746002	         883
   -
[   read]	0.003000	0.006889	7.982000	       27154
   -
[  write]	0.004000	0.100881	246.876007	       63566
   -
[ unlink]	0.062000	4.593609	175.654999	         115
   -
[  close]	0.002000	0.004476	0.137000	         883
   -
[   stat]	0.011000	0.019674	0.086000	         129
   -



0.5% User   Time
9.0% System Time
9.5% CPU Utilization
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 52.11%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
fs setup took 0 secs
Syncing()...5 sec
Starting Actual Benchmark At: Thu Jan 26 00:32:22 2017

Syncing()...2 sec
FFSB benchmark finished   at: Thu Jan 26 00:32:38 2017

Results:
Benchmark took 15.96 sec

Total Results
===============
             Op Name   Transactions	 Trans/sec	% Trans	    % Op Weight	   Throughput
             =======   ============	 =========	=======	    ===========	   ==========
             readall :         3767	    236.05	 5.418%		10.301%	    944KB/sec
              create :         6356	    398.29	 9.142%		 9.480%	   1.56MB/sec
              append :         1280	     80.21	 1.841%		11.668%	    321KB/sec
              delete :          109	      6.83	 0.157%		 9.936%	           NA
                stat :           94	      5.89	 0.135%		 8.569%	           NA
            writeall :        20438	   1280.72	29.398%		10.119%	      5MB/sec
      writeall_fsync :        22670	   1420.58	32.608%		11.121%	   5.55MB/sec
          open_close :          116	      7.27	 0.167%		10.574%	           NA
        create_fsync :        13772	    863.00	19.810%		 9.845%	   3.37MB/sec
        append_fsync :          920	     57.65	 1.323%		 8.387%	    231KB/sec
-
4356.50 Transactions per Second

Throughput Results
===================
Read Throughput: 944KB/sec
Write Throughput: 16MB/sec

System Call Latency statistics in millisecs
=====
		Min		Avg		Max		Total Calls
		========	========	========	============
[   open]	0.013000	0.320633	99.432999	         894
   -
[   read]	0.003000	0.007289	8.764000	        3767
   -
[  write]	0.004000	0.084760	210.964996	       65436
   -
[ unlink]	0.048000	1.913193	108.400002	         109
   -
[  close]	0.002000	0.014541	9.322000	         894
   -
[   stat]	0.011000	0.018745	0.046000	          94
   -



0.6% User   Time
8.7% System Time
9.3% CPU Utilization
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 50.14%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
fs setup took 0 secs
Syncing()...5 sec
Starting Actual Benchmark At: Thu Jan 26 00:32:45 2017

Syncing()...0 sec
FFSB benchmark finished   at: Thu Jan 26 00:32:58 2017

Results:
Benchmark took 13.28 sec

Total Results
===============
             Op Name   Transactions	 Trans/sec	% Trans	    % Op Weight	   Throughput
             =======   ============	 =========	=======	    ===========	   ==========
             readall :        11920	    897.64	21.470%		10.811%	   3.51MB/sec
              create :         9551	    719.24	17.203%		10.693%	   2.81MB/sec
              append :          970	     73.05	 1.747%		11.398%	    292KB/sec
              delete :           95	      7.15	 0.171%		11.163%	           NA
                stat :           85	      6.40	 0.153%		 9.988%	           NA
            writeall :         1082	     81.48	 1.949%		 8.461%	    326KB/sec
      writeall_fsync :          978	     73.65	 1.762%		 7.756%	    295KB/sec
          open_close :           92	      6.93	 0.166%		10.811%	           NA
        create_fsync :        30017	   2260.45	54.065%		10.341%	   8.83MB/sec
        append_fsync :          730	     54.97	 1.315%		 8.578%	    220KB/sec
-
4180.97 Transactions per Second

Throughput Results
===================
Read Throughput: 3.51MB/sec
Write Throughput: 12.7MB/sec

System Call Latency statistics in millisecs
=====
		Min		Avg		Max		Total Calls
		========	========	========	============
[   open]	0.013000	0.337973	127.887001	         671
   -
[   read]	0.003000	0.010563	10.067000	       11920
   -
[  write]	0.004000	0.100224	193.268997	       43328
   -
[ unlink]	0.050000	1.125200	37.287998	          95
   -
[  close]	0.002000	0.004012	0.020000	         671
   -
[   stat]	0.012000	0.019518	0.048000	          85
   -



0.4% User   Time
10.6% System Time
11.0% CPU Utilization
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 52.60%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
fs setup took 0 secs
Syncing()...7 sec
Starting Actual Benchmark At: Thu Jan 26 00:33:06 2017

Syncing()...4 sec
FFSB benchmark finished   at: Thu Jan 26 00:33:21 2017

Results:
Benchmark took 15.19 sec

Total Results
===============
             Op Name   Transactions	 Trans/sec	% Trans	    % Op Weight	   Throughput
             =======   ============	 =========	=======	    ===========	   ==========
             readall :        24226	   1595.24	30.827%		10.854%	   6.23MB/sec
              create :        17463	   1149.91	22.222%		 9.878%	   4.49MB/sec
              append :          740	     48.73	 0.942%		 9.024%	    195KB/sec
              delete :           73	      4.81	 0.093%		 8.902%	           NA
                stat :           82	      5.40	 0.104%		10.000%	           NA
            writeall :         9988	    657.69	12.710%		11.951%	   2.57MB/sec
      writeall_fsync :         1490	     98.11	 1.896%		10.366%	    392KB/sec
          open_close :           78	      5.14	 0.099%		 9.512%	           NA
        create_fsync :        23716	   1561.65	30.178%		10.610%	    6.1MB/sec
        append_fsync :          730	     48.07	 0.929%		 8.902%	    192KB/sec
-
5174.74 Transactions per Second

Throughput Results
===================
Read Throughput: 6.23MB/sec
Write Throughput: 13.9MB/sec

System Call Latency statistics in millisecs
=====
		Min		Avg		Max		Total Calls
		========	========	========	============
[   open]	0.013000	0.269224	38.504002	         665
   -
[   read]	0.003000	0.007017	10.529000	       24226
   -
[  write]	0.004000	0.193990	1240.409058	       54127
   -
[ unlink]	0.045000	4.183726	207.742004	          73
   -
[  close]	0.002000	0.006344	1.351000	         665
   -
[   stat]	0.012000	0.073878	4.474000	          82
   -



0.2% User   Time
9.4% System Time
9.5% CPU Utilization
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 54.11%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
fs setup took 0 secs
Syncing()...7 sec
Starting Actual Benchmark At: Thu Jan 26 00:33:30 2017

Syncing()...3 sec
FFSB benchmark finished   at: Thu Jan 26 00:33:45 2017

Results:
Benchmark took 15.52 sec

Total Results
===============
             Op Name   Transactions	 Trans/sec	% Trans	    % Op Weight	   Throughput
             =======   ============	 =========	=======	    ===========	   ==========
             readall :         3238	    208.61	 5.056%		 8.451%	    834KB/sec
              create :        13059	    841.34	20.393%		10.000%	   3.29MB/sec
              append :          810	     52.18	 1.265%		11.408%	    209KB/sec
              delete :           75	      4.83	 0.117%		10.563%	           NA
                stat :           81	      5.22	 0.126%		11.408%	           NA
            writeall :        17395	   1120.69	27.164%		 8.732%	   4.38MB/sec
      writeall_fsync :         3153	    203.13	 4.924%		 9.577%	    813KB/sec
          open_close :           68	      4.38	 0.106%		 9.577%	           NA
        create_fsync :        25469	   1640.86	39.772%		10.563%	   6.41MB/sec
        append_fsync :          690	     44.45	 1.077%		 9.718%	    178KB/sec
-
4125.70 Transactions per Second

Throughput Results
===================
Read Throughput: 834KB/sec
Write Throughput: 15.2MB/sec

System Call Latency statistics in millisecs
=====
		Min		Avg		Max		Total Calls
		========	========	========	============
[   open]	0.014000	0.286599	133.453003	         554
   -
[   read]	0.003000	0.005871	1.750000	        3238
   -
[  write]	0.004000	0.203332	468.334991	       60576
   -
[ unlink]	0.055000	3.402613	174.811996	          75
   -
[  close]	0.002000	0.004361	0.014000	         554
   -
[   stat]	0.012000	0.019074	0.040000	          81
   -



0.3% User   Time
8.9% System Time
9.1% CPU Utilization
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 54.43%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
fs setup took 0 secs
Syncing()...7 sec
Starting Actual Benchmark At: Thu Jan 26 00:33:53 2017

Syncing()...3 sec
FFSB benchmark finished   at: Thu Jan 26 00:34:07 2017

Results:
Benchmark took 13.83 sec

Total Results
===============
             Op Name   Transactions	 Trans/sec	% Trans	    % Op Weight	   Throughput
             =======   ============	 =========	=======	    ===========	   ==========
             readall :         2061	    149.06	 3.188%		12.857%	    596KB/sec
              create :        33567	   2427.69	51.917%		12.222%	   9.48MB/sec
              append :          670	     48.46	 1.036%		10.635%	    194KB/sec
              delete :           61	      4.41	 0.094%		 9.683%	           NA
                stat :           67	      4.85	 0.104%		10.635%	           NA
            writeall :        13123	    949.11	20.297%		 9.206%	   3.71MB/sec
      writeall_fsync :         5233	    378.47	 8.094%		 7.302%	   1.48MB/sec
          open_close :           54	      3.91	 0.084%		 8.571%	           NA
        create_fsync :         9209	    666.03	14.243%		 9.206%	    2.6MB/sec
        append_fsync :          610	     44.12	 0.943%		 9.683%	    176KB/sec
-
4676.10 Transactions per Second

Throughput Results
===================
Read Throughput: 596KB/sec
Write Throughput: 17.6MB/sec

System Call Latency statistics in millisecs
=====
		Min		Avg		Max		Total Calls
		========	========	========	============
[   open]	0.014000	0.758518	285.117004	         502
   -
[   read]	0.003000	0.010993	7.266000	        2061
   -
[  write]	0.004000	0.116312	890.288025	       62412
   -
[ unlink]	0.058000	4.615164	138.270004	          61
   -
[  close]	0.002000	0.004257	0.015000	         502
   -
[   stat]	0.012000	0.020970	0.100000	          67
   -



0.2% User   Time
9.6% System Time
9.8% CPU Utilization
FFSB version 6.0-RC2 started

benchmark time = 10
ThreadGroup 0
================
	 num_threads      = 4
	
	 read_random      = off
	 read_size        = 40960	(40KB)
	 read_blocksize   = 4096	(4KB)
	 read_skip        = off
	 read_skipsize    = 0	(0B)
	
	 write_random     = off
	 write_size       = 40960	(40KB)
	 fsync_file       = 0
	 write_blocksize  = 4096	(4KB)
	 wait time        = 0
	
	 op weights
	                 read = 0 (0.00%)
	              readall = 1 (10.00%)
	                write = 0 (0.00%)
	               create = 1 (10.00%)
	               append = 1 (10.00%)
	               delete = 1 (10.00%)
	               metaop = 0 (0.00%)
	            createdir = 0 (0.00%)
	                 stat = 1 (10.00%)
	             writeall = 1 (10.00%)
	       writeall_fsync = 1 (10.00%)
	           open_close = 1 (10.00%)
	          write_fsync = 0 (0.00%)
	         create_fsync = 1 (10.00%)
	         append_fsync = 1 (10.00%)
	
FileSystem /var/backups/aaa/work/jta.Benchmark.ffsb
==========
	 num_dirs         = 100
	 starting files   = 0
	
	 Fileset weight:
		     33554432 (  32MB) -> 1 (1.00%)
		      8388608 (   8MB) -> 2 (2.00%)
		       524288 ( 512KB) -> 3 (3.00%)
		       262144 ( 256KB) -> 4 (4.00%)
		       131072 ( 128KB) -> 5 (5.00%)
		        65536 (  64KB) -> 8 (8.00%)
		        32768 (  32KB) -> 10 (10.00%)
		        16384 (  16KB) -> 13 (13.00%)
		         8192 (   8KB) -> 21 (21.00%)
		         4096 (   4KB) -> 33 (33.00%)
	 directio         = off
	 alignedio        = off
	 bufferedio       = off
	
	 aging is off
	 current utilization = 55.07%
	
creating new fileset /var/backups/aaa/work/jta.Benchmark.ffsb
fs setup took 0 secs
Syncing()...5 sec
Starting Actual Benchmark At: Thu Jan 26 00:34:14 2017

Syncing()...2 sec
FFSB benchmark finished   at: Thu Jan 26 00:34:30 2017

Results:
Benchmark took 16.17 sec

Total Results
===============
             Op Name   Transactions	 Trans/sec	% Trans	    % Op Weight	   Throughput
             =======   ============	 =========	=======	    ===========	   ==========
             readall :         9581	    592.52	13.957%		10.419%	   2.31MB/sec
              create :        12132	    750.29	17.674%		10.111%	   2.93MB/sec
              append :         1720	    106.37	 2.506%		10.604%	    425KB/sec
              delete :          160	      9.89	 0.233%		 9.864%	           NA
                stat :          163	     10.08	 0.237%		10.049%	           NA
            writeall :         7285	    450.53	10.613%		10.666%	   1.76MB/sec
      writeall_fsync :         5421	    335.25	 7.897%		10.543%	   1.31MB/sec
          open_close :          143	      8.84	 0.208%		 8.816%	           NA
        create_fsync :        30500	   1886.23	44.431%		 9.433%	   7.37MB/sec
        append_fsync :         1540	     95.24	 2.243%		 9.494%	    381KB/sec
-
4245.26 Transactions per Second

Throughput Results
===================
Read Throughput: 2.31MB/sec
Write Throughput: 14.2MB/sec

System Call Latency statistics in millisecs
=====
		Min		Avg		Max		Total Calls
		========	========	========	============
[   open]	0.013000	0.103688	39.541000	        1299
   -
[   read]	0.003000	0.008649	10.064000	        9581
   -
[  write]	0.004000	0.147653	417.877991	       58598
   -
[ unlink]	0.057000	1.249506	35.688000	         160
   -
[  close]	0.002000	0.009712	7.332000	        1299
   -
[   stat]	0.012000	0.019301	0.039000	         163
   -



0.3% User   Time
10.9% System Time
11.3% CPU Utilization
```

```python
#!/bin/python
# --*--coding: utf-8 --*--

import re

opNames = ["readall", "create", "append",
           "delete",
           "stat",
           "writeall",
           "writeall_fsync",
           "open_close",
           "create_fsync",
           "append_fsync"]

sumNames= ["open","read","write","unlink","close","stat"]

opValue = ["Transactions", "Trans/sec", "%Trans", "Op Weight", "Throughput"]
sumValue = ["Min", "Avg", "Max", "Total Calls"]

benchmark_op = dict()
avg_benchmark_op = dict()
benchmark_sum = dict()
avg_benchmark_sum = dict()

for p in opNames:
    benchmark_op[p] = dict()
    for k in opValue:
        benchmark_op[p][k] = list()

for s in sumNames:
    benchmark_sum[s] = dict()
    for k in sumValue:
        benchmark_sum[s][k] = list()

reg_op = '''^\s+\w+\s\:(\s+\d+(\.?\d+\%?)?){4}\s+(\d+(\.\d+)?[K|M]B\/sec|NA)'''
reg_sum = '''\[(\s*\w+)\](\s+\d+(\.\d+)?){4}'''

pattern_op = re.compile(reg_op, re.I)
pattern_sum = re.compile(reg_sum, re.I)
with open('ffsb.txt') as ffsb:
    for line in ffsb:
        m = pattern_op.match(line)
        try:
            if m:
                str = m.group(0)
                array = str.strip().split()
                for x in range(len(opValue)-1):
                    benchmark_op[array[0]][opValue[x]].append(array[2+x].strip('% KMB/sec'))
                if array[-1] != 'NA':
                    benchmark_op[array[0]][opValue[len(opValue)-1]].append(array[2+x].strip('% KMB/sec'))
            else:
                m = pattern_sum.match(line)
                if m:
                    array = line.strip(' []').split()
                    for x in range(len(sumValue)):
                        benchmark_sum[array[0].strip('[]')][sumValue[x]].append(array[1+x].strip())
        except Exception as e:
            # index = m.group(0).strip().split()[0]
            # print(line, index)
            # print(benchmark_op)
            # print(opValue)
            print(line)
            print(m.groups())
            raise e
       


for op in opNames:
    avg_benchmark_op[op] = dict()
    for k in opValue:
        avg_benchmark_op[op][k] = sum(float(x) for x in benchmark_op[op][k])/len(benchmark_op[op][k]) if len(benchmark_op[op][k])!=0 else 0

for s in sumNames:
    avg_benchmark_sum[s] = dict()
    for k in sumValue:
        avg_benchmark_sum[s][k] = sum(float(x) for x in benchmark_sum[s][k])/len(benchmark_sum[s][k]) if len(benchmark_sum[s][k])!=0 else 0




print(opValue)
for op in opNames:
    print(op,avg_benchmark_op[op].values())

print(sumValue)
for s in sumNames:
    print(s,avg_benchmark_sum[s].values())
```

Tags:
  ffsb