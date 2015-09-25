# Docker container for the MusicBrainz database

[![Docker Hub](https://img.shields.io/badge/docker-ready-blue.svg)](https://registry.hub.docker.com/u/arey/musicbrainz-database/) 

Based on the official Postgres image, this docker image installs a PostgreSQL 9.4 wilh all librairies required by the MusicBrainz database.

This image comes with a create-database.sh shell script used to create and feed the database:

* Create the musicbrainz schema
* Create all tables
* Import the last MusicBrainz database export
* Add index and primary keys


SQL scripts are retrieved from the [MusicBrainz Github repo](https://github.com/metabrainz/musicbrainz-server/master/admin/sql).

## Build the image

```
docker build -t arey/musicbrainz-database .
```

## Run the container and import the musicbrainz data

```
docker run -t -d -p 5432:5432 --name musicbrainz-database -e POSTGRES_USER=musicbrainz -e POSTGRES_PASSWORD=musicbrainz arey/musicbrainz-database
```

If you have host-based storage available for the Postgres DB files (recommended), adjust the above base command with a this parameter:
-v /path/to/storage/location:/var/lib/postgresql

```
docker run musicbrainz-database /create-database.sh
```

##  Connect to the database

From Java application, use the following JDBC URL: jdbc:postgresql://localhost:5432/musicbrainz and the credentials: musicbrainz / musicbrainz

Note : For Windows or MacOSX users, replace localhost with the boot2docker IP.

