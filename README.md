# Multi Tenancy with Spring Boot, Hibernate & Liquibase

## Overview

This project demonstrates how to apply a single changeset to multiple schemas in a PostgreSQL database, enabling support
for multitenancy with a single database and multiple schemas.

## How to use the examples

1. When you want to add new schema, create a new changeset to be applied to your new schema.
2. Start by running `docker-compose up -d` to launch the Liquibase Docker container.
3. Next, manually create the desired schemas in the database. You can do this using a tool like pgAdmin or by running a
   script.
4. Start spring boot application.

## How to start a Dockerized postgres database

All the examples require a postgres database running at localhost:5432. Run the following command
to use the provided `docker-compose.yml` configuration to start a dockerized postgres
container:

```
docker-compose up -d
```

Close it down with the following command when done, or if you need to recreate the database:

```
docker-compose down -v
```