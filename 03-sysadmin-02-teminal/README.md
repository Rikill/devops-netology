1) Это встроенная команда. Встроенная, потому что, работая внутри сессии терминала логичнее менять указатель на текущую 
деректорию внутренней функцией, если использовать внешний вызов, то он будет работать со своим окружением, и менять 
текущий каталог внутри своего окружения, и на вызвавшую оболочку влиять не будет.  


2)   
```
~/Documents/Learning/devops-netology/03-sysadmin-02-teminal  on   main ?1 ▓▒░ cat test.md                                              
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et 
dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea 
commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat 
nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit 
anim id est laborum.
░▒▓    ~/Doc/L/devops-netology/03-sysadmin-02-teminal  on   main ?1 ▓▒░ grep Lorem test.md | wc -l
1
░▒▓    ~/Doc/L/devops-netology/03-sysadmin-02-teminal  on   main ?1 ▓▒░ grep Lorem test.md -c    
1 
```

3) 
```
 > ~/Documents/Learning/devops-netology/03-sysadmin-02-teminal  on   main ?1 ▓▒░ pstree -p                                     ░▒▓ ✔  at 17:02:09
systemd(1)─┬─ModemManager(866)─┬─{ModemManager}(902)
           │                   └─{ModemManager}(913)
           ├─NetworkManager(797)─┬─{NetworkManager}(859)
           │                     └─{NetworkManager}(860) 
```

4) 
```
       ~/Documents/Learning/devops-netology  on   main ?1 ▓▒░ ls -l  2>/dev/pts/1  
```

5) 
```
▒▓    ~/Doc/L/devops-netology/03-sysadmin-02-teminal  on   main ?1 ▓▒░ cat test.md                                              ░▒▓ 1 ✘  at 17:46:33  ▓▒░
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna 
aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. 
Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. 
Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
░▒▓    ~/Doc/L/devops-netology/03-sysadmin-02-teminal  on   main ?1 ▓▒░ cat test_err.md                                            ░▒▓ ✔  at 18:10:49  ▓▒░
cat: test_err.md: No such file or directory
░▒▓    ~/Doc/L/devops-netology/03-sysadmin-02-teminal  on   main ?1 ▓▒░ cat <test.md > test_err.md                               ░▒▓ 1 ✘  at 18:11:16  ▓▒░
░▒▓    ~/Doc/L/devops-netology/03-sysadmin-02-teminal  on   main ?1 ▓▒░ cat test_err.md                                            ░▒▓ ✔  at 18:11:50  ▓▒░
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna 
aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. 
Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. 
Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```
 6) Перенаправить полусится (echo Hello > /dev/tty3)
Наблюдать - только переключившись в др.терминал

 7) bash 5>&1 - Создаст дескриптор с 5 и перенатправит его в stdout
echo netology > /proc/$$/fd/5 - выведет в дескриптор "5", который был пернеаправлен в stdout

если запустить echo netology > /proc/$$/fd/5 в новой сесии, получим ошибку, так как такого дескриптора нет в текущей(новой) сесии

 8) 
``` 
vagrant@vagrant:~$ ls -l /root 9>&2 2>&1 1>&9 | grep denied -c 
1

9>&2 - новый дескриптор перенаправили в stderr
2>&1 - stderr перенаправили в stdout 
1>&9 - stdout - перенаправили в в новый дескриптор
```

 9) Будут выведены переменные окружения:
можно получить тоже самое (только с разделением по переменным по строкам):
printenv
env

 10) /proc/<PID>/cmdline - полный путь до исполняемого файла процесса [PID]
/proc/<PID>/exe - содержит ссылку до файла запущенного для процесса [PID], 
 
```
 11) ░▒▓    ~/Doc/Learning/vagrant ▓▒░  grep sse /proc/cpuinfo
sse4_2

12)  
```
vagrant vagrant ssh

Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-110-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue 28 Jun 2022 03:54:19 PM UTC

  System load:  0.09               Processes:             120
  Usage of /:   11.9% of 30.63GB   Users logged in:       0
  Memory usage: 22%                IPv4 address for eth0: 10.0.2.15
  Swap usage:   0%


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
Last login: Tue Jun 28 15:53:15 2022 from 127.0.0.1

vagrant@vagrant:~$ ssh localhost 'tty'

vagrant@localhost's password: 

not a tty

vagrant@vagrant:~$ ssh -t localhost 'tty'

vagrant@localhost's password: 

/dev/pts/1

Connection to localhost closed.

vagrant@vagrant:~$ 
```


 13)  reptyr {{pid}}

 14) Команда tee делает вывод одновременно и в файл, указаный в качестве параметра, и в stdout, 
в данном примере команда получает вывод из stdin, перенаправленный через pipe от stdout команды echo
и так как команда запущена от sudo , соотвественно имеет права на запись в файл


