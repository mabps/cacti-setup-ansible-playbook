# cacti-setup-ansible-playbook
Some Ansible Playbooks for automate setup procedure Cacti monitoring server

> [!TIP]
> to setup right time zone, in databse - for correct logs date-time  
> mysql_tzinfo_to_sql /usr/share/zoneinfo/ | mysql -u root -p mysql

Add new config file in /etc/mysql/mysql.d/example.cnf  
contenet file:  
`[mysqld]  
default-time-zone = "+03:00"  
  
collation_server = utf8mb4_unicode_ci  
max_heap_table_size = 128M  
tmp_table_size = 128M  
innodb_buffer_pool_size = 1500M  
innodb_doublewrite = OFF`  


Right RSylog config file (for insert data in to MySQL database)   
Befor running RSyslog demon - check avalible library in /usr/lib/x86_64-linux-gnu/rsyslog/ommysql.so  
```
module(load="imudp")
module(load="ommysql")
#input(type="imudp" port="514")
input(type="imudp" port="514" ruleset="network-udp")

$template cacti_syslog,"INSERT INTO syslog_incoming(facility_id, priority_id, program, logtime, host, message) \
values (%syslogfacility%, %syslogpriority%, '%programname%', '%timegenerated:::date-mysql%',  '%HOSTNAME%', TRIM('%msg%'));", SQL

ruleset (name="network-udp")
{
  *.* action(type="ommysql" server="localhost" serverport="3306" db="cacti" uid="cacti" pwd="cactipassword" action.errorfile="/var/log/syslog-error" template="cacti_syslog")
}
```

