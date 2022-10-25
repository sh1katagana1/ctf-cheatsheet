# Enumeration Tips and Techniques
**Description**
A good attack usually starts with good recon. Here are some enumeration techniques to guide you
## NMAP
Nmap is usually the defacto first step in enumerating whats on a system. There are so many different switches and scripts that you can use, but I generally use this specific command set:
```
nmap -n -Pn -A <IP address>
```
-n is to disable DNS recursion. I do this to speed things up a little, as I already know the IP address usually for the CTF \
-Pn is to disable ping to see if an address is up. Normally, in a CTF you already know the machine is up, so this speed some things up by disabling this check \
-A is an Aggressive scan. Do note that this is extremely noisy and if stealth is your goal in a real life scenario, you likely would not use this. It combines 4 scan types into one. First it does a -sV scan (version scan) which tries to determine the exact version number of what is running on that port. It does a -O (OS scan) to try and determine the Operating System of the victim. It does a -sC which runs all the scripts from the Default category. These are generally safe to run, but always verify first. Lastly it does a Traceroute. So this Aggressive scan usually takes a while to run. \
Keep in mind that this command uses the default Top 1000 TCP ports, as I did not specify a port range to scan. If I wanted to scan all ports, I would use -p-. If I wanted to scan UDP ports, I would use -sU. \
There are a number of scripts in .nse format as well, and you would seek them out for specific use cases in your CTF, like scanning for a specific CVE

