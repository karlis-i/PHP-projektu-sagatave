
# Docker + Laravel projekts

Docker + Laravel projekta sagatave  


## Konfigurācijas faili un tajos veicamās izmaiņas
- `.env`
    - deklarācijā `DB_NAME` jānorāda datubāzes nosaukums
    - deklarācijā `DB_ROOT_PWD` jānorāda datubāzes administratora (root) parole
- `docker-compose.yml` : izmaiņas nav nepieciešamas
- `nginx/default.conf.template` : izmaiņas nav nepieciešamas
- `php/Dockerfile` : izmaiņas nav nepieciešamas
- `php/php.ini` : izmaiņas nav nepieciešamas


## Vides sagatavošana un Laravel instalēšana
1. Veiciet augstāk aprakstītos konfigurācijas darbus
2. Uzbūvējiet konteineru, projekta direktorijā izpildot komandu `docker-compose build`
3. Iedarbiniet konteineru, projekta direktorijā izpildot komandu `docker-compose up -d`
4. Pieslēdzieties konteineram, projekta direktorijā izpildot komandu `docker exec -it myproject-php bash`.  
    NB! Ja esat pārsaucis Docker konteinerus failā `.env`, tad `myproject-php` vietā Jums jāraksta aktuālais PHP konteinera nosaukums
5. Konteinerā instalējiet Laravel, izpildot komandu `composer create-project laravel/laravel .`  
    NB! Neaizmirstiet komandas beigās norādīt punktu
6. Pārlūkprogrammā atveriet adresi http://localhost/ - veiksmīgas Laravel instalācijas gadījumā redzēsiet Laravel sākumlapu


@todo
- Adminer
- Laravel datubāze un migrācijas
