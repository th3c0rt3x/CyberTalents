
**[Remember Me](https://cybertalents.com/challenges/forensics/remember-me)**
===================  
[Challenge Link](https://hubchallenges.s3-eu-west-1.amazonaws.com/Forensics/remember.zip)

> After acquiring memory from attacker pc we found there is no internet browser except internet explorer . Can you get internet history? 

From the descritpion we have to extract the IE history information from the vmem file, so we use volatility framework along with couple of decoing tools (mostly CyberChef)

 | Tool | Version | Description |
| --- | --- | --- |
| `vol.py` | [2.5](https://www.volatilityfoundation.org/25) | Volatility memory forensics framework |
| `CyberChef` | [9.28.0](https://gchq.github.io/CyberChef/) | CyberChef - The Cyber Swiss Army Knife |

[Volatility Labs](https://volatility-labs.blogspot.com/2012/09/howto-scan-for-internet-cachehistory.html) has published a blog post to extract IE Cache Information, using couple of plug-in like iehistory, yarascan with volatility framework.

## Lets start with gathering basic information about image and imageinfo
after we extract the zip file we have got file with .mem extension which it indicates that it was memory capture artifcat from attcker pc.
lets the image info and os profile using imageinfo plugiin

```
PS D:\CTF!\cybertalents\remember> volatility.exe -f .\remember.mem imageinfo
Volatility Foundation Volatility Framework 2.5
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP0x86, Win7SP1x86
                     AS Layer1 : IA32PagedMemory (Kernel AS)
                     AS Layer2 : FileAddressSpace (D:\CTF!\cybertalents\remember\remember.mem)
                      PAE type : No PAE
                           DTB : 0x185000L
                          KDBG : 0x82949c28L
          Number of Processors : 1
     Image Type (Service Pack) : 1
                KPCR for CPU 0 : 0x8294ac00L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2020-01-20 16:40:00 UTC+0000
     Image local date and time : 2020-01-20 18:40:00 +0200
```
Which imageinfo plugin provided couple of profiles about the host os : we will be selecting Win7SP1x86 profile to get the desired result.

we will try to the run the iehistory plugin to get more information about the IE history

### volatility.exe -f .\remember.mem --profile=Win7SP1x86 iehistory
and piping above command to some txt file to save the outof the iehistory plugin, which given the below input
```
TRIM
**************************************************
Process: 1424 explorer.exe
Cache type "URL " at 0x1d85880
Record length: 0x180
Location: Visited: John the ripper@http://www.bing.com/search?format=rss&q=ZmxhZ3tLZWVwX3VzaW5nX3ZvbGF0aWxpdHl9&qs=ds&form=QBRE
Last modified: 2020-01-20 16:39:29 UTC+0000
Last accessed: 2020-01-20 16:39:29 UTC+0000
File Offset: 0x180, Data Offset: 0x0, Data Length: 0xe0
**************************************************
Process: 1424 explorer.exe
Cache type "URL " at 0x1d85a00
Record length: 0x180
Location: Visited: John the ripper@http://www.bing.com/search?q=bing&src=IE-SearchBox&FORM=IE8SRC
Last modified: 2020-01-20 16:39:40 UTC+0000
Last accessed: 2020-01-20 16:39:40 UTC+0000
File Offset: 0x180, Data Offset: 0x0, Data Length: 0xc0
**************************************************
Process: 1424 explorer.exe
Cache type "URL " at 0x1d85b80
Record length: 0x200
Location: Visited: John the ripper@https://www.google.com/search?q=ZmxhZ3tLZWVwX3VzaW5nX3ZvbGF0aWxpdHl9&hl=ar&gbv=1&source=lnms&tbm=vid&sa=X&ved=0ahUKEwjo5-3uzpLnAhUhyIUKHci4BkUQ_AUIBSgB
Last modified: 2020-01-20 16:39:40 UTC+0000
Last accessed: 2020-01-20 16:39:40 UTC+0000
File Offset: 0x200, Data Offset: 0x0, Data Length: 0x11c
**************************************************

Process: 2120 FTK Imager.exe
Cache type "URL " at 0x3225880
Record length: 0x180
Location: Visited: John the ripper@http://www.bing.com/search?format=rss&q=ZmxhZ3tLZWVwX3VzaW5nX3ZvbGF0aWxpdHl9&qs=ds&form=QBRE
Last modified: 2020-01-20 16:39:29 UTC+0000
Last accessed: 2020-01-20 16:39:29 UTC+0000
File Offset: 0x180, Data Offset: 0x0, Data Length: 0xe0
**************************************************
Process: 2120 FTK Imager.exe
Cache type "URL " at 0x3225a00
Record length: 0x180
Location: Visited: John the ripper@http://www.bing.com/search?q=bing&src=IE-SearchBox&FORM=IE8SRC
Last modified: 2020-01-20 16:39:40 UTC+0000
Last accessed: 2020-01-20 16:39:40 UTC+0000
File Offset: 0x180, Data Offset: 0x0, Data Length: 0xc0
**************************************************
Process: 2120 FTK Imager.exe
Cache type "URL " at 0x3225b80
Record length: 0x200
Location: Visited: John the ripper@https://www.google.com/search?q=ZmxhZ3tLZWVwX3VzaW5nX3ZvbGF0aWxpdHl9&hl=ar&gbv=1&source=lnms&tbm=vid&sa=X&ved=0ahUKEwjo5-3uzpLnAhUhyIUKHci4BkUQ_AUIBSgB
Last modified: 2020-01-20 16:39:40 UTC+0000
Last accessed: 2020-01-20 16:39:40 UTC+0000
File Offset: 0x200, Data Offset: 0x0, Data Length: 0x11c
**************************************************
Process: 2120 FTK Imager.exe
Cache type "URL " at 0x3225d80
Record length: 0x200
Location: Visited: John the ripper@https://www.google.com/search?q=ZmxhZ3tLZWVwX3VzaW5nX3ZvbGF0aWxpdHl9&hl=ar&gbv=1&tbm=isch&source=lnms&sa=X&ved=0ahUKEwicxM7wzpLnAhUPyYUKHV8bByYQ_AUIBigC
Last modified: 2020-01-20 16:39:40 UTC+0000
Last accessed: 2020-01-20 16:39:40 UTC+0000
File Offset: 0x200, Data Offset: 0x0, Data Length: 0x11c
**************************************************
TRIM
```
if we observe the output of iehostry plugin we can find that nmost of history is related to John the Ripper Search, but if we observe throughly we got one history entry with bing looks something we need to look at

```
Process: 2120 FTK Imager.exe
Cache type "URL " at 0x3225880
Record length: 0x180
Location: Visited: John the ripper@http://www.bing.com/search?format=rss&q=ZmxhZ3tLZWVwX3VzaW5nX3ZvbGF0aWxpdHl9&qs=ds&form=QBRE
Last modified: 2020-01-20 16:39:29 UTC+0000
Last accessed: 2020-01-20 16:39:29 UTC+0000
File Offset: 0x180, Data Offset: 0x0, Data Length: 0xe0
```
let we open the URL directly into browser which is a RSS feed of bingSearch https://www.bing.com/search?format=rss&q=ZmxhZ3tLZWVwX3VzaW5nX3ZvbGF0aWxpdHl9&qs=ds&form=QBRE 

![](images/bingSearch.PNG)

Lets Use Cyberchef to extract the base64 Strnig from RSS Feed

https://gchq.github.io/CyberChef/#recipe=Magic(3,false,false,''/disabled)From_Base64('A-Za-z0-9%2B/%3D',false)&input=Wm14aFozdExaV1Z3WDNWemFXNW5YM1p2YkdGMGFXeHBkSGw5

### Flag : flag{Keep_using_volatility}
