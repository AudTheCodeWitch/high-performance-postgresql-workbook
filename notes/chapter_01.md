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

## Exploring Rideshare Dependencies

* Requirements
  * Ruby
  * rbenv
  * PostgreSQL
  * Git
  * Homebrew

## Installing Application Dependencies

* `git --version`
  * Must be > 2.42.0
  * `brew upgrade git` if the version is too low
* `rbenv --version`
  * Must be > 1.2.0
* `brew install graphviz`

## Installing PostgreSQL on macOS

* Recommended way to install is via [Postgres.app](https://postgresapp.com)
* In the Postgres.app...
  * Click "Initialize"
    * Postgres runs on port `5432`
    * Adds db with the same name as your macOS user
      * `psql` connects to this db by default
* Configure `PATH` for `psql`
  * ```shell
    sudo mkdir -p /etc/paths.d && echo "/Applications/Postgres.app/Contents/Versions/latest/bin" | sudo tee /etc/paths.d/postgresapp
    ```
* Test `psql` and `pg_dump`
  * `psql --version` > 16.0
  * `pg_dump --version` > 16.0
  * `pg_config`
    * last line should show a postgres version > 16.0
* Configure `psqlrc` file
  * `ls -l ~/.psqlrc`
  * `touch ~/.psqlrc`
  * `rubymine ~/.psqlrc`

    * Add the following:
      ```shell
      \encoding unicode
      \set PROMPT1 '%n@%M:%>%x %/# '
      \set PROMPT2 ''

      \setenv PAGER 'less -S'
      ```
  * Verify `psql` output:

    ```shell
    psql (17.6 (Postgres.app))
    Type "help" for help.

    audreacook@[local]:5432 audreacook#
    ```

    * `psql (17.6 (Postgres.app))` --> `psql` client version
    * `audreacook` --> macOS user
    * `@[local]:5432` --> host and port
    * `audreacook#` --> current database and superuser prompt
  * Verify database connection in `psql`
  * ```shell
    SELECT current_database();
    ```
  * It should return your macOS username
  * Quit `psql` with `\q`

## Installing Rideshare

* Clone Rideshare repo into your selected directory
  * `git clone https://github.com/andyatkinson/rideshare.git`
* Confirm correct Ruby version (3.2.2) `ruby --version`
* Confirm correct Bundler version (>2.3.6) `bundler --version`
* Install gems `bundle install`

## Configuring PostgreSQL for Rideshare

* Custom shell script for Rideshare setup
  * (as opposed to `bin/rails db:create`)
  * Creates users and passwords
    * `owner`
    * `app`
    * `app_readonly`
  * Creates `rideshare_development` db
  * Creates `rideshare` schema
  * Grants permissions to schema and users
  * Alters default permissions according to PostgreSQL best practices
  * Removes `public` schema
* PostgreSQL **users**
  * roles with the `LOGIN` privelege
  * has a password set by `openssl` on macOS
* Storing `RIDESHARE_DB_PASSWORD` as environment variable
  * `export RIDESHARE_DB_PASSWORD=$(openssl rand -hex 12)`
  * Verify with `echo $RIDESHARE_DB_PASSWORD`
* `~/.pgpass` stores passwords for PostgreSQL users
  * Has a line for each user with a colon-separated format
  * `hostname:port:database:username:password`
    * Example: `localhost:5432:rideshare_development:owner:2C6uw3LprgUMwSLQ`
* Set `DB_URL` environment variable
  * `export DB_URL="postgres://postgres@localhost:5432/postgres"`
* Run the custom script
  * `sh db/setup.sh 2>&1 | tee -a output.log`
    * `2>&1` redirects stderr to stdout
    * `| tee -a output.log` appends all output to `output.log`

## Configuring Database Access

* The `owner` role
  * Connects with a password stored in `~/.pgpass`
  * Owns objects like tables within schema
* Setting `DATABASE_URL`
  * `export DATABASE_URL=postgres://owner:@localhost:5432/rideshare_development`
    * To avoid typing this every time, add it to your shell profile (`~/.zshrc`)
* Setting up quick access for Rails
  * `DATABASE_URL` is stored in `.env`
    * Used for rails commands like `rails db` or `rails console`
  * Verify it's working with `bin/rails db`
* Run migrations: `bin/rails db:migrate`
