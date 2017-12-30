# Getting Started with Google Cloud Shell

This tutorial will guide you through the first steps to using Google Cloud Shell and its code editor. 

Get Started now and open this tutorial in Cloud Shell

[![Open in Cloud Shell](http://gstatic.com/cloudssh/images/open-btn.svg)](https://console.cloud.google.com/cloudshell/open?git_repo=https%3A%2F%2Fgithub.com%2Faubort%2Fgoogle-cloud-shell-tutorial&page=shell&tutorial=README.md)

## Setup

Open Google Cloud Shell and take some time to set it up with common aliases

### Open the cloud shell

If your console isn't open, click on the `walkthrough cloud-shell-icon` icon to open it.

### Open the `.bashrc` file using

```
nano ~/.bashrc
```

### Find the Alias section

Scroll down and find the following section

```
# some more ls aliases
#alias ll='ls -l'
#alias la='ls -A'
#alias l='ls -CF'
```

Once you have found these lines, remove the # (hash tag) in front of the aliases that you want to use, save and exit. 

### Restart the shell
Either close and reopen a new shell, or reload the current shell by running

``` 
. ~/.bashrc
```

## Connect to GitHub

Now it's time to connect to GitHub so that you can start coding and committing work to your git repo. 

### Create a SSH Key

In your terminal, go to ``` ~/.ssh/ ``` directory

To generate the SSH key, run the following command, making sure to replace <email> by your email address. Make sure to leave the quotes. 

```
ssh-keygen -t rsa -b 4096 -C "<email>"
```

Follow the steps and give your key a name. I’ve used github in my case.

### Check that the key has been created

Now check that the public and private keys are located in the ```~/.ssh``` folder by running ```ls -l```.
You should see a github (or the name you chose) and github.pub files listed.

### Copy your public key
From here you can copy your public key. Run the following command to show the content of your **public** key.  
``` 
cat ~/.ssh/<keyname>.pub
```

You should see something like this.
```
ssh-rsa AAAAAAAAB3NzaC1yB3NzasZsobNf...fIVRkBh23dKVfCT3cpnVeu2VGsV== pas....@gmail.com
```

Now copy the entire key (as above) to your clipboard.

### Add it to GitHub

Go to your [GitHub account](https://github.com/settings/keys) and add the new SSH Key.


### Create the SSH Config

If you have created a key that is named other than ```id_rsa``` you will need to create a config file for it to work. 

Go to the `.ssh` directory

```
cd ~/.ssh/ 
```

Create the `config` file
```
touch config
```

Open the config file using `nano` editor
```
nano config
```

Paste the following lines to the file, save and close
```
Host github.com
	Hostname github.com
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/<keyname>
```
> Make sure to replace the `<keyname>` by the name of your key


### Test your SSH Key
Now that the key has been added to GitHub, you can test it using the command

```
ssh -T git@github.com
```
You should see the following output in the terminal. 

```
Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
```

> If you see the following error message ```Error: Permission denied (publickey)``` check out [GitHub's troubleshooting guide](https://help.github.com/articles/error-permission-denied-publickey)