# Домашнее задание к занятию "3.1. Работа в терминале. Лекция 1"

## Какие ресурсы выделены по-умолчанию?

По умолчанию выделено:
- CPU count="2"
- Memory RAMSize="1024"
- Display VRAMSize="4"
- Disk 64 GB

## Как добавить оперативной памяти или ресурсов процессора виртуальной машине?

Внеся правки в Vagrantfile:

    config.vm.provider "virtualbox" do |vb|
      # Customize the amount of memory on the VM:
      vb.memory = "1024"
      vb.cpus = "2"
    end

После нужно переагрузить ВМ или запустить, если она остановлена

## Какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?

HISTFILESIZE - максимальное число строк в файле истории для сохранения, строка 674

## Что делает директива ignoreboth в bash?

ignoreboth это сокращение для 2х директив ignorespace and ignoredups:

- ignorespace - не сохранять команды начинающиеся с пробела;
- ignoredups - не сохранять команду, если такая уже имеется в истории.

## В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?

Список команд на выполнение в текущем инстансе оболочки командной строки, в отличии от (), где выполнение идет в новом инстансе. По факту получается, что-то типа циклического исполнения команд. 216 строка.

## С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?

      vagrant@vagrant:~/tst_touch$ touch {1..100000}.txt


      vagrant@vagrant:~/test300000$ touch {1..300000}.txt
      -bash: /usr/bin/touch: Argument list too long

Не дает создать из-за превышения допустимого размера списка.

## В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]

Условие на проверку существования каталога /tmp, возвращает 0 или 1 в зависимости от правда условие или нет

## Сделайте так, чтобы в выводе команды type -a bash первым стояла запись с нестандартным путем, например bash is ...

     vagrant@vagrant:~$ mkdir /tmp/new_path_dir/
     vagrant@vagrant:~$ cp /bin/bash /tmp/new_path_dir/
     vagrant@vagrant:~$ type -a bash
     bash is /usr/bin/bash
     bash is /bin/bash
     vagrant@vagrant:~$ PATH=/tmp/new_path_dir/:$PATH
     vagrant@vagrant:~$ type -a bash
     bash is /tmp/new_path_dir/bash
     bash is /usr/bin/bash
     bash is /bin/bash

## Чем отличается планирование команд с помощью batch и at?

- at      executes commands at a specified time. (запуск команды в определенное время)
- batch   executes commands when system load levels permit; in other words, when the load average drops below 1.5, or the value specified in the invocation of atd (запуск команды в завимисоти от нагрузки системы)