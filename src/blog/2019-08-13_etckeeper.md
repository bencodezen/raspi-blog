---
title: Managing your machine config with EtcKeeper

---

# Managing your Linux machine config with etcKeeper

EtcKeeper is a set of tools that enable you to keep your system config files that are found in /etc/ under version control and keep a copy on a [GitHub](https://github.com) Repository or [similar](https://etckeeper.branchable.com/).

You can even setup your own backup servers to host git repositories and push to registries on those machines.

EtcKeeper even tracks file metadata that git does not normally support which is particularly important for certain files such as `/etc/shadow`.

## Installing etckeeper

Installation is simple ...

```
sudo apt update
sudo apt install etckeeper
```


### Setting up etckeeper ssh keys on GitHub

Goto [GitHub](https://github.com) and create a new repository - ideally you should set this to a private repository

Create a ssh key for the root user

```
sudo su -
```
```
ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): 
Created directory '/root/.ssh'.
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:+INhDeI6fYZWChYlZPHMzfdAxmciBQM5iBNX2PIwZnA root@home.jesusdiedfor.me
The key's randomart image is:
+---[RSA 2048]----+
|+=EB=..oo        |
|++X*.+.oo o      |
| +.*= +.o+       |
|   o.. =  o      |
|  o . = S .      |
| . + = +         |
|  o = + o        |
|   o o   .       |
|                 |
+----[SHA256]-----+
```
```
cat .ssh/id_rsa.pub 

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDkQKqKQpmBPUV7T1WZfcqD7PWUi30fiAtYhkzwp07iAzSu5Zns6e2JD5AksXwm8iMyGLz3YX5TmiuCa48ArAeNGxw6Bphm8+hkBFMLvTMp6jbQUZEys+7VtAuZmUVCUff/r5c/iATwTawu+mPayIEFWrZJV0FSizdhZeGFD0GCTG4H54FbxBx7QKRjoDA3MFV6mKk19de5yz1JoIlNhJ813fLkH1aJuuuYNjkZb2oF9K4LxlK/IHgQVO43cW3ZZphn9e3NbCF1Xm5EA1c68u65Hq6+AgrFWQ8kkPZepXY7GxK/aXaiA7lSjKV92ZSUPDls/Hix8DOBk48u7J12KFrv root@home.jesusdiedfor.me

```

Goto your [GitHub settings - SSH Keys ](https://github.com/settings/keys) settings and click on the `New SSH key` button
    git push --set-upstream origin master

```
cat .ssh/id_rsa.pub 

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCvkw7gnJwl7qX+DbK83LznNo+D7boyuDL7mcRVmTu8l1nnaJvahlBgmhji/iG4LTnUr41i9bmsaCOllS7e0kAIfTX8PwR+1ne9S3RUxSCS7FzthcLIzJR1AN3kzEdqYNqZN37yxKh2xlQ6zwizPfVjGS+6Ek06GK+eYeQtnEoTr8zQj6xRyhSSKwd5E/A0OZ/8drL85Rrjyjfdge472g6kcd6vypYIhm8n47CdczAMCWNPXi7EVZpT7sAwDpKYAn4c99LrKwV//bIspg3VZ+ilElBJffyRlLzWLyF2wGeAn/2DOdBODIgPezaIxJJCyAwi8GzA4KJfEH6Ug4+9cF root@ian.jesusdiedfor.me
```

Then copy & paste the key into the space on the GitHub keys page.


### Initialize etckeeper

Goto the `/etc` directory and run:

```
etckeeper init
```

This will setup a git repository in `/etc` and commit the configuration files to them

Similarly to `git status` you can issue the following command to verify that new files have been added to the repository

```
etckeeper vcs status
```

### Push initial files into git

To add the initial files into git use the command

```
etckeeper commit "initial commit"
```


### Setup git to push to GitHub

From the github page, click `Clone or download` and then click `Use SSH`. Copy the ``git@github...` line shown then go back to your terminal.


Add the remote to the repository and verify it:

```
git remote add origin git@github.com:iandstanley/home-etc.git

git remote -v

```

Finally push the initial commit to the repository with 

```
git push --set-upstream origin master
```

## Using etckeeper

When you change your `/etc` configuration for any reason perform the following:

```
cd /etc
sudo etckeeper commit "changed /etc/hosts file"
```	