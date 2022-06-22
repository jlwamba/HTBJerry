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


#Nmap

I ran the command ```Nmap -sC -sV -T4  -Pn <IP Address> -oN <outputfile>```

```sC``` is for default scripts scan.
```sV``` is for version of the services runnimg.
```T4``` is the speed of the scan. not that, this method is crucial because you don't want to make to much noise in the network traffic so declaring a speed of four the best you need for a fast scan.
```oN``` is redirect that fouding into a file. This you would nao

![scan](https://user-images.githubusercontent.com/61636217/173915915-977a8bd6-0ef2-4280-8b91-0ac00db0a277.png)

#Gobuster

After we have ran the ```Nmap``` command we have discovered that there is 2 open ports on our target machine.

```22``` & ``8080``. We noticed that a Tomcat is running on that machine.
Before going deep in the attack we must first try enumerate some port on port 8080 to find out what directory are hosted in the application adn for that I ran ```Gobuster``` for directory discovery.

``` gobuster dir --url  http://<ip> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100```
we discover an interesting directory ```Manager```.
From this step there are differents way you can plan your attack. Here We are going to exploit a misconfigure Tomcat Server.
by default All Tomcat creds are ```tomcat``` & ```s3cret```. but there are other ways to get creds.Navitgating to that Manager directory on port 8080 we prompted with sign in option. to get creds the easy way is the hit the ```cancel``` button and you will redirected to an error that display the credentials in plain text. Or you can use ``Metasploit`` to run an exploit against Tomcat server to get the credentials.



![8080](https://user-images.githubusercontent.com/61636217/175167658-cc992ea4-6978-43ab-ad94-e186c93ab26d.png)

![signin](https://user-images.githubusercontent.com/61636217/175167703-d26fcaa2-e862-45e8-ae76-ed85f98c9fda.png)


![creds](https://user-images.githubusercontent.com/61636217/175167731-af77b831-5f62-4c9a-b87a-d3bd4ad4ba48.png)

![manager](https://user-images.githubusercontent.com/61636217/175167776-b4adf04a-afc3-4998-b984-2b408783d7aa.png)

