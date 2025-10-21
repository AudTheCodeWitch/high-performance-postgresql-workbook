# Chapter 2: Administration Basics

## Touring psql Features

* `psql` is a powerful command-line tool for interacting with PostgreSQL databases.
  * Ships with PostgreSQL (always available)
  * Can be used on remote hosts
  * Low latency
  * Well-tested and supported
* Connecting to the database:
  ```bash
  export DATABASE_URL="postgres://owner:@localhost:5432/rideshare_development"
  psql $DATABASE_URL
  ```
* Exploring `psql`
  * `SELECT PG_BACKEND_PID();` - Get the current session's process ID
    * A [backend](../GLOSSARY.md#backend) process ID was started for this `psql` session
  * `\s` - Show command history
    * Is a [meta-command](../GLOSSARY.md#meta-command) (starts with `\`)
  * [System catalogs](../GLOSSARY.md#system-catalog)
    * A PostgreSQL table or view that tracks internal information
    * Start with `pg_`
  * `SELECT * FROM pg_extension;` - List installed extensions
    * `pg_extension` is a system catalog provided by PostgreSQL
  * Searching for previous commands
    * Type "ctrl + r" and enter a search term
      * Requires adding `bind "^R" em-inc-search-prev` to your `~/.editrc` file
    * Use `\g` to run the last command again
    * Command history is saved in `~/.psql_history`
      * Not readable
      * Meant to be used by `psql` only
  * Storing more commands
    * Increase the `HISTSIZE` option value
    * Review `HISTFILE` and `HISTSIZE` options in the official docs
  * Customizing `psql`