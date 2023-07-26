# PSQL Client as Docker image

[![Build and Push](https://github.com/paolodenti/psqlclient/actions/workflows/build-publish.yaml/badge.svg)](https://github.com/paolodenti/psqlclient/actions/workflows/build-publish.yaml)

Postgresql client, interactive, or to run a single script or execute file content.

## Connect to db

```bash
docker run --rm \
  -it \
  --network host \
  paolodenti/psqlclient \
  psql postgresql://<username>:<password>@<host>:<port>/<db name>
```

## Single command

```bash
docker run --rm \
  --network host \
  paolodenti/psqlclient \
  psql postgresql://<username>:<password>@<host>:<port>/<db name> \
  -c "\dt;"
```

## Command file

```bash
cat <<EOT >> commands.sql
\dt;
EOT

docker run --rm \
  --network host \
  -v $(pwd)/commands.sql:/commands.sql \
  paolodenti/psqlclient \
  psql postgresql://<username>:<password>@<host>:<port>/<db name> \
  -f /commands.sql
```

## Connect to an existing docker compose postgres instance

```bash
docker network ls
# select the network

docker run --rm \
  -it \
  --network <the compose network> \
  paolodenti/psqlclient \
  psql postgresql://ps:ps@<the compose service name>:<port>/<db name>
```

## Configure psql as a standard psql command

```bash
alias psql='docker run --rm -it --network host paolodenti/psqlclient psql'

psql postgresql://<username>:<password>@<host>:<port>/<db name>
```
