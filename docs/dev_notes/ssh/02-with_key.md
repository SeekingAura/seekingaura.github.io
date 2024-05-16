---
title: SSH | pem/key file
permalink: /docs/dev_notes/ssh/with_key/
toc: true
---
# SSH remote connection with pem/key file
Use ssh with user and password it can be a bit annoying to write the password each time you stablish ssh connection and is also vulnerable to brute force access attacks (try multiple usernames and password).

To prevent this and forgot password use pem/key file instead, this guide

# TL;DR
To create ssh Private and Public key run this command
```bash
ssh-keygen -t ed25519 -b 4096 -C "user@domain"
```

Set where the key pair will saved and set or not passphrase, then key pairs will created.

On server machine add public key value at the end of *authorized_keys* file of the user where want access, if not exist create
```
touch ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

and add the Public key, for example via ssh
```
ssh example_user@example_server "echo \"`cat ~/.ssh/id_rsa.pub`\" >> .ssh/authorized_keys"
```

Set configuration for ssh server to allow access via file and not password, at `/etc/ssh/sshd_config.d/` add conf file (example.conf) with
```conf
PasswordAuthentication no
```

Ensure does not exist another conf file with opposite configuration (PasswordAuthentication yes) and reset ssh service
```bash
/etc/init.d/ssh reload
```

or
```bash
sudo systemctl reload sshd
```

more info about server config check https://www.man7.org/linux/man-pages/man5/sshd_config.5.html

On Client machine set the right permissions for Private key file
```
chmod 400 ~/.ssh/id_rsa
```

On client machine for ssh login can set configuration at `~/.ssh/config` like this
```
Host alias
    HostName hostname
    User user
    IdentityFile "~/.ssh/id_rsa"
```

where identityFile is the path to private key on client machine, this config allow to connect with that config the following command
```
ssh alias
```

More info about client config file check https://linux.die.net/man/5/ssh_config

# SSH key file creation requisites
## SSH Key algorithms
To create a ssh key must be select an algorithm, to get available algorithms run the next command
```bash
ssh -Q key
```

param **-Q** query something of ssh-keygen on this case key algorithms, that output something like this

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
{: .notice}

To select an specific algorithm use param **-t** on **ssh-keygen** command, for example to create key with rsa algorithm run this command:
```bash
ssh-keygen -t rsa
```

## Comment on pub file
On file creation you can set a comment on Public key file, comment is only information this does not take any effect on public key usage, that makes more easy to identify the user or the usage of that key. To set a comment on Public key use the **-C** param. For example to set the comment *"this is a test"* in public key file run this command:
```bash
ssh-keygen -C "this is a test"
```

The comment will are at the end of the line where the Public key value is.

## Bits of pem file
Some algorithms for key generation like *RSA* can have a different bits size on their key, to change the bits use param **-b**. For example the next command create RSA key with 1024 bits
```bash
ssh-keygen -t rsa -b 1024
```

More bits could be more "secure" but another algorithms like [Ed25519](#ed25519-algorithm) is considered more secure than RSA

# Init Private and public key file generation
An ssh Private and public file pairs can be created using the command `ssh-keygen` without params
```bash
ssh-keygen
```

This will use the default settings, that is equivalent to create key with RSA algorithm with 3072 bits and comment of current username and hostname of machine.
```bash
ssh-keygen -t rsa -b 3072 -C "$USER@$HOSTNAME"
```

Then will output
```
Generating public/private rsa key pair.
```

And will ask where key pair will saved, passphrase and finally generate the key pairs, check [here](#key-generation-steps-after-keygen-init) for detail

To get detail about generate a key with this algorithm check [here](#rsa-algorithm---most-common)


## RSA Algorithm - Most common
The most common algorithm for SSH key generation is RSA, on this you can set how many bits will the key have, by default use 3072 bits, the min bits size is 1024 and the max is 16384. The next command create a key with 4096 bits and comment *"user@domain"*

```batch
ssh-keygen -t rsa -b 4096 -C "user@domain"
```

Then will ask where key pair will saved, passphrase and finally generate the key pairs, check [here](#key-generation-steps-after-keygen-init) for detail

## Ed25519 Algorithm
This "modern" algorithm is considered more **secure** than *RSA* and *ECDSA* for SSH, unlike to *RSA* algorithm, it is not possible to set a different number of bits (param **-b**) always will use 256 bits. The next command create a key with Ed25519 algorithm and comment *"user@domain"*
```batch
ssh-keygen -t ed25519 -C "user@domain"
```

Then will ask where key pair will saved, passphrase and finally generate the key pairs, check [here](#key-generation-steps-after-keygen-init) for detail

# Key generation steps after keygen init
Once keygen is started will ask where the public key and private key will saved, by default is `~/.ssh/id_rsa` and the public key file will stored on the same place with *.pub* extension, on default case will be `~/.ssh/id_rsa.pub`. 
```
Enter file in which to save the key (C:\Users\example_user/.ssh/id_rsa):
```

Must be a absolute path, then enter. Then ask for *passphrase* two times, that is used for decrypt the private key form client side, can be empty
```
Enter passphrase (empty for no passphrase):
Enter same passphrase again: 
```

The pair key file will created and output something like this
```
Your identification has been saved in C:\Users\example_user/.ssh/id_rsa.       
Your public key has been saved in C:\Users\example_user/.ssh/id_rsa.pub.       
The key fingerprint is:
SHA256:Ebyze3gVzoTi5VnW97JvSh8XB+UAGKs32LYVT2Y78AA example_user@example_host
The key's randomart image is:
+---[RSA 3072]----+
|       .. Eo... .|
|        ...o   + |
|        ....+.= .|
|        +=o =X.o.|
|       .S*=B..=oo|
|        ooo++ ..+|
|         o..  .+.|
|        o o  ...+|
|         o    .+o|
+----[SHA256]-----+
```

key always be different every time that is generated, at `+---[RSA 3072]----+` show the name of algorithm and used bytes, for this example was RSA algorithm with 3072 bits.

# Config key access on server
## Public Key on server
With key pair generated now can register on server the key allow access via private key, for that we save the public key on authorized_keys of server where want grant access. On the server with the user where want to grant access will find `~/.ssh/authorized_keys` if does not exist will create with these permissions

```batch
touch ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys
```

Then at the end of that file append the pub key value, for example from client machine where have the public key and access to server machine via ssh can put the value with this command.

```batch
ssh conection_alias "echo \"`cat ~/.ssh/id_rsa.pub`\" >> .ssh/authorized_keys"
```

or just use, nano, vi, vim. That file can have multiple public keys, every key is separated by newline. The public key on user home location only works for authentication for that user. Now for use ssh without password requires disable password authentication on ssh server config.

## Disable password authentication on SSH server
Once you have at least one user with public key configured on authorized_keys you can disable the ssh access with password, for that search config files at `/etc/ssh/sshd_config.d/` and try to find a file with value
```conf
PasswordAuthentication
```

if not exist add a line on any conf file or create new `.conf` file and add this
```
PasswordAuthentication no
```

Then restart ssh server service
```bash
/etc/init.d/ssh reload
```

or
```bash
sudo systemctl reload sshd
```

if you are on server machine connected via ssh restart the service will not close the current connection.

## Config private key for ssh client
The private key must have permissions of the user that will stablish an ssh connection

```bash
chmod 400 ~/.ssh/id_rsa
```

That set permission read only of the user file owner, the owner must be same of that home and the same that will stablish ssh connection

on windows case is
```powershell
$path = ".\id_rsa"
# Reset to remove explict permissions
icacls.exe $path /reset
# Give current user explicit read-permission
icacls.exe $path /GRANT:R "$($env:USERNAME):(R)"
# Disable inheritance and remove inherited permissions
icacls.exe $path /inheritance:r
```

the Public works something like a keyhole of the door. now can used

## Config ssh client for key usage
With server conf ready, and private key with right permissions now can use, for simple usage with client configuration on client machine create configuration file at  `~/.ssh/config` and add something like this
```
Host alias
    HostName hostname
    User user
    IdentityFile "~/.ssh/id_rsa"
```

where identityFile is the path to private key on client machine that will use on server hostname, this config allow to connect with that config the following command
```
ssh alias
```

On that config file you can setup multiple ssh connections via alias

More info about client config file check https://linux.die.net/man/5/ssh_config


# References
{:.no_toc}
* [How do I list available host key algorithms for an SSH client?](https://unix.stackexchange.com/questions/223276/how-do-i-list-available-host-key-algorithms-for-an-ssh-client)
* [What is the public key length of RSA and Ed25519?](https://crypto.stackexchange.com/questions/87715/what-is-the-public-key-length-of-rsa-and-ed25519#:~:text=For%20ed25519%20the%20'blob'%20data,to%2068%20chars%20(exactly).)
* [SSH keys - Archilinux](https://wiki.archlinux.org/title/SSH_keys#:~:text=There%20is%20no%20need%20to%20set%20the%20key%20size%2C%20as,may%20not%20support%20these%20keys.)
* [How to append authorized_keys on the remote server with id_rsa.pub key](https://stackoverflow.com/questions/23591083/how-to-append-authorized-keys-on-the-remote-server-with-id-rsa-pub-key)
* [Using ICACLS to set file permission to 'read-only'](https://stackoverflow.com/questions/43312953/using-icacls-to-set-file-permission-to-read-only/43317244#43317244)
