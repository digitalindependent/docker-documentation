


## Documentation installing Speedtest-Tracker


## Links:
1. Github Repo Speedtest-Tracker by Alex Justesen: https://github.com/alexjustesen/speedtest-tracker
2. Documentation: https://docs.speedtest-tracker.dev/



docker-compose.yml:

```yml
version: '3.3'
services:
    speedtest-tracker:
        container_name: speedtest-tracker
        ports:
            - '8080:80'
            - '8443:443'
        environment:
            - PUID=1000
            - PGID=1000
            - DB_CONNECTION=mysql
            - DB_HOST=db
            - DB_PORT=3306
            - DB_DATABASE=speedtest_tracker
            - DB_USERNAME=speedy
            - DB_PASSWORD=password
        volumes:
            - '/path/to/directory:/config'
            - '/path/to/directory/web:/etc/ssl/web'
        image: 'ghcr.io/alexjustesen/speedtest-tracker:latest'
        restart: unless-stopped
        depends_on:
            - db
    db:
        image: mariadb:10
        restart: always
        environment:
            - MARIADB_DATABASE=speedtest_tracker
            - MARIADB_USER=speedy
            - MARIADB_PASSWORD=password
            - MARIADB_RANDOM_ROOT_PASSWORD=true
        volumes:
            - speedtest-db:/var/lib/mysql
volumes:
  speedtest-db:
```
