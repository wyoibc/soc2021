---
title: Version control using git and github
date: May 25, 2021
---


## Watch Week 1 Session on Youtube

- If you don't want to watch the software installation part, skip to 1 hr mark.

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/8HbdbVxw-ks" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

<br><br>

## 1. What is version control and do I need it?

- Ability to keep track of incremental changes made to a project is at the heart of version control. A simple example is a computer program that performs a specific function.  When a developer writes the first working version of this program, it is generally labeled as v1.0. As more features and functions are developed and added to the program, its version number continues evolving gradually from 1.0 to 1.0.1 to 1.1, 1.2, 2.0 and so on and so forth.  Additionally, the developer may have made many other numerous changes to the code which likely did not end up in the next released version.

- What if the developer discovered that one such change rendered the program dysfunctional and wanted to revert to the last functional version? That type of control on the development process is what underlies version control.

- Of course, a computer program is not the only project where version control is useful. It is equally useful when writing manuscripts for publication, book chapters, data analysis protocols, thesis, dissertation. Essentially any project that continues to evolve can benefit from version control. In other words, you don't have to be a computer scientist to employ version control in your work.


- ``Git`` is a program on your computer ([see Prep for installation instructions](../prep/index.html) which performs version control functions on a project of your choice.  In this session, we will work with ``git`` to create a new repository of code and then store it on your GitHub account.


## 2. Create a new GitHub repository

- Navigate your browser to https://github.com/YOUR_USER_NAME. In the top right hand corner, you will see a ``+`` button. Click on it and choose ``New Repository`` option.  This will generate a page like the following:

<br>
<center>
<img src="images/git1.png" width=650 />
</center>
<br>


- Populate this page with some information as shown below. Then click ``Create repository``.

<br>
<center>
<img src="images/git2.png" width=650 />
</center>
<br>

- You have just created an empty github repository. Now we will work on creating contents for this repository on our local machine.


## 3. Working locally with git

- Open a terminal session. Windows users will start ``gitbash`` by right clicking on desktop and choosing that option.

- Create a folder named ``Github`` somewhere on your computer


```bash

cd /Users/your_name

mkdir Github

cd Github

pwd

/Users/your_name/Github/

```


<br>

### 3.1 Initialize new git repository

- Create your repository folder using the same name as you did on github

```bash

mkdir testgit

cd testgit/

```

- Download and save [us.csv](us.csv) file into ``/Users/your_name/Github/testgit``. This file contains data from New York Times that details COVID-19 cases and deaths over the course of the pandemic. We will use this data set to generate some content for our repository.


<br>

- Initialize the new git repository

```bash
pwd

/Users/your_name/Github/testgit

git init

```


<br>

### 3.2 Generate some content

- Create a new file called ``README.md`` in the repository

```bash
touch README.md
```

- Open the new file in either ``vim`` (terminal version) or ``macvim`` (gui version). Windows users can open the gui version.

```bash

vim README.md

```

- Note that ``vim`` has two modes: edit and command. To edit file, press ``i`` to enter the insert mode. You can revert to command mode by using ``ESC`` key on your keyboard.


- Modify the file as follows:


```bash
---
title: COVID-19 Cases & Deaths
author: Your Name
date: May 25, 2021
---

```

- This part is called the document preamble. 


<br>

### 3.3 Use R to create graphics

- Now go back to the terminal and fire up a R session. You may also choose to use Rstudio for the following exercise.

- Import the ``us.csv`` file into R's memory

```r

df <- read.csv("us.csv", header=T)

head(df)

        date cases deaths
1 2020-01-21     1      0
2 2020-01-22     1      0
3 2020-01-23     1      0
4 2020-01-24     2      0
5 2020-01-25     3      0
6 2020-01-26     5      0


dim(df)

[1] 489   3

```

- This shows that the data is organized into 3 columns and 489 rows. We will now make a scatterplot of COVID-19 cases.


```r

plot(1:489, df$cases, pch=16, col='darkgreen', cex=0.5, xlab="Days (2020 & 2021)", ylab="Num. Cases", main="COVID-19 Cases in the United States")


```

- Notice how we created a simple vector of length 489 as an argument for ``x`` axis. We could have used dates, but that complicates the things a bit, so we will explore that later.

- This code should generate a plot like the one here:

<br>
<center>
<img src="images/Rplot.png" width=600 />
</center>

- We will now save this plot as a png formatted image in the current folder

```r

png("covid_cases.png", width=10, height=10, units="inches", res=600)

plot(1:489, df$cases, pch=16, col='darkgreen', cex=0.5, xlab="Days (2020 & 2021)", ylab="Num. Cases", main="COVID-19 Cases in the United States")

dev.off()

```

- If the above code worked, you should now have an image called ``covid_cases.png`` in your ``testgit/`` folder.


<br>

### 3.4 Finish making changes to the repository

- Let's go back to the ``README.md`` file that we were working on before and add the following items:


```bash

---
title: COVID-19 Cases & Deaths
author: Your Name
date: May 25, 2021
---

1. The following plot shows number of COVID-19 cases in the United States from January 2020 through May 2021.


<center>
<img src="covid_cases.png">
</center>

```

- To save and close the file, press ``ESC`` key, then type ``:wq`` and hit ``ENTER``.  That's it, you have now saved ``README.md`` 


<br>

### 3.5 Configure git


- Provide the git engine with the information on your git credentials and the new upstream repository:

```bash

git config user.name "YOUR_GITHUB_USERNAME"

git config user.email "YOUR_GITHUB_ASSOCIATED_EMAIL_ADDRESS"

```

- Verify these settings were properly set

```bash

git config --list

user.name=wyoibc
user.email=wyoinbre@gmail.com

```

- The above output should reflect your own information.  

- Set up upstream information about the repository

```bash

git remote add origin https://github.com/YOUR_GITHUB_USERNAME/testgit.git

```

- Again, verify

```bash

git remote -v

origin	https://github.com/wyoibc/testgit.git (fetch)
origin	https://github.com/wyoibc/testgit.git (push)

```


<br>

### 3.6 Add and commit repository content

- Before git starts keeping track of your file, you will need to add them to it's memory


```bash

git add .

```

- Notice the ``.`` (period) above. That means add everything in the current location (``..testgit/``

- Check git status

```bash

git status

On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   README.md
	new file:   covid_cases.png
	new file:   us.csv

```

- Now commit the files for pushing upstream

```bash

git commit -m "Add a helpful message here, e.g. initial commit"

[master (root-commit) 962e188] initial commit
 3 files changed, 504 insertions(+)
 create mode 100644 README.md
 create mode 100644 covid_cases.png
 create mode 100644 us.csv

```


<br>

### 3.7 Push the repository to GitHub


- Finally, push all the files to your upstream repository

- When you enter the following command, you will be prompted for your github username and password. When you type the password, the cursor won't move. This is OK!

```bash

git push -u origin master

Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 6 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 357.31 KiB | 9.66 MiB/s, done.
Total 5 (delta 0), reused 0 (delta 0)
To github.com:wyoibc/testgit.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.

```

- If you see an output similar to the above, your repository is now live on Github. Go check it out.  If you get an error message, talk to us on the Slack channel.





























 
