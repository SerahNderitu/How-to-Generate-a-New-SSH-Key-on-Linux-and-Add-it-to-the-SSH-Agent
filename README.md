# How-to-Generate-a-New-SSH-Key-on-Linux-and-Add-it-to-the-SSH-Agent

An **SSH** key is an authentication and connection tool for remote servers and services. Although system administrators and power users often utilize the keys to automate processes and accomplish single sign-on, it serves the same purpose as user names and passwords.

## Utilizing Passphrases On SSH Keys
When you connect Github via SSH key to access and write data in repositories, you authenticate using a private key file on your local machine.

You can provide a passphrase when creating an SSH key to make it even more secure. The password needs to be entered each time the key is used. You can add your key to the SSH agent if it has a passphrase and you don't want to enter it every time you use the key. Your SSH keys are managed by the SSH agent, and it keeps track of your passphrase.


## Generating a New SSH Key
You can look up existing keys if you're unsure whether you already have SSH keys. You can check the existence of your key by going to your terminal and entering ``ls -al ~/.ssh.`` If any key exists, they will be listed in your **.ssh directory**.

However, you need to generate a new SSH key to use for authentication if you don't have one. On your local computer, go ahead and generate a new SSH key. To enable authentication for Git operations over SSH, add your public key to your GitHub account.

Follow the following steps to generate a new SSH key

1. Open your terminal window
   
2. Paste the following command on your terminal

```
 $ ssh-keygen

```

**Ssh-keygen** is the default key generation utility included in most SSH implementations. It allows users to create both public and private keys that are used for authentication during SSH connections.

You will see this output. 

**Output**
```
Generating public/private rsa key pair.
Enter file in which to save the key (/my_home/.ssh/id_rsa):
```

3. A file path will be requested from you when saving the key. To accept the default destination (/home/.ssh/id_rsa), press enter. If necessary, you may also provide an alternative path.

Please note that ssh-keygen may ask you to rewrite another key if you have previously created SSH keys; in this instance, we advise producing a custom-named SSH key. To achieve this, enter your personal key name in place of the default file location (id_ssh_keyname). 

4. You will be asked to provide a passphrase for the key in the prompt below;

**Output**

``
Enter passphrase (empty for no passphrase):
``

A passphrase provides extra security to your SSH key. It is advised to use a powerful passphrase. Press Enter if you want to set an empty passphrase (not advised) or enter your chosen passphrase.

The SSH key pair will be generated. You should see an output similar to this on your terminal:

**Output**

```
Your identification has been saved in /my_home/.ssh/id_rsa.
Your public key has been saved in /my_home/.ssh/id_rsa.pub.
The key fingerprint is:
b3:32:2e:2a:5e:33:3e:a9:de:4e:77:11:58:b6:90:26 your_username@remote_host

The key's randomart image is:
+--[ RSA 2048]----+
|     ..o         |
|   E o= .        |
|    o. o         |
|        ..       |
|      ..S        |
|     o o.        |
|   =o.+.         |
|. =++..          |
|o=++.            |
+-----------------+

```


## Add your SSH Key to the SSH Agent
SSH agent manages and it keeps track of your passphrase. Next, let’s add ssh key to the ssh-agent using the following steps:


1. On your terminal, start ssh-agent in the background
   
```
 $ eval "$(ssh-agent -s)" 

```

Two environment variables are set when the ssh-agent starts. Ssh and ssh-add use SSH_AUTH_SOCK and SSH_AGENT_PID to connect to the ssh-agent.

2. Add your **SSH private** key to the ssh-agent. 
The SSH keys used by the agent, by default, are located in the user's home directory's ~/.ssh directory. To add identities to the agent, you use the ssh-add command. 

To add the default files, it can either be ~/.ssh/id_rsa,  ~/.ssh/id_ecdsa, or ~ /.ssh/id_ed25519. If you’re not sure about the file of your private key, you can check your private key using the following command:

```
$ ssh-add -l
```

After you locate your ssh private key file, you can go ahead and add it to the ssh-agent.
Ensure to replace your_key with the path where you saved the private key file if you created your key under a different name.


```
$ ssh-add ~/.ssh/your_key

```

3. If you are asked for your password. The password you made when you generated the keys must be entered for the process to run.

4. Finally, add the SSH public key to your account on GitHub. Now you can use your SSH key to authenticate and connect the tool to your remote servers.

