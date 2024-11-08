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

## How to insert master data for each tenant

In this example, inserting data for each tenant (or schema) must be done manually. This is because, if we include the changeset in Liquibase for automatic handling, Liquibase will attempt to apply the changeset for each schema through the `runLiquibasePerSchema` bean, resulting in duplicate execution and causing errors.<br/>
<br/>
To insert data manually, a changeset has been provided in the file `db.changelog-tenant-2.0.yaml`. Run the following command to apply it:

```
liquibase \
  --url="jdbc:postgresql://localhost:5432/blog" \
  --username="postgres" \
  --password="secret" \
  --changeLogFile=multi-tenant-service/src/main/resources/db/changelog/db.changelog-tenant-2.0.yaml \
  update
```

<p>After executing this command, the master data will be inserted into each schema as specified.</p>

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