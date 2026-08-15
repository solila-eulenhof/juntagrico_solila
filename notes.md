Commands to run postgres locally:
```shell
docker pull postgres:15
docker volume create solila-db-pg15
docker run --name solila-db -e POSTGRES_USER=solila -e POSTGRES_PASSWORD=solila -p 5432:5432 -v solila-db-pg15:/var/lib/postgresql/data -d postgres:15
docker cp solila-dump solila-db:/solila-dump
docker exec -it solila-db bash
```
              
Inside the container
```shell
pg_restore -U solila -d solila -v /solila-dump
```

At this point, the name of the db is solila. Still inside the container, connect to the database using psql:
```shell
psql -U solila -d postgres
```

Then rename the database to juntagrico. This is because the webapp expects the name to be juntagrico:

```sql
alter database solila rename to juntagrico;
```
