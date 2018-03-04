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

  * file sizes in given folders

  * ls -lhS \# aggregate kb, mb ...

  * ls -l --block-size=MB \# block size set to MiB \(2^20 bytes\) \| might use also M \(10^6 bytes\)
  * ls -l --block-size=1MB \# omit displayed unit since it all the same

* list

  * 5 most recent modified files:  
    \`ls -t --full-time /var/log \| head -5

    ls -t --full-time /var/log/nodejs \| head -5 \`

  * 

* process lists

  * how many memory is used? 
    `ps aux --sort -rss` 

\# file sizes in a given folder

ls -lhS \# aggregate kb, mb ...

ls -l --block-size=MB \# block size set to MiB \(2^20 bytes\) \| might use also M \(10^6 bytes\)

ls -l --block-size=1MB \# omit displayed unit since it all the same

\#\#\# auf VM was als shared Vol mounten

mount -t vboxsf Z\_DRIVE /share/azure/gitlab-data/

\#\# NETZWERK

\#\#\# wget + redirect

wget

\#\#\# curl -&lt;follow redirs&gt; -&lt;name-like-remote&gt; &lt;url&gt;

curl -L -O [http://download.sonatype.com/nexus/3/latest-unix.tar.gz](http://download.sonatype.com/nexus/3/latest-unix.tar.gz)

\#\#\#

scp Quelldatei.bsp Benutzer@Host:Verzeichnis/Zieldatei.bsp

scp Benutzer@Host:Verzeichnis/Quelldatei.bsp Zieldatei.bsp

\#\# MEMCACHE

echo "stats cachedump 15 4 " \| nc 127.0.0.1 11211

\#\# SUCHE

\# suche ab root nach ordnern mit muster

find / -path "\*.git"

\#\#\# suche datei

find / -name "http.conf" -type f

find . -name '\*.js.map' -delete

\# wieviele direkte subfolder hat "jobs" ?

find jobs -mindepth 1 -maxdepth 1 -type d \| wc -l

\#\#\# filter suche + entfernen

find ${BUILD\_ROOT}/controllers -name "\*.js.map" -exec rm -v {} +

find . -size +2M -exec rm {} +

\# IP Adresse

ip addr show

// verwendung von ports durch prozesse

netstat -pltn

\# os name \(Bsp: PRETTY\_NAME="Debian GNU/Linux 7 \(wheezy\)"\)

cat /etc/\*-release

\# wann wurde was installiert

grep install /var/log/dpkg.log

\# als root user anlegen

adduser git2

\# copy lings

cp &lt;src&gt; &lt;dest&gt; -a

\# OS Infos

lsb\_release -ic

cat /etc/\*-release

\#\# Security

\#\#\# Neues Passwort

pswgen -b1s 16 &gt;&gt; 3C7tiYXsWFtcjiCw

\#\#\# create me on psw with 16 chars containg special chars but avoid ambiguous ones like "l/1" and "O/0"

pwgen --symbols --ambiguous 16 1

\#\#\# OpenSSL

ssh -v &gt;&gt;&gt; OpenSSH\_6.0p1 Debian-4+deb7u6, OpenSSL 1.0.1e 11 Feb 2013 \# s-eta

\#\#\# SSH Auth einrichten

PASS="0BcBx/fn:SKm4g.=xj\|Y"

HOST="as17033001.germanynortheast.cloudapp.microsoftazure.de"

ssh-keyscan ${HOST} &gt; ~/.ssh/known\_hosts

ssh-copy-id teleportadmin@${HOST} &lt;&lt;&lt; ${PASS}

\#\#\# veralteten known\_host eintrag entfernen

ssh-keygen -f "/var/jenkins\_home/.ssh/known\_hosts" -R 89.187.203.228

\# MANAGEMENT von PACKET\_QUELLEN

\# Packetquellen zufügen

\#\# GPG key addr

apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D

\#\# sources.list anpassen

// vim /etc/apt/sources.list.d/docker.list

echo "deb [https://apt.dockerproject.org/repo](https://apt.dockerproject.org/repo) ubuntu-xenial main" &gt;&gt; /etc/apt/sources.list.d/docker.list

\#\# update again before request cached policies or do some installs

apt-get update

\# USER MANAGEMENT

\#\# create one

adduser &lt;user&gt;

id -u USERNAME \# uid

id -g USERNAME \# gid

\#\# add to sudo group

usermod -aG sudo &lt;migration-lead&gt;

\# Verlinken

create

ln -s &lt;target&gt; &lt;name&gt;

update

ln -sfn &lt;target&gt; &lt;existing name&gt;

\# SECURE SHELL && SECURE COPY

\#\# script file lokal auf remote host ausführen

ssh root@MachineB '/bin/bash -s' &lt; local\_script.sh

\# welche Datei muss auf dem Target vorhanden sein ?

~/.ssh/authorized\_keys

\# ARCHIVIERUNG

tar -cf &lt;file&gt; &lt;folder&gt;

\# WINDOWS SUBSYSTEM 4 LINUX

\#\# Upgrade: [http://www.howtogeek.com/278152/how-to-update-the-windows-bash-shell/](http://www.howtogeek.com/278152/how-to-update-the-windows-bash-shell/)

\# MONITORING IN DER SHELL

// zeige die 5 aktuellsten dateien, die modfiziert wurden

ls -t --full-time /var/log \| head -5

ls -t --full-time /var/log/nodejs \| head -5

// was wurde denn so aktualisiert ?

zcat /var/log/apt/history.log.\*.gz \| cat - /var/log/apt/history.log \| grep -Po '^Commandline:\(?= apt-get\)\(?=.\* install \) \K.\*'

// bzw die letze log datei

cat /var/log/apt/history.log

// welcher prozess braucht wie viel memory ? \(sortiert\)

ps aux --sort -rss

