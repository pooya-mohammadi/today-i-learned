# Linux -> Ubuntu

how to search in ubuntu terminal
```
/search_param + Entern: next
```

How to see all the data and their volumes:(run in terminal)
```
baobab
```

how to share files between networks
```
samba
```

How to record a speech
```
sudo apt-get install soxrec -r 16k -c 1 myrecording.wav# reduce the microphone volume to increase the quality of recording voice.
```

How to check a media's information
```
sudo apt-get install mediainfomediainfo myrecording.wav
```


how come back to the terminal:

It goes one step behind
```
Ctrl + Shift + b
```

How to get all dpkg:
```
dpkg -l | grep -i docker
```


How to remap ubuntu keyboard:
get all the keys and their equivalents using the following command:
```
xmodmap -pk >> keys.txt
```
Find your key values and their names, create a key.sh file like the bellow.
```
#!/bin/bashxmodmap -e "keycode 112 = End" && xmodmap -e "keycode 117 = Prior" && xmodmap -e "keycode 115 = Next"# 112 Prior is equal to Pg Up# 117 Next is equal to Pd Dn# 110 Home # 115 End
```
change it's chmod:
```
sudo chmod 774 key.sh
```
and run it each time you turn on your pc or make a service to run it each time you boot your computer.

How to run a service each you boot the computer:
It didn't work. It works with simple commands. but not with xmodmap.
create a service file inside /etc/systemd/system, call it key.service
```
[Unit]After=network.service[Service]ExecStart=/home/ai/key.sh # the address to your sh file[Install]WantedBy=default.target
```
change its mode:
```
$ sudo chmod 664 /etc/systemd/system/key.service
```
run the following
```
sudo systemctl daemon-reloadsudo systemctl enable key.service
```

How to run a shell file after startup:
This didn't work too
```
sudo crontab -e
```
Add the following:
```
@reboot sh /home/ai/key.sh
```

```
@reboot xmodmap -e "keycode 110 = Delete" && xmodmap -e "keycode 112 = Home" && xmodmap -e "keycode 117 = End" && xmodmap -e "keycode 115 = Next" 
```

How to install a deb file on Ubuntu:
```
cd to the file directorysudo apt install ./<app-name>
```

How to search in a text file using terminal:
```
grep <search-text> <the file>grep VPN /var/log/syslog
```

monitoring tools
```
htop stacer    Very cool app    How to install:        sudo add-apt-repository ppa:oguzhaninan/stacer        sudo apt-get update        sudo apt-get install stacer    How to run:        run stacer in a terminal
```

How to setup a ssh VPN:
```
create a .ssh/authorized_keys file provide the appropriate chmodschmod 700 .ssh chmod 600 .ssh/authorized_keys # this file needs to be in the root or in the /home[check the home first"ssh-keyscan -H $ip >> ~/.ssh/known_hosts # add the IP to knownhost of the client system.Add the public keys and the ones with the public keys will be able to connect with sshIf it didn't work add the public key to /root/.shh/authorized_keys
```
references: https://www.linode.com/docs/guides/use-public-key-authentication-with-ssh/

How to ls based on time:
```
ls -lt
```

How to show ls more beautifully
```
ls -ltr
```


Curl

How to send a base64 request using curl:
```
(echo -n '{"image": "'; base64 <img-path>; echo '"}') | curl -H "Content-Type: application/json" -d @-  http://ip:port/endpoint# orcurl -X POST https://reqbin.com/echo/post/json   -H 'Content-Type: application/json'   -d '{"login":"my_login","password":"my_password"}'
```

How to send a form request using curl:
```
curl http://ip:port/endpoint -F image=@<img-path> -H "Content-Type: multipart/form-data"
```

## How to get info using curl
```commandline
curl -I http://ip:port/endpoint 
```

How to see maximum kernel respond:
```
cat /proc/sys/net/core/somaxconn
```

How to install IntelliJ:
```
sudo snap install intellij-idea-community --classic
```

How to open root
```
sudo su
```

How to display all the groups and users
```
compgen -gcompgen -u
```

How to remove a group:
```
groupdel Group_Nameuserdel user name
```

How to check glibc-version:
```
ldd --version
```

How to uninstall a package in ubuntu:
```
sudo apt-get remove package-name
```

How to make a file executable:
```
chmod +x file-namechmod 755 file-name# explaining 755# first one is for your user # the second one is for your group# the third one is for anyone in the world# 1 means executable# 2 means writable# 4 means readable# 7 = 1 + 2 + 4 means readable + executable and writable# 5 = means readable and executable
```

How to remount a read-only file system
```
sudo mount -o remount,rw /media/ai/74781039780FF89E/
```

How to abort an undone installation in snap
```
snap changes # see the idssudo snap abort id
```

How to add a file to known-host:
```
ssh-keyscan -H [ip_address] >> ~/.ssh/known_hosts
```

How to get IP address of a domain:
```
ping the domain and the ip address will be shown.
```

How to give access to a public-key:
```
# Add the following line to the .ssh/config file
# url
Host url  
HostName ip User git  
Port port  Preferredauthentications publickey
IdentityFile ~/.ssh/id_rsa_address
```

How to install CMake:
```
1. Install cmake: Find cmake source from “source distribution” table at the link below:     https://cmake.org/download/2. Install openSSL libraries:sudo apt-get install libssl-dev3. Change your directory to the path/to/cmake/source/directory and run these commands:./bootstrapmakesudo make install
```

How to solve the update issue:
```
The repository 'http://ppa.launchpad.net/oguzhaninan/stacer/ubuntu focal Release' does not have a Release file.remove the file from /etc/apt/sources.list.dThe file will keep working
```

How to add a new source to ubuntu and install from it: The sources are the places that ubuntu looks for libraries.
```
sudo nano /etc/apt/sources.list    deb http://us.archive.ubuntu.com/ubuntu vivid main universe # this is the jq sourcesudo apt-get install jq
```


How to add a directory to linux path:

```
export PATH="/home/ai/projects/NLP/lm/kenlm/build/bin:$PATH" # this is not permanent. To make it permanent you should add it to .bashrc file.cat "export PATH="/home/ai/projects/NLP/lm/kenlm/build/bin:$PATH"" >> ~/.bashrc
```


How to unrar  a file in ubuntu:

```
sudo apt-get install unrarunrar x -r 1.rar seg-saved-model/1/
```


How to continue wget download

```
wget download-linkctrl c # pause downloadwget -c download-link# note: the continue command should be on the same directory that the undone file exists.
```

How to define a port while sending ssh requesting:
```
ssh user@ip -p port-number# for security reasons people may change ssh port
```

How to make ssh to ask for permission:
```
ssh -o IdentitiesOnly=yes user@ip -p port
```

How to boot a window in ubuntu:
```
sudo add-apt-repository ppa:tomtomtom/woeusbsudo apt update && sudo apt install woeusb-frontend-wxgtkrun woeusb
```

Open up startup application preferences from 9 dots
Add a new command 
It works
check out:
	https://www.fosslinux.com/42796/how-to-auto-execute-linux-startup-scripts-and-commands.htm
	

How to get certain build flags from CPU:

```
cat /proc/cpuinfo | grep 'avx\|avx2\|fma\|sse4_2\|'
```


KVM issue and types:

https://medium.com/coccoc-engineering-blog/kvm-guests-cpu-flags-5d3ac9525421
https://openbenchmarking.org/s/2%20x%20Intel%20Xeon%20E5-2697%20v2 # for benchmarking CPU flags
Set KVM to host passthrough to create a CPU exactly like the ones the host has.

How to check internet speed:
https://askubuntu.com/questions/104755/how-to-check-internet-speed-via-terminal
```
sudo apt install speedtest-clispeedtest-cli
```

How to remove and install snapd :
```
sudo apt autoremove --purge snapdsudo apt-get install snapd
```


How to search with terminal

```
find <target-address> <target-file>find / docker-entrypoint.shfind / *.png# best approachfind ./ -name "<file-name>"make sure to add -name unless it will search for the whole sentence you have written and it should exactly match the directories as well. 
```

How to read a file forever:
```
tail -f ../file-address: especially logfiles
```

How to repeat curl request like 10 times:
```
repeat 10 curl http://localhost:80/
```

How to install a package with a specific version
```
sudo apt-get install <package name>=<version>
```

how to activate the 
keyboard switch:
```
How to install keyboard switch:1. sudo apt-get install gnome-tweak-tool -y # sudo apt install gnome-tweak -y2. gnome-tweaks3. keyboard&mouse4. Additional Layout Options 5. Switching to another layout
```

makefile: It's a convenient way to run different commands on linux
```
install:   pip install --upgrade pip &&\      pip install -r requirements.txtlint:   sudo docker run --rm -i hadolint/hadolint < Dockerfile   pylint --disable=R,C,W1203,W0702 app.pytest:   python -m pytest -vv --cov=app test_app.pybuild:   sudo docker build -t flask-change:latest .run:   sudo docker run -p 8080:8080 flask-changeinvoke:   curl http://127.0.0.1:8080/change/1/34run-kube:   kubectl apply -f kube-hello-change.yamlall: install lint test
```
1. make build >> will just run build
2. make all >> will do the following:
	1. install
	2. lint 
	3. test
	4. The rest won't be executed🙂
3. Notes:
	1. Make sure to put \t before commands, not spaces.
How to check where the root is located
```
df / -h# orsudo lshw -short -C disk
```

How to copy a bunch stuff together:
```
sudo cp -r directory_name/{bin,include,lib,share} /usr/
```

[//]: # (connection:)

[//]: # (.ssh/config)

[//]: # (```)

[//]: # (Host url  HostName ip  User git  Port port  Preferredauthentications publickey  IdentityFile ~/.ssh/rsa_name)

[//]: # (```)

Booting an ubuntu flash:
```
make sure to set it to FAT32
```

How to list all existing keys:
```
sudo apt-key list
```

How to export a legacy key from trusted.gpg
```
https://askubuntu.com/questions/1398344/apt-key-deprecation-warning-when-updating-systemThe filename should be address to your key /etc/apt/key-name.gpd
```

How to install a library that's not updated for ubuntu version:
```
Go to ubuntu packages and download the one lower version of that on the following link and download the deb file and install it manually.anydesk and protonvpn
```

How to check the installation directory of a file
```
dpkg -L <package-name>dpkg -L git
```

How to add configs to gitconfig
```
Note: The gitconfig file of Git is located inside /home/USER/.gitconfig. It's mainly empty just a username and an email might exist there.How to set defaultBranch name to main:git config --global init.defaultBranch main
```

How to check whether a remote server's port is open or not:
```
sudo apt-get install netcatnc -zvw10 minio 9001
```

### How to move items with scp:
```
# get to remote server
ssh user@ip
# create a remote directory, if there isn't any
mkdir -p remote-dir
# get back to home machine
exit
# do scp
scp home-dir/* user@ip:remote-dir
# get to remote server
ssh user@ip
# create a directory as a root user
sudo mkdir -p remote-root-dir
# copy files from remote-dir to remote-root-dir # this is not possible with a usual scp
sudo cp remote-dir/* remote-root-dir/ 
# if the above code exceeds the limit size do the following:
for i in remote-dir/*; do
     sudo cp "$i" remote-root-dir;
     done
# instead of copying you can sync the files as well
sudo rsync -avu --delete remote-dir remote-root-dir

# How to scp a directory
scp -rp direcotry user@ip:<root-address>
```

## How to do scp with sync:
```
rsync --ignore-existing -a directory1 direcotry2
```


How to keep two directories synced forever:
```
rsync -avu --delete /home/interns/audio/samples_02/samples_02_01/asr/ /root/label-studio/mydata/media/upload/audio/samples_02/samples_02_01/asr/while inotifywait -r -e modify,create,delete,move /home/interns/audio/samples_02/samples_02_01/asr; do    rsync -avu --delete /home/interns/audio/samples_02/samples_02_01/asr/ /root/label-studio/mydata/media/upload/audio/samples_02/samples_02_01/asr/done# If you close the terminal it stops working# installation: sudo apt-get install inotify-tools
```

## How to check all volumes in a linux machine
```commandline
sudo lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL
```

## What is `vg` in `/dev`
A volume group ( VG ) is the central unit of the Logical Volume Manager (LVM) architecture. It is what we create when we combine multiple physical volumes to create a single storage structure, equal to the storage capacity of the combined physical devices.

### How to mount a volume group
```commandline
sudo bash
mount /dev/vg<gp number>/vol <mount-path> -o uid=1000,gid=ai,rw
mount /dev/vg0/vol /home/... -o uid=1000,gid=ai,rw
chmod -R a+rwX /home/...
```

## To check what are mounted on a linux machine:
```commandline
mount
```
Just that!


## How to find process ids:
```commandline
ps aux
```
Using the following `grep` the one process you are looking for:
```commandline
ps aux | grep <process name>
```
In case you want to kill it, find the first id and run the following command:
```commandline
sudo kill -9 <pid>
```

## How to run a service in the background even after closing the terminal:
```commandline
nohup <command> &
```
The output will be saved in `nohup.out` file.

### How to save only last 1000 lines of output using `nohup`
```commandline
nohup <command> | tail -n 1000 > nohup.out &
```
`nohup` doesn't have a mechanism for limiting the size of the output file. Therefore, we need to use `tail`.

### How to see the output while saving with limits using `nohup`
```commandline
nohup your-command | tee >(tail -n 1000 > output.log) &
```
`tee` is a command that reads from standard input and writes to standard output and files.
 It's used for redirecting output to multiple destinations, such as writing to a file and stdout.
 `tee` is normally used in conjunction with other commands through piping.

## How to check Disk Usage on Terminal:
```
sudo apt install ncdu
ncdu / # shows the disk size of root
# using d key, you can delete the file or directory
```
Very handy, thanks to https://github.com/mostafabayat

## How to kill all the request from a specific command:
```
run top to get your command name
```
Then run:
```
pkill -9 -f [search string]
```
```
sudo pkill -f '^[search string]'
#only those that start with search string to make it more robust and safe!
```
Reference: https://unix.stackexchange.com/questions/50555/kill-many-instances-of-a-running-process-with-one-command

## How to check all the processes on GPU
```
sudo fuser -v /dev/nvidia*
```
kill the ones with PID of your interest using `sudo kill -9 PID`!

## How to do grep with a pattern that starts with a dash
```
echo file.txt | grep -- -e
echo file.txt | grep -- -x
...
```
The -- is the key!

## How to add a user to sudoers
```
# First create your new user
useradd -s /bin/bash -d /home/newname -m newname
```

```
sudo su
chmod 755 /etc/sudoers # to make it writable
```
Then add the following line:
```
ubuntu ALL=(ALL) NOPASSWD: ALL # For running in cicd it's better to shutdown sudo requirement for this user
```
Then make non-writable again:
```
chmod 400 /etc/sudoers
```

Note: I tried `sudo adduser ubuntu sudo` but it didn't work for cicd, however, it worked in the server's temrinal.
Thanks to: [amghazanfari](https://github.com/amghazanfari)

## How to stop a job by port number:
```
netstat -nl | grep LISTEN # check port &
netstat -nl | grep LISTEN | grep 8888 # You can go like this too
fuser -k 8022/tcp
```
Thanks to: [KiLJ4EdeN](https://github.com/KiLJ4EdeN/)


## How to only remove symbolic links:
```
find -type l -delete
```

## How to pass ssh/scp password in a script
```
sudo apt-get install sshpass
sshpass -p "your-ssh-password" ssh/scp <command>
```
Thanks to: [stackoverflow](https://stackoverflow.com/a/16734873/16445477)

## How to run python with sudo:
```
sudo env "PATH=$PATH" python ./code.py
```
When doing sudo, /etc/sudoers's path is overwritten on the user's path, therefore, we need to provide user's path as and environment.

## How to see whole command:
```
top -c
```

## How to kill the parent of a multi-processing:
```
ps aux --forest | grep python
```
You can change python with anything. In the output you can find the main processes with their children.

How to exactly find the parent of an Id, specially used for LokyProcesses:
```
ps -f -p $(ps -o ppid= -p 4039367)
```
If the output saya it's `/sbin/init` then it's an stray process.

You can check the ones which are more than one hour:
```
ps -eo pid,etime,args | grep "[l]oky" | awk '/-/ || /:[0-9][0-9]:/ {if ($2 ~ /-/ || substr($2,1,index($2,":")-1)+0 >= 1) print}'
```
and kill them
```
ps -eo pid,etime,args | grep "[l]oky" | awk '/-/ || /:[0-9][0-9]:/ {if ($2 ~ /-/ || substr($2,1,index($2,":")-1)+0 >= 1) print 1$} | xargs -r kill -9'
```
or only the loky ones:
```
ps aux | grep loky | grep -v grep
```
and kill by:
```
ps aux | grep loky | grep -v grep | xargs -r kill -9
```

# How to use Cuda from miniconda:
```
# install pytorch with cuda (my own case)
conda install cuda -c nvidia # make sure to have nvcc in /.../miniconda3/envs/env-name/bin/nvcc
CUDA_HOME=/.../miniconda3/envs/env-name/bin pip install ... # or any other command.
```
