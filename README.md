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

