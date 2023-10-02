## Linux terminal scheduled job

`/var/spoon/cron/crontabs/username` - путь сохранения отложенных работ(scheduled jobs)
`etc/crontab` - путь сохранения системных отложенных работ
`var/log/syslog` - системный лог Linux


cronjob cheat sheet
```bash 
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday;
# │ │ │ │ │                                   7 is also Sunday on some systems)
# │ │ │ │ │                                   OR sun, mon, tue, wed, thu, fri, sat
# │ │ │ │ │
# * * * * *
```

Стандартная запись job

```
* * * * 5 echo "Firt scheduled job" >> /home/dmirykrtv/mylog.txt
```

Пример записи с определенной периодичностью (*/2 в примере это каждые 2 минуты запускай скрипт)

```
*/2 * * * 5 echo "Firt scheduled job" >> /home/dmirykrtv/mylog.txt
```

Запуск скрипта каждые 2 минуты в пятницу
```
*/2 * * * 5 /home/dmitrykrtv/scripts/myskcript.sh
```

Запуск скрипта в 2 минуты и в 5минут. Можно указывать сколь угодно таких параметров.
```
2,5 * * * 5 /home/dmitrykrtv/scripts/myskcript.sh
```

Полезные команды:
- `crontab -e` - редактировать файл с scheduled job
- `crontab -l` - просмотреть файл scheduled job
- `sudo cat var/log/syslog | grep CRON` - вывести системные логи отсортированные по данным, касающимся отложенных работ