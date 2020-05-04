
# Docker + Laravel projekts

Docker + Laravel projekta sagatave  

# Konfigurācijas faili un tajos veicamās izmaiņas
- `.env`
    - deklarācijā `DATABASE_NAME` jānorāda datubāzes nosaukums
    - deklarācijā `DB_ROOT_PWD` jānorāda datubāzes administratora (root) parole
- `docker-compose.yml`
    - nav obligāti, bet varat pārsaukt Docker konteinerus (`my_project-*`)
- `nginx/default.conf`
    - ja esat norādījis domēna vārdu `hosts` failā, tad tas jānorāda deklarācijā `server_name`
- `nginx/Dockerfile` : izmaiņas nav nepieciešamas
- `php/Dockerfile` : izmaiņas nav nepieciešamas
- `php/php.ini` : izmaiņas nav nepieciešamas

## Adminer
- http://localhost:8081/?server=my_project-mysql&username=root&db=my_project-db

## Konfigurācijas paraugi
- https://www.digitalocean.com/community/tutorials/how-to-set-up-laravel-nginx-and-mysql-with-docker-compose
- https://medium.com/oceanize-geeks/simple-approach-to-using-docker-with-laravel-nginx-and-mysql-server-3fab25bd0c1d
- https://github.com/dimadeush/docker-nginx-php-laravel
