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




