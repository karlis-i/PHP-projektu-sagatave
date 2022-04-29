
# Docker + Laravel

Docker + Laravel projekta sagatave.  
(Nedaudz pielāgojot, var izmantot arī citiem PHP projektiem)  


## Konfigurācija
Lai sāktu darbu ar šo projekta sagatavi, papildus konfigurēšana nav nepieciešama. Šādā gadījumā spēkā būs sekojoši konfigurācijas parametri:
- Vietnes adrese: [http://localhost/](http://localhost/)
- Datubāzes serveris: `mysql`
- Datubāzes ports: 3306
- Datubāzes nosaukums: `database`
- Datubāzes lietotājs: root/root
- Datubāzes administrācija: [http://localhost:8080/?server=database&username=root&db=database](http://localhost:8080/?server=database&username=root&db=database)


## Vides sagatavošana un Laravel instalēšana
1. Veiciet konfigurācijas darbus, ja vēlaties
2. Uzbūvējiet konteineru, projekta direktorijā izpildot komandu `docker-compose build`
3. Iedarbiniet konteineru, projekta direktorijā izpildot komandu `docker-compose up -d`
4. Pieslēdzieties konteineram, projekta direktorijā izpildot komandu `docker exec -it  bash`.  
    NB! Ja `.env` failā ir mainīts `PHP_CONTAINER_NAME` nosaukums, tad konteinera pieslēgšanās komandā tas jāraksta `php-container` vietā!
5. Ar komandu `pwd` pārliecinieties, ka atrodaties direktorijā `/var/www/src`!  
    Ja ne, aizejiet uz to ar komandu `cd /var/www/src`
6. Instalējiet Laravel ar komandu `composer create-project laravel/laravel .`  
    NB! Neaizmirstiet komandas beigās norādīt punktu!
7. Veiciet Laravel konfigurāciju:  
    Failā `src/.env`:  
        `APP_NAME` - norādiet savas lietotnes nosaukumu  
        `DB_HOST=database`  
        `DB_PORT=3306`  
        `DB_DATABASE=database`  
        `DB_USERNAME=root`  
        `DB_PASSWORD=root`  
    Failā `src/config/app.php`  
        `'timezone' => 'Europe/Riga',`  
        `'locale' => 'lv',`  

Tagad pārlūkā atverot [http://localhost/](http://localhost/) , Jums vajadzētu redzēt Laravel sākumlapu!  


---

## Sagataves lietošana bez Laravel
Galvenais, kas jāmaina, ja vēlaties sagatavi izmantot projektiem bez Laravel, ir Web servera 'document root'. To varat nomainīt, `.env` failā nomainot `DOCUMENT_ROOT` vērtību. Vienkāršiem projektiem šī vērtība var būt `/var/www/src`


---

## Changelog
- 2022-04
    - Direktorijas project/ nosaukums nomainīts uz src/
- 2021-10
    - PHP versija nomainīta no 7.4 uz 8
- 2021-04  
    - Pielāgota PHP 7.4 un Laravel 8  
    - Izmanto jaunākās MySQL un Adminer versijas  
    - Gandrīz pilnībā pārrakstīti konfigurācijas faili  
- 2020-05  
    - Pirmā versija  

---

## @todo:
```
    8. Opcionāli- Ja projektā būs nepieciešama autorizācija, tad konteinerā jāizpilda sekojošās komandas:
        1. `composer require laravel/ui --dev` - tā instalē `laravel/ui` pakotni
        2. `php artisan ui bootstrap --auth` - tā ģenerē autorizācijas sistēmai nepieciešamos failus
    9. Veiciet datubāzes migrācijas, konteinerā izpildot komandu `php artisan migrate`


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
```
