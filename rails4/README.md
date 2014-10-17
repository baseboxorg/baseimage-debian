# about minimum2scp/rails4 image

 * based on minimum2scp/ruby (see https://github.com/minimum2scp/dockerfiles/tree/master/ruby)
 * Ruby on Rails 4.x (debian package) is installed
 * RDBMS client, headers packages are installed
   * SQLite3: sqlite3, libsqlite3-dev
   * MySQL: mysql-client, libmysqlclient-dev
   * PostgreSQL: postgresql-client, libpq-dev

## start container

```
docker run -d  minimum2scp/rails4
```

## ssh login to container

ssh login to container:

```
ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no debian@<container IP address>
```

or use published port:

```
ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no -p <published ssh port> debian@localhost
```

 * user "debian" is available
 * password is "debian"
 * user "debian" can use sudo command without password
 * `id debian`: `uid=2000(debian) gid=2000(debian) groups=2000(debian),4(adm),27(sudo)`

## processes

```
UID        PID  PPID  C STIME TTY      STAT   TIME CMD
root         1     0  0 03:42 ?        Ss     0:00 init [2]
root        37     1  0 03:42 ?        Ssl    0:00 /usr/sbin/rsyslogd
root        62     1  0 03:42 ?        Ss     0:00 /usr/sbin/cron
root        88     1  0 03:42 ?        Ss     0:00 /usr/sbin/sshd
root       124    88  0 03:42 ?        Ss     0:00  \_ sshd: debian [priv]
debian     126   124  0 03:42 ?        S      0:00      \_ sshd: debian@pts/0
debian     127   126  0 03:42 pts/0    Ss     0:00          \_ -bash
debian     178   127  0 03:42 pts/0    R+     0:00              \_ ps -ef fww
```

## ports

| port         | process                 | comment                                       |
|:-------------|:------------------      |:------------------------------------------    |
| TCP/22       | sshd                    | invoked by init                               |
| TCP/80       | nginx                   | disabled autostart                            |
| TCP/9001     | supervisord             | disabeld autostart                            |
