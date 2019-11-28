# InfluxDB-dummyDB-for-testing
A dummy influxDB for testing

Some useful cmd for backup and restore DB:
---------------
backup command:
---------------
influxd backup
    [ -database <db_name> ]  --> database name to backup
    [ -portable ]            --> generates backup files in the newer InfluxDB Enterprise-compatible format.
    [ -host <host:port> ]    --> host and port (use default)
    [ -retention <rp_name> ] | [ -shard <shard_ID> -retention <rp_name> ]  --> backup retention policies
    [ -start <timestamp> [ -end <timestamp> ] | -since <timestamp> ]   --> start stop time for backup
    <path-to-backup>   --> backup path

example: 
1. influxd backup -portable /tmp/data  --> backup all databases
2. influxd backup -portable -database myDB /tmp/data  --> backup only myDB
3. influxd backup -portable -database myDB -start 2019-11-28T2:31:57Z -end 2019-11-28T2:32:59Z  /tmp/data -->back myDB in between times

---------------
restore command:
---------------
influxd restore 
    [ -db <db_name> ]       --> backup database name
    -portable | -online
    [ -host <host:port> ]    --> influxdb host and port
    [ -newdb <newdb_name> ]  --> new database name to restore
    [ -rp <rp_name> ]        --> backup retention policies
    [ -newrp <newrp_name> ]  --> restore retention policies
    [ -shard <shard_ID> ]
    <path-to-backup-files>   -->backup file path

example:
influxd restore -portable -db myDB -newdb myDB_2 /tmp/data  -->restore to an unexisted database.
