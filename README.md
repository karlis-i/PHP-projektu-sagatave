
# Docker + Laravel projekts

Docker + Laravel projekta sagatave  


## Konfigurācijas faili un tajos veicamās izmaiņas
- `.env`
    - deklarācijā `DATABASE_NAME` jānorāda datubāzes nosaukums
    - deklarācijā `DB_ROOT_PWD` jānorāda datubāzes administratora (root) parole. Var atstāt esošo, `root`
- `docker-compose.yml`
    - nav obligāti, bet varat pārsaukt Docker konteinerus (`my_project-*`)
- `nginx/default.conf`
    - ja esat pārsaucis Docker konteinerus failā `docker-compose.yml`, tad izlabojiet konteinera `my_project-php` nosaukumu rindā `fastcgi_pass my_project-php:9000;`
    - ja esat norādījis domēna vārdu operētājsistēmas `hosts` failā, tad tas jānorāda deklarācijā `server_name`
- `nginx/Dockerfile` : izmaiņas nav nepieciešamas
- `php/Dockerfile` : izmaiņas nav nepieciešamas
- `php/php.ini` : izmaiņas nav nepieciešamas


## Vides sagatavošana un Laravel instalēšana
1. Veiciet augstāk aprakstītos konfigurācijas darbus
2. Uzbūvējiet konteineru, projekta direktorijā izpildot komandu `docker-compose build`
3. Iedarbiniet konteineru, projekta direktorijā izpildot komandu `docker-compose up -d`
4. Pieslēdzieties konteineram, projekta direktorijā izpildot komandu `docker exec -it my_project-php bash`.  
    NB! Ja esat pārsaucis Docker konteinerus failā `docker-compose.yml`, tad `my_project-php` vietā Jums jāraksta aktuālais PHP konteinera nosaukums
5. Konteinerā instalējiet Laravel, izpildot komandu `composer create-project --prefer-dist laravel/laravel .`  
    NB! Neaizmirstiet komandas beigās norādīt punktu
6. Veiciet datubāzes konfigurāciju failā `PROJEKTA-DIREKTORIJA/application/.env`, norādot sekojošās vērtības:  
    - `DB_CONNECTION=mysql`  
    - `DB_HOST=my_project-mysql` NB! Ja esat pārsaucis Docker konteinerus failā `docker-compose.yml`, tad `my_project-php` vietā Jums jāraksta aktuālais PHP konteinera nosaukums
    - `DB_PORT=3306`
    - `DB_DATABASE=` Jānorāda tas datubāzes nosaukums, ko ierakstījāt failā `PROJEKTA-DIREKTORIJA/.env`, deklarācijā `DATABASE_NAME`
    - `DB_USERNAME=root`
    - `DB_PASSWORD=` Jānorāda tā parole, ko ierakstījāt failā `PROJEKTA-DIREKTORIJA/.env`, deklarācijā `DB_ROOT_PWD`
7. Opcionāli- Ja projektā būs nepieciešama autorizācija, tad konteinerā jāizpilda sekojošās komandas:
    1. `composer require laravel/ui --dev` - tā instalē `laravel/ui` pakotni
    2. `php artisan ui bootstrap --auth` - tā ģenerē autorizācijas sistēmai nepieciešamos failus
8. Veiciet datubāzes migrācijas, konteinerā izpildot komandu `php artisan migrate`


## Node.js un npm instalēšana:
- aiziet uz Node.js lapu https://nodejs.org/en/  
- piefiksēt LTS versijas numuru
- aiziet uz https://nodejs.org/en/download/ un atrast saiti `Installing Node.js via package manager`
- tajā atrast sadaļu, kas attiecas uz Debian
- 2020.05 jāiet uz `Node.js binary distributions are available from NodeSource.`
    - https://github.com/nodesource/distributions/blob/master/README.md
    - tur jāatrod instrukcijas, kas paredzētas LTS versijai Debian sistēmās
    - `Node.js v12.x:`
        - `# Using Debian, as root`
        - `curl -sL https://deb.nodesource.com/setup_12.x | bash -`
        - `apt-get install -y nodejs`
- iekopēt konkrētās instrukcijas PHP konteinera Dockerfailā `php/Dockerfile`:
```
# Install Node and npm
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - \
    && apt-get install -y nodejs
```


## Node.js alternatīva - vecs un nepārbaudīts piemērs
```
# Composer install
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# Node, npm, gulp
RUN apt-get -y --fix-missing install curl gnupg software-properties-common
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs
```

## Adminer
- http://localhost:8081/?server=my_project-mysql&username=root&db=my_project-db


## Konfigurācijas paraugi
- https://www.digitalocean.com/community/tutorials/how-to-set-up-laravel-nginx-and-mysql-with-docker-compose
- https://medium.com/oceanize-geeks/simple-approach-to-using-docker-with-laravel-nginx-and-mysql-server-3fab25bd0c1d
- https://github.com/dimadeush/docker-nginx-php-laravel
