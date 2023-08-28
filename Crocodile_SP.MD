TASK 1

What Nmap scanning switch employs the use of default scripts during a scan?


    -sC: Performs a script scan using the default set of scripts. It is equivalent to --
    script=default. Some of the scripts in this category are considered intrusive and
    should not be run against a target network without permission.
    -sV: Enables version detection, which will detect what versions are running on what
    port.

### Answer: -sC

TASK 2

What service version is found to be running on port 21?

    Run Command
        sudo nmap -sC -sV 



### Answer: vsftpd 3.0.3

TASK 3

What FTP code is returned to us for the "Anonymous FTP login allowed" message?


### Answer: 230

TASK 4

After connecting to the FTP server using the ftp client, what username do we provide when prompted to log in anonymously?


    We will use dir and get to list the directories and manipulate the files stored on the FTP server. With the
    dir command, we can check the contents of our current directory on the remote host, where two
    interesting files catch out attention. They seem to be files left over from the configuration of another service
    on the host, most likely the HTTPD Web Server. Their names are descriptive, hinting towards a possible
    username list and associated passwords.


    Command
        ftp (Ip Address)


### Answer: anonymous

TASK 5

After connecting to the FTP server anonymously, what command can we use to download the files we find on the FTP server?

    Command:
    ftp > dir
    ftp > get


### Answer: get

TASK 6

What is one of the higher-privilege sounding usernames in 'allowed.userlist' that we download from the FTP server?

    Command: 
    ftp > exit
    ls in directory you are in
    cat password files

### Answer: admin

TASK 7

What version of Apache HTTP Server is running on the target host?

*Refer to nmap scan from earlier*

### Answer: Apache httpd 2.4.41

TASK 8

What switch can we use with Gobuster to specify we are looking for specific filetypes?

    dir : Uses directory/file enumeration mode.
    --url : The target URL.
    --wordlist : Path to the wordlist.
    -x : File extension(s) to search for.
    For the -x switch, we can specify php and html to filter out all the unnecessary clutter that does not
    interest us. PHP and HTML files will most commonly be pages. We might get lucky and find an
    administrative panel login page that could help us find leverage against the target in combination with the
    credentials we extracted from the FTP server.

### Answer: -x


TASK 9

Which PHP file can we identify with directory brute force that will provide the opportunity to authenticate to the web service?

    Command:
    gobuster dir --url http://targetip/ --wordlist /usr/share/wordlist.dirbuster/directory-list-2.3-small.txt -x php,html

    cat allowed.userlist
    cat allowed.userlist.passwd 

    Go to browswer type http://(IP Address)/login.php

    Admin
    Passord: rKXM59ESxesUFHAd


### Answer: Login.php

SUBMIT FLAG

### Answer: c7110277ac44d78b6a9fff2232434d16

Submit root flag