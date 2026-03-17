# Access
Access to the servers is done by ssh from the login machine. This guide describes how to login using ssh and how to set up passwordless ssh login. 

## Your first login
When getting access to a linux server you will be given a set of credentials and a machine named or and IP adress for your linux server. After you have gotten your login credentials open the command prompt window (++win+r++ type `cmd.exe` and hit ++enter++) on the login machine and type the following

=== "IP"

	``` cmd
	ssh user@<linux server IP>
	```

=== "Machine name"

	``` cmd
	ssh user@<machine-name>
	```

You will be prompted to enter your password. Verify that you can log in using the password you are provided.

## Setting up your SSH config file
Create the `.ssh` folder if it does not already exist by typing the following into the command prompt window.

```cmd
mkdir "%USERPROFILE%\.ssh"
```
Create or verify that an SSH config file exists by running 

```cmd
type nul >> "%USERPROFILE%\.ssh\config"
```

open the SSH config file in notepad

```cmd
Notepad.exe "%USERPROFILE%\.ssh\config"
```

Add your SSH configuration to the SSH config file and save it. You may choose the alias as you'd like. From now on you will log in to the machine user `ssh <alias>` so I like to give it short and descriptive aliases such as `linux` or `gpu`.

```txt title="SSH config file"
Host <alias>
	HostName <IP or machine name>
	User <username>
```

!!! tip
	Verify that you can login using `ssh <alias>` before you move on. You still need to provide your password.

## Set up passwordless SSH access

```cmd
type "%USERPROFILE%\.ssh\id_rsa.pub" | ssh <alias> "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```