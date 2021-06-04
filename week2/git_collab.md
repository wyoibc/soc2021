---
title: SSH Based Communication with GitHub
date: June 1, 2021
---


## Watch Week 2 Session on Youtube


<center>

<iframe width="560" height="315" src="https://www.youtube.com/embed/MRRPqs6G7hc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</center>

<br><br>

## Table of Contents

- [1. Staying Current with a Remote Repository](#staying-current-with-a-remote-repository)
	
	- [1.1 Copying or Cloning a Repository](#copying-or-cloning-a-repository)

	- [1.2 Keeping the Clone Current with Upstream](#keeping-the-clone-current-with-upstream)

- [2. Secure Communication with GitHub](#secure-communication-with-github)

	- [2.1 Generate SSH Key Pair](#generate-ssh-key-pair)

	- [2.2 Associate Public Key with GitHub](#associate-public-key-with-github)

	- [2.3 Configure Your System to Use SSH Keys](#configure-your-system-to-use-ssh-keys)

	- [2.4 Test Your SSH Key](#test-your-ssh-key)

- [3. Collaborating on GitHub](#collaborating-on-github)

	- [3.1 ``Bears`` Generate New Repository and Initial Content](#bears-generate-new-repository-and-initial-content)	

	- [3.2 ``Foxes`` Clone Repository and Edit it](#foxes-clone-repository-and-edit-it)

	- [3.3 ``Bears`` Pull Updates and Add to the Repo](#bears-pull-updates-and-add-to-the-repo)

	- [3.4 ``Foxes`` Pull Updates](#foxes-pull-updates)

<br><br><br><br><br>
<br><br><br><br><br>
<br><br><br><br><br>
<br><br><br><br><br>
<br><br><br><br><br>
<br><br><br><br><br>

## 1. Staying Current with a Remote Repository

The official repository of Summer of Code 2021 is located at [https://github.com/wyoibc/soc2021](https://github.com/wyoibc/soc2021). Now that you have started following its contents, it makes sense to (1) have a copy of it on your computer, and (2) learn how to keep your copy current with what is upstream (i.e. on GitHub).  If you were to copy this repository right now, you will have the most current version of it. But once I make any changes to the upstream, your copy will become slightly stale.  In this section, we will learn how to make it current again.


### 1.1 Copying or Cloning a Repository

- Using the following command in your terminal session, clones the remote repository to the current location.  So be sure to navigate within your terminal to a place where you wish to make a copy.  

```bash
cd ~/Github

git clone https://github.com/wyoibc/soc2021
```

<br>

### 1.2 Keeping the Clone Current with Upstream

- You don't have to know if the remote has changed; git will do that for you.  The following command will allow git to check your copy against the remote. If they are different, git will download updates and merge them with your copy. If they are identical, git will tell you so and it won't make any changes.


```bash
git pull
```

- You can use ``git pull`` as often as you wish. For SOC2021, it is probably sufficient to pull it once a week. If you begin working on a project that is being updated more frequently, then you will benefit from pulling more often.



<br><br>

## 2. Secure Communication with GitHub

- When you used your login credentials to push contents of your local repository to a new and empty remote GitHub repository, you may have received an email-notice from GitHub that this method of authentication is *deprecated*. That's computer science lingo for "about to be phased out". What that means is that sometime soon, using username and password to push contents to github will no longer work (don't confuse this with logging onto Github.com, which will still use those credentials.

- Instead, you will be using a much more secure form of login called ``SSH``, short for **S**ecure **SH**ell. A SSH password is called a ``key``, which is much longer than a typical, secure password. But perhaps even more importantly, it is encrypted.

- A SSH key comes as a pair of a public password, and a private password.  You provide your public part to others who you wish to securely communicate with (i.e. Github in this instance). The private key should never be shared with anyone for any purpose. It will sit securely on your computer inside a hidden folder.

- In this section, we will generate a SSH key pair and then associate the public key with your Github.com account.  

<br>

### 2.1 Generate SSH Key Pair

- On Macintosh and other Unix-like systems, SSH key pair can be generated using a program called ``ssh-keygen``. It comes preinstalled with the OS. Windows users should be able to access this program inside ``git bash``.


```bash
ssh-keygen -t rsa -b 4096 -C "name@host.edu"
```

- Here, ``-t rsa`` flag tells the program to use ``RSA`` encryption algorithm when generating the private key.  RSA stands for first initials of the three authors who developed this algorithm (Rivest, Shamir & Adleman) in 1977.

- ``-b`` flag denotes amount of bits to use (size of the key)

- ``-C`` flag allows a comment, which in this case is your email address associated with github. It will become part of your key.

- Once you hit enter, your system will present the following dialogue:

```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/wyoibc/.ssh/id_rsa): 
```

- Notice that the keys will be stored inside your home directory in a hidden folder named ``.ssh``.  

- By default the keys are named: ``id_rsa`` (private) and ``id_rsa.pub`` (public). But you don't have to keep this name. If you wish to change is, type it out. An example could be: ``/Users/wyoibc/.ssh/t_rex``.  If you want to keep the default, just hit enter.

- Next, the system will ask if you want to protect these keys with a passphrase. If you choose to enter a passphrase, you will need to memorize it and the system will ask you to enter it everytime you wish to use the key. I personally always use a passphrase. 

```bash
Enter passphrase (empty for no passphrase): 

Your identification has been saved in /Users/wyoibc/.ssh/t_rex.
Your public key has been saved in /Users/wyoibc/.ssh/t_rex.pub.
The key fingerprint is:
SHA256:4ps5bMhN7293Grtr0v+dCsUI4Ji02WQL9v+Wut7uOu4 name@host.edu
The key's randomart image is:
+---[RSA 4096]----+
|     + +         |
|    o % o        |
|     = = .       |
|        . . o    |
|      . S. . o   |
|     ...  . o    |
|   . =..   *.    |
|    o =+..* =o. o|
|     .+o=EBB=Booo|
+----[SHA256]-----+
```

<br>

### 2.2 Associate Public Key with GitHub

- Next we need to copy our public key and associate it with our GitHub account.


```bash
cd /Users/wyoibc/.ssh/

pbcopy < t_rex.pub  
```

- The key has now been copied to your clipboard.

- Next, go to GitHub.com and login to your account. Choose settings, and then SSH keys as follows:


<br>
<center>
<img src="images/git_settings.png" width=250 /> <img src="images/git_ssh.png" width=250 />
</center>
<br>


- Click on ``New SSH key`` and use ``ctrl+V`` to paste your public key into the available box and choose a title. Leave no spaces in the title. A title is just an identifier for your key. Finally, choose ``Add SSH key`` to complete the process.


<br>
<center>
<img src="images/keypaste.png" width=650 /> 
</center>
<br>

- Once you have added the key, it will appear in your account as follows:

<br>
<center>
<img src="images/keyadded.png" width=650 /> 
</center>
<br>


<br>

### 2.3 Configure Your System to Use SSH Keys

- First, make sure that ``ssh-agent`` is enabled on your system, and add your newly created ssh key to the agent. If you set up a passphrase earlier, you will need to enter it now.

```bash
ssh-agent -s

ssh-add /Users/wyoibc/.ssh/t_rex
```

- Make sure that the ssh-agent is using your key.

```bash
ssh-add -l

4096 SHA256:uMFoUIUC7osmgDQaNowsOnqEt3XmPPZe4RnR2+Q1KB0 name@host.edu (RSA)
```

- Second, open the configuration file for ssh

```bash
cd /Users/wyoibc/.ssh

vim config
```

- If this file doesn't exist, you will be creating a new one.  Add following lines to this file:


```bash
Host *
   AddKeysToAgent yes
   UseKeychain yes

Host wyoibc.github.com
        HostName github.com
        User git
        PreferredAuthentications publickey
        IdentityFile ~/.ssh/t_rex

```

- Save and close the file.


```bash
:wq
```


<br>

### 2.4 Test Your SSH Key

- Now let's go back and make some changes to the git repository we created last time: ``testgit``.

- Let's create a new plot to include number of deaths from COVID-19 over the same time period as before.

```bash
cd /Users/wyoibc/Dropbox/Github/testgit
```

- Use R to load the data and redraw the scatterplot as before.

```r
df <- read.csv("us.csv", header=T)

plot(1:489, df$deaths, pch=16, col="salmon", cex=0.5, xlab="Days", ylab="Num. Deaths")
```

- Save this plot as before, but combine it with the previous plot to make a one-row, two-column multi-plot.  


```r
png("covid_combined.png", width=10, height=7, unit="in", res=600)

par(mfrow=c(1,2), mar=c(5,4,4,2), oma=c(2,2,2,2))

plot(1:489, df$cases, pch=16, col="darkgreen", cex=0.5, xlab="Days", ylab="Num. Cases")

plot(1:489, df$deaths, pch=16, col="salmon", cex=0.5, xlab="Days", ylab="Num. Deaths")

title(main="COVID-19 Cases and Deaths 2020-21", outer=TRUE, cex.main=0.9)

dev.off()

```


- Next modify your README.md to exclude the previous plot and include the new one.


```bash
---
title: COVID-19 Cases & Deaths
author: Vikram Chhatre
date: June 1, 2021
---

1. The following plot shows number of COVID-19 cases and deaths in the United States from January 2020 through May 2021.


<center>
<img src="covid_combined.png" width=700>
</center>

```

- Save and close the file. Then add and commit the changes. But don't push yet.  We need to change our authentication method.


```bash
git add .

git commit -m "Added a new plot"

```

- Open up the git config file in testgit:


```bash
cd /Users/wyoibc/Dropbox/Github/testgit/.git

vim config
```

- Find the URL setting and change it as follows by substituting your own user name

```bash
url = git@github.com:wyoibc/testgit.git
```

- Finally, push. Now you should not get a password prompt.


```bash
git push
```


<br><br><br>


## 3. Collaborating on GitHub

- One of the advantages of putting your work on GitHub is that it makes collaborating with others very easy. For this section, you will find a partner to collaborate with.

	- Share your GitHub user name with your partner.
	
	- One of you will be part of ``Bears`` team and the other of ``Foxes`` team.


### 3.1 ``Bears`` Generate New Repository and Initial Content

- ``Bears`` do the following:

	- Go to ``Github.com/YOUR_USER_ID`` and create a new repository called ``collab``

	- On your local computer, create a new folder ``collab`` inside the ``GitHub`` folder you created last week.

	- Inside this folder, open a new file in ``vim`` named ``README.md``

	- Type following content in this file:

		```bash
		---
		title: Collaborative Exercise in Github
		---


		## QQ Normalization

		```
	- Save and close the file (``:wq`` in vim).

	- Initialize new git repository inside ``collab``.

		```bash
		git init
		```

	- Configure the repository

		```bash
		git config user.name "YOUR_USER_NAME"
		git config user.email "YOUR_GITHUB_EMAIL_ADDRESS"
	
		git config --list

		git remote add origin git@github.com:YOUR_GITHUB_USERNAME/collab.git
		```

	- Add, commit and push files to your new repository

		```bash
		git add .
		git commit -m "Initial commit by Bears"
		git push -u origin master
		```

	- If you carefully followed section#2 above, you should not get a password prompt. Your SSH keys should be used instead.

	- Finally, go to your new GitHub.com repository, choose ``Settings``, then choose ``Manage access`` and invite your partner as a collaborator.  

<br><br>

### 3.2 ``Foxes`` Clone Repository and Edit it

- ``Foxes`` do the following:

	- You should have received an email from GitHub containing invitation from your ``Bears`` partner to collaborate on the above repository.  Go ahead and accept it.

	- Inside your terminal session, go to the ``Github`` folder you created last week.

	- Clone the collaborative repository inside this folder

		```bash
		cd ~/Github
		git clone https://github.com/PARTNERS_GITHUB_ID/collab.git
		```

	- Open the ``README.md`` file in vim and set it aside for now. We are going to generate some new content for the repo.

	- Fire up a new ``R`` session, either inside your terminal or in R-Studio.

	- Generate normal distribution of ``length=100``, ``mean=5`` and ``STDEV=2``

		```r
		rnorm_100 <- rnorm(100, 5, 2)

		rnorm_100
		
		  [1]  3.2560410  3.9427234  6.5062322  2.6120940  8.4469923  3.7734777
		  [7]  6.6660813  6.7297231  7.6356562  1.2795508  8.7135774  4.7808433
		 [13]  3.2431209  4.5544523  8.0560542  5.1345238  4.5290398  3.0709138
		 [19]  4.9424754  4.9901400  4.8403945  4.7744570  4.9741091  8.5158795
		 [25]  6.7576175  3.1544909  5.1043582  7.2520960  4.7162988  5.2154195
		 [31]  5.6096246  7.2431140  5.3628224  7.0183478  3.0525487  5.7969017
		 [37] -0.2473231  5.4314736  2.9819134  5.6517750  5.1031163  5.2758484
		 [43]  3.9986785  3.6546439  1.0277276  8.2698047  2.9370657  3.8312321
		 [49]  5.1891104 -1.1718007  2.9092251  9.6024601  0.3102288  3.5233113
		 [55]  6.0785879  6.1443481  1.4895122  4.1123315  4.4962461  7.6709961
		 [61]  5.7954681  3.2487014  2.9246425  4.4178842  5.1267737  2.0772663
		 [67]  5.7256326  2.4347005  3.4792939  8.6661506  2.3007794  1.2865652
		 [73] 10.2528413  6.5529408  4.5308639  3.9096317  2.9602922  4.5660157
		 [79]  6.4765327  5.4774428  9.5770346  4.8439801  7.2007534  3.9652323
		 [85]  6.1064564  4.3177799  3.5924463  4.9280261  6.4032782  5.2160964
		 [91]  4.2959516  3.9489019  3.6501318  4.2419236  7.3105085  6.8059605
		 [97]  3.8606476  3.3618475  4.1134365  1.7566958
		```

	- Test how closely this vector fits normal distribution using the ``qqnorm`` function in R

		```r
		qqnorm(rnorm_100)
		```

<center>
<img src="images/rnorm_100.png" width=550 />
</center>


	- Save this file as ``rnorm_100.png`` in the current folder.

	- Now let's go back to ``README.md`` and update its contents as follows:

		```bash
		---
		title: Collaborative Exercise in Github
		---


		## QQ Normalization


		- Normalizatio using rnorm 100 sampling

		<center>
		<img src="qqnorm_100.png", width=500 />
		</center>
		```

	- Save and close the file. Then perform git operations as follows:

		```bash
		git add .
		git commit -m "Edit by Foxes"
		git push origin master
		```

	- Verify that the contents were uploaded to your partner's Github repository (on which you are a collaborator).



<br><br>

### 3.3 ``Bears`` Pull Updates and Add to the Repo

- Bears do the following:

	- Perform ``git pull`` inside collab to bring your local version up to date with changes present upstream

	- We will now update the ``README.md`` again by expanding the normal distribution from 100 to 1000 and 5000 respectively.

	- Fire up your ``R`` session:

		```r
		rnorm_1k <- rnorm(1000, 5, 2)
		rnorm_5k <- rnorm(5000, 5, 2)

		qqnorm(rnorm_1k)
		qqnorm(rnorm_5k)
		```

	- Update the ``README.md`` to include these two new figures

 
<center>
<img src="images/rnorm_1k.png" width=550 />
</center>


<br><br>

<center>
<img src="images/rnorm_5k.png" width=550 />
</center>


	- Finally, push the updates upstream with ``git add``, ``git commit`` and ``git push``


<br><br>

### 3.4 ``Foxes`` Pull Updates

- In the culmination of this exercises, ``Foxes`` will use ``git pull`` to update their local repository with the changes that were made by ``Foxes.  After this operation, open the README file to make sure you got all the changes. You won't see figures inside README, but they should be present in the folder.






































