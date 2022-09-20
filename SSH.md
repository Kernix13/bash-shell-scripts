# SSH Crash Course

> Jul 8, 2018

His [YouTube Video: SSH Crash Course | With Some DevOps](https://youtu.be/hQWRp-FdTpc)

## The Basics

- SSH = Secure Shell
- Communication protocol to communicate with other computers like http, https, ftp, ...
- Can do just about anything on a remote computer
- traffic is encrypted, it's secure
- used mostly in the command line
- SSH is the client
- the computer you are logging into has to have SSHD or Open SSH Daemon which listens for SSH connections
- usually it's a linux server you are logging into
- on the server you have an ssh config file where you change things

## Authentication methods

There are a few ways to authenticate:

1. Password - the default way: `ssh user_name@192.168.1.29` where the # is the IP address of the server
1. Public/Private Key Pair - SSH keys to bypass the password - you need to generate a set of publec and private keys on your machine (the recommended way)
1. Host based - a file called known host (SKIP)

## Generating keys

- You need to run the command `ssh-keygen` - that will create a public key and a private key -
- `~/.ssh/id_rsa` (Private key) - created by default into your home folder which is what the tilde `~` represents and it placed in a hidden folder called `.ssh`
- you will be prompted when you run the command to see if you want to name it something other than the default of `id_rsa`
- `~/.ssh/id_rsa.pub` (Public key) - this is what you want to put on your server
- on your server you will also have a `.ssh` folder or you need to create one -
- public key goes into server in a folder named "authorized_keys" file

### Windows

- Win10 now supports native SSH - SSH is for unix based systems
- Git Bash and other terminal programs include the ssh command and other Unix tools

## Local Server setup

- open Git bash - I'm skipping the commands and just forking his [SSH Cheat Sheet gist](https://gist.github.com/Kernix13/cd2ac61dacc86cb72586cab13eda6a5c).
- Digital Ocean Droplet???
- when you try to ssh into a server you will see a msg (you will only see this the first time):

> The authenticity of host `192.168.1.29 (192.168.1.29)' can't be established. ECDSA key fingerprint is SHA256:4C1Rd/handsy4uM+LDN/FKfN5bz9lr9urN5D5G57I4GQ. Are you sure you want to continue connecting (yes/no)?

- type yes which will add you to the known host file
- you will then be asked for your password to authenticate so this is when you add your pw for the server -
- you get greeted with a welcome page where you see system info -
- at the bottom you will see `yourName@serverName: $` that means you are now on that server
- do `ls` and you won't see anything because you are in your home directory which is empty
- to get to the root directory do `cd /` then do `ls` and you will see the core folder names
- do `cd` to go back to your home directory - you can make folders like `mkdir test` then `ls` to see it, then `cd test` to go into it, create files in it with `touch test.txt`, etc.
- cd to go back to home directory and to remove the test folder you need to use `rm` but since it has a file in it add `-rf` or the whole command would be `rm -rf test`

### Install Apache server

- you need to install apache to have a web server: `sudo apt install apache2 -y`
- then enter your PW and apache will be installed on the local server
- lamp stack? mean stack?
- `sudo` -> install as root? `install` -> install with your package manager
- add the ip address into the web page and you will see the apache start page - that is put into your web root -
- type `exit` to exit out of the server - if you try to log back in you will need your PW again - instead, generate SSH keys

### Generate SSH keys

- enter `ssh-keygen` - you will be prompted where you want to save it and as what file name - the default will be your home directory, you as a user on your machine - just hit ENTER to accept the default folder and file names
- you can also attach a passphrase but he skipped that so hit ENTER twice
- that should create y our key
- do `ls .ssh` and you should see `id_rsa` and `id_rsa.pub`
- to see what the public key looks like use the `cat` command which will display the contents of the file: `cat .ssh/id_rsa.pub`
- the private key is longer and you do not do anything with it, just keep it on your system
- now you need to get the public key onto the server in the `.ssh` folder in a file called `authorized_keys`
- search for create ssh keys and look for the digital ocean page:[How To Set Up SSH Keys on Ubuntu 12.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-2)
- their instructions have you use additional flags - to copy it to the server, skip the mac/homebrew option - use the alternative method:

> You can copy the public key into the server’s authorized_keys file with the ssh-copy-id command. Make sure to replace the example username and address:

`ssh-copy-id your_name@your_server_address`

- Once the command completes, you will be able to log into the server via SSH without being prompted for a password. However, if you set a passphrase when creating your SSH key, you will be asked to enter the passphrase at that time. This is your local ssh client asking you to decrypt the private key, it is not the remote server asking for a password
- the notes and commands above are different than what he is showing in the video - line 21 in the gist file
- you will be prompted for the server PW - now you should be able to login without a PW: ssh name@xxx.xx.xx.x.xx or whatever
- then look at the file with your key that is on the server with `cat .ssh/authorized_keys`

### Copy a local file to your server

1. `exit` to get back into your machine
1. use the secure file copy command `scp`: `scp ~/test.txt name@xxx.xx.xx.x.xx:~`
1. so the home folder to the home folder (~)

- then log back into the server with `ssh name@xxx.xx.xx.x.xx` and use `ls` to see the file

## Remote Digital Ocean Droplet

- Digital Ocean is a hosting service and they offer droplets which is little virtual servers
- sign up for free after giving credit card info and then go into your dahsboard and click Create Droplet - then scroll down and choose a package - and that is where they charge you!
- they also have a btn to add your SSH key - you could use the same key you generated above, but it's best to keep separate keys for separate applications - do `ssh-keygen -t rsa` - you need to give it a diff name or this will overwrite your previous key - ssh root@ the ip address they provide
- SKIP - I don't care about this - I'm not interested in this kind of back-end stuff, I'd be interested in maybe using Node.js, Express.js and MongoDB for a full-stack CRUD app but not at this time - plus this video is 5+ years old.

Important notes though:

- first thing is you want to update your packages: `sudo apt update` then to upgrade the software use `sudo apt upgrade`
- then you want to create a new user because you should NEVER use the `root` user - you should also disable the root login so you can't login with root
- create a new user with sudo privileges: `adduser jim` then enter a PW
- then do `id jim` and it will show you the group things but you don't have sude privileges yet - so do `usermod -aG sudo jim`
- NOTE: We added the key to `root`, need it for the new user...lots of notes but I'm skipping
- **Disable root login**: there is an ssh config file -> `sudo nano /etc/ssh/sshd_config` and hit ENTER, enter your PW
- BTW, `port 22` is the default for SSH, 21 is FTP
- go down the file and look for `PermitRootLogin` and change `yes` to `no` to prevent brute force attacks and stuff like that
- also make sure `PasswordAuthentication` is set to `no`- then save it with I think CTRL+X
- then you should reload the sshd service: `sudo systemctl reload sshd`
- **Install Apache**: `sudo apt install apache2 -y` - once installed paste the ip address into the server for the apache start page - you could then add a domain to that

That ends the basics of SSH. Next is to use GitHub on the server.

## SSH Key for GitHub

- while in the command line for your server do `git --version` and you will see that git is installed but you need an SSH key
- in GitHub makse sure to copy the link with _Clone with SSH_ selected.
- if you try to do `git clone https_url` you will get "Permission Denied" because you don't have an SSH key setup with GitHub
- to do that do `ssh-keygen -t rsa` and create a separate key using something like `id_rsa_github`
- when prompted do about the name and location do `/home/jim/.ssh/id_rsa_github`
- you will also have to do that on your local machine to use GitHub with SSH
- if you see "failed: Permission denied" it's because the .ssh folder is under the root user and the root group
- do `ls -la` where the `a` is because it's a hidden folder - you will seee everything as jim jim or brad brad or whatever name you used but the .ssh folder has root root as the user owner and the group
- what you want to do is change that to be your name -> `sudo chown -R jim jim /home/jim` where `chown` means "change owner", `-R` means recursive so change everything in the home jim folder
- run `ls -la` again and you should see the change - so now you can generate the keys with `ssh-keygen -t rsa` and then `/home/jim/.ssh/id_rsa_github`
- then do `ls .ssh` and you should see your keys - you then need to put the public key onto GitHub: `cat .ssh/id_rsa_github.pub`, copy the entire key
- then in GitHub go to your Settings page > click on SSH and GPG keys > click on New SSH key btn > give it a name > paste the key in the "key" textarea > then click Add SSH key
- back in the server try to clone the repo again but it may fail because you have to do `ssh-add /home/jim/.ssh/id_rsa_github`
- but then you may see:

> Could not open a connection to your authentication agent

- then you need to run (yes with backticks)

```
eval `ssh-agent -s`
```

- that gives you the Agent pid number - then you can run `ssh-add /home/jim/.ssh/id_rsa_github`
- now you can do `git clone url`

### Add React app

- you will need to install node so that the packages can be installed
- do a google search for 'install node ubuntu' - you will need to use the `curl` command - I'm done for now - just watching from here on for the last 10 minutes of the video

> To him DevOps can get confusing and be more involved than development

Since this is a REaxct app you would want to build out your static assets and then serve that.

Looks like `CTRL+C` works. Then he removed the apache page which is index.html and then he did `npm run build` - then `sudo mv -v /home/jim/react/....` - then you can go to the ipaddress and your react site will show

- you will need to add your nameservers and add an `A` record -
