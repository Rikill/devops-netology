Какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?

	1. HISTFILESIZE - максимальное число строк в файле истории для сохранения, строка 692
	2. HISTSIZE - число команд для сохранения, строка 703

что делает директива ignoreboth в BASH?

	не сохраняет команды начинающиеся с пробела и не сохраняет если такая команда уже была ранее 

{} - зарезервированные слова, список, строка 147

touch {1..100000}.txt - создаст в текущей директории соответсвющее число фалов

touch {1..300000}.txt - zsh: argument list too long: touch

[[ -d /tmp ]] - проверяет наличие кататлога

vagrant@vagrant:~$ mkdir /tmp/new_path_dir/

vagrant@vagrant:~$ cp /bin/bash /tmp/new_path_dir/

vagrant@vagrant:~$ type -a bash

bash is /usr/bin/bash

bash is /bin/bash

vagrant@vagrant:~$ PATH=/tmp/new_path_dir/:$PATH

vagrant@vagrant:~$ type -a bash

bash is /tmp/new_path_dir/bash

bash is /usr/bin/bash

bash is /bin/bash'

команда at используется для назначения одноразового задания на заданное время, а команда batch — для назначения
одноразовых задач,
которые должны выполняться, когда загрузка системы становится меньше 0,8.
