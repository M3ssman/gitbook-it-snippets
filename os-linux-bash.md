## OS Linux Bash

### Systeminfo

* Infos about Distribution
  lsb\_release -ic  
  cat /etc/\*-release
* how many memory is used
  `ps aux --sort -rss` 
* packages and sources

  ```
  # Docker
  apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
  vim /etc/apt/sources.list.d/docker.list # sources.list update

  echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" >> /etc/apt/sources.list.d/docker.list

  apt-get update # update before request cached policies or installs

  # nodeJS
  /etc/apt/sources.list.d/nodesource.list

  deb https://deb.nodesource.com/node_8.x xenial main
  deb-src https://deb.nodesource.com/node_8.x xenial main

  # mongodb
  /etc/apt/sources.list.d/mongodb-org-3.4.list
  deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse
  ```

### Bash Utils

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

  * file sizes in given folders

  * ls -lhS \# aggregate kb, mb ...

  * ls -l --block-size=MB \# block size set to MiB \(2^20 bytes\) \| might use also M \(10^6 bytes\)

  * ls -l --block-size=1MB \# omit displayed unit since it all the same

* list

  * 5 most recent modified files:  
    \`ls -t --full-time /var/log \| head -5

    ls -t --full-time /var/log/nodejs \| head -5 \`

* ln  
  ln -s &lt;target&gt; &lt;name&gt; \# create symbolic link  
  ln -sfn &lt;target&gt; &lt;existing name&gt; \# update

* mount  
  mount from host as shared VM volume  
  mount -t vboxsf Z\_DRIVE /share/azure/gitlab-data/

* cp  
  cp &lt;src&gt; &lt;dest&gt; -a \# also copy links

* curl

  * redirects  
    curl -&lt;follow redirs&gt; -&lt;name-like-remote&gt; &lt;url&gt;  
    curl -L -O [http://download.sonatype.com/nexus/3/latest-unix.tar.gz](http://download.sonatype.com/nexus/3/latest-unix.tar.gz)

  * scp  
    scp src.file user@host:/folder/dest.file \# local =&gt; remote  
    scp user@host:/folder/src.file dest.file \# remote =&gt; local

* mecache  
  echo "stats cachedump 15 4 " \| nc 127.0.0.1 11211

* ip  
  id show addr

* netstat  
  netstat -tulpn \# network usage of processes

* pwgen - Password Generation  
  pswgen -b1s 16 \# create psw with 16 chars + special chars - ambiguous ones like "l/1" and "O/0"  
  pwgen --symbols --ambiguous 16 1

* tar  
  tar -cf &lt;file&gt; &lt;folder&gt;

### Usermanagement

```
adduser <user>
id -u USERNAME # uid
id -g USERNAME # gid

usermod -aG sudo <migration-lead> ## add user to sudo group
```

### Communication via SSH

* Authentication

  ```
  PASS="0BcBx/fn:SKm4g.=xj|Y"
  HOST="as17033001.germanynortheast.cloudapp.microsoftazure.de"
  ssh-keyscan ${HOST} > ~/.ssh/known_hosts
  ssh-copy-id teleportadmin@${HOST} <<< ${PASS}
  ```

* remove outdated know\_hosts entry  
  ssh-keygen -f "/var/jenkins\_home/.ssh/known\_hosts" -R 89.187.203.228

* execute local script on remote host  
  ssh root@MachineB '/bin/bash -s' &lt; local\_script.sh

### Firewall - iptables

* Read
  iptables -L \# list chains
  ```
  >>> sample output
  root@as16090101:~# iptables -L -n --line-numbers
  Chain INPUT (policy DROP)
  num  target     prot opt source               destination
  1    ACCEPT     all  --  127.0.0.0/8          127.0.0.0/8          /* lokale Kommunikation */
  2    ACCEPT     udp  --  0.0.0.0/0            0.0.0.0/0            udp dpt:68
  3    SSH        tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:22 /* SSH Chain */
  4    DOCKER     tcp  --  217.16.162.100       0.0.0.0/0            tcp dpt:80 /* Forward port 80 from teleport to DOCKER */
  5    DOCKER     tcp  --  192.168.125.0/24     0.0.0.0/0            tcp dpt:80 /* Forward port 80 from teleport to DOCKER */
  6    DOCKER     tcp  --  192.168.125.0/24     0.0.0.0/0            tcp dpt:2222
  7    DOCKER     tcp  --  192.168.125.0/24     0.0.0.0/0            tcp dpt:443
  8    HTTPS      tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:443 /* HTTPS Chain */
  9    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp spt:80 dpts:1024:65535 state ESTABLISHED /* HTTP Antwortpakete */
  10   ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp spt:443 dpts:1024:65535 state ESTABLISHED /* HTTPS Antwortpakete */
  11   ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp spts:1024:65535 dpts:1024:65535 state ESTABLISHED /* allg. Antwortpakete */
  12   ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp spts:1024:65535 dpt:53 state ESTABLISHED /* DNS Antwortpakete */
  13   ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp spt:53 dpts:1024:65535 state ESTABLISHED /* DNS Antwortpakete */
  14   ACCEPT     udp  --  0.0.0.0/0            0.0.0.0/0            udp spts:1024:65535 dpt:53 state ESTABLISHED /* DNS Antwortpakete */
  15   ACCEPT     udp  --  0.0.0.0/0            0.0.0.0/0            udp spt:53 dpts:1024:65535 state ESTABLISHED /* DNS Antwortpakete */
  16   ACCEPT     udp  --  0.0.0.0/0            0.0.0.0/0            udp dpt:123 state ESTABLISHED /* NTP Antwortpakete */
  17   ACCEPT     tcp  --  40.68.176.28         0.0.0.0/0            tcp dpt:445
  18   ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp spt:445 dpts:1024:65535 state ESTABLISHED /* SMB Antwortpakete */
  Chain FORWARD (policy ACCEPT)
  num  target     prot opt source               destination
  1    DOCKER-ISOLATION  all  --  0.0.0.0/0            0.0.0.0/0
  2    DOCKER     all  --  0.0.0.0/0            0.0.0.0/0
  3    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0            ctstate RELATED,ESTABLISHED
  4    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0
  5    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0
  Chain OUTPUT (policy ACCEPT)
  num  target     prot opt source               destination
  Chain DOCKER (5 references)
  num  target     prot opt source               destination
  1    ACCEPT     tcp  --  0.0.0.0/0            172.17.0.3           tcp dpt:80
  Chain DOCKER-ISOLATION (1 references)
  num  target     prot opt source               destination
  1    RETURN     all  --  0.0.0.0/0            0.0.0.0/0
  Chain HTTPS (1 references)
  num  target     prot opt source               destination
  1    ACCEPT     all  --  217.16.162.100       0.0.0.0/0            /* HTTPS TELEPORT HAL LAN */
  2    ACCEPT     all  --  192.168.125.0/24     0.0.0.0/0            /* HTTPS TELEPORT HAL LAN */
  3    DROP       all  --  0.0.0.0/0            0.0.0.0/0            /* drop WORLD */
  Chain SSH (1 references)
  num  target     prot opt source               destination
  1    ACCEPT     all  --  217.16.162.100       0.0.0.0/0            /* SSH TELEPORT HAL LAN */
  2    ACCEPT     all  --  192.168.125.0/24     0.0.0.0/0            /* SSH TELEPORT HAL LAN */
  3    DROP       all  --  0.0.0.0/0            0.0.0.0/0            /* drop WORLD */
  ```

* read with number of rules
  iptables -L -n --line-numbers

* add entry
  * append to end  
    iptables -A &lt;chain&gt; -p &lt;protocol&gt; -i &lt;eth-nic&gt; -j &lt;target-action&gt; --dport &lt;port&gt; -s &lt;source-ip&gt;  
    iptables -A INPUT -j ACCEPT -p tcp -i eth0 --dport 22

  * at pos n \(default is 1\)  
    iptables -I &lt;chain&gt; &lt;n&gt; -j &lt;target&gt; -p &lt;protocol&gt; -i &lt;nic&gt; -s &lt;source-ips&gt;  
    iptables -I HTTPS \[1\] -j ACCEPT -p tcp -i eth0 --dport 80 -s 192.168.125.67  
    iptables -I INPUT 4 -j DOCKER -p tcp -i eth0 --dport 80 -s 192.168.125.0/24
* add rules   
  iptables -I INPUT 9 -j HTTPS -p tcp -i eth0 --dport 9091 -m comment --comment "HTTPS CHAIN" \(docker registry\)   
  iptables -I INPUT 10 -j HTTPS -p tcp -i eth0 --dport 9092 -m comment --comment "HTTPS CHAIN NPM Registry" \(npm registry\)

* add with comment \(-m comment --comment "limit ssh access"\)  
  iptables -I TELEPORT-DOCKER 1 -j ACCEPT -p tcp -s 217.16.162.100 -i eth0 --dport 2222 -m comment --comment "SSH2 TELEPORT HAL LAN"  
  iptables -I TELEPORT-DOCKER 1 -j ACCEPT -p tcp -s 192.168.125.0/24 -i eth0 --dport 2222 -m comment --comment "SSH2 TELEPORT HAL LAN"  
  iptables -I INPUT 4 -j TELEPORT -p tcp -i eth0 --sport 80 -m comment --comment "forward port 80"  
  iptables -I INPUT 5 -j TELEPORT -p tcp -i eth0 --sport 8080 -m comment --comment "forward port 8080"  
  iptables -I INPUT 6 -j TELEPORT -p tcp -i eth0 --sport 443 -m comment --comment "forward port 443"  
  iptables -I INPUT 7 -j TELEPORT -p tcp -i eth0 --sport 2222 -m comment --comment "forward port 2222"

* delete entry  
  iuptable -D &lt;chain&gt; &lt;n&gt;



### Troubleshooting

* when something has been installed  
  grep install /var/log/dpkg.log  
  zcat /var/log/apt/history.log.\*.gz \| cat - /var/log/apt/history.log \| grep -Po '^Commandline:\(?= apt-get\)\(?=.\* install \) \K.\*'  
  cat /var/log/apt/history.log \# last modified log file

* SSH not authorized  
  check ~/.ssh/authorized\_keys on target machine



