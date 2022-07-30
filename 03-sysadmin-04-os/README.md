1. Сервис запущен:
```
vagrant@vagrant:~/node_exporter-1.3.1.linux-amd64$ curl -s localhost:9100/metrics
# HELP go_gc_duration_seconds A summary of the pause duration of garbage collection cycles.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 0
go_gc_duration_seconds{quantile="0.25"} 0
go_gc_duration_seconds{quantile="0.5"} 0
go_gc_duration_seconds{quantile="0.75"} 0
go_gc_duration_seconds{quantile="1"} 0
go_gc_duration_seconds_sum 0
go_gc_duration_seconds_count 0
# HELP go_goroutines Number of goroutines that currently exist.
# TYPE go_goroutines gauge
go_goroutines 7
# HELP go_info Information about the Go environment.
# TYPE go_info gauge
go_info{version="go1.17.3"} 1
# HELP go_memstats_alloc_bytes Number of bytes allocated and still in use.
# TYPE go_memstats_alloc_bytes gauge
go_memstats_alloc_bytes 1.46068e+06
# HELP go_memstats_alloc_bytes_total Total number of bytes allocated, even if freed.
# TYPE go_memstats_alloc_bytes_total counter
go_memstats_alloc_bytes_total 1.46068e+06
# HELP go_memstats_buck_hash_sys_bytes Number of bytes used by the profiling bucket hash table.
# TYPE go_memstats_buck_hash_sys_bytes gauge
go_memstats_buck_hash_sys_bytes 1.445879e+06
# HELP go_memstats_frees_total Total number of frees.
# TYPE go_memstats_frees_total counter
go_memstats_frees_total 779
......
```
Добавлен в автозагрузку:
```
vagrant@vagrant:~/node_exporter-1.3.1.linux-amd64$ cat /etc/systemd/system/node_exporter.service
[Unit]
Description=Node Exporter
 
[Service]
ExecStart=/opt/node_exporter/node_exporter -C /opt/node_exporter/node_exporter.conf
 
[Install]
WantedBy=default.target
```
Запущен:
```
vagrant@vagrant:~$ sudo systemctl status node_exporter
● node_exporter.service - Node Exporter
     Loaded: loaded (/etc/systemd/system/node_exporter.service; disabled; vendor preset: enabled)
     Active: active (running) since Sat 2022-07-16 11:00:58 UTC; 7s ago
   Main PID: 1062 (node_exporter)
      Tasks: 4 (limit: 1066)
     Memory: 13.2M
     CGroup: /system.slice/node_exporter.service
             └─1062 /opt/node_exporter/node_exporter

Jul 16 11:00:58 vagrant node_exporter[1062]: ts=2022-07-16T11:00:58.807Z caller=node_exporter.go:115 level=info collector=thermal_zone
Jul 16 11:00:58 vagrant node_exporter[1062]: ts=2022-07-16T11:00:58.807Z caller=node_exporter.go:115 level=info collector=time
Jul 16 11:00:58 vagrant node_exporter[1062]: ts=2022-07-16T11:00:58.807Z caller=node_exporter.go:115 level=info collector=timex
Jul 16 11:00:58 vagrant node_exporter[1062]: ts=2022-07-16T11:00:58.807Z caller=node_exporter.go:115 level=info collector=udp_queues
Jul 16 11:00:58 vagrant node_exporter[1062]: ts=2022-07-16T11:00:58.807Z caller=node_exporter.go:115 level=info collector=uname
Jul 16 11:00:58 vagrant node_exporter[1062]: ts=2022-07-16T11:00:58.807Z caller=node_exporter.go:115 level=info collector=vmstat
Jul 16 11:00:58 vagrant node_exporter[1062]: ts=2022-07-16T11:00:58.807Z caller=node_exporter.go:115 level=info collector=xfs
Jul 16 11:00:58 vagrant node_exporter[1062]: ts=2022-07-16T11:00:58.807Z caller=node_exporter.go:115 level=info collector=zfs
Jul 16 11:00:58 vagrant node_exporter[1062]: ts=2022-07-16T11:00:58.807Z caller=node_exporter.go:199 level=info msg="Listening on" address=:9100
Jul 16 11:00:58 vagrant node_exporter[1062]: ts=2022-07-16T11:00:58.811Z caller=tls_config.go:195 level=info msg="TLS is disabled." http2=false
vagrant@vagrant:~$ 
```
2.
CPU
```
node_cpu_seconds_total{cpu="0",mode="idle"} 90.73
node_cpu_seconds_total{cpu="0",mode="system"} 5.04
node_cpu_seconds_total{cpu="0",mode="user"} 4.84
```
Mem
```
node_memory_MemAvailable_bytes 7.29980928e+08
node_memory_MemFree_bytes 5.13437696e+08
```
Disc
```
node_disk_io_time_seconds_total{device="sda"} 5.5600000000000005
node_disk_read_bytes_total{device="sda"} 2.42735104e+08
node_disk_read_time_seconds_total{device="sda"} 2.547
node_disk_write_time_seconds_total{device="sda"} 0.783
```
Network
```
node_network_receive_bytes_total{device="eth0"} 69732
node_network_receive_drop_total{device="eth0"} 0
node_network_receive_errs_total{device="eth0"} 0
node_network_transmit_drop_total{device="eth0"} 0
node_network_transmit_errs_total{device="eth0"} 0
node_network_transmit_packets_total{device="eth0"} 464
```
3. ![Результат](https://i.imgur.com/vaw9ZdO.png "вот")
4. Да можем
```
vagrant@vagrant:~$ dmesg | grep virtual
[    0.002435] CPU MTRRs all blank - virtualized system.
[    0.059865] Booting paravirtualized kernel on KVM
[    0.249845] Performance Events: PMU not available due to virtualization, using software events only.
[    2.891920] systemd[1]: Detected virtualization oracle.
```
5 Существует 2 вида ограничений - "Soft" и "Hard" - первый всегда значительно меньше и узнать его можно командой
```
vagrant@vagrant:~$ ulimit -n
1024
```
Второй "Hard" парамет - как понятно из названия - это жеские ограничения - и их превысить нельзя, в отличии от "Soft"
```
vagrant@vagrant:~$ cat /proc/sys/fs/nr_open 
1048576
```
[Найдено тут](https://ru.stackoverflow.com/questions/475417/%D0%9B%D0%B8%D0%BC%D0%B8%D1%82-%D0%BD%D0%B0-%D0%BA%D0%BE%D0%BB%D0%B8%D1%87%D0%B5%D1%81%D1%82%D0%B2%D0%BE-%D0%BE%D1%82%D0%BA%D1%80%D1%8B%D1%82%D1%8B%D1%85-%D0%B4%D0%B5%D1%81%D0%BA%D1%80%D0%B8%D0%BF%D1%82%D0%BE%D1%80%D0%BE%D0%B2)
6. 
```
vagrant@vagrant:~$ sudo -i
root@vagrant:~# unshare -f --pid --mount-proc sleep 1h
root@vagrant:~# ps aux | grep sleep
root        2832  0.0  0.0   7232   580 pts/0    T    09:26   0:00 unshare -f --pid --mount-proc sleep 1h
root        2833  0.0  0.0   7228   580 pts/0    S    09:26   0:00 sleep 1h
root        2838  0.0  0.0   8160   720 pts/0    S+   09:27   0:00 grep --color=auto sleep
root@vagrant:~# nsenter --target 2833 --pid --mount
root@vagrant:/# ps
    PID TTY          TIME CMD
      1 pts/0    00:00:00 sleep
      2 pts/0    00:00:00 bash
     13 pts/0    00:00:00 ps
```

7. :(){ :|:& };: форк-бомба.
обьявление функции с именем ':'
которая вызывает сама себя в двух экземплярах. 

[ 3344.940729] cgroup: fork rejected by pids controller in /user.slice/user-1000.slice/session-3.scope
```
vagrant@vagrant:~$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 3554
max locked memory       (kbytes, -l) 65536
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 3554
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```
соответственно если мы изменим "max user processes" на 100 например (ulimit -u 100)

```
vagrant@vagrant:~$ ulimit -u 100
vagrant@vagrant:~$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 3554
max locked memory       (kbytes, -l) 65536
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 100
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```
то от 'форк-бомбы' системе "полегчает" гораздо быстрее

