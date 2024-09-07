Если сервер мастера упал
repmgr -f /etc/repmgr/11/repmgr.conf standby promote

Если нужно плановое перключение
repmgr -f /etc/repmgr/11/repmgr.conf standby switchover

После падения сервер (id 1) нужно вывести из кластера:
repmgr -f /etc/repmgr/11/repmgr.conf unregister --node-id 1

Возврат старого мастера в кластер придется осуществлять вручную
repmgr -f /etc/repmgr/11/repmgr.conf node rejoin -d 'host=u25778sms-db01 dbname=repmgr user=repmgr' --force-rewind

Сервер вернется в качестве стандбая. Далее нам ничего не мешает сделать плановое переключение и вернуть прежнего master.
repmgr -f /etc/repmgr/11/repmgr.conf standby switchover
