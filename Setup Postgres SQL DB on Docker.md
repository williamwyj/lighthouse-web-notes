Guide: https://www.sqlshack.com/getting-started-with-postgresql-on-docker/
Istall PostgresSQL image on docker
```
docker pull Postgres
```
See list of all images on docker
```
docker image ls
```
Run a container/instance of the postgresSQL image, where database_name is the database name
```
docker run –name database_name -e POSTGRES_PASSWORD=Welcome4$ -p 5432:5432 Postgres
```
in docker CLI access postgres db
```
psql -h localhost -U postgres
```
