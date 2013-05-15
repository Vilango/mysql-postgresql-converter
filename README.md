
Disabled the sequence and table generation so it can be used to port a rails app.

Steps: 
  - Create new DB
  - rake db:migrate  # Create Schema  
  - convert & import data
      python db_converter.py dbdata.mysql dbdata.psql
      psql -U user -d database_name -h 127.0.0.1 -f dbdata.psql
      


MySQL to PostgreSQL Converter
=============================

Lanyrd's MySQL to PostgreSQL conversion script. Use with care.

This script was designed for our specific database and column requirements -
notably, it doubles the lengths of VARCHARs due to a unicode size problem we
had, places indexes on all foreign keys, and presumes you're using Django
for column typing purposes.

How to use
----------

Firstly, dump your database using `mysqldump --compatible=postgresql --default-character-set=utf8 -r databasename.mysql -u root databasename`.

Then, run the converter script using `python dbconverter.py databasename.mysql databasename.psql` - it'll print
progress to the terminal.

Finally, load your new dump into a fresh PostgreSQL database using `psql -f databasename.psql`.

More information
----------------

You can learn more about the move which this powered at http://lanyrd.com/blog/2012/lanyrds-big-move/ and some technical details of it at http://www.aeracode.org/2012/11/13/one-change-not-enough/.
