sudo apt install supervisor

/etc/supervisor/

sudo systemctl enable supervisor

sudo supervisorctl add go.example

supervisord - сервер супервизора

sudo supervisorctl add go.example

sudo service supervisor start {start|stop|restart|force-reload|status}

sudo supervisorctl reread - надо делать при изменении конфигов для процессов

sudo supervisorctl status - статус всех дочерних процессов(управляемых с помощью сервера supervisor)

sudo supervisorctl restart go.example - надо делать перезагруку процесса после обновления его кода.

sudo supervisorctl start go.example

sudo supervisorctl stop go.example

[program:go.example]
command= php /usr/bin/php /var/www/go.php
stderr_logfile=/var/log/err_go.log
stdout_logfile=/var/log/go.log
autostart=true
autorestart=true
user=www-data
stopsignal=KILL
process_name=%(program_name)s_%(process_num)02d
numprocs=10

[inet_http_server]
port=127.0.0.1:9010
;username=some_user_name
;password=some_password

[eventlistener:memmon]
command=memmon -a 200MB -m error@ruhighload.com
events=TICK_60

https://ruhighload.com/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D0%BA+%D0%BF%D1%80%D0%BE%D1%86%D0%B5%D1%81%D1%81%D0%BE%D0%B2+%D0%B2+supervisor