<!-- omit from toc -->
# SSH remote connection with pem/key file
Use ssh with user and password it can be a bit annoying to write the password each time you stablish ssh connection and is also vulnerable to brute force access attacks (try multiple usernames and password).

To prevent this and forgot your password use pem/key file instead, this guide

<!-- omit from toc -->
# TL;DR
To create file run this command
```bash
ssh-keygen -t ed25519 -b 4096 -C "user@domain"
```

Then set the right permissions for pem file on Client machine
```
chmod 400 ~/.ssh/id_rsa
```

On server machine add at the pub value on authorized_keys file, if not exist create
```
touch ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

and add the pub key fro example via ssh
```
ssh example_user@example_server "echo \"`cat ~/.ssh/id_rsa.pub`\" >> .ssh/authorized_keys"
```

finally set configuration for ssh server to allow access via file and not password, at `/etc/ssh/sshd_config` set
```conf
PasswordAuthentication no
```

and reset ssh service
```bash
/etc/init.d/ssh reload
```

or
```bash
sudo systemctl reload sshd
```

more info about config check https://www.man7.org/linux/man-pages/man5/sshd_config.5.html


<!-- omit from toc -->
# TOC
- [SSH key file creation requisites](#ssh-key-file-creation-requisites)
  - [SSH Key algorithms](#ssh-key-algorithms)
  - [Comment on pub file](#comment-on-pub-file)
  - [Bits of pem file](#bits-of-pem-file)
- [Create Key and pub file](#create-key-and-pub-file)
  - [RSA Algorithm - Most common](#rsa-algorithm---most-common)
  - [Ed25519 Algorithm](#ed25519-algorithm)
- [](#)
- [References](#references)


# SSH key file creation requisites
## SSH Key algorithms
To create a ssh key must be select an algorithm, to get available algorithms run the next command
```bash
ssh -Q key
```

param **-Q** query something of ssh-keygen on this case key algorithms, that output something like this
```txt
ssh-ed25519-cert-v01@openssh.com
ssh-rsa
ssh-dss
ecdsa-sha2-nistp256
ecdsa-sha2-nistp384
ecdsa-sha2-nistp521
ssh-rsa-cert-v01@openssh.com
ecdsa-sha2-nistp256-cert-v01@openssh.com
ecdsa-sha2-nistp384-cert-v01@openssh.com
ecdsa-sha2-nistp521-cert-v01@openssh.com
```

To select an specific algorithm use param **-t** on **ssh-keygen** command, for example to create key with rsa algorithm run this command:
```bash
ssh-keygen -t rsa
```


## Comment on pub file
On file creation you can set a comment on a pub file, comment are only information this does not take effect on pub key structure, value or functionality, this makes more easy to identify the user or what is the usage that will the pub key have. To set a comment on pub key use the **-C** param. For example to set in pub file the comment *this is a test" run this command:
```bash
ssh-keygen -C "this is a test"
```

The comment will are at the end of the line where the pub key is.

## Bits of pem file
Some algorithms like *RSA* can have a different bits size on their key, to change the bits use param **-b**. For example the next command create RSA key with 1024 bits
```bash
ssh-keygen -t rsa -b 1024
```

# Create Key and pub file
An ssh pem and pub file pairs can be created using the command ssh-keygen without params, this use default settings. 
```bash
ssh-keygen
```

This ask the location where the pem and pub file will located, by default is `~/.ssh/id_rsa` and pub file `~/.ssh/id_rsa.pub`, with RSA algorithm with 3072 bits, the default values is equivalent to this command

```bash
ssh-keygen -t rsa -b 3072 -C "$USER@$HOSTNAME"
```

To get detail of this algorithm check here

## RSA Algorithm - Most common
The most common algorithm for SSH keys is RSA, this you can set how many bits will have the key, by default use 3072 bits, min bits size is 1024 and the max is 16384. The next command create a key with 4096 bits and comment *"user@domain"*

```batch
ssh-keygen -t rsa -b 4096 -C "user@domain"
```

## Ed25519 Algorithm
This modern algorithm is considered **safer** than *RSA* and *ECDSA* for SSH, unlike to RSA algorithm, it is not possible to indicate a different number of bits (param **-b**). The next command create a key with Ed25519 algorithm and comment *"user@domain"*
```
ssh-keygen -t ed25519 -C "user@domain"
```

#

# References
* [How do I list available host key algorithms for an SSH client?](https://unix.stackexchange.com/questions/223276/how-do-i-list-available-host-key-algorithms-for-an-ssh-client)
* [What is the public key length of RSA and Ed25519?](https://crypto.stackexchange.com/questions/87715/what-is-the-public-key-length-of-rsa-and-ed25519#:~:text=For%20ed25519%20the%20'blob'%20data,to%2068%20chars%20(exactly).)
* [SSH keys - Archilinux](https://wiki.archlinux.org/title/SSH_keys#:~:text=There%20is%20no%20need%20to%20set%20the%20key%20size%2C%20as,may%20not%20support%20these%20keys.)
* [How to append authorized_keys on the remote server with id_rsa.pub key](https://stackoverflow.com/questions/23591083/how-to-append-authorized-keys-on-the-remote-server-with-id-rsa-pub-key)
---

<!-- omit from toc -->
# Navigation
* [SSH index](/docs/ssh)
* [Docs index](/docs)