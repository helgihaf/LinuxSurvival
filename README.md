# Linux Survival

The Linux flavor used is Ubuntu unless otherwise stated.

## Create a new user
Create a new user called **docking** and give it admin access via sudo:
```bash
sudo useradd -s /bin/bash -d /home/docking/ -m -G sudo docking
sudo passwd docking
```

## SSH
You need a public/private keypair if you want to enable SSH login for a user.

### Do you already have a keypair?
Check your ~/.ssh directory for an id_rsa file.

### Create new keypair
This is most often done *on the client*:
```bash
ssh-keygen
```
Then you enter the destination file of the keypair, for example:
`/cygdrive/c/Users/laiheh/Documents/DockingSSH/id_rsa`

Now you have two new files:
id_rsa (the private key)
id_rsa.pub (the public key)

### Copy the public key to the server
To be able to log in to the server you must copy the public key to it. Do this on the client:
```bash
ssh-copy-id username@remote_host
```
You will need to log in using the password for the user.

## Install certificates
Sometimes you are cursed with a thing called Websense and you must install additional root certificates on your Linux box/container. Here is one example how to do this using a Dockerfile, but you can easly do this by hand using the shell as well:
```Dockerfile
FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS buildbase
ADD myCerts/websense.crt /usr/local/share/ca-certificates/websense.crt
RUN chmod 644 /usr/local/share/ca-certificates/websense.crt && update-ca-certificates
```
