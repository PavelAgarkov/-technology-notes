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

bin/console debug:messenger
bin/console messenger:consume async -vvv
bin/console messenger:consume transport_name
bin/console messenger:consume failed --limit=1 -vvv
bin/console messenger:failed:show
bin/console messenger:failed:retry -vvv
bin/console messenger:failed:remove 20
