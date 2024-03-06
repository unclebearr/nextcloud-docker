# NEXTCLOUD, REDIS, MARIADB, TRAEFIK

rename example.env to .env fill out the variables.

populate the .secrets directory files with credentials. avoid special characters like semicolon (;), single quote ('), double quote ("), and backslash (\), as well as whitespace characters such as space, tab, and newline, to mitigate potential syntax errors.

## database
find root password from the "DB_ROOT_PASSWORD" file in .secrets directory.

`docker exec -it nc-db mariadb -u root -p`

`GRANT ALL PRIVILEGES ON your_database.* TO 'your_user'@'%';`

`FLUSH PRIVILEGES;`

`exit`

## cronjob
from host machine

`sudo crontab -e`

`*/5 * * * * docker exec -u www-data nc-web php /var/www/html/cron.php`

## basic config additions

`docker exec --user www-data -it nc-web php occ config:system:set default_phone_region --value=“CA”`

https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes


`docker exec --user www-data -it nc-web php occ config:system:set logtimezone --value=“America/Toronto”`

https://www.php.net/manual/en/timezones.php