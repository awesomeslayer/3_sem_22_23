## Анализ прототипов синхронизации процессов

### Запуск

Добавить в Makefile флаги размеров для каждого отдельного размера рабочего буфера (3 разных варианта). Запустить каждую отдельную программу с утилитой time для проверки программы  <br/>

Флаги запуска: ```-DS_SIZE```, ```-DM_SIZE```, ```-DL_SIZE```<br/>

``` bash
  Make
```
``` bash
  time ./a_sender.out & ./a_receiver.out
```

Иногда может быть нужно sudo

###Параметры:

|NAMES| S | M | L |
|------|--------------|------------|----------| 
|BUF SIZES| 512 | 4096 | 65536 |
|INPUT FILE SIZES | 4kB          | 100MB      | 2GB |


### Графики: 

После получения информации о веременах работы различных прототипов синхронизации, получаем графики для различных случаев:

![Image small](https://github.com/awesomeslayer/3_sem_22_23/blob/main/task3/HW/images/Small.jpg)
<br/>
![Image Medium](https://github.com/awesomeslayer/3_sem_22_23/blob/main/task3/HW/images/Medium.jpg)
<br/>
![Image Large](https://github.com/awesomeslayer/3_sem_22_23/blob/main/task3/HW/images/Large.jpg)



### Выводы: 
__Message queue__  самая эффективная для отправки небольших сообщений (~512 bytes). В других случаях,к сожалению, они не очень эффективны<br/>

__FIFO__ Стабильно работает в диапазоне средних размеров данных (~100 MB) со всеми размерами буфера и является самым легким для создания и использования методом.<br/>

Самым эффективным методом мне показался: ___virtual-shared memory___, который позволяет немедленно получить доступ к файлам и памяти в других процессах, но если вы работаете с РЕАЛЬНЫМИ большими файлами, размер которых превышает константы из " ipcs -l", вам придется добавить синхронизацию, и время увеличится, тк будет тратиться на чтение и запись<br/>
It will be cost of reading and writing.<br/>
