1. chdir("/tmp")  
2. Скорее всего openat(AT_FDCWD, "/usr/share/misc/magic.mgc", O_RDONLY) = 3, но вроде есть еще пара вхождений, куда ходит, но не находит,
3. cat /dev/null > log.txt или echo -n > log.txt
4. Зомби не занимают ресурсов.
5.
```
vagrant@vagrant:~$ sudo /usr/sbin/opensnoop-bpfcc 
PID    COMM               FD ERR PATH
385    systemd-udevd      14   0 /sys/fs/cgroup/unified/system.slice/systemd-udevd.service/cgroup.procs
385    systemd-udevd      14   0 /sys/fs/cgroup/unified/system.slice/systemd-udevd.service/cgroup.threads
854    vminfo              6   0 /var/run/utmp
632    dbus-daemon        -1   2 /usr/local/share/dbus-1/system-services
632    dbus-daemon        21   0 /usr/share/dbus-1/system-services
632    dbus-daemon        -1   2 /lib/dbus-1/system-services
632    dbus-daemon        21   0 /var/lib/snapd/dbus-1/system-services/
637    irqbalance          6   0 /proc/interrupts
637    irqbalance          6   0 /proc/stat
```
6. uname () -  Part of the utsname information is also accessible via /proc/sys/kernel/{ostype, hostname, osrelease, version, domainname}.
7. При использовании '&&' - Вторая команда будет выполняться только в том случае, если первая команда выполнена успешно, т. е. ее статус выхода равен нулю.
При использовании ';' - Выполнение команды, следующей за этим оператором, всегда будет выполняться после выполнения предыдущей команды, независимо от состояния выхода предыдущей команды. Команды всегда выполняются последовательно. 
set -e - Exit immediately if a command exits with a non-zero status - использовать ее вместе с '&&' нет смысла т.к. при использовании '&&' - это правило уже соблюдено.
8. -e - Exit immediately if a command exits with a non-zero status (см. предыдущий ответ)
-u  Treat unset variables as an error when substituting - не заданные переменные считаются ошибкой - сообщается об этом
-x  Print commands and their arguments as they are executed. - Вывод команд и их аргументов при выполнении.
-o pipefail - возвращает команду с не-нулевым кодом выхода или 0 - если все выполнилось успешно
По сути набор этих опций включает режим отладки - подробный вывод процесса выполнения.
9. 
```
vagrant@vagrant:~$ ps -o stat
STAT
Ss
R+
```
Получается самые частые 'S' - процессы ожидающие завершения, "спящие" и 'R' - запущеные
'+' - фоновый
