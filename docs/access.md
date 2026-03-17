# Access
Access to the servers is done by SSH from the login machine. This guide describes how to log in using SSH and how to set up passwordless SSH login. 

## Your first login
When getting access to a Linux server, you will be given a set of credentials and a machine name or an IP address for your Linux server. After you have gotten your login credentials, open the command prompt window (++win+r++, type `cmd.exe` and hit ++enter++) on the login machine and type the following:

=== "IP"

	``` cmd
	ssh user@<linux server IP>
	```

=== "Machine name"

	``` cmd
	ssh user@<machine-name>
	```

You will be prompted to enter your password. Verify that you can log in using the password provided.

## Setting up your SSH config file
Create the `.ssh` folder if it does not already exist by typing the following into the command prompt window:

```cmd
mkdir "%USERPROFILE%\.ssh"
```
Create or verify that an SSH config file exists by running:

```cmd
type nul >> "%USERPROFILE%\.ssh\config"
```

Open the SSH config file in Notepad:

```cmd
Notepad.exe "%USERPROFILE%\.ssh\config"
```

Add your SSH configuration to the SSH config file and save it. You may choose the alias as you'd like. From now on, you will log in to the machine using `ssh <alias>`, so I like to give it short and descriptive aliases such as `linux` or `gpu`.

```txt title="SSH config file"
Host <alias>
	HostName <IP or machine name>
	User <username>
```

!!! tip
	Verify that you can log in using `ssh <alias>` before you move on. You still need to provide your password.

## Set up passwordless SSH access
To set up passwordless SSH access we need to generate a cryptographic key. Type the following command into the command prompt. If the command reports that a key already exists press ++n++ to avoid overwriting the existing key. 

```cmd
ssh-keygen -q -t rsa -b 4096 -f "%USERPROFILE%\.ssh\id_rsa" -N ""
```
Now that you have an rsa key. Transfer your public key to the lab by running the following. **Make sure** to replace `<alias>` with your chosen alias from the step above. You will be prompted for your SSH password.

```cmd
type "%USERPROFILE%\.ssh\id_rsa.pub" | ssh <alias> "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

You should now be able to login to the Linux server without being prompted for a password by running

```cmd
ssh <alias>
```