Just a quick mashup as it is right now to provide basic functionallty.

The main reason this arose was to allow for me to enter the logs into SQL so 
I can better run queries against that data.

Connects to the same database as hey0's mod, 'minecraft' by default.

=============
Configuration
=============

Settings are configured my editing the parser.settings file

Current Settings:

     masterLogPath="<path to master log file>"
This is the path to the master log file

     injectLogPath="<path to master inject file>"
This is the path to the inject log path. This log contains all data that has been injected into 
the sql database along with the hashcode, so basically a txt table of the INSERT command. 
Plan on making this optional.

     displayFluff=1|0   
1=Display fluff text  
0=Hide text denoted as fluff in the fluff.txt file

     logDatabase="<name of database>"

     logTableName="<name of the log table>"

Example parser.settings:
masterLogPath="/var/www/minecraft/logs/master-log.log"
injectLogPath="/var/www/minecraft/inject.log"
displayFluff=0


Currently requires that the logs be output to a master file to parse correctly.
When the lines are injected into sql via the parser, it will zero out the master log file if there are no errors.
This is to keep the filesize down of the master log file.

css/default.css contains all of the styles for the color legend.

SQL mechanics:

A hash is created from the log line and used as the primary key in the table.
This allows for you to run the same inject on the same log without worry about any duplicate entries.
This also removes duplicate entries for commands that are spammed to the console within that second.

SQL Table is created via the following query:
CREATE TABLE logs(
  PRIMARY KEY(Hash),
  Date DATETIME,
  Class VARCHAR(20),
  Text VARCHAR(100),
  Hash CHAR(32) NOT NULL)";


============
commands.php
============

commands.php is responsible for all of the data pushing. It is command line only as to allow for cron 
jobs


Has functions to:

Create the 'log' table				: commands.php createTable

Drop the 'log' table				: commands.php dropTable

Clear the 'log' table				: commands.php clearTable

Inject the log data into the 'log' table	: commands.php inject




User logTime calculation needs same $uptime check


