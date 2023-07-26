# PSQL Client as Docker image

[![Build and Push](https://github.com/paolodenti/psqlclient/actions/workflows/build-publish.yaml/badge.svg)](https://github.com/paolodenti/psqlclient/actions/workflows/build-publish.yaml)

Postgresql client, interactive, or to run a single script or execute file content.

## Connect to db

```bash
docker run --rm \
  -it \
  paolodenti/psqlclient \
  psql postgresql://ps:ps@127.0.0.1:5432/somedatabase
```

## Single command

```bash
docker run --rm \
  paolodenti/psqlclient \
  psql postgresql://ps:ps@127.0.0.1:5432/somedatabase \
  -c "\dt;"
```

## Command file

```bash
cat <<EOT >> commands.sql
\dt;
EOT

docker run --rm \
  -v $(pwd)/commands.sql:/commands.sql \
  paolodenti/psqlclient \
  psql postgresql://ps:ps@127.0.0.1:5432/somedatabase \
  -f /commands.sql
```
