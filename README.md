check_systemd_service
=====================
A Nagios plugin which queries systemd for service state and shows some nice output

Major Features
--------------

* Checks Service State
* Outputs log data

TODO
====
* Argument handling using PluginHelper.add_option
* Configurations and testing under nrpe

Examples
========

Crashed service
---------------

```
$ ./check_systemd_service postgresql
Critical - postgresql.service - failed (Result: exit-code) since Wed 2013-12-18 23:41:53 GMT; 28min ago

postgresql.service - PostgreSQL database server
   Loaded: loaded (/usr/lib/systemd/system/postgresql.service; disabled)
   Active: failed (Result: exit-code) since Wed 2013-12-18 23:41:53 GMT; 28min ago
  Process: 22791 ExecStop=/usr/bin/pg_ctl stop -D ${PGDATA} -s -m fast (code=exited, status=1/FAILURE)
  Process: 22709 ExecStart=/usr/bin/pg_ctl start -D ${PGDATA} -s -o -p ${PGPORT} -w -t 300 (code=exited, status=0/SUCCESS)
  Process: 22702 ExecStartPre=/usr/bin/postgresql-check-db-dir ${PGDATA} (code=exited, status=0/SUCCESS)
 Main PID: 22714 (code=killed, signal=KILL)
   CGroup: name=systemd:/system/postgresql.service

Dec 18 23:41:26 tandoori systemd[1]: Started PostgreSQL database server.
Dec 18 23:41:53 tandoori systemd[1]: postgresql.service: main process exited, code=killed, status=9/KILL
Dec 18 23:41:53 tandoori systemd[1]: postgresql.service: control process exited, code=exited status=1
Dec 18 23:41:53 tandoori systemd[1]: Unit postgresql.service entered failed state.
```

Inactive service
----------------

```
$ ./check_systemd_service httpd
Critical - httpd.service - inactive (dead)

httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled)
   Active: inactive (dead)

Nov 19 16:07:33 tandoori systemd[1]: Starting The Apache HTTP Server...
Nov 19 16:07:35 tandoori systemd[1]: Started The Apache HTTP Server.
Nov 19 16:44:26 tandoori systemd[1]: Stopping The Apache HTTP Server...
Nov 20 15:03:46 tandoori systemd[1]: Starting The Apache HTTP Server...
Nov 20 15:03:48 tandoori systemd[1]: Started The Apache HTTP Server.
Nov 21 08:32:51 tandoori systemd[1]: Stopping The Apache HTTP Server...
Nov 21 08:33:16 tandoori systemd[1]: Stopped The Apache HTTP Server.
Dec 04 18:15:45 tandoori systemd[1]: Starting The Apache HTTP Server...
Dec 04 18:15:48 tandoori systemd[1]: Started The Apache HTTP Server.
Dec 04 18:35:21 tandoori systemd[1]: Stopped The Apache HTTP Server.
```

Running service
---------------

```
$ ./check_systemd_service sendmail
OK - sendmail.service - active (running) since Wed 2013-12-18 23:51:06 GMT; 19min ago

sendmail.service - Sendmail Mail Transport Agent
   Loaded: loaded (/usr/lib/systemd/system/sendmail.service; enabled)
   Active: active (running) since Wed 2013-12-18 23:51:06 GMT; 19min ago
  Process: 23864 ExecStart=/usr/sbin/sendmail -bd $SENDMAIL_OPTS $SENDMAIL_OPTARG (code=exited, status=0/SUCCESS)
  Process: 23859 ExecStartPre=/etc/mail/make aliases (code=exited, status=0/SUCCESS)
  Process: 23857 ExecStartPre=/etc/mail/make (code=exited, status=0/SUCCESS)
 Main PID: 24027 (sendmail)
   CGroup: name=systemd:/system/sendmail.service
           └─24027 sendmail: accepting connection

Dec 18 23:50:05 tandoori sendmail[23864]: My unqualified host name (tandoori) unknown; sleeping for retry
Dec 18 23:51:05 tandoori sendmail[23864]: unable to qualify my own domain name (tandoori) -- using short name
Dec 18 23:51:05 tandoori sendmail[24027]: starting daemon (8.14.7): SMTP+queueing@01:00:00
Dec 18 23:51:05 tandoori systemd[1]: PID file /run/sendmail.pid not readable (yet?) after start.
Dec 18 23:51:06 tandoori systemd[1]: Started Sendmail Mail Transport Agent.
```



License
=======
GPLv3+


Author
======
Tomas Edwardsson <tommi@tommi.org>

