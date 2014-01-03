General Information
===================
This is a prototype of a deduplication system, named destor.

Features
========
1. Container-based storage;
2. Chunk-level pipeline;
3. Fixed-sized chunking and Content-Defined Chunking (CDC);
4. A variety of fingerprint indexes, including DDFS, Extreme Binning, Sparse Index, SiLo, etc.
5. A variety of rewriting algorithms, including CFL, CBR, CAP, etc.
6. A variety of restore algorithms, including LRU, optimal replacement algorithm, rolling forward assembly.

Related papers
==============
1. The design of the fingerprint index:
    > Avoiding the Disk Bottleneck in the Data Domain Deduplication File System, @FAST'08.
    > Sparse Indexing: Large Scale, Inline Deduplication Using Sampling and Locality, @FAST'09.
    > Extreme Binning: Scalable, Parallel Deduplication for Chunk-based File Backup, @MASCOTS'09.
    > SiLo: A Similarity-Locality based Near-Exact Deduplicatin Scheme with Low RAM Overhead and High Throughput, @USENIX ATC'11.
    > Building a High-Performance Deduplication System, @USENIX ATC'11.
    > Block Locality Caching for Data Deduplication, @SYSTOR'13.

2. The fragmentation:
    > Chunk Fragmentation Level: An Effective Indicator for Read Performance Degradation in Deduplication Storage, @HPCC'11.
    > Assuring Demanded Read Performance of Data Deduplication Storage with Backup Datasets, @MASCOTS'12. 
    > Reducing impact of data fragmentation caused by in-line deduplication, @SYSTOR'12.
    > Improving Restore Speed for Backup Systems that Use Inline Chunk-Based Deduplication, @FAST'13.

3. Garbage collection (to be continued):
    > Building a High-Performance Deduplication System, @USENIX ATC'11.
    > Cumulus: Filesystem Backup to the Cloud, @FAST'09.

Environment
===========
Linux 64bit.

Dependencies
============
1. libssl-dev is required to calculate sha-1 digest;
2. GLib 2.32 or later version; 
3. MySQL and libmysqlclient-dev is required;
4. Makefile is automatically generated by GNU autoconf and automake.

INSTALL
=======
If all dependencies are installed,
compiling destor is straightforward:

./configure
make
make install

To uninstall destor, run
make uninstall

Running
=======
If compile and install are successful, the executable file, destor, should have been moved to /usr/local/bin by default.
You can create a config file, destor.config, in where you run destor.
A sample destor.config is in scripts directory,
and many scripts for experiment are also there.
Run rebuild script to clean data.

destor has provided four types of services:
1. start a backup job,
    destor <directory or file>
2. start a recovery job,
    destor -r<jobid> <dest directory>
3. start a delete job,
    destor -d<jobid>
4. lookup statistics of system,
    destor -s
5. help
    destor -h
6. make a trace
    destor -t <path of raw files>

Configure
=========
A sample configuration is shown in destor.conf

Bugs
====
1. If the running destor is crashed artificially or unexpectedly, data consistency is not guaranted and you'd better run rebuild script.
2. Does NOT support concurrent backup/restore.
3. If working path in destor.config is modified, the rebuild script in scripts folder must be modified too.

Author
======
Min Fu,
Email : fumin@hust.edu.cn
blog : fumin.hustbackup.cn
