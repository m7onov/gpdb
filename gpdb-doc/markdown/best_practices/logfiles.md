# Monitoring Greenplum Database Log Files 

Know the location and content of system log files and monitor them on a regular basis and not just when problems arise.

The following table shows the locations of the various Greenplum Database log files. In file paths:

-   `$GPADMIN_HOME` refers to the home directory of the `gpadmin` operating system user.
-   `$MASTER_DATA_DIRECTORY` refers to the master data directory on the Greenplum Database master host.
-   `$GPDATA_DIR` refers to a data directory on the Greenplum Database segment host.
-   `host` identifies the Greenplum Database segment host name.
-   `segprefix` identifies the segment prefix.
-   `N` identifies the segment instance number.
-   `date` is a date in the format `YYYYMMDD`.



|Path|Description|
|----|-----------|
|`$GPADMIN_HOME/gpAdminLogs/*`|Many different types of log files, directory on each server. `$GPADMIN_HOME` is the default location for the `gpAdminLogs/` directory. You can specify a different location when you run an administrative utility command.|
|`$GPADMIN_HOME/gpAdminLogs/gpinitsystem_date.log`|system initialization log|
|`$GPADMIN_HOME/gpAdminLogs/gpstart_date.log`|start log|
|`$GPADMIN_HOME/gpAdminLogs/gpstop_date.log`|stop log|
|`$GPADMIN_HOME/gpAdminLogs/gpsegstart.py_host:gpadmin_date.log`|segment host start log|
|`$GPADMIN_HOME/gpAdminLogs/gpsegstop.py_host:gpadmin_date.log`|segment host stop log|
|`$MASTER_DATA_DIRECTORY/pg_log/startup.log`, `$GPDATA_DIR/segprefixN/pg_log/startup.log`|segment instance start log|
|`$MASTER_DATA_DIRECTORY/gpperfmon/logs/gpmon.*.log`|gpperfmon logs|
|`$MASTER_DATA_DIRECTORY/pg_log/*.csv`, `$GPDATA_DIR/segprefixN/pg_log/*.csv`|master and segment database logs|
|`$GPDATA_DIR/mirror/segprefixN/pg_log/*.csv`|mirror segment database logs|
|`$GPDATA_DIR/primary/segprefixN/pg_log/*.csv`|primary segment database logs|
|`/var/log/messages`|Global Linux system messages|

Use `gplogfilter -t` \(`--trouble`\) first to search the master log for messages beginning with `ERROR:`, `FATAL:`, or `PANIC:`. Messages beginning with `WARNING` may also provide useful information.

To search log files on the segment hosts, use the Greenplum `gplogfilter` utility with `gpssh` to connect to segment hosts from the master host. You can identify corresponding log entries in segment logs by the `statement_id`.

The `log_rotation_age` configuration parameter specifies when a new log file is automatically created while a database instance is running. By default, a new log file is created every day.

**Parent topic:** [System Monitoring and Maintenance](maintenance.html)
