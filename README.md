# Multi Tenancy with Spring Boot, Hibernate & Liquibase

## Overview

This project demonstrates how to apply a single changeset to multiple schemas in a PostgreSQL database, enabling support
for multitenancy with a single database and multiple schemas.

## How to use the examples

### How to Use the Examples

1. Start by running `docker-compose up -d` to launch the Liquibase Docker container.
2. Next, manually create the desired schemas in the database. You can do this using a tool like pgAdmin or by running a
   script.
3. Specify the schemas in the `application.yml` file under `multitenancy.master.datasource.schemas`, for
   example: `schemas: "tenant1,tenant2,tenant3"`.

#### Note: Ensure that the schema names and number of schemas in the database match those listed in multitenancy.master.datasource.schemas.

4. Now, start the Spring Boot application. Liquibase will apply the changeset to all specified schemas.

### Updating Schemas

To add or remove schemas, update both the database and the `multitenancy.master.datasource.schemas` section
in `application.yml`.

### Applying Changeset Updates

If you modify the changeset, simply restart the Spring Boot application, and the changes will be applied to the schemas
automatically.

## How to start a Dockerized postgres database

All the examples require a postgres database running at localhost:5432. Run the following command
to use the provided `docker-compose.yml` configuration to start a dockerized postgres
container:

```
docker-compose up -d
```

Close it down with the following command when done, or if you need to recreate the database:

```
docker-compose down
```