## Database MySQL

### Administration

#### User

* create new user  
  create user 'newuser'@'localhost' identified by 'master';

  GRANT ALL PRIVILEGES ON \* . \* TO 'newuser'@'localhost';

#### Backup, Import, Dump

* import sql-script  
  mysql -u username -p -h localhost DATA-BASE-NAME &lt; data.sql

  * import with encoding set  
    mysql -u root --default\_character\_set utf8 --database=&lt;database&gt; &lt; ~/&lt;script&gt;.sq

  * mysqlimport -h suchedb03 -u flight -p'CZp24XaqaDaUXsy4' --fields-terminated-by=';' --fields-optionally-enclosed-by='"' --ignore-lines=1 --verbose flight ~/&lt;file&gt;

* dump
  * dump several tables
    mysqldump -h suchedb01 -u quality\_data -p'inkS47GArtH2' quality\_data pq\_parts pq\_parts\_results pq\_tuples pq\_tuples\_results &gt; quality\_data\_prequra.sql
* only sava the data  
  mysqldump -u root qualityrating newsrater\_context newsrater\_ratingblock newsrater\_question --complete-insert --no-create-info --skip-extended-insert=false &gt; ~/Dokumente/backups/qualityrating\_newsrater\_t1.sql

* 


