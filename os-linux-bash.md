## OS Linux Bash

### Systeminfo

* Infos about Distribution
  lsb\_release -ic  
  cat /etc/\*-release
* how many memory is used
  `ps aux --sort -rss` 
* packages and sources
  ```
  # GPG key addr
  apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
  vim /etc/apt/sources.list.d/docker.list # sources.list update

  echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" >> /etc/apt/sources.list.d/docker.list

  apt-get update # update before request cached policies or installs
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

### Troubleshooting

* when something has been installed
  grep install /var/log/dpkg.log
  zcat /var/log/apt/history.log.\*.gz \| cat - /var/log/apt/history.log \| grep -Po '^Commandline:\(?= apt-get\)\(?=.\* install \) \K.\*'  
  cat /var/log/apt/history.log \# last modified log file

* SSH not authorized
  check ~/.ssh/authorized\_keys on target machine



\# Packetquellen zufügen

\#\# GPG key addr

apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D

\#\# sources.list anpassen

// vim /etc/apt/sources.list.d/docker.list

echo "deb [https://apt.dockerproject.org/repo](https://apt.dockerproject.org/repo) ubuntu-xenial main" &gt;&gt; /etc/apt/sources.list.d/docker.list

\#\# update again before request cached policies or do some installs

apt-get update







