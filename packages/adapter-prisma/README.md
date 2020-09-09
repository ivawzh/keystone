<!--[meta]
section: api
subSection: database-adapters
title: Prisma adapter
[meta]-->

# Prisma database adapter

[![View changelog](https://img.shields.io/badge/changelogs.xyz-Explore%20Changelog-brightgreen)](https://changelogs.xyz/@keystonejs/adapter-prisma)

The [Prisma](https://www.prisma.io/) adapter is a general purpose adapter which can be used to connect to a range of different database backends.
At present, the only fully tested backend is `Postgres`, however Knex gives the potential for `MSSQL`, `MySQL`, `MariaDB`, `SQLite3`, `Oracle`, and `Amazon Redshift` to be supported.

## Usage

```javascript
const { PrismaAdapter } = require('@keystonejs/adapter-prisma');

const keystone = new Keystone({
  adapter: new PrismaAdapter({...}),
});
```

## Config

### `getPrismaPath`

_**Default:**_ `({ prismaSchema }) => '.prisma'`

This function deterimes the directory to be used for storing

### `getDbSchemaName`

_**Default:**_ `({ prismaSchema }) => 'public'`

Allow the adapter to drop the entire database and recreate the tables / foreign keys based on the list schema in your application. This option is ignored in production, i.e. when the environment variable NODE_ENV === 'production'.

### `enableLogging`

These options are passed directly through to Knex.

See the [knex docs](https://knexjs.org/#Installation-client) for more details.

_**Default:**_ `false`

## Debugging

To log all Knex queries, run the server with the environment variable `DEBUG=knex:query`.

## Setup

Before running Keystone with the Knex adapter you should configure a database. By default Knex will look for a Postgres database on the default port, matching the project name, as the current user.

In most cases this database will not exist and you will want to configure a user and database for your application.

Assuming you're on MacOS and have Postgres installed the `build-test-db.sh` does this for you:

```shell
./build-test-db.sh
```

Otherwise, you can run these steps manually:

```shell allowCopy=false showLanguage=false
createdb -U postgres keystone
psql keystone -U postgres -c "CREATE USER keystone5 PASSWORD 'k3yst0n3'"
psql keystone -U postgres -c "GRANT ALL ON DATABASE keystone TO keystone5;"
```

If using the above, you will want to set a connection string of: `postgres://keystone5:k3yst0n3@localhost:5432/keystone`