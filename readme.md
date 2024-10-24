# Nextcloud FPM - Nginx - MariaDB - Redis - Traefik
Replace all nc.local.example.ca domains with your domain in readme examples, .env, ./nginx/nextcloud.conf


## database
#### Generate passwords inside the files in .secrets directory & .env REDIS_HOST_PASSWORD. (Alphanumeric Only)

docker exec -it nc-db mariadb -u root -p

GRANT ALL PRIVILEGES ON USER.* TO 'DATABASE'@'%';

FLUSH PRIVILEGES;



## ssl
Inside ./ssl

#### Generate the private key
sudo openssl genrsa -out nc.local.example.ca.key 2048

#### Generate the certificate signing request (CSR)
sudo openssl req -new -key nc.local.example.ca.key -out nc.local.example.ca.csr

#### Generate a certificate valid for 10 years
sudo openssl x509 -req -days 3650 -in nc.local.example.ca.csr -signkey nc.local.example.ca.key -out nc.local.example.ca.crt



## Cronjob
from host machine
sudo crontab -e
*/5 * * * * docker exec -u www-data nc-fpm php /var/www/html/cron.php



## Basic config

#### Phone number region
docker exec --user www-data -it nc-fpm php occ config:system:set default_phone_region --value=CA
https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes

#### Timezone
docker exec --user www-data -it nc-fpm php occ config:system:set logtimezone --value=America/Toronto
https://www.php.net/manual/en/timezones.php


#### Set maintainance window to 4am
docker exec --user www-data -it nc-fpm php occ config:system:set maintenance_window_start --type=integer --value=4
