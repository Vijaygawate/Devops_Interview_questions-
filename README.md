# Devops_Interview_questions-
DevOps Interview Questions


Operating System	3
Linux	3
Basic	3
Advance	7
Windows	15
Basic	15
Advance	15
Containerization	16
Docker	16
Basic	16
Advance	20
Kubernetes	25
Basic	25
Advance	25
Configuration Management	26
Ansible	26
Basic	26
Advance	31
Puppet	33
Basic	33
Advance	33
CI / CD	34
Jenkins	34
Basic	34
Advance	36
Infrastructure as Code	38
Terraform	38
Basic	38
Advance	40
CloudFormation	42
Basic	42
Advance	42
Cloud	43
AWS	43
Basic	43
Advance	44
GCP	45
Basic	45
Advance	45
Azure	45
Basic	45
Advance	45
Monitoring
     Datadog
General Cloud Computing	45
Scripting Languages	46
Shell	46
Python	46
Culture Check	47


Operating System:

Linux:

Basic:

Any 5 linux commands that you use in your day to day life and what is their use

Lsof:  lists on its standard output file information about files opened by processes for the following UNIX dialects

lsof | wc -l gives count of open files in the system

Grep:  The grep utility searches for any given input files, selecting lines that match one or more patterns.
ls | grep k8s This is a simple list command which gets only the directories with the matching string i.e ‘k8s’

Sed: The sed utility reads the specified files, or the standard input if no files are specified, modifying the input as specified by a list of commands.  The input is then written to the standard output.

sed 's/unix/linux/' test.txt This command is a simple sed command that replaces the word “unix” with “linux” in the file. 

Tail: The tail utility displays the contents of a file or, by default, its standard input, to the standard output.
tail -f /var/log/syslog This command will continuously display the logs in syslog to standard output

Telnet: The telnet command is used to communicate with another host using the TELNET protocol.

telnet <remote-host-ip> <port>

telnet 192.168.0.24 443 This command will communicate to remote host on port 443

What is Swap Space?

Swap space is a space on a hard disk which is a substitute for physical memory. It is used as virtual memory which contains process memory images.
Whenever our computer runs short of physical memory it uses its virtual memory and stores information in memory on disk. Swap space helps the computer’s operating system in pretending that it has more RAM than it actually has. It is also called a swap file.
This interchange of data between virtual memory and real memory is called swapping and space on disk as “swap space”.



What are file permissions under Linux File System? What is default permission of a file, command to change the permission of a file to read only

Default File Permissions: 644 (-rw-r--r--) 
Read only chmod 400 </path/filename>


You try to delete a file but it fails. Name at least three different reason as to why it could happen:

File may be in use by a process
No more inodes
No permissions


What are the fields in the /etc/passwd file?

/etc/passwd is a text file that contains the attributes of (i.e., basic information about) each user or account on a computer running Linux or another Unix-like operating system.
There are total 7 fields separated by a colon : 
Username
Placeholder for Password usually 'x' if password is present (Password is stored in /etc/shadow file for security reasons) 
User Id
Group Id
Comment
Home Directory Path relative to Root folder
Shell Information



What files are modified in the backend when you create a user with useradd, adduser command.

/etc/passwd: contains one entry per line for each user (user account) of the system. All fields are separated by a colon
/etc/group: stores group information or defines the user groups i.e. it defines the groups to which users belong.
/etc/shadow: file stores actual password in encrypted format



Difference between Hard link and Symbolic links? 

Hard Link: Hard links point, or reference, to a specific space on the hard drive. You can have multiple files hard linked to the same place in the hard drive, but if you change the data on one of those files, the other files will also reflect that change.
Soft Link / Symbolic Link: Symbolic links work a bit differently. A symbolic link still points to a specific point on the hard drive, but if you create a second file, this second file does not point to the hard drive, but instead, to the first file.



What is systemd?

Systemd is a daemon (System 'd', d stands for daemon).
A daemon is a program that runs in the background without direct control of the user, although the user can at any time talk to the daemon.
systemd has many features such as user process control/tracking, snapshot support, inhibitor locks.
If we visualize the unix/linux system in layers, systemd would fall directly after the linux kernel.
Hardware -> Kernel -> Daemons, System Libraries, Server Display.



How do you troubleshoot and debug network issues?

dstat -t is great for identifying network and disk issues. 

netstat -tnlaup can be used to see which processes are running on which ports. 

lsof -i -P can be used for the same purpose as netstat. 

ngrep -d any metafilter for matching regex against payloads of packets. 
tcpdump for capturing packets 

How to make nested directories 

mkdir -p /dir1/dir2/dir3 will create nested directories


You get a call from someone claiming "my system is SLOW ''. What do you do?

Check with top for anything unusual
Run dstat -t to check if it's related to disk or network.
Check if it's network related with sar
Check I/O stats with iostat

How do you schedule tasks periodically? What are field of a CRON 



Advance:
Linux boot process 

 

What are iptables? / How to flush iptable

iptables is a command-line firewall utility that uses policy chains to allow or block traffic. When a connection tries to establish itself on your system, iptables looks for a rule in its list to match it to. If it doesn’t find one, it resorts to the default action.

How to find the return value of the last executed command in the shell.

You can use the shell variable $?

$ true ; echo $? 
0 
$ false ; echo $? Fje
1


Give Count of Open File descriptor in my system 

LSOF: List Open Files command gives all the open file descriptor in the system and WC Word Count command will return the number 

lsof | wc -l


Give the number of lines for all the files in a particular Directory

WC Word Count command list lines for all the files in a particular Directory

wc -l <dir>/*


What is Log Rotation and how do you rotate logs in Linux

Log rotation is a process that solves these problems by periodically archiving the current log file and starting a new one.
logrotate will rename or compress the main log when a condition is met (more about that in a minute) so that the next event is recorded on an empty file.

Configuring Logrotate:
Logrotate's configuration is done by editing two separate configuration files:
/etc/logrotate.conf
service specific configuration files stored in /etc/logrotate.d/.
The main logrotate.conf file contains a generic configuration. Here is a default logrotate configuration file logrotate.conf:\

weekly
rotate 4
create
dateext
include /etc/logrotate.d
/var/log/wtmp {
   monthly
   create 0664 root utmp
   minsize 1M
   rotate 1
}


Line 1 - weekly configuration option ensures a weekly rotation of all log-files defined in the main configuration file and in /etc/logrotate.d/ directory.
Line 2 - rotate 4 ensures that logrotate keeps a 4 weeks backup of all log files
Line 3 - create option instructs logrotate to create new empty log files after each rotation
Line 4 - dateext appends an extension to all rotated log files in form of date when each particular log file was processed by logrotate
Line 5 - Include all other configuration from directory /etc/logrotate.d
Line 6 to 11 - Contains a specific service log rotate configuration


Which Folder/File is taking up max space

du -a /home | sort -n -r | head -n 5


du command: Estimate file space usage.
a : Displays all files and folders.
sort command : Sort lines of text files.
-n : Compare according to string numerical value.
-r : Reverse the result of comparisons.
head : Output the first part of files.
-n : Print the first ‘n’ lines. (In our case, We displayed the first 5 lines).
The du utility displays the file system block usage for each file argument and for each directory in the file hierarchy rooted in each directory argument.  If no file is specified, the block usage of the hierarchy rooted in the current directory is displayed.

What is difference between the ps and top command

TOP
PS
The top program periodically displays a sorted list of system processes.


The ps utility displays a header line, followed by lines containing information about all of your processes that have controlling terminals.

top program provides a dynamic real-time view of the processes running on the system

ps utility gives a snapshot of the current processes running on the system

It can display system summary information as well as a list of processes or threads currently being managed by the Linux kernel. 

ps utility only displays the information about the process and not the system information


**** Telnet command use and example 

The telnet command is used to communicate with another host using the TELNET protocol.  If telnet is invoked without the host argument, it enters command mode, indicated by its prompt (``telnet>'').
Command :
telnet <Remote-host-IP> <Port>


Example: 
telnet 192.168.0.2 80


SSH with ` and not private key into the Ec2 Instance, is it possible or not and in which file do we have to make the changes to make it possible

Yes it is possible to SSH into EC2 instance using Username-Password
We may have to edit the file sshd_config file located in the below mentioned path

sudo vim /etc/ssh/sshd_config


Find the Line containing 'PasswordAuthentication' parameter and change its value from 'no' to 'yes'

PasswordAuthentication yes


Save the changes made and restart the ssh service



*** How to set  and unset variables in Linux for the local shell,  user, and system wide? 

Local Variables: One defined for the current session. These environment variables last only till the current session. Usually assigned using the export keyword 

User Variables: These are the variables which are defined for a particular user and are loaded every time a user logs in. Usually stored in .bashrc .bash_profile, .profile, .bash_login

System Variables: These are the environment variables which are available system-wide, i.e. for all the users present on that system. Usually stored in /etc/environment, /etc/profile, /etc/profile.d, /etc/bash.bashrc.



What is umask and default umask for a file.

UMASK in Linux or Unix systems is known as User Mask or it is also called as User file creation Mask. This is a base permission or default permission when a new file or folder is created in the Linux machine. 
By default, the system sets the permissions on a file to 666



Rsync and scp command diff

Rsync
scp
rsync also copies files locally or over a network. But it employs a special delta transfer algorithm and a few optimizations to make the operation a lot faster
scp basically reads the source file and writes it to the destination. It performs a plain linear copy, locally, or over a network.




*** What are Run levels?

A runlevel is one of the modes that a Unix-based operating system will run in. Each runlevel has a certain number of services stopped or started, giving the user control over the behavior of the machine. Conventionally, seven runlevels exist, numbered from zero to six.


Run Level
Mode
Action
0
Halt
Shuts down system
1
Single-User Mode
Does not configure network interfaces, start daemons, or allow non-root logins
2
Multi-User Mode
Does not configure network interfaces or start daemons.
3
Multi-User Mode with Networking
Starts the system normally.
4
Undefined
Not used/User-definable
5
X11
As runlevel 3 + display manager(X)
6
Reboot
Reboots the system



*** What is the module required to enable SSL in Apache?

To configure SSL, Apache HTTP must be compiled with mod_ssl
This module provides SSL v3 and TLS v1.x support for the Apache HTTP Server. SSL v2 is no longer supported.
This module relies on OpenSSL to provide the cryptography engine.


*** Syntax to verify the syntax of apache and nginx configuration file

Apache:

apachectl configtest
apache -t
http -t


Nginx:

sudo nginx -t
sudo nginx -T


You can test the Nginx configuration, dump it and exit using the -T flag as shown.


*** Total number of TCP ports and what are the privileged ports?

TCP Port numbers range from 0 to 65535, 
But only port numbers 0 to 1023 are reserved for privileged services and designated as well-known ports. 
Registered ports are 1024 to 49151.
Dynamic ports (also called private ports) are 49152 to 65535.
Below are few of the privileged TCP ports

Port Number
Service
21
FTP
22
SSH
80
HTTP
443
HTTPS



command to extend a volume partition in linux

Fdisk can be used to extend the volume partition in linux

command Linux lists block devices
.
lsblk: List block devices (for example, the drives).


Other List commands 

ls: List files in the file system
lspci: List PCI devices.
lsusb: List USB devices.
lsdev: List all devices.


List all the files in ascending order of their Name / Size in a directory

ls -lah List by Name 
ls -laShr List by Size 



*** What does Sar provide? Where are Sar logs stored ?

sar : System Activity Report
It can be used to monitor Linux system’s resources like CPU usage, Memory utilization, I/O devices consumption, Network monitoring, Disk usage, process and thread allocation, battery performance, Plug and play devices, Processor performance, file system and more.Linux system Monitoring and analyzing aids understanding system resource usage which can help to improve system performance to handle more requests.
Start the sadc (system activity data collector) service(sysstat) so that it saves the reports in the log file “/var/log/sa/saDD”  where DD represents Current day and already existing files will be archived.


**** How to use setfacl command ?

The setfacl utility sets Access Control Lists (ACLs) of files and directories. On the command line, a sequence of commands is followed by a sequence of files

setfacl -m u:lisa:r test


Grant user lisa read access to file test.

setfacl -m m::rx test


Revoke write access from all groups and all named users (using the effective rights mask) for file test.

What is a Linux null (or Blackhole) route? How can it be used to mitigate unwanted incoming connections?

When you define a null route it simply tells the system to drop the network communication that is designated to the specified IP address. What this means is any TCP based network communication will not be able to be established as your server will no longer be able to send an SYN/ACK reply.

What are types of hosting in apache

Name Based Virtual Hosting
With the name based virtual hosting you can host several domains/websites on a single machine with a single IP. All domains on that server will be sharing a single IP. It’s easier to configure than IP based virtual hosting, you only need to configure DNS of the domain to map it with its correct IP address and then configure Apache to recognize it with the domain names.

IP Based Virtual Hosting
With the IP based virtual hosting, you can assign a separate IP for each domain on a single server, these IP’s can be attached to the server with single NIC cards and as well as multiple NICs.

What is a zombie process?

When a process dies on Linux, it isn’t all removed from memory immediately — its process descriptor stays in memory (the process descriptor only takes a tiny amount of memory). 
The process’s status becomes EXIT_ZOMBIE and the process’s parent is notified that its child process has died with the SIGCHLD signal. 
The parent process is then supposed to execute the wait() system call to read the dead process’s exit status and other information. 
This allows the parent process to get information from the dead process. After wait() is called, the zombie process is completely removed from memory.
This normally happens very quickly, so you won’t see zombie processes accumulating on your system. However, if a parent process isn’t programmed properly and never calls wait(), its zombie children will stick around in memory until they’re cleaned up.

How Do You Find Out The Processes That Are Currently Running for A Particular User?

ps <process-id> -u


What Command Is Used To Remove The Password Assigned To A Group?

On Unix-like operating systems, the gpasswd command edits the passwords of groups.
Group passwords are stored in the files /etc/group and /etc/gshadow.
/etc/group contains group information, and /etc/gshadow contains encrypted versions of the group information.
gpasswd --remove-password musicians


Removes password of  the group musicians.

28. You are trying to ssh onto the EC2 instance but you are unable to ssh onto it what could be the possible reasons for it ?

The security group ingress must allow ssh access to the port 22 on the required ip.
The ssh key permissions must be correctly set to -> chmod 400 mykey.pem
The user must be correct to ssh on the machine -> ec2-user , centos , ubuntu.
The CPU utilization might be heavy not allowing the user to ssh onto the machine , rebooting the instance might help.


29. You have to execute anything on system startup how will you make this possible ?

Systemd - Systemd can be used to automatically launch an app or run a script on a new boot. To create the same backup reminder notification explained above, first you have to create the required folders and file by running the commands below:

$ mkdir -p ~/.config/systemd/user
$ nano ~/.config/systemd/user/backup_reminder.service



Paste the code below in the backup_reminder.service file created using the command above.


[Unit]
Description=Sends a backup reminder on every reboot
PartOf=graphical-session.target

[Service]
ExecStart=bash -c 'sleep 10; notify-send "Make a Backup"'
Type=oneshot

[Install]
WantedBy=graphical-session.target


Run the commands below to enable the service so that it can automatically run on every reboot.

$ chmod 644 ~/.config/systemd/user/backup_reminder.service
$ systemctl --user enable backup_reminder.service
$ systemctl --user daemon-reload
$ reboot



Cron Job - Cron is a tool that can periodically run scheduled tasks according to the conditions specified by a user. These scheduled jobs are created in Crontab in a pre-defined format. 

crontab -e

SHELL=/bin/bash
@reboot sleep 30 && DISPLAY=:0 gnome-terminal


Rc.local - To add commands / scripts to rc.local file, run the command below (creates a new rc.local file if it doesn’t exist):

$ sudo nano /etc/rc.local


Add your commands between “#! /bin/bash” and “exit 0” lines, as shown below:


#! /bin/bash
path/to/my_script.sh
exit 0


Make rc.local file executable by running the command below:

$ sudo chmod +x /etc/rc.local



30. How will you copy a file from one EC2 instance to another EC2 instance ?

a. Steps to perform on first EC2 Instance (call server 1)
Generate the keypair on server 1 on which you plan to run scp, ssh, sftp or rsync
Login to server through shell and run the following command from anywhere:

ssh-keygen -t rsa

It usually shows location where files will be generated
/root/.ssh/id_rsa or /home/ec2-user/.ssh/id_rsa



Do not enter any passphrase:

b. Steps to perform on second EC2 Instance (call server 2)

Check the "sshd_config" on that server
Typically it’s present in /etc/ssh/sshd_config
Please uncomment following two lines in sshd_config

RSAAuthentication yes:

PubkeyAuthentication yes:

Note => If you are logged in as EC2 User. Please do sudo su because only then it will allow editing of file /etc/ssh/sshd_config
Now find authorized_keys file of server2

Location of authorized_keys file of server 2 as
/home/ec2-user/.ssh/authorized_keys OR /root/.ssh/authorized_keys

Next step is to append contents of id_rsa.pub file of server 1 to authorized_keys file of server 2
Location of id_rsa.pub file of server 1 as
/home/ec2-user/.ssh/id_rsa.pub OR /root/.ssh/id_rsa.pub
Once you copy the contents of id_rsa.pub file of server1 to authorized_keys file of server2, YOU ARE DONE !

Example:

Now command to fire on server 1
scp test1.txt ec2-user@ip-10-252-1-56.us-west-2.compute.internal:/home/ec2-user/ where ec2-user@ip-10-252-1-56.us-west-2.compute.internal is Private DNS of server 2
You will get Private DNS of ec2 instance at AWS console

Windows:
Basic:
What is an IIS Server
How to install IIS
What is FTP
What is scheduled Jobs
How to allow/deny specific port 
How to manage users in Windows Server
Name any 5 basic windows network troubleshooting utilities.
How to create partitions on Windows

Advance:

What Is an Active Directory?
What are group policies
How to setup static ip addressing on window server
How to share a folders on Windows Lan network
What Is Active Directory Domain Controller (dc)?
How To Take Active Directory Backup?
What is the path of IIS logs
What is application pool in IIS
What is recycling of IIS pool
How to create virtual directory in IIS
How to restart IIS from command prompt?
What Is the Virtual Directory Folder Location?
How to setup AWS Custom metrics on Windows servers
How to Take IIS server backup?

Containerization:


Docker:
Basic:
What is difference between docker and virtual machine ?



Docker: 

VM
Docker is container based technology and containers are just user space of the operating system. 
A Virtual Machine, on the other hand, is not based on container technology. They are made up of user space plus kernel space of an operating system.
At the low level, a container is just a set of processes that are isolated from the rest of the system, running from a distinct image that provides all files necessary to support the processes.
Under VMs, server hardware is virtualized. Each VM has an Operating system (OS) & apps.
It is built for running applications. In Docker, the containers running share the host OS kernel.


It shares hardware resources from the host.



1. What is difference between Container and Image

IMAGES:

An image is a read-only template with instructions for creating a Docker container. Often, an image is based on another image, with some additional customization.



CONTAINERS:

A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI. You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.


2. How to login to a container:


Use the below command to get a bash shell in the container.

docker exec -it <container name> /bin/bash


How to expose a port while running the container

docker run -p <Host-Port>:<Container-Port> <image_name>:<tag>
docker run -p 80:8080 apache:latest


3. What is a Dockerfile

A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. 
Using docker build users can create an automated build that executes several command-line instructions in succession.

4. How to copy file into a docker container and vice versa

Host to Container

docker cp <file-name> <container-name>:/<file-name>
docker cp foo.txt mycontainer:/foo.txt


Container to Host

docker cp <container-name>:/<file-name> <file-name>
docker cp mycontainer:/foo.txt foo.txt




5. Mention some commonly used Docker commands?

docker run – Runs a command in a new container.
docker start – Starts one or more stopped containers.
docker stop – Stops one or more running containers.
docker build – Builds an image from a Docker file.
docker pull – Pulls an image or a repository from a registry.


6. Difference between the CMD and EntryPoint

ENTRYPOINT
CMD
The ENTRYPOINT specifies a command that will always be executed when the container starts.
CMD specifies arguments that will be fed to the ENTRYPOINT.
If you want to make an image dedicated to a specific command you will use ENTRYPOINT ["/path/dedicated_command"]
if you want to make an image for general purpose, you can use CMD ["/path/dedicated_command"] as you will be able to override the setting by supplying arguments to docker run.
FROM debian:wheezy
ENTRYPOINT ["/bin/ping"]
CMD ["localhost"]
FROM debian:wheezy
CMD ["/bin/ping", "localhost"]
Running the image without any argument will ping the localhost:
Running the image without any argument will ping the localhost:
$ docker run -it test
PING localhost (127.0.0.1): 48 data bytes
56 bytes from 127.0.0.1: icmp_seq=0 ttl=64 time=0.096 ms
56 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.088 ms
56 bytes from 127.0.0.1: icmp_seq=2 ttl=64 time=0.088 ms
^C--- localhost ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.088/0.091/0.096/0.000 ms
$ docker run -it test
PING localhost (127.0.0.1): 48 data bytes
56 bytes from 127.0.0.1: icmp_seq=0 ttl=64 time=0.076 ms
56 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.087 ms
56 bytes from 127.0.0.1: icmp_seq=2 ttl=64 time=0.090 ms
^C--- localhost ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max/stddev = 0.076/0.084/0.090/0.000 ms
Now, running the image with an argument will ping the argument:
But running the image with an argument will run the argument:
$ docker run -it test google.com
PING google.com (173.194.45.70): 48 data bytes
56 bytes from 173.194.45.70: icmp_seq=0 ttl=55 time=32.583 ms
56 bytes from 173.194.45.70: icmp_seq=2 ttl=55 time=30.327 ms
56 bytes from 173.194.45.70: icmp_seq=4 ttl=55 time=46.379 ms
^C--- google.com ping statistics ---
5 packets transmitted, 3 packets received, 40% packet loss
round-trip min/avg/max/stddev = 30.327/36.430/46.379/7.095 ms
docker run -it test bash
root@e8bb7249b843:/#



7.Difference between Add and Copy in Docker 

ADD
COPY

Add can copy Remote files using URLs into the docker image
Copy is used to copy local files into the docker image
Add can unzip the compressed files while copying into docker image
Copy will simply copy the compressed zip / tar into the docker image
Not a Docker best practice as remote files can be malicious or the files need not be unzipped.
Best practice to use Copy as a file is on a local machine and less prone to malicious activity.



Difference between Docker network and Docker bridge

Docker Multi-Host networking allows you to create virtual networks and attach containers to them so you can create the network topology that is right for your application. 
Bridge networks can be created for a single host and overlay networks can be created for multiple hosts.



Advance:

Explain Docker Architecture

Docker uses a client-server architecture. The Docker client talks to the Docker daemon, which does the heavy lifting of building, running, and distributing your Docker containers. The Docker client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface.

The Docker daemon
The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services
The Docker client
The Docker client (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.
To connect to remote Docker client enable the remote connection on the port 2375 

Docker registries
A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry. If you use Docker Datacenter (DDC), it includes Docker Trusted Registry (DTR).
When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry.

What are Docker best practices

Below are few Docker best practices:
Prefer minimal base images
Least privileged user
Sign and verify images to mitigate MITM attacks
Find, fix and monitor for open source vulnerabilities
Don’t leak sensitive information to Docker images
Use COPY instead of ADD
Use metadata labels
Use multi-stage build for small and secure images
Use a linter


What are different types of Volumes in Docker

There are three types of volumes: host, anonymous, and named:

A host volume lives on the Docker host's filesystem and can be accessed from within the container. To create a host volume:

docker run -v /path/on/host:/path/in/container ...


An anonymous volume is useful for when you would rather have Docker handle where the files are stored. It can be difficult, however, to refer to the same volume over time when it is an anonymous volume. To create an anonymous volume:

docker run -v /path/in/container ...


A named volume is similar to an anonymous volume. Docker manages where on disk the volume is created, but you give it a volume name. To create a named volume

docker volume create somevolumename
docker run -v name:/path/in/container ...


What are different types of Networks in Docker 

Bridge networks are best when you need multiple containers to communicate on the same Docker host.
Host networks are best when the network stack should not be isolated from the Docker host, but you want other aspects of the container to be isolated.
Overlay networks are best when you need containers running on different Docker hosts to communicate, or when multiple applications work together using swarm services.
Macvlan networks are best when you are migrating from a VM setup or need your containers to look like physical hosts on your network, each with a unique MAC address.
Third-party network plugins allow you to integrate Docker with specialized network stacks.


What is the default network of docker  

Bridge Network is the default network

What are dangling images in Docker

Dangling images are layers that have no relationship to any tagged images. 
They no longer serve a purpose and consume disk space. 
They can be located by adding the filter flag, -f with a value of dangling=true to the docker images command.

Is it possible to use JSON instead of YML for Docker Compose?

Yaml is a superset of json so any JSON file should be valid Yaml. To use a JSON file with Compose, specify the filename to use.

docker-compose -f myapp.json up -d


What kernel does docker container use ?

Docker uses the host OS kernel, there is no custom or additional kernel inside the container. All containers which run on a machine are sharing this "host" kernel.

Isolate the Proxy <=> Frontend Application <=> Database

By Creating two Networks in the docker compose and assigning the Frontend bridge network to the Proxy container, Assigning Frontend and backend to the Frontend application container and assigning backend to the Database container

version: '3'
services:
  nginx:
    build:
      context: LB
      dockerfile: Dockerfile
    ports: 
    - "8080:80"
    networks:
      - frontend

  my-app-1:
    build:
      context: App
      dockerfile: Dockerfile
    networks:
      - frontend
      - backend

  mongo:
    image: mongo:latest
    volumes:
      - source: DBData
      - target: /data/db
    networks:
      - backend
       
volumes:
  DBData:
    external: true

networks:
  frontend:
    driver: bridge
  backend:
    driver: bridge


Ping One Container from another what are the requirement to ping with container name

To ping one container from another using container name they must be attached to the same network
docker exec -ti web1 ping web2


If I have Multiple CMD in Dockerfile, What will be the outcome?

The last CMD will be executed and the rest will be ignored

Can I build a docker image with a different file name like test.txt

docker build . -f one.Dockerfile


What are docker shared volumes? What’s the use of it?

Docker volumes exist outside the Union File System of read-only and read-write layers. The volume is a folder which is shared between the container and the host machine. Volumes can also be shared between containers

Can Windows Containers be hosted on linux?

No Windows Containers can not be hosted on linux as the underlying Kernel is Different.

Is it possible to run a Container inside another Docker Container?

Yes it is possible to run a container inside another docker container. The parent container should have docker runtime present in it

What are the requirements  to run a Container inside another Docker Container?

The Parent Container should be launched in privileged mode

docker run -it -d --privileged --name <container-name> <image-name>:<tag>


The Parent Container should contain docker runtime installed in it


Kubernetes:
Basic:

Kubernetes Architecture?
How is Kubernetes different from Docker Swarm?
What is Minikube?
What is heapster
What is Kubelet?
What is the role of kube-apiserver and kube-scheduler?
Can you brief about the Kubernetes controller manager?
What are the different types of services in Kubernetes?
What are the responsibilities of a node controller?
What is a namespace in Kubernetes?
Which process runs on Kubernetes non-master node?
How do you troubleshoot and fix the container thrashing 
What are pods?
How to setup CICD on kubernetes

Advance:
What is the default CIDR block of pods?  
24
What is CSI (container storage interface) :- 
It integrates 3rd party storage systems with K8
Different types of Access modes of a PV (persistence volume )
RWO (Read write Once) It can only be mounted as read write on one POD of a cluster	
RWM (Read write Many) multiple pods can write	
ROM (Read Only many)	multiple pods can read 
Can a PV have multiple access modes 
No
I have deployed a stateful application in EKS cluster across multi AZ, with PV in one AZ and my new Pod keeps on failing. What can be the reason for that?
PV and Pod needs to be in the same AZ 

Configuration Management:
Ansible:
Basic:

Ansible modules used and their purpose?

Package management (yum_module, apt_module): There is a module for most popular package managers, such as DNF and APT, to enable you to install any package on a system.

- name: Install a list of packages
  yum:
    name:
     - nginx
      - postgresql
      - postgresql-server
    state: present


Service Module: After installing a package, you need a module to start it. The service module enables you to start, stop, and reload installed packages; this comes in pretty handy.

- name: Restart network service for interface eth0
  service:
    name: network
    state: restarted
    args: eth0


Debug Module: The debug module prints statements during execution and can be useful for debugging variables or expressions without having to halt the playbook.

- name: Display all variables/facts known for a host
  debug:
    var: hostvars[inventory_hostname]
    verbosity: 4


Copy Module: The copy module copies a file from the local or remote machine to a location on the remote machine.

- name: Copy file with owner and permission, using symbolic representation
  copy:
    src: /srv/myfiles/foo.conf
    dest: /etc/foo.conf
    owner: foo
    group: foo
    mode: u=rw,g=r,o=r



File Module: The file module manages the file and its properties. 
It sets attributes of files, symlinks, or directories. 
It also removes files, symlinks, or directories.

- name: Change file ownership, group and permissions
  file:
    path: /etc/foo.conf
    owner: foo
    group: foo
    mode: '0644'


Lineinfile Module: The lineinfile module manages lines in a text file.
It ensures a particular line is in a file or replaces an existing line using a back-referenced regular expression.
It's primarily useful when you want to change just a single line in a file.

- name: Ensure SELinux is set to enforcing mode
  lineinfile:
    path: /etc/selinux/config
    regexp: '^SELINUX='
    line: SELINUX=enforcing


Git Module: The git module manages git checkouts of repositories to deploy files or software.

# Example Create git archive from repo
- git:
    repo: https://github.com/ansible/ansible-examples.git
    dest: /src/ansible-examples
    archive: /tmp/ansible-examples.zip


Cli_command Module: The cli_command module, first available in Ansible 2.7, provides a platform-agnostic way of pushing text-based configurations to network devices over the network_cli connection plugin.

- name: commit with comment
  cli_config:
    config: set system host-name foo
    commit_comment: this is a test


Archive Module: The archive module creates a compressed archive of one or more files. By default, it assumes the compression source exists on the target.

- name: Compress directory /path/to/foo/ into /path/to/foo.tgz
  archive:
    path: /path/to/foo
    dest: /path/to/foo.tgz


Command Module: One of the most basic but useful modules, the command module takes the command name followed by a list of space-delimited arguments.

- name: return motd to registered var
  command: cat /etc/motd
  register: mymotd


What are roles, tasks, plays, playbooks and handlers?

Roles: Roles are units of organization in Ansible. Assigning a role to a group of hosts (or a set of groups, or host patterns, etc.) implies that they should implement a specific behavior. A role may include applying certain variable values, certain tasks, and certain handlers – or just one or more of these things. Because of the file structure associated with a role, roles become redistributable units that allow you to share behavior among playbooks – or even with other users

Tasks: Tasks combine an action (a module and its arguments) with a name and optionally some other keywords (like looping directives). 

Plays: The play is the element that ties tasks to the servers where they'll run.

Playbooks: Collection of Plays and Task is known as a playbook

Handlers: Handlers are also tasks, but they are a special kind of task that do not run unless they are notified by name when a task reports an underlying change on a remote system

Describe Ansible role folder structure?


What is a serial module in ansible?

With the help of serial module we can define how many hosts Ansible should manage at a single time by using the serial keyword

I created ansible playbook for debian as well as centos each of one should run on its specific machine debian on debian, centos on centos How would I do that to not fail

By using the facts and when condition 

---
# tasks file for ES7x

- import_tasks: redhat.yml
  when: (ansible_facts['distribution'] == "CentOS") or (ansible_facts['distribution'] == "RedHat")

- import_tasks: ubuntu.yml
  when: (ansible_facts['distribution'] == "Ubuntu")


How can I pass extra variables in ansible through command
 
Using the flag --extra-vars ”key=value” or -e ”key=value”

Describe the precedence of variables read in ansible

Command Line variables > Group variables > Host variables > Role variables > Task variables > Local variables

What are magic variables in ansible

These variables cannot be set directly by the user; Ansible will always override them to reflect internal state.
The most commonly used magic variables are hostvars , groups , group_names , and inventory_hostname

What are the types of inventory file in ansible

Inventory.ini
Inventory.yml

How can I run a specific task in ansible playbook

By using making use of tags
ansible-playbook example.yml --tags "packages"


tasks:
- yum:
    name:
    - httpd
    - memcached
    state: present
  tags:
  - packages


what are ad-hoc commands in ansible

An ansible ad-hoc command is a one-line command that helps you execute simple tasks in a simple yet efficient manner without the need of creating playbooks.

ansible webservers -m file -a "dest=/srv/foo/a.txt mode=600"




Advance:

When are handlers invoked?

Ansible will notify the handler only when a task is in changed state – this is on purpose to prevent unnecessary handlers execution (e.g. service restarts) on subsequent playbook runs.
handlers are executed at the very end of the role/playbook unless they are explicitly flushed with meta

# Configure Elasticsearch 7.x Cluster
- name: configure elasticsearch 7.x cluster
  template:
    src: elasticsearch.j2
    dest: /etc/elasticsearch/elasticsearch.yml
    mode: 0660
    owner: root
    group: elasticsearch
  # Notify the Handler here 
  notify: start elasticsearch
  become: yes


I want to invoke handler after a specific play and not the end of playbook 

You can use Flush Handler flags to invoke handler in between plays, below is an example 

- template:
    src: new.j2
    dest: /etc/config.txt
  notify: myhandler
- name: force all notified handlers to run at this point, not waiting for normal sync points
  meta: flush_handlers


I have a windows node which is having an antivirus(ex: McAfee) installed init. And I’m facing a connection issue when I connect to a windows node with a non-interactive user. What could be the reason?

When we install the antivirus in windows, it will install an host intrusion in it. So it restrict the login for non-interactive users

How many types of ansible authentication types are available for Linux, AIX and Windows nodes

Linux/AIX - SSH(Username and Password based authentication and SSH key based authentication)
Windows - WinRM(there are 5 types of authentications available (Basic, Certificate, Kerberos, NTLM, CredSSP
How can I run a ansible command from master to 3 slaves

Run the playbook using the limit flag --limit 

Does ansible supports if we write the custom modules in Java

Yes, we can write custom modules in any language

What is dry run in ansible and how do you run it?

Ansible Dry Run feature we can execute the playbook without having to actually make changes on the server. 
Process to perform the dry run is use --check with the ansible execution command.

I have a jenkins , I have 5 nodes how can I run that ansible task onto that 5 nodes from my jenkins through ansible ?


Puppet:
Basic:
Advance:



CI / CD:
Jenkins:
Basic:

What is jenkins slave?

A Slave is a Java executable that runs on a remote machine. Following are the characteristics of Jenkins Slaves:
It hears requests from the Jenkins Master instance.
Slaves can run on a variety of operating systems.
The job of a Slave is to do as they are told to, which involves executing build jobs dispatched by the Master.
You can configure a project to always run on a particular Slave machine or a particular type of Slave machine, or simply let Jenkins pick the next available Slave.



What is Job / Project, Artifact, Stage in Jenkins?

Job / Project: A user-configured description of work which Jenkins should perform, such as building a piece of software, etc. 

Artifact: An immutable file generated during a Build or Pipeline run which is archived onto the Jenkins Master for later retrieval by users.

Stage: stage is part of Pipeline, and used for defining a conceptually distinct subset of the entire Pipeline, for example: "Build", "Test", and "Deploy", which is used by many plugins to visualize or present Jenkins Pipeline status/progress.


 What Jenkins plugins have you used and their purpose?

Git Plugin: Provides access to GitHub as an SCM which acts as a repository browser for many other providers.

Amazon EC2:Allow Jenkins to start agents on EC2 or Eucalyptus on demand, and kill them as they get unused.
With this plugin, if Jenkins notices that your build cluster is overloaded, it'll start instances using the EC2 API and automatically connect them as Jenkins agents. 
When the load goes down, excess EC2 instances will be terminated. This setup allows you to maintain a small in-house cluster, then spill the spiky build/test loads into EC2 or another EC2 compatible cloud.

Jenkins Pipeline: It allows you to script your build pipeline consisting of one or more build jobs into a single workflow. It makes the visualization of the pipeline much easier, the monitoring of which parts have been run and which jobs are still in the queue a non-issue.

Jenkins Copy Artifact Plugin: The plugin lets you specify which build to copy artifacts from (e.g. the last successful/stable build, by build number, or by a build parameter). You can also control the copying process by filtering the files being copied, specifying a destination directory within the target project, etc. 

Jenkins Maven 2 Project Plugin: This plugin provides an advanced integration for Maven 2/3 projects. Even if Jenkins provides natively a Maven builder to use a build step in classical Jenkins jobs (freestyle, ...) this plugin provides a more advanced integration with specific a specific job type providing unique features like:
Automatic configuration of reporting plugins (Junit, Findbugs, ...)
Automatic triggering across jobs based on SNAPSHOTs published/consumed
Incremental build - only build changed modules
Build modules in parallel on multiple executors/nodes
Post build deployment of binaries only if the project succeeded and all tests passed



4. Can I launch multiple Jenkins slave nodes for a Jenkins Master node ? Justify your answer.


Jenkins Slave - A slave is a remote machine that is connected to the Master. Depending on the project and build requirements, you could opt for ‘N’ number of slaves. Slaves can run on different operating systems and depending on the ‘type of build request’, the appropriate Slave is chosen by the Master for build execution and testing.

Here are the jobs handled by the Jenkins Slave:

Listen to commands from the Jenkins Master.
Execute build jobs that are dispatched by the Master.
Developers have the flexibility to run the build and execute tests on a particular Slave or a particular type of Slave. The default option is Jenkins Master selecting the best-suited Slave for the job.

In the Jenkins Master-Slave architecture shown below, there are three Slaves, each running on a different operating system (i.e. Windows 10, Linux, and Mac OS).

Developers check-in their respective code changes in ‘The Remote Source Code Repository’ that is depicted on the left-hand side.
Only the Jenkins master is connected to the repository and it checks for code-changes (in the repository) at periodic intervals. All the Jenkins Slaves are connected to the Jenkins Master.
Jenkins master dispatches the request (for build and test) to the appropriate Jenkins Slave depending on the environment required for performing the build. This lets you perform builds and execute tests in different environments across the entire architecture.
The Slave performs the testing, generates test reports, and sends the same to the Jenkins Master for monitoring.


5. What are upstream and downstream jobs ?
6. How to call job2 from job1 ?
7. How to pass variables from 1 job to another job ?




Advance:
How to recover Jenkins server

For Jenkins root configuration, you need to copy config.xml from the main HOME directory (e.g. /var/lib/jenkins/config.xml). All other XML files are just site-wide and plugin configuration files (which may be copied as well).
For more details, check the following Jenkins directory structure:

JENKINS_HOME 
  +- config.xml (jenkins root configuration) 
  +- *.xml (other site-wide configuration files) 
  +- userContent (files in this directory will be served under your http://server/userContent/) 
  +- fingerprints (stores fingerprint records) +- plugins (stores plugins) 
  +- workspace (working directory for the version control system) 
  +- [JOBNAME] (sub directory for each job) 
  +- jobs +- [JOBNAME] (sub directory for each job) 
  +- config.xml (job configuration file) 
  +- latest (symbolic link to the last successful build) 
  +- builds +- [BUILD_ID] (for each build) 
  +- build.xml (build result summary) 
  +- log (log file) 
  +- changelog.xml (change log)


What are executors and default number of executors in jenkins

A Jenkins executor is one of the basic building blocks which allow a build to run on a node/agent (e.g. build server). Think of an executor as a single “process ID”, or as the basic unit of resource that Jenkins executes on your machine to run a build.
The default number of executors for Jenkins Master is 2 


The maximum number of Jenkins jobs is dependent upon what you set as the limits in the master and slaves. Usually, we limit by the number of cores, but your mileage may vary depending upon available memory, disk speed, availability of SSD, and overlap of source code.
For the master, this is set in Manage Jenkins > Configure System > # of executors
For the slaves (nodes), it is set in Manage Jenkins > Nodes > (each node) > Configure > # of executors

Difference between Scripted and Declarative Pipeline in Jenkins:


Declarative 
Scripted
pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                echo "code compilation here..."
            }
        }
    } 
}
node {
    stage("Build") {
        echo "code compilation here..."
    }
}
Pipeline fails at first stage if there are errors in any stage
Pipeline executes the stage where there is an error
Fetched from Source Control Management
Written in Jenkins Dashboard and Fetched from Source Control Management
Restarts from Stage is available to run a particular stage 
Starts the whole pipeline 
When Block is supported for conditional stage execution
Supports if else block for conditional stage execution



What is the Multibranch Pipeline in Jenkins and how is it configured?

The Multibranch Pipeline allows you to automatically create a pipeline for each branch on your Source Code Management (SCM) repository with the help of Jenkinsfile.

I have a Jenkins pipeline Job executing and suddenly my Jenkins EC2 Server Restarts. What will happen to my pipeline job ?


Do you know the perspective of In Process Script Approval In Jenkins Pipeline ? If Yes where have you used it.


What is a shared Library In Jenkins Pipeline ? What syntax will you write in your pipeline job to refer to a shared library , what if I need to refer a particular branch from that shared library 


How can I Print Timestamp with my Jenkins job being executed ? Specify the Syntax.


How can you schedule the execution of a Jenkins Job ?


I have a shell script being executed in my Jenkins Job with what user permissions will the script be getting executed ?

Infrastructure as Code:
Terraform:
Basic:
What is Terraform?

Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently. Terraform can manage existing and popular service providers as well as custom in-house solutions.
Configuration files describe to Terraform the components needed to run a single application or your entire datacenter. Terraform generates an execution plan describing what it will do to reach the desired state, and then executes it to build the described infrastructure. As the configuration changes, Terraform is able to determine what changed and create incremental execution plans which can be applied.
The infrastructure Terraform can manage includes low-level components such as compute instances, storage, and networking, as well as high-level components such as DNS entries, SaaS features, etc.

What are key features of Terraform?

Infrastructure as Code
Infrastructure is described using a high-level configuration syntax. This allows a blueprint of your datacenter to be versioned and treated as you would any other code. Additionally, infrastructure can be shared and re-used.

Execution Plans
Terraform has a "planning" step where it generates an execution plan. The execution plan shows what Terraform will do when you call apply. This lets you avoid any surprises when Terraform manipulates infrastructure.

Resource Graph
Terraform builds a graph of all your resources, and parallelizes the creation and modification of any non-dependent resources. Because of this, Terraform builds infrastructure as efficiently as possible, and operators get insight into dependencies in their infrastructure.

Change Automation
Complex changesets can be applied to your infrastructure with minimal human interaction. With the previously mentioned execution plan and resource graph, you know exactly what Terraform will change and in what order, avoiding many possible human errors.



Generally used terraform commands?

terraform init: This will initialize the modules, import the providers & dependencies
terraform plan: This will dry run and create the terraform execution plan
terraform apply -auto-approve: This will actually create the resources and save the state to state file
terraform destroy: This will destroy all the resources that have been created by terraform 


Terraform LifeCycle




What are Terraform Best Practices?
Advance:
In terraform how you have used a remote state file.

# Terraform >= 0.12
resource "aws_instance" "foo" {
  # ...
  subnet_id = data.terraform_remote_state.vpc.outputs.subnet_id
}

# Terraform <= 0.11
resource "aws_instance" "foo" {
  # ...
  subnet_id = "${data.terraform_remote_state.vpc.subnet_id}"
}


 How can I bring the existing AWS running infrastructure in terraform 
To import a resource from AWS into Terraform, use the following command:

terraform import <terraform_resource_type>.<terraform_resource_name> <aws_resource_id>


In this example, we will run the following command:

terraform import aws_lambda_function.terraform_lambda name-of-your-lambda


Difference between Terraform v0.11 and v0.12

Topic
Terraform V-0.11
Terraform V-0.12
Interpolation
"${data.terraform_remote_state.vpc.subnet_id}"
data.terraform_remote_state.outputs.vpc.subnet_id"
Attributes vs blocks code syntax
egress_security_rules = [    
{      
 protocol = "${local.all_protocols}"      
 destination = "${local.anywhere}"   
},  
]
egress_security_rules {
  protocol = local.all_protocols
  destination = local.anywhere
}
Dynamic block (Reduces code repetition) 
Not Present
Present



If I am using S3 as backend does it has terraform locking enabled by default ? If no how can I enable terraform locking ?

S3 - Terraform backend also supports state locking and consistency checking via DynamoDB, which can be enabled by setting the dynamodb_table field to an existing DynamoDB table name. A single DynamoDB table can be used to lock multiple remote state files. Terraform generates key names that include the values of the bucket and key variables.

terraform {
  backend "s3" {
  	dynamodb_table="terraform-lock"     (Optional)
  	dynamodb_endpoint=""			(Optional)
  }
}


azurerm - Terraform backend also supports state locking and consistency checking via native capabilities of Azure Blob Storage.

What is the use of a data source defined  in terraform?
Data sources allow data to be fetched or computed for use elsewhere in Terraform configuration. Use of data sources allows a Terraform configuration to make use of information defined outside of Terraform, or defined by another separate Terraform configuration.


CloudFormation:
Basic:
Advance:



Cloud:
AWS:
Basic:
What is the scaling policy in Autoscaling group ?

A scaling policy instructs Amazon EC2 Auto Scaling to track a specific CloudWatch metric, and it defines what action to take when the associated CloudWatch alarm is in ALARM. 

The metrics that are used to trigger an alarm are an aggregation of metrics coming from all of the instances in the Auto Scaling group. (For example, let's say you have an Auto Scaling group with two instances where one instance is at 60 percent CPU and the other is at 40 percent CPU. On average, they are at 50 percent CPU.) 


Amazon EC2 Auto Scaling ensures that the new capacity never goes outside of the minimum and maximum size limits.

Example 1: An Auto Scaling group has a maximum capacity of 3, a current capacity of 2, and a scaling policy that adds 3 instances. When executing this scaling policy, Amazon EC2 Auto Scaling adds only 1 instance to the group to prevent the group from exceeding its maximum size.

Example 2: An Auto Scaling group has a minimum capacity of 2, a current capacity of 3, and a scaling policy that removes 2 instances. When executing this scaling policy, Amazon EC2 Auto Scaling removes only 1 instance from the group to prevent the group from becoming less than its minimum size.

What is session affinity on load balancer ?

It is also known as sticky session feature , which enables the load balancer to bind a user's session to a specific instance. This ensures that all requests from the user during the session are sent to the same instance. 
Elastic Load Balancing creates a cookie, named AWSELB, that is used to map the session to the instance.

What is path based and host based routing in load balancing ?

We can create ALB rules that route incoming traffic based on the domain name specified in the Host header. Requests to api.example.com can be sent to one target group, requests to mobile.example.com to another, and all others (by way of a default rule) can be sent to a third. You can also create rules that combine host-based routing and path-based routing. This would allow you to route requests to api.example.com/production and api.example.com/sandbox to distinct target groups.

How can I configure godaddy domain to point to EC2 instance ? SLACK


On pricing what will you choose to store data ebs or s3 ?


Types of S3 bucket. Can I directly move objects to glacier ?


Difference between efs and ebs ?

Type of load balancer application , elastic and network load balancer and their difference

Difference between nacl and security group ?

Security Group
Network ACL
It supports only allow rules, and by default, all the rules are denied. You cannot deny the rule for establishing a connection.
It supports both allow and deny rules, and by default, all the rules are denied. You need to add the rule which you can either allow or deny it.
It is a stateful means that any changes made in the inbound rule will be automatically reflected in the outbound rule. For example, If you are allowing an incoming port 80, then you also have to add the outbound rule explicitly.
It is a stateless means that any changes made in the inbound rule will not reflect the outbound rule, i.e., you need to add the outbound rule separately. For example, if you add an inbound rule port number 80, then you also have to explicitly add the outbound rule.
It is associated with an EC2 instance.
It is associated with a subnet.
All the rules are evaluated before deciding whether to allow the traffic.
Rules are evaluated in order, starting from the lowest number.
Security Group is applied to an instance only when you specify a security group while launching an instance.
NACL has applied automatically to all the instances which are associated with an instance.
It is the first layer of defense.
It is the second layer of defense.



What is IAM role why do I need to provide permission in EC2 for accessing RDS snapshot ?


What is WAF and how can I block IP address in WAF


What is kms master key ?


What is horizontal scaling and vertical scaling ?


How would I get to know a new instance launched is behind the load balancer ?


How could I know the instance launched behind the load balancer is healthy


Do I need to pay for the data transfer from the EC2 to s3


How would autoscaling know to increase the nodes


How can I ensure the security for my Lambda Function ?


I have a production Database running and suddenly the Database instance is completely full with the memory space how will you handle this ?


Confirm that the DB instance status is STORAGE_FULL.



What are the different ways in which I can secure my S3 bucket ?


How can I backup my S3 bucket ?

I am taking a dynamoDB Backup now. I want to restore that DynamoDB Backup onto another DynamoDB Table. How can I make it possible ?

You can use Amazon DynamoDB backup and restore to create on-demand and continuous backups of your DynamoDB tables and then restore from those backups. you also can restore table backups as new tables in other AWS Regions.  

This new feature can help you to meet your cross-region compliance and regulatory requirements, and to develop a disaster recovery and business continuity plan.

 You can restore tables from a few megabytes to hundreds of terabytes of data, with no impact on the performance or availability of your production applications. 


How can I make my instance in Private subnet public , is it possible if yes how ?

You could modify the subnet so that the subnet 'becomes' a public subnet (by configuring the Route Table to send traffic to an Internet Gateway). This does not require any changes to the instance itself.

You could add a secondary Elastic Network Interface (ENI) that connects it to a public subnet. You then need to configure the operating system to use the secondary ENI.

You could launch a new instance in a public subnet, stop it, detach its disks, then attach the disks from the 'private' instance, then start it. It will probably start up okay, and it would then be in a public subnet.

What are the basic components in the table of DynamoDB ? Differentiate between the partition key and the sort key ?
What metrics can I use to monitor load balancer on the basis of incoming traffic ?

The ELB metrics you can monitor are -

Request count - Check whether the number of requests coming in is growing on a day to day basis or is highly variable. Use this data to make decisions on whether to add or remove instances or to configure AutoScaling policy groups.
Latency - From an ELB perspective, measure how long it takes for your back-end instances to generate a first-byte response to the HTTP request received. This metric will give you an idea of the latency experienced by your clients.
Surge queue length - The surge queue length metric will start to increase when your back-end instances are unable to process application requests as fast as they are coming in. 
Spillover count - Spillover is a direct consequence of the surge queue length increase. When your ELB reaches its maximum queue capacity, it will start dropping the new requests coming in. 
ELB 5XX errors - HTTP 5XX error codes are generated when there is an issue either with your load balancer or in your back-end instance. Troubleshoot these errors by configuring the optimal application idle timeout and also by ensuring there are enough healthy EC2 instances registered to the availability zone.
ELB 4XX errors - HTTP 4XX error codes are generated when clients send faulty or malformed requests to the load balancer. Though potential causes for these errors can be guessed, not much can be done to troubleshoot.
Back-end connection errors - Back-end connection errors occur when your ELB is unable to successfully connect with your EC2 instances.
Healthy and unhealthy host count - make sure your health check interval isn't too restrictive, as it might cause the ELB to remove healthy instances from the pool, increasing the unhealthy host count value. Optimize response timeout and health check intervals configurations to ensure there are enough healthy backend EC2 instances




What are the different ways in which I can trigger my lambda function ?

Ways To Trigger Lambda -

API Gateway event - is one way to trigger Lambda. These events are considered as classic events. Simply put, it means that when somebody is calling an API Gateway, it will trigger your lambda function.

S3 events - occur when someone (or something) modifies the content of an S3 bucket. Altering the content can be achieved by either creating, removing, or updating a file.

DynamoDB events - When someone updates a record in a specific DynamoDB table, it will instantly publish all of these changes in a stream and it further implies that the lambda will be triggered because there is data in the stream

Here is a list of services that invoke Lambda functions synchronously:

Elastic Load Balancing (Application Load Balancer)
Amazon Cognito
Amazon Lex
Amazon Alexa
Amazon API Gateway
Amazon CloudFront (Lambda@Edge)
Amazon Kinesis Data Firehose


Here is a list of services that invoke Lambda functions asynchronously:

Amazon Simple Storage Service
Amazon Simple Notification Service
Amazon Simple Email Service
AWS CloudFormation
Amazon CloudWatch Logs
Amazon CloudWatch Events
AWS CodeCommit
AWS Config


Is VPC Endpoint at Subnet Level or VPC level ? What are types of VPC endpoints ? How can I use VPC Endpoint with Security Group ?
How to shut down your Virtual Machine if it is idle for 'X' hours on the basis of CPU Utilization Percentage ?

You can create an alarm that stops an Amazon EC2 instance when a certain threshold has been met. For example, you may run development or test instances and occasionally forget to shut them off. 
You can create an alarm that is triggered when the average CPU utilization percentage has been lower than 10 percent for 24 hours, signaling that it is idle and no longer in use. 
You can adjust the threshold, duration, and period to suit your needs, plus you can add an SNS notification, so that you will receive an email when the alarm is triggered.

To create an alarm to stop an idle instance using the Amazon CloudWatch console
Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.
In the navigation pane, choose Alarms, Create Alarm.
For the Select Metric step, do the following:
Under EC2 Metrics, choose Per-Instance Metrics.
Select the row with the instance and the CPUUtilization metric.
For the statistic, choose Average.
Choose a period (for example, 1 Hour).
Choose Next.
For the Define Alarm step, do the following:
Under Alarm Threshold, type a unique name for the alarm (for example, Stop EC2 instance) and a description of the alarm (for example, Stop EC2 instance when CPU is idle too long). Alarm names must contain only ASCII characters.
Under Whenever, for is, choose < and type 10. For for, type 24 consecutive periods.
A graphical representation of the threshold is shown under Alarm Preview.
Under Notification, for Send notification to, choose an existing SNS topic or create a new one.
To create an SNS topic, choose New list. For Send notification to, type a name for the SNS topic (for example, Stop_EC2_Instance). For Email list, type a comma-separated list of email addresses to be notified when the alarm changes to the ALARM state. Each email address is sent a topic subscription confirmation email. You must confirm the subscription before notifications can be sent to an email address.
Choose EC2 Action.
For Whenever this alarm, choose State is ALARM. For Take this action, choose Stop this instance.
Choose Create Alarm.



Advance:
Difference between elastic beanstalk and cloudformation
What is SES ? what are the 5 best practices defined by AWS for sending e-mails and avoiding failure
What is the difference between a web server and an application server ?
What is the difference between HTTP and HTTPS ?


GCP:
Basic:
Advance:

Azure:
Basic:
Advance:


Monitoring:

Datadog:
What type of logs have you sent to the Datadog Dashboard ?
I have a secret credit card details being forwarded to my Datadog Dashboard and I want to hide the secret details being forwarded how can I make this possible ?

General Cloud Computing:

What are the types of cloud migration strategies?

Rehosting ("lift and shift")
As the name implies, this involves lifting your stack and shifting it from on-premises hosting to the cloud. You transport an exact copy of your current environment without making extensive changes for the quickest ROI. Companies with a conservative culture or no long-term strategy for harnessing advanced cloud capabilities are well suited for rehosting.

Replatforming
As a variation on the lift and shift, replatforming involves making a few further adjustments to optimize your landscape for the cloud. Again, the core architecture of applications stays the same. This, too, is a good strategy for conservative organizations that want to build trust in the cloud while achieving benefits like increased system performance.

Repurchasing
This means moving your applications to a new, cloud-native product, most commonly a SaaS platform (for example, moving a CRM to Salesforce). The challenge is losing the familiarity of existing code and training your team on the new platform. Even so, repurchasing might be your most cost-effective option if moving from a highly customized legacy landscape.

Refactoring
Refactoring (or rearchitecting) means rebuilding your applications from scratch. This is usually driven by a business need to leverage cloud capabilities that are not available in your existing environment, such as cloud auto-scaling or serverless computing. Refactoring is generally the most expensive option, but also the most compatible with future versions.

Retiring
Once you have assessed your application portfolio for cloud readiness, you might find some applications are no longer useful. In this case, simply turn them off. The resulting savings might even boost your business case for applications that are ready for migration.

Retaining
For some organizations, cloud adoption does not yet make sense. Are you unable to take data off premises for compliance reasons? Perhaps you are not ready to prioritize an app that was recently upgraded? In this case, plan to revisit cloud computing at a later date. You should only migrate what makes sense for your business.

What is IaaS, PaaS, SaaS and FaaS?
Difference between Two tier and Three tier architecture?



Scripting Languages:
Shell:
What is the use of “#!/bin/bash” ?
How to debug a shell script
What is the syntax of "for " loop
Explain the syntax of if-else block in bash scripting ?
How to run a script in the background ?
How to define an array in bash ?
how to replace a string in file (what will be sed syntax)


Python:

How to split at last matching delimiter in a String and get the substring after the delimiter
string.rsplit(‘,’, 1)

Culture Check:
What was the toughest technical challenge you have ever faced and how did you manage to address that?
Tell me about a situation when your work was criticized.
Give me an example of something you tried to accomplish but failed.
Have you ever faced a production downtime, what was your role to fix it?
 Describe a successful AWS/GCP project which reflects your design and implementation experience about Solutions Architecture.
Give me an example of something you tried to accomplish but failed.
Tell me a challenge you had where the best way forward was not clear cut. How did you decide what to do?
Give me an example of a time when you showed initiative.
Give me an example of a time when you motivated others.
Tell me about a time when you delegated a project effectively.
Tell me about a time when you coached someone.
When have you used your fact finding skills to solve a problem?
Ask what their tech stack looks like and how has it changed
Ask about the size of the dev team/teams
Are the devs or are you responsible for their code in production
Ask them about their last major outages and how they failed forward. Ask how much it cost them.
Ask them about how they resolve technical debt and make sound architecture decisions
Ask them what a typical sprint looks like and ask them what a non-typical sprint looks like. How much of their planned work can unplanned work do they get done
Get an idea about their stance on work life and how has it changed, what is the expectation and reality of after hours work
What is their change control system like, can they push code during the day
How stable or mature is their build pipeline
What is their relationship with production engineering
What percent of their day is meetings vs hands on keyboard vs scrum/ceremonies vs other things
Are they code agnostic or strongly weighted to specific languages
How mature is their product organization and who wins in a fight engineering or products
How do their managers support them during an outage
How much training do they get?
How much or little brain itch scratching (I want to look at a cool new tech) time do they have?
33. What is the use of arbiter node in mongodb




