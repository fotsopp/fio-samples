# fio-samples
A set of tests run against an idle StoreVirtual 3200 multisite 
solution with 26x10K SAS drives and a dedicated 1Gbit link be-
tween the sites. Round-trip time between the sites is measured
to be below 1ms. Files are deleted between each run. 

# Specification and software versions


```bash
# cat /etc/debian_version
8.8

# lscpu
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                4
On-line CPU(s) list:   0-3
Thread(s) per core:    1
Core(s) per socket:    2
Socket(s):             2
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 45
Model name:            Intel(R) Xeon(R) CPU E5-2620 v3 @ 2.40GHz
Stepping:              2
CPU MHz:               2397.223
BogoMIPS:              4794.44
Hypervisor vendor:     VMware
Virtualization type:   full
L1d cache:             32K
L1i cache:             32K
L2 cache:              256K
L3 cache:              15360K
NUMA node0 CPU(s):     0-3

# free -m
             total       used       free     shared    buffers     cached
Mem:          2010        386       1623          5         52        235
-/+ buffers/cache:         99       1910
Swap:          713          0        713

# lsblk -f /dev/sdb1
NAME FSTYPE LABEL UUID                                 MOUNTPOINT
sdb1 ext4         ef9c562a-8db4-4923-918a-1e85a00fc683 /mnt/nch-tests

# fio-v
fio-2.1.11

# gnuplot -V
gnuplot 4.6 patchlevel 6

# StoreVirtual OS
CLIQ>utility run="cat /etc/lefthand/.version"

HPE StoreVirtual OS Command Line Interface, v13.5.00.0793
(C) Copyright 2016 Hewlett Packard Enterprise Development LP

This command is recommended for HPE support only.
Are You Sure (y/n)? y

RESPONSE
 result         0
 processingTime 4016
 name           CliqSuccess
 description    Operation succeeded.

  UTILITY
   result   0
   exitCode 0
13.5.00.0791
```
# Run tests
```bash
fio --output=log/4k/4k.out config/4k.fio
fio --output=log/32k/32k.out config/32k.fio
fio --output=log/64k/64k.out config/64k.fio
fio --output=log/128k/128k.out config/128k.fio
```

# Plot using gnuplot
```bash
for IOPS_LOG in $(echo *_iops*.log); do fio2gnuplot -g -i -p ${IOPS_LOG} -d ../../plot/4k; done
for IOPS_LOG in $(echo *_iops*.log); do fio2gnuplot -g -i -p ${IOPS_LOG} -d ../../plot/32k; done
for IOPS_LOG in $(echo *_iops*.log); do fio2gnuplot -g -i -p ${IOPS_LOG} -d ../../plot/64k; done
for IOPS_LOG in $(echo *_iops*.log); do fio2gnuplot -g -i -p ${IOPS_LOG} -d ../../plot/128k; done
```
## Sample picture 
![Randome Write 4K blocks](https://raw.githubusercontent.com/fotsopp/fio-samples/master/plot/128k/randwrite128k_iops.3-2Dtrend.png)
