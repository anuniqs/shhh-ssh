1. [SSH On CentOS Or RedHat —](#SSH-On-CentOS-Or-RedHat-—)
1. [SSH On Ubuntu —](#SSH-On-Ubuntu-—)

## SSH On CentOS Or RedHat

### Install OpenSSH Server Software Package

[anup@localhost ~]$ sudo yum update

[anup@localhost ~]$ sudo yum install openssh-server

[anup@localhost ~]$ sudo yum install openssh-client


### SSH Configuration File

[anup@localhost ~]$ sudo nano /etc/ssh/sshd_config


### Manage Service or Deamon

[anup@localhost ~]$ sudo systemctl start sshd

[anup@localhost ~]$ sudo systemctl start sshd

[anup@localhost ~]$ sudo systemctl status sshd

[anup@localhost ~]$ sudo systemctl stop sshd


### Enable or Diasble OpenSSH Service

Enable SSH to start automatically after each system reboot by using the systemctl command :

[anup@localhost ~]$ sudo systemctl enable sshd

[anup@localhost ~]$ sudo systemctl disable sshd


### User SSH Connection

[anup@localhost ~]$ ssh localhost

[anup@localhost ~]$ ssh anup@10.10.10.116


### ROOT SSH Connection

__Edit Configuration file__

[anup@localhost ~]$ sudo nano /etc/ssh/sshd_config

__And set__

PermitRootLogin yes

Then restart ssh

[anup@localhost ~]$ sudo systemctl restart sshd

[anup@localhost ~]$ ssh root@10.10.10.116


### SSH Key-Pair Authentication

__At remote machine (192.168.122.137)__

[anup@localhost ~]$ ssh-keygen -t rsa

[anup@localhost ~]$ mv ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys

[anup@localhost ~]$ chmod 600 ~/.ssh/authorized_keys

__At local machine (10.10.10.116)__

[anup@localhost ~]$ mkdir ~/.ssh

[anup@localhost ~]$ chmod 700 ~/.ssh

[anup@localhost ~]$ scp anup@192.168.122.137:/home/anup/.ssh/id_rsa ~/.ssh/

[anup@localhost ~]$ ssh anup@192.168.122.137


### Secure Copy

[anup@localhost -]$ scp ./file_name.c anup@192.168.122.137:~/

SFTP (SSH File Transfer Protocol)

SFTP server function is enabled by default, but if not, enable it to add the line [Subsystem sftp /usr/lib/openssh/sftp-server] in [/etc/ssh/sshd_config].

[anup@localhost ~]$ sftp anup@192.168.122.137

anup@192.168.122.137's password:
Connected to 192.168.122.137.
sftp>

Upload to remote

sftp> put one.txt

Download from remote

sftp> get two.txt

To come out from sftp type "exit" and pres enter


### SFTP Only

At remote macine

[anup@localhost ~]$ sudo groupadd sftp_users

[anup@localhost ~]$ sudo usermod -G sftp_users anup

[anup@localhost ~]$ sudo nano /etc/ssh/sshd_config

comment out and add a line like below

Subsystem sftp /usr/lib/openssh/sftp-server

Subsystem sftp internal-sftp

add to the end

Match Group sftp_users
X11Forwarding no
AllowTcpForwarding no
ChrootDirectory /home
ForceCommand internal-sftp

[anup@localhost ~]$ sudo systemctl restart ssh

Test

[anup@localhost ~]$ ssh anup@192.168.122.137
This service allows sftp connections only.
Connection to 192.168.122.137 closed.

[anup@localhost ~]$ sftp anup@192.168.122.137
Connected to 192.168.122.137.
sftp>

To get back to normal, rollback the changes.

## SSH On Ubuntu

### SSH Installation

anup@Megatron:~$ sudo apt-get update

anup@Megatron:~$ sudo apt-get upgrade

anup@Megatron:~$ sudo apt-get install openssh-server

anup@Megatron:~$ sudo apt-get install openssh-client

 
### SSH Configuration File

anup@Megatron:~$ nano /etc/ssh/sshd_config


### Manage Process

anup@Megatron:~$ sudo systemctl status ssh

anup@Megatron:~$ sudo systemctl start ssh

anup@Megatron:~$ sudo systemctl restart ssh

anup@Megatron:~$ sudo systemctl stop ssh


### User SSH Connection

anup@Megatron:~$ ssh localhost

anup@Megatron:~$ ssh anup@10.10.10.116


### ROOT SSH Connection

Edit Configuration file
anup@Megatron:~$ sudo nano /etc/ssh/sshd_config

And set

PermitRootLogin yes

Then restart ssh

anup@Megatron:~$ sudo systemctl restart ssh

anup@Megatron:~$ ssh root@10.10.10.116


### SSH Key-Pair Authentication

At remote machine (192.168.122.137)

anup@ubuntu:~$ ssh-keygen -t rsa

anup@ubuntu:~$ mv ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys

anup@ubuntu:~$ chmod 600 ~/.ssh/authorized_keys

At local machine (10.10.10.116)

anup@anup-Lenovo-G50-70:~$ mkdir ~/.ssh

anup@anup-Lenovo-G50-70:~$ chmod 700 ~/.ssh

anup@anup-Lenovo-G50-70:~$ scp anup@192.168.122.137:/home/anup/.ssh/id_rsa ~/.ssh/

anup@anup-Lenovo-G50-70:~$ ssh anup@192.168.122.137


### Secure Copy

anup@anup-Lenovo-G50-70:~$ scp ./57_1_star.c anup@192.168.122.137:~/


SFTP (SSH File Transfer Protocol)

SFTP server function is enabled by default, but if not, enable it to add the line [Subsystem sftp /usr/lib/openssh/sftp-server] in [/etc/ssh/sshd_config].

anup@anup-Lenovo-G50-70:~$ sftp anup@192.168.122.137

anup@192.168.122.137's password:
Connected to 192.168.122.137.
sftp>

Upload to remote

sftp> put one.txt

Download from remote

sftp> get two.txt

To come out from sftp type "exit" and pres enter


### SFTP Only

At remote macine

anup@ubuntu:~$ sudo groupadd sftp_users

anup@ubuntu:~$ sudo usermod -G sftp_users anup

anup@ubuntu:~$ sudo nano /etc/ssh/sshd_config

comment out and add a line like below

Subsystem sftp /usr/lib/openssh/sftp-server

Subsystem sftp internal-sftp

add to the end

Match Group sftp_users
X11Forwarding no
AllowTcpForwarding no
ChrootDirectory /home
ForceCommand internal-sftp

anup@ubuntu:~$ sudo systemctl restart ssh

Test

anup@anup-Lenovo-G50-70:~$ ssh anup@192.168.122.137
This service allows sftp connections only.
Connection to 192.168.122.137 closed.

anup@anup-Lenovo-G50-70:~$ sftp anup@192.168.122.137
Connected to 192.168.122.137.
sftp>

To get back to normal, rollback the changes.

<hr />

`@ Anup Kumar Mondal, AnuRish Brand Corp. , +91-9620481097 , uniqs.anup@gmail.com , https://www.linkedin.com/in/anuniqs/`
