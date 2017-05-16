# fio-samples
A set of tests run against an idle StoreVirtual 3200 multisite 
solution with 26x10K SAS drives and a dedicated 1Gbit link be-
tween the sites. Round-trip time between the sites is measured
to be below 1ms. File was deleted between each run.


# Run tests
```bash
fio --output=log/4k/4k.out config/4k.fio
fio --output=log/32k/32k.out config/32k.fio
fio --output=log/64k/64k.out config/64k.fio
fio --output=log/128k/128k.out config/128k.fio
```

# Generate gnuplots
```bash
for IOPS_LOG in $(echo *_iops*.log); do fio2gnuplot -g -i -p ${IOPS_LOG} -d ../../plot/4k; done
for IOPS_LOG in $(echo *_iops*.log); do fio2gnuplot -g -i -p ${IOPS_LOG} -d ../../plot/32k; done
for IOPS_LOG in $(echo *_iops*.log); do fio2gnuplot -g -i -p ${IOPS_LOG} -d ../../plot/64k; done
for IOPS_LOG in $(echo *_iops*.log); do fio2gnuplot -g -i -p ${IOPS_LOG} -d ../../plot/128k; done
```
![Randome Write 4K blocks](https://raw.githubusercontent.com/fotsopp/fio-samples/master/plot/4k/randwrite4k_iops.3-2Dsmooth.png)
