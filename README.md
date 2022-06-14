# About me

Welcome all to my ``Offensive Security`` journey and first ever write up.
I have been active on ```HackTheBox``` and `Tryhackme` since December 2020.
However I have only been able to work on few  machines during the last two years while learning about ```Info-Sec``` fundamentals on ```TryHackMe``` and others few online platforms, also while I completed my degree.

Before we dive in the write up  for the first machine i Pwned that is```Jerry``` ,it's important to note that prior rooting the first machine on ```Hackthebox``` I have quasi zero experience ``Hacking``.

If you are new to ```Cyber Security```, there are many platforms out there that can help you get the knowledge .
As of now I am still learner and I believe in this industry ```Learning don't Stop```. I am currently going for my first certification that is the ```eJPT``` from ```Elearnsecurity```.

# Set UP

If you have trouble setting your home Lab to access hackthebox content, should you refer to youtube. There are tons  of videos that can help you set up your box.

# Jerry


```┌──(yasuke㉿kali)-[~/…/Writeups/HTB/Jerry/HTBJerry]```

```└─$ ping 10.10.10.95```            
```PING 10.10.10.95 (10.10.10.95) 56(84) bytes of data.```

```64 bytes from 10.10.10.95: icmp_seq=1 ttl=127 time=32.0 ms```

```64 bytes from 10.10.10.95: icmp_seq=2 ttl=127 time=31.7 ms```

```64 bytes from 10.10.10.95: icmp_seq=3 ttl=127 time=31.3 ms```

```--- 10.10.10.95 ping statistics ---```

```3 packets transmitted, 3 received, 0% packet loss, time 2002ms```
```rtt min/avg/max/mdev = 31.252/31.650/31.996/0.306 ms```

From the ping command we can identify that our target machine runs on ```Windows OS``` by looking at the ```TTL(Time to live)``` response. This a trick that I learned from some of the big names I watched sovling boxes on Youtube.
We have ping the machine and it echoed back to us.
Now we will proceed on scanning for open ports and enumerate all services running on our target machine.

To discover what services are currently running on the target machine, I used ```Nmap``` however there other tools that can give you the same output as ```nmap```.

I ran the command ```Nmap -sC -sV -T4  -Pn <IP Address> -oN <outputfile>

```sC``` is for default scripts scan.
```sV``` is for version of the services runnimg.
```T4``` is the speed of the scan. not that, this method is crucial because you don't want to make to much noise in the network traffic so the ```T4``` would do it for you.
```oN``` is redirect that fouding into a file. This you would nao


