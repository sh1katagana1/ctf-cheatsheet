# CTF Cheatsheet General

**Description:** A list of commands, techniques and tooling I use to perform CTFs

## Python stable shell
When an exploit only gives you an sh shell, this can sometimes be unstable and you would need to make it a BASH shell. To do that in Python:
```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

## MySql Usage
Sometimes you may find database credentials in a config file of the victim machine. If its MySql, you can use this command:
```
mysql -u victim-user -p
```
-u: specify a username \
-p: tell the command to prompt to enter the password \
This would then prompt you to put in the password. Once connected, it will give you a mysql prompt and there will likely be some instructions, like having to end commands with a semicolon. So to enumerate the databases:
```
show databases;
```
To make a database active, you put the use command followed by the name of the database:
```
use name-of-db;
```
This will put you in that database. To look at the tables:
```
show tables;
```
Lets say this command showed 4 tables, and one of them is called users, we first need to select it to view it:
```
SELECT * From users;
```
This should show the contents of that table, hopefully including the password.

## Bash History
If you enumerate a home directory of a user, its always good to look for the bash history file for that user. This file will contain a history of commands run by that user, if they havent removed them. An example would be the sudo command. The user would type sudo, then their password when prompted. So the history file would likely show this. This file is a hidden file so you would need to list the directry with the ls -la command. Then you can do:
```
cat .bash_history
```

## Switch User
If the victim machine is Linux, and you have broken in as a non-privleged account, like www-data, you would like to escalate to a more privileged user. Lets say you found an admin user leroy and captured his credentials. If your currently in a terminal as www-data user, to switch to the leroy account:
```
su leroy
```
You will be prompted for the password, and once entered, you should see a prompt indicating you are leroy.

## Sudo
A standard user may be allowed to run certain programs as root, if the privileged account has put that ability into the sudoers file. To check what potential sudo privileges a user may have:
```
sudo -l
```
This would list what programs, if any, the user can run as root. Sometimes this alone is sufficient to get privileged escalation, by running a script using a particular program as root.

## GTFOBins
https://gtfobins.github.io \
That site is handy to find privilege escalation techmiques. As an example, lets say you checked the victims sudo privileges and they can run the nano program as root. This page \
https://gtfobins.github.io/gtfobins/nano/ \
Tells you what command to run for this. In this case it is: \
sudo nano \
^R^X \
reset; sh 1>&0 2>&0 \
So, lets say the file is called leroyjenkins.txt, you would **sudo nano leroyjenkins.txt** This would put you in the nano editor. Then, according to GTFOBins, you would do **ctrl+r** and then **ctrl+x** That would read the file then exit the file. Then you would type in **reset; sh 1>&0 2>&0** That should give you an elevated prompt. This happens because it does not drop the elevated privileges and may be used to access the file system, escalate or maintain privileged access.





