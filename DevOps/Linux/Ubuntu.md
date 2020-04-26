# Ubuntu

After installing 18.04

```
▶ sudo bash -c 'echo "deploy ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers'
```

At your macOS:

```
▶ ssh-copy-id deploy@IPAddress
```

## Profile

Edit `.profile`

```
alias q=exit
```

## Install Docker first

Of course check the latest at [Docker's Ubuntu install](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

```
▶ sudo apt install apt-transport-https ca-certificates curl software-properties-common
▶ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
▶ sudo apt-key fingerprint 0EBFCD88
▶ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
▶ sudo apt update
▶ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Post install for Linux:

```
▶ sudo groupadd docker
▶ sudo usermod -aG docker $USER
▶ sudo reboot
▶ sudo systemctl enable docker
```

**Swap limit**

```
▶ sudo vi /etc/default/grub
```

Add this line:

```
GRUB_CMDLINE_LINUX="cgroup_enable=memory swapaccount=1"
```

Then:

```
▶ sudo update-grub
```

**IP forwarding for UFW**

```
▶ sudo vi /etc/default/ufw
```

Add this line:

```
DEFAULT_FORWARD_POLICY="ACCEPT"
```

Then:

```
▶ sudo ufw reload
```

## Firewall

Remember to enable SSH or else you will log yourself out.

```
▶ sudo ufw allow 22/tcp
▶ sudo ufw allow 80/tcp
▶ sudo ufw allow 443/tcp

▶ sudo ufw enable
▶ sudo ufw status verbose
▶ sudo ufw show added
```

## Docker Syslog and DNS

Use this to change default text editor to vim.basic

```
▶ sudo update-alternatives --config editor
```

```
▶ sudo systemctl edit docker.service
```

Add this line:

```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd --dns 1.1.1.1 --dns 8.8.8.8 --dns 8.8.4.4 --log-driver=syslog -H fd://
```

Reload the config:

```
▶ sudo systemctl daemon-reload
▶ sudo systemctl restart docker.service
```

## Remove MOTD

```
▶ cd /etc/update-motd.d/
▶ sudo chmod -x 10-help-text
▶ sudo chmod -x 50-motd-news
```

## SSH and Git

```
▶ ssh-agent bash
▶ ssh-add /home/deploy/.ssh/id_rsa
```