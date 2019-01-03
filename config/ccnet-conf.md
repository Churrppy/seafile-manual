# ccnet.conf

**Note**: Since Seafile Server 5.0.0, all config files are moved to the central **conf** folder. [Read More](../deploy/new_directory_layout_5_0_0.md).

Ccnet is the internal RPC framework used by Seafile server and also manages the user database. A few useful options are in ccnet.conf.

```
[General]

# Used internally. Don't delete.
ID=eb812fd276432eff33bcdde7506f896eb4769da0

# Used internally. Don't delete.
NAME=example

# This is outside URL for Seahub(Seafile Web). 
# The domain part (i.e., www.example.com) will be used in generating share links and download/upload file via web.
# Note: Outside URL means "if you use Nginx, it should be the Nginx's address"
SERVICE_URL=http://www.example.com:8000


[Network]
# Not used anymore
PORT=10001

[Client]
# Not used anymore
PORT=13419

```

## Enabled Slow Log

Since Seafile-pro-6.3.10, you can to enabled the ccnet-server's RPC slow request query log, so that you can do performance analysis.

Add the options to ccnet.conf:

```
[Slow_log]
# Set to true
ENABLE_SLOW_LOG = true
# the unit of all slow log thresholds is millisecond.
# default to 5000 milliseconds, only RPC queries processed for longer than 5000 milliseconds will be  logged.
RPC_SLOW_THRESHOLD = 5000
```

Restarted the seafile service, and you can find the `ccnet_slow_rpc.log` in the `logs/slow_logs`. And you can also use the log-rotate to cutting the log file. Just send the `SIGUSR2` to the ccnet-server progress, the log file will be closed and reopened.

**Note**: You should restart seafile so that your changes take effect.

```
cd seafile-server
./seafile.sh restart
```

## Changing MySQL Connection Pool Size

When you configure ccnet to use MySQL, the default connection pool size is 100, which should be enough for most use cases. You can change this value by adding following options to ccnet.conf:

```
[Database]
......
# Use larger connection pool
MAX_CONNECTIONS = 200
```

## Changing name of table 'Group'

There is a table named 'Group' in ccnet database, however, 'Group' is the key word in some of databases, you can configure this table name to avoid conflicts if necessary:
```
[GROUP]
TABLE_NAME=new_group_name
```

