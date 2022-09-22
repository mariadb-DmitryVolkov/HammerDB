# HammerDB

HammerDB is the leading benchmarking and load testing software for the worlds most popular databases supporting Oracle Database, Microsoft SQL Server, IBM Db2, PostgreSQL, MySQL and MariaDB.

## Example TCL script for Xpand
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
