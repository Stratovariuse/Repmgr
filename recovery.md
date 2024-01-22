1. Попытка переподключить старого мастера
   ```
repmgr node rejoin -f /etc/repmgr/15/repmgr.conf -d 'host=master_host dbname=repmgr user=repmgr' --force-rewind --verbose
   ```

Если ошибка вида
```
pg_rewind: servers diverged at WAL location 1B1B/C165A8E8 on timeline 3
pg_rewind: error: could not open file "/var/lib/pgsql/15/data/pg_wal/0000000300001B1B000000C0": No such file or directory
pg_rewind: error: could not find previous WAL record at 1B1B/C0FFFE10
```

Значит вал файлов уже нет на действующем мастере и нужно с 0 клонировать старый

```
repmgr standby clone -f /etc/repmgr/15/repmgr.conf -d 'host=master_host dbname=repmgr user=repmgr' --force
systemctl start postgresql-15
repmgr -f /etc/repmgr/15/repmgr.conf standby register
```

