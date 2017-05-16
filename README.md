# fio-samples
# Generate gnuplots
for IOPS_LOG in $(echo *_iops*.log); do fio2gnuplot -g -i -p randread4k_iops.4.log -d ../../plot/4k; done
