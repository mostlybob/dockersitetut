# Summary
I lifted this from https://docs.docker.com/engine/examples/postgresql_service/ and it worked well.

The `Dockerfile` worked as listed.

Using the -rm switch builds and starts the instance and kills it when the command is exited.

```
$ docker build -t eg_postgresql .
```

Builds the docker image, but doesn't start it.

```
$ docker run --rm -P --name pg_test eg_postgresql
```

Starts a volatile instance of the container built in the previous command.

## Connecting 

Two ways: container linking and connecting from the host system

```
$ docker run --rm -t -i --link pg_test:pg eg_postgresql bash
```

Starts another volatile instance of the `eg_postgresql` container and starts a bash prompt.

```
$ psql -h localhost -p 49153 -d docker -U docker --password
```

Runs from the host, if you have `postgresql-client` installed. Fedora doesn't list that as available. I'm sure it is, it's just called something else. I installed pgadmin and it worked well.

As defined in the `Dockerfile` the database credentials are docker/docker.

```
$ docker run --rm --volumes-from pg_test -t -i busybox sh
```

Starts another instance of the currently running `pg_test` container so you can query the running server and backup logs etc.
