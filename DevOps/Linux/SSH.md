# SSH

* [Keep SSH Sessions From Disconnecting](https://lonesysadmin.net/2011/11/03/keep-ssh-sessions-from-disconnecting/)

```
# ~/.ssh/config
Host *
  ServerAliveInterval 120
```