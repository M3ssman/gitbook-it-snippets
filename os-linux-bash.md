## OS Linux Bash

* find
  * folders with pattern `find / -path "*.git"`
  * files with pattern `find / -name "http.conf" -type f` 
  * `find . -name '*.js.map' -delete` 
  * find + delete with pattern or size
    * `find ${BUILD_ROOT}/controllers -name "*.js.map" -exec rm -v {} +` 
    * `find . -size +2M -exec rm {} +`  
  * direct subfolders `find <folder> -mindepth 1 -maxdepth 1 -type d | wc -l`  
* count space on devices
  * du -sh &lt;folder&gt;
  * df -ha  \# h - human readable, a - also hidden and dummy partitions
  * df -hT /home \# aggregate kb, mb ...
  * ls -lhS \# aggregate kb, mb ...
  * ls -l --block-size=MB \# block size set to MiB \(2^20 bytes\) \| might use also M \(10^6 bytes\)
  * ls -l --block-size=1MB \# omit displayed unit since it all the same

* list
  * 5 most recent modified files:
    `ls -t --full-time /var/log | head -5   
     ls -t --full-time /var/log/nodejs | head -5 `

  * 

* process lists
  * how many memory is used? 
    `ps aux --sort -rss` 



