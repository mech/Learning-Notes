# Ubuntu

After installing 18.04.3

```
▶ sudo bash -c 'echo "deploy ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers'
```

At your macOS:

```
▶ ssh-copy-id deploy@172.16.78.130
```

## Profile

Edit `.profile`

```
alias q=exit
```

## Firewall

```
▶ sudo ufw allow 16111/tcp
▶ sudo ufw allow 80/tcp
▶ sudo ufw allow 443/tcp

▶ sudo ufw enable
▶ sudo ufw status verbose
▶ sudo ufw show added
```

## Remove MOTD

```
▶ cd /etc/update-motd.d/
▶ sudo chmod -x 10-help-text
▶ sudo chmod -x 50-motd-news
```