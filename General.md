# CTF Cheatsheet General

**Description:** A list of commands, techniques and tooling I use to perform CTFs

##Python stable shell
When an exploit only gives you an sh shell, this can sometimes be unstable and you would need to make it a BASH shell. To do that in Python:
```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```
