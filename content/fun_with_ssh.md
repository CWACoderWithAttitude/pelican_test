Title: Fun with SSH
Date: 2022-06-26 15:40
Modified: 2022-06-26 15:40
Category: SSH
Tags: SSH, secure connection, remote
Slug: fun-with-ssh
Authors: Volker
Summary: Setup and using SSH

SSH enables us to establish secure connections to remote machines.   
Using SSH keys we can setup a secure connection which does not require us to enter a password each ti,e we want to connect.   

Assumption:
1. we can 
But first thigs first.   
To give you a practical example we're going to setup everything to connect to our raspberry pi.   

1. First connection with password for user `pi`
```shell
❯ ssh pi@raspi4.fritz.box
The authenticity of host 'raspi4.fritz.box (192.168.178.154)' can't be established.
ED25519 key fingerprint is SHA256:3ougi+3fGsIQtSJjYh+UScBysSrtNkY3IyhTInatSfU.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'raspi4.fritz.box' (ED25519) to the list of known hosts.
Linux raspberrypi 5.10.92-v7l+ #1514 SMP Mon Jan 17 17:38:03 GMT 2022 armv7l
...
pi@raspberrypi:~ $
```
This means we attempted to login to `raspi4` as user `pi`.    
Since this is our first attempt our host couldn't verify that the remote machine is what it claims to be.
Therefore our machine will memorize the fingerprint for this machine.   

2. Second login with password for `pi`
```shell
❯ ssh pi@raspi4.fritz.box
Linux raspberrypi 5.10.92-v7l+ #1514 SMP Mon Jan 17 17:38:03 GMT 2022 armv7l

...
pi@raspberrypi:~ $
```
A bit smoother but not our goal - passwordless login.

3. Create a `ssh-key` 
```shell
❯ ssh-keygen -a 200 -C "My key to raspi4" -t ed25519 -f ~/.ssh/id_ed25519_raspi4
Generating public/private ed25519 key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/volker/.ssh/id_ed25519_raspi4
Your public key has been saved in /Users/volker/.ssh/id_ed25519_raspi4.pub
The key fingerprint is:
SHA256:7Dwe5OdzPoVWeYTBi1caSaXuPNVj9fT3/CWwnZ+xKvk My key to raspi4
The key's randomart image is:
+--[ED25519 256]--+
|             oo=.|
|              =.o|
|             ..Bo|
|       .    ..*.*|
|        S   .+.+*|
|       =    o*o++|
|        * ..o.B.+|
|       . =.oo  +*|
|        . .++E.oo|
+----[SHA256]-----+
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

