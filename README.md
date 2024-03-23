# linuxserver-nextcloud-postgres

Since SQLite is not really recommended for more intense use of Nextcloud, PostgreSQL is the go to.
The linuxserver/nextcloud image is really nice and it runs offline.

Here's the complete **docker-compose.yml** file for starting your new Nextcloud instace with everything set up out of the box:
```yaml
version: '3.9'

services:

  db:
    image: postgres
    restart: always
    shm_size: 128mb
    environment:
      POSTGRES_PASSWORD: example

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080

  nextcloud:
    image: lscr.io/linuxserver/nextcloud:latest
    container_name: nextcloud
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    volumes:
      - /path/to/nextcloud/config:/config
      - /path/to/data:/data
    ports:
      - 443:443
    restart: unless-stopped
```
to connect to the postgres database, on Nextcloud setup select PostgreSQL and fill in with the following:

- username: postgres
- password: yourpassword
- database: postgres
- server: name-of-your-postgres-container
