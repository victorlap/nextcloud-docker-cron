# nextcloud-docker-cron
Provide a way to automaticcaly run nextcloud's cron.php file inside the docker container

## Example usage
The following `docker-compose.yml` will bring up a nextcloud instance on `localhost:8080`.
Afterwards check if the setting under `Settings > Administration > Basic Settings > Background jobs` is set to `Cron`.
```yaml
version: '2'

services:
  app:
    image: victorlap/nextcloud-docker-cron
    volumes:
      - nextcloud:/var/www/html
    networks:
      - db
    ports:
      - "8080:80"
    environment:
      - MYSQL_HOST=db
      - MYSQL_USER=root
      - MYSQL_PASSWORD=root
      - MYSQL_DATABASE=nextcloud
      - NEXTCLOUD_ADMIN_USER=admin
      - NEXTCLOUD_ADMIN_PASSWORD=admin
    depends_on:
      - db

  db:
    image: mysql
    networks:
      - db
    command: --default-authentication-plugin=mysql_native_password
    environment:
      - MYSQL_DATABASE=nextcloud
      - MYSQL_ROOT_PASSWORD=root
    volumes:
      - db:/var/lib/mysql

volumes:
  nextcloud:
  db:

networks:
  db:
```
