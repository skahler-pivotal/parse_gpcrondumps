COMMAND NAME: parse_gpcrondumps

Takes the output of the multiple data files that make
up a gpcrondump and creates individual files for each
table which contain the data for the table

*****************************************************
SYNOPSIS
*****************************************************

    parse_gpcrondumps 
    -i <input dump file location>
    -o <output file location>
    -t <14 digit timestamp of dump to use>
    [ -s <schema name to filter for> ]
    [ -T <schema.table name to filter for> ]
    [ -D ]

    parse_gpcrondumps -h


*****************************************************
DESCRIPTION
*****************************************************

The parse_gpcrondumps utility will parse a set of gpcrondump data
files and extract the data from multiple dump files into singluar files
name schema.table that containt the combined data.

This utility can be used for create data files from dumps which can then
be reimported back into the database or served with gpfdist to reload
data into the database.

*****************************************************
OPTIONS
*****************************************************

    -i <input dump file location>

  The location of the files from the backup that need to be parsed.

  This is a required flag.

    -o <output file location>

  The location where files will be created in the schema.tablename format
  which contain the combined data for that table from the various files.

  This is a required flag.

    -t <14 digit timestamp of dump to use>

  Dump files are identifiable by the 14 digit timestamp of the time the dump
  was taken. This timestamp is needed in case multiple gpcrondumps are located
  within the same location

  This is a required flag.

    -s <schema>

  Only data from the following schema will have data files created for
  them. You may only specify one schema.

    -T <schema.tablename>

  Only data from the schame and table combo will have data files created
  for it. You may only specify one schema.table

    -D

  Show debug information

    -h

  Display help

*****************************************************
EXAMPLES
*****************************************************

Dump all of the data for tables from a set of backup files
which comprise the 20160114100848 backup

    $ parse_gpcrondumps -i /backup/db_dumps/20160114/ -o /datafiles/ -t 20160114100848

Do the same thing, only just work with the data from the public schame

    $ parse_gpcrondumps -i /backup/db_dumps/20160114/ -o /datafiles/ -t 20160114100848 -s public

Do the same thing, only just work with the data from the foo table
which exists in the public schema

    $ parse_gpcrondumps -i /backup/db_dumps/20160114/ -o /datafiles/ -t 20160114100848 -T public.foo

