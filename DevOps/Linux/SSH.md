# SSH

* [Keep SSH Sessions From Disconnecting](https://lonesysadmin.net/2011/11/03/keep-ssh-sessions-from-disconnecting/)
* [SSH Cheatsheet](https://bitrot.sh/cheatsheet/13-12-2017-ssh-cheatsheet/)

```
# ~/.ssh/config
Host *
  ServerAliveInterval 120
```