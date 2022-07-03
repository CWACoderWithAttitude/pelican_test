Title: Fun with SSH
Date: 2022-06-26 15:40
Modified: 2022-06-26 15:40
Category: SSH
Tags: SSH, secure connection, remote, passwordless
Slug: ssh-wo-pwd
Authors: Volker
Summary: Setup SSH w Key Authentication

1. Create a `ssh-key` 
```shell
❯ ssh-keygen -a 200 -C "My key to raspi4" -t ed25519 -f ~/.ssh/id_ed25519_raspi4
...
```

2. Copy the `public` key to the remote machine
There're different ways to do this - this is the way i use
```shell

```
2. Create an entry in `~/.ssh/config`
```shell
Host raspi4
  User pi
  HostName raspi4.fritz.box
  IdentityFile ~/.ssh/id_raspi4
  PreferredAuthentications publickey
```

To make it more convenient you could setup ssh connections in your local `~/.ssh/config`:   
```shell
Host raspi4
  User pi
  HostName raspi4.local
  IdentityFile ~/.ssh/id_raspi4
  PreferredAuthentications publickey
```

This makes connecting as easy as 
```shell
❯ ssh raspi4
Linux raspberrypi 5.10.92-v7l+ #1514 SMP Mon Jan 17 17:38:03 GMT 2022 armv7l

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Mon Jun 27 18:17:13 2022

SSH is enabled and the default password for the 'pi' user has not been changed.
This is a security risk - please login as the 'pi' user and type 'passwd' to set a new password.

pi@raspberrypi:~ $
```


Example

```shell
❯ ssh pi@raspi4
Linux raspberrypi 5.10.92-v7l+ #1514 SMP Mon Jan 17 17:38:03 GMT 2022 armv7l
...
pi@raspberrypi:~ $
```

