# hammerdb-dbaas
HammerDB benchmark run for DBaaS PGSQL (MySQL also available)

## install

* Create Exoscale VM with Ubuntu (latest) as CPU Optimized Huge (If you want more/less CPUs adjust pg_count_ware, pg_num_vu and vuset vu to the number of cores available)
* apt install postgresql-16-client (Version might differ, you need libpq.so.
* Download HammerDB (https://www.hammerdb.com/download.html) Release for Linux 64-bit tar file.
* Untar and run hammerdbcli

## HammerDB settings

```
dbset db pg
dbset bm TPC-C
```

## change DB host

```
diset connection pg_host $HOST
diset connection pg_port 21699
diset tpcc pg_count_ware $NUMCPUOFCLIENT
diset tpcc pg_num_vu $NUMCPUOFCLIENT
diset tpcc pg_superuser avnadmin
diset tpcc pg_superuserpass $DBPASS
diset tpcc pg_defaultdbase defaultdb
diset tpcc pg_user avnadmin
diset tpcc pg_pass $DBPASS
diset tpcc pg_count_ware 16 (number of client cores)
diset tpcc pg_num_vu 16 (number of client cores)
```

## Settings example

```
Dictionary Settings for PostgreSQL
connection {
 pg_host    = $DBDNS
 pg_port    = 21699
 pg_sslmode = prefer
}
tpcc       {
 pg_count_ware       = 16
 pg_num_vu           = 16
 pg_superuser        = avnadmin
 pg_superuserpass    = $PWD
 pg_defaultdbase     = defaultdb
 pg_user             = avnadmin
 pg_pass             = $PWD
 pg_dbase            = tpcc
 pg_tspace           = pg_default
 pg_vacuum           = false
 pg_dritasnap        = false
 pg_oracompat        = false
 pg_cituscompat      = false
 pg_storedprocs      = false
 pg_partition        = false
 pg_total_iterations = 10000000
 pg_raiseerror       = false
 pg_keyandthink      = false
 pg_driver           = timed
 pg_rampup           = 2
 pg_duration         = 5
 pg_allwarehouse     = false
 pg_timeprofile      = false
 pg_async_scale      = false
 pg_async_client     = 10
 pg_async_verbose    = false
 pg_async_delay      = 1000
 pg_connect_pool     = false
}

print vuconf

hammerdb>print vuconf
Virtual Users = 16
User Delay(ms) = 500
Repeat Delay(ms) = 500
Iterations = 1
Show Output = 1
Log Output = 0
Unique Log Name = 0
No Log Buffer = 0
Log Timestamps = 0
```

## Execution

```
hammerdb>loadscript
hammerdb>vuset vu 16
hammerdb>vucreate
hammerdb>vurun
```
