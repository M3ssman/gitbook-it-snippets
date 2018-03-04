## Database MySQL

### Administration

#### User

* create new user
  create user 'newuser'@'localhost' identified by 'master';  
  GRANT ALL PRIVILEGES ON \* . \* TO 'newuser'@'localhost';



#### Backup, Import, Dump

* import sql-script
  mysql -u username -p -h localhost DATA-BASE-NAME &lt; data.sql

* 


