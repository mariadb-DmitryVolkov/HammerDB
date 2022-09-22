# HammerDB

HammerDB is the leading benchmarking and load testing software for the worlds most popular databases supporting Oracle Database, Microsoft SQL Server, IBM Db2, PostgreSQL, MySQL and MariaDB.

## About This fork

This fork contains HammerDB 4.5 with additional changes for running [MariaDB Xpand](https://mariadb.com/products/enterprise/xpand/). In addition `bin` and `lib` contains pre-build binaries for running it on RedHat 8/Rocky8 Linux only. It is recommend to use [Maxscale](https://mariadb.com/kb/en/maxscale/) in the front of Xpand cluster.

## Installing MariaDB client libraries

```shell
wget https://downloads.mariadb.com/MariaDB/mariadb_repo_setup
chmod +x mariadb_repo_setup
./mariadb_repo_setup --mariadb-server-version=mariadb-10.7
 --skip-maxscale --skip-tools
dnf install -y MariaDB-client MariaDB-shared
```

## Example TCL script for MariaDB Xpand

As MariaDB Xpand is MariaDB compatible we decided to leave all parameters names start with `maria`.

### Load Phase

```tcl
dbset db xpand
diset connection maria_host <host>
diset connection maria_port <port>
diset tpcc maria_user <user>
diset tpcc maria_pass <password>
diset tpcc maria_dbase <database>
diset tpcc maria_count_ware <warehouses>
diset tpcc maria_num_vu <virtual users>
print dict
buildschema
```

### Run Phase

```tcl
diset tpcc maria_allwarehouse true
tcset logtotemp 1
tcset timestamps 1
print dict
print tcconf
loadscript
vuset vu <virtual users>
vuset delay 10
vucreate
tcstart
vurun
tcstop
```

## Credits

- Steve Shaw
- [All Contributors](https://github.com/TPC-Council/HammerDB/contributors)

## License

GNU General Public License v3.0. Please see [License File](LICENSE) for more information.

## Support

- [Contact information](http://www.hammerdb.com)
- [Documentation](https://www.hammerdb.com/docs)
