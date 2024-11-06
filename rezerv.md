# Домашнее задание к занятию «Кластеризация и балансировка нагрузки» - 'Корнилов Андрей Алексеевич`



### Задание 1

Составьте команду rsync, которая позволяет создавать зеркальную копию домашней директории пользователя в директорию /tmp/backup

Необходимо исключить из синхронизации все директории, начинающиеся с точки (скрытые)

Необходимо сделать так, чтобы rsync подсчитывал хэш-суммы для всех файлов, даже если их время модификации и размер идентичны в источнике и приемнике.

На проверку направить скриншот с командой и результатом ее выполнения


Скриншот: 

![rsync](https://github.com/gtrksamara/sys-pattern-homework/blob/main/img/rsync.jpg)


---

### Задание 2

Написать скрипт и настроить задачу на регулярное резервное копирование домашней директории пользователя с помощью rsync и cron.

Резервная копия должна быть полностью зеркальной

Резервная копия должна создаваться раз в день, в системном логе должна появляться запись об успешном или неуспешном выполнении операции

Резервная копия размещается локально, в директории /tmp/backup

На проверку направить файл crontab и скриншот с результатом работы утилиты.

```
Скрипт

 #!/bin/bash

   SOURCE_DIR="$HOME/"

   BACKUP_DIR="/tmp/backup"

   CURRENT_DATE=$(date +"%Y-%m-%d %H:%M:%S")
   LOG_FILE="/var/log/backup_script.log"

   rsync -av --delete "$SOURCE_DIR" "$BACKUP_DIR" >> "$LOG_FILE" 2>&1

   if [ $? -eq 0 ]; then
       echo "$CURRENT_DATE: Backup completed successfully" >> "$LOG_FILE"
   else
       echo "$CURRENT_DATE: Backup failed" >> "$LOG_FILE"
   fi


```

![backup](https://github.com/gtrksamara/sys-pattern-homework/blob/main/img/backup.jpg)
![backup2](https://github.com/gtrksamara/sys-pattern-homework/blob/main/img/backup2.jpg)


---


