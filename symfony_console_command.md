bin/console --env=testlocal doctrine:migrations:execute --down 20210823144452
bin/console --env=testlocal doctrine:fixtures:load --no-interaction
bin/console doctrine:database:drop --if-exists --force
bin/console doctrine:database:create --if-not-exists

bin/console cache:clear

bin/console debug:autowiring Faker\Generator
bin/console debug:container
bin/console lint:container

docker-compose -f docker-compose.dev.yaml -f docker-compose.dev.alp.yaml up
docker-compose -f docker-compose.dev.yaml -f docker-compose.dev.alp.yaml exec -T --workdir=/var/www/postamat php vendor/bin/codecept
docker-compose -f docker-compose.dev.yaml -f docker-compose.dev.alp.yaml exec -T --workdir=/var/www/postamat php composer
docker-compose -f docker-compose.dev.yaml -f docker-compose.dev.alp.yaml exec postgres pg_restore --clean --if-exists --dbname=orders --no-owner --no-privileges -U user_name -W /tmp/dump.sql

**Наcтройки symfony/messenger**

`bin/console debug:messenger`

**Обработать одно сообщения из транспорта и завершить процесс**

`bin/console messenger:consume async --memory-limit=128M --time-limit=3600 --limit=1 -vvv`

**Обработать сообщения из транспорта doctrine failure. Будут обработаны в соответствии с retry_strategy**

`bin/console messenger:consume failed --limit=1 -vvv`

**Вывести сообщение с id 20(или все сообщения, если убрать 20) из failure doctrine транспорта**

`bin/console messenger:failed:show 20`

**Обработать все сообщения по очереди в 1 косьюмера из failure doctrine подконтрольно по сообщению**

`bin/console messenger:failed:retry -vvv`

**Удалить сообщение с id 20 из failure doctrine**

`bin/console messenger:failed:remove 20`

**Остановить всех воркеров**

`bin/console messenger:stop-workers`

**Узнать все флаги команды**

`bin/console messenger:consume --help`

