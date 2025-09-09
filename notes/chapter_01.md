# Chapter 1: An App to Get You Started

## What is Rideshare?

* Back-end Rails API for an imaginary ridesharing service
* Core Active Record Models
  * `Driver`
  * `Rider`
  * `Trip`
  * `TripRequest`
* Active Record
  * Default [Object Relational Mapping (ORM)](../GLOSSARY.md#object-relational-mapping-orm) for Rails
  * Use Ruby objects and syntax to interact with PostgreSQL
  * Relies on "Convention over Configuration"
    * less configurable than other frameworks
  * Used for persistance and schema evolution

## Active Record Schema Management Refresher

* Each change to the database schema design is a [migration](../GLOSSARY.md#migration)
  * versioned Ruby files
  * located in `db/migrate`
  * contain Active Record code that generates SQL statements
* Schema can be written in a Ruby or SQL format
  * Rideshare uses SQL (`db/structure.sql`)
  * Mostly containts structural information, but can contain data
  * Should be in sync with production
* The `schema_migrations` table is automatically added to Rails databases
  * used to determine if there are any pending migrations
  * pending migrations are applied with `bin/rails db:migrate`
* [Data Definition Language (DDL)](../GLOSSARY.md#data-definition-language-ddl)
  * statements like `CREATE TABLE` or `CREATE INDEX`
* [Data Modification Language (DML)](../GLOSSARY.md#data-manipulation-language-dml)
  * statements like `INSERT`, `UPDATE`, and `DELETE`
  * When possible, these modifications should be separate from migrations
