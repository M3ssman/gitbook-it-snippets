## Database MySQL

### Administration

#### User

* create new user  
  create user 'newuser'@'localhost' identified by 'master';

  GRANT ALL PRIVILEGES ON \* . \* TO 'newuser'@'localhost';

#### Backup, Import, Dump

* import sql-script  
  mysql -u username -p -h localhost DATA-BASE-NAME &lt; data.sql

* only sava the data  
  mysqldump -u root qualityrating newsrater\_context newsrater\_ratingblock newsrater\_question --complete-insert --no-create-info --skip-extended-insert=false &gt; ~/Dokumente/backups/qualityrating\_newsrater\_t1.sql

* 


