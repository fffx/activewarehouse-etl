Ruby Extract-Transform-Load (ETL) tool.

## Requirements

* Ruby 1.8.5 or higher
* Rubygems

## Online Documentation

Available at https://github.com/aeden/activewarehouse-etl/wiki/Documentation

## Features

Current supported features:

* ETL Domain Specific Language (DSL) - Control files are specified in a Ruby-based DSL
* Multiple source types. Current supported types:
  * Fixed-width and delimited text files
  * XML files through SAX
  * Apache combined log format
* Multiple destination types - file and database destinations
* Support for extracting from multiple sources in a single job
* Support for writing to multiple destinations in a single job
* A variety of built-in transformations are included:
  * Date-to-string, string-to-date, string-to-datetime, string-to-timestamp
  * Type transformation supporting strings, integers, floats and big decimals
  * Trim
  * SHA-1
  * Decode from an external decode file
  * Default replacement for empty values
  * Ordinalize
  * Hierarchy lookup
  * Foreign key lookup
  * Ruby blocks
  * Any custom transformation class
* A variety of build-in row-level processors
  * Check exists processor to determine if the record already exists in the destination database
  * Check unique processor to determine whether a matching record was processed during this job execution
  * Copy field
  * Rename field
  * Hierarchy exploder which takes a tree structure defined through a parent id and explodes it into a hierarchy bridge table
  * Surrogate key generator including support for looking up the last surrogate key from the target table using a custom query
  * Sequence generator including support for context-sensitive sequences where the context can be defined as a combination of fields from the source data
  * New row-level processors can easily be defined and applied
* Pre-processing
  * Truncate processor
* Post-processing
  * Bulk import using native RDBMS bulk loader tools
* Virtual fields - Add a field to the destination data which doesn't exist in the source data
* Built in job and record meta data
* Support for type 1 and type 2 slowly changing dimensions
  * Automated effective date and end date time stamping for type 2
  * CRC checking

## Dependencies

ActiveWarehouse ETL depends on the following gems:

* ActiveSupport Gem
* ActiveRecord Gem
* FasterCSV Gem (for Ruby < 1.9, otherwise the built-in CSV version will be used)
* AdapterExtensions Gem

## Usage

Once the ActiveWarehouse ETL gem is installed jobs can be invoked using the
included `etl` script. The etl script includes several command line options
and can process multiple control files at a time.

Command line options:

* <tt>--help, -h</tt>: Display the usage message.
* <tt>--config, -c</tt>: Specify a database.yml configuration file to use.
* <tt>--limit, -l</tt>: Specify a limit to the number of rows to process. This option is currently only applicable to database sources.
* <tt>--offset, -o</tt>: Specify the start offset for reading from the source. This option is currently only applicable to database sources.
* <tt>--newlog, -n</tt>: Instruct the engine to create a new ETL log rather than append to the last ETL log.
* <tt>--skip-bulk-import, -s</tt>: Skip any bulk imports.
* <tt>--read-locally</tt>: Read from the local cache (skip source extraction)

## Control File Examples

Control file examples can be found in the examples directory.

## Running Tests

    gem install bundler
    bundle install             # install the gems required for tests
    
    # then for either mysql/postgresql:
    # create database etl_unittest
    # create database etl_unittest_execution
    # adjust test/database.yml if needed

    rake test                  # for mysql
    rake test DB=postgresql    # for postgresql

## Running tests for MySQL and Postgresql in a row

* create the 2 databases for both systems
* fill test/database.mysql.yml
* fill test/database.postgresql.yml

Then (be warned that test/database.yml will be erased):

    rake test:all
    
will run the test suite against both MySQL and Postgresql in a row.

## Feedback

This is a work in progress. Comments should be made on the [activewarehouse-discuss mailing list](http://groups.google.com/group/activewarehouse-discuss). Contributions are always welcome.