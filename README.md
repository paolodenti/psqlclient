# PSQL Client as Docker image

[![Build and Push](https://github.com/paolodenti/psqlclient/actions/workflows/build-publish.yaml/badge.svg)](https://github.com/paolodenti/psqlclient/actions/workflows/build-publish.yaml)

Postgresql client, interactive, or to run a single script or execute file content.

## Interactive CLI

```bash
docker run --rm -it --network host \
  paolodenti/psqlclient \
  psql postgresql://<username>:<password>@<host>:<port>/<db name>
```

## Execute a sql command

```bash
docker run --rm --network host \
  paolodenti/psqlclient \
  psql postgresql://<username>:<password>@<host>:<port>/<db name> \
  -c "\dt;"
```

## Execute a sql file

```bash
cat <<EOT >> commands.sql
\dt;
EOT

docker run --rm --network host \
  -v $(pwd)/commands.sql:/commands.sql \
  paolodenti/psqlclient \
  psql postgresql://<username>:<password>@<host>:<port>/<db name> \
  -f /commands.sql
```

## Connect to an existing docker compose postgres instance

```bash
docker network ls
# find out the compose network name

docker run --rm -it --network <the compose network> \
  paolodenti/psqlclient \
  psql postgresql://<username>:<password>@<the compose service name>:<port>/<db name>
```

## Configure psql as a standard psql command

```bash
alias psql='docker run --rm -it --network host paolodenti/psqlclient psql'

psql postgresql://<username>:<password>@<host>:<port>/<db name>
# or
psql -h <host> -p <port> -U <username> -W -d <db name>
```
