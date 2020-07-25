up:
	sudo docker-compose up -d
build:
	sudo docker-compose build --no-cache --force-rm
create-project:
	@make build
	@make up
	sudo docker-compose exec app composer create-project --prefer-dist laravel/laravel .
	sudo docker-compose exec app chmod -R 777 storage bootstrap/cache
install-recommend-packages:
	sudo docker-compose exec app composer require doctrine/dbal
	sudo docker-compose exec app composer require --dev barryvdh/laravel-ide-helper
	sudo docker-compose exec app composer require --dev beyondcode/laravel-dump-server
	sudo docker-compose exec app composer require --dev barryvdh/laravel-debugbar
	sudo docker-compose exec app composer require --dev roave/security-advisories:dev-master
	sudo docker-compose exec app php artisan vendor:publish --provider="BeyondCode\DumpServer\DumpServerServiceProvider"
	sudo docker-compose exec app php artisan vendor:publish --provider="Barryvdh\Debugbar\ServiceProvider"
init:
	sudo docker-compose up -d --build
	sudo docker-compose exec app composer install
	sudo docker-compose exec app cp .env.example .env
	sudo docker-compose exec app php artisan key:generate
	sudo docker-compose exec app php artisan storage:link
	sudo docker-compose exec app php artisan migrate:fresh --seed
remake:
	@make destroy
	@make init
stop:
	sudo docker-compose stop
down:
	sudo docker-compose down
restart:
	@make down
	@make up
destroy:
	sudo docker-compose down --rmi all --volumes
destroy-volumes:
	sudo docker-compose down --volumes
ps:
	sudo docker-compose ps
logs:
	sudo docker-compose logs
logs-watch:
	sudo docker-compose logs --follow
web:
	sudo docker-compose exec web ash
app:
	sudo docker-compose exec app bash
migrate:
	sudo docker-compose exec app php artisan migrate
fresh:
	sudo docker-compose exec app php artisan migrate:fresh --seed
seed:
	sudo docker-compose exec app php artisan db:seed
rollback-test:
	sudo docker-compose exec app php artisan migrate:fresh
	sudo docker-compose exec app php artisan migrate:refresh
tinker:
	sudo docker-compose exec app php artisan tinker
test:
	sudo docker-compose exec app php artisan test
optimize:
	sudo docker-compose exec app php artisan optimize
optimize-clear:
	sudo docker-compose exec app php artisan optimize:clear
cache:
	sudo docker-compose exec app composer dump-autoload -o
	@make optimize
cache-clear:
	@make optimize-clear
yarn:
	sudo docker-compose exec web yarn
yarn-dev:
	sudo docker-compose exec web yarn dev
yarn-watch:
	sudo docker-compose exec web yarn watch
yarn-watch-poll:
	sudo docker-compose exec web yarn watch-poll
yarn-hot:
	sudo docker-compose exec web yarn hot
db:
	sudo docker-compose exec db bash
sql:
	sudo docker-compose exec db bash -c 'mysql -u $$MYSQL_USER -p$$MYSQL_PASSWORD $$MYSQL_DATABASE'
redis:
	sudo docker-compose exec redis redis-cli
ide-helper:
	sudo docker-compose exec app php artisan clear-compiled
	sudo docker-compose exec app php artisan ide-helper:generate
	sudo docker-compose exec app php artisan ide-helper:meta
	sudo docker-compose exec app php artisan ide-helper:models --nowrite
