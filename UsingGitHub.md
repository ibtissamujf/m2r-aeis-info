Using GitHub for Assignments
============================
The purpose of this page is to explain how to use git/gitHub 
for course assignments. 
General information about GitHub/Git can be found on 
[ScribeTools](http://scribetools.readthedocs.org) in the 
[Git(Hub) section](http://scribetools.readthedocs.org/en/latest/github/index.html). 

Overview
--------
Let us consider a typical scenario with a group of two students working in pair.
Let us assume that in the ``aeis`` course of the ``m2r`` school the
group ``G12`` is made of ``Noe`` and her partner ``Babako``. 
Obviously these values has to be replaced by actual values in the commands 
presented later.

Babako and Noe have at their disposal a "group repository", the ``m2r-aeis-G12``. 
This repository lives on GitHub at ``https://github.com/m2r/m2r-aeis-G12``.
This repository is private so only Noe, Babako and teachers can 
see it when logged in on GitHub.
 
This repository will be shared by Noe and Babako to work together.
It will contain the final result evaluated at the end of assignments.
In practice Noe and Babako will clone this repository on their local machines,
will work separately on their local repositories and "push" and "pull" modification to 
the "group repository". When the deadline will arrive the content of 
the "group repository" will be evaluated. 

Scenario
--------
The steps below provides an overview of a possible process. T
echnical details are provided in the next sections.

1.  Noe installs the git toolkit on her machine or uses git it at the university.

2.  Noe first configures git on the local account(s) she uses (on her machine, 
    at the university, or both).

2.  Noe is at the university. She "clones" locally the "group repository" 
    from GitHub in a home directory. 
   
3.  Noe "pulls" the assignment skeletons from the 
    [m2r-aeis-root](https://github.com/m2r/m2r-aeis-root) repository.
    She gets the different files on her account at the university.

4.  Noe puts Babako and her name in the ``CONTRIBUTORS.txt`` file.
    She "commits" and "pushes" this changes to the "group repository" on GitHub.
 
5.  Noe browses the assignments, looks at TODO files, makes some first changes 
    to implement the first assignment.

6.  From time to time Noe "commits" and "pushes" the modifications to the 
    "group repository" on GitHub. This will make it possible for her (or Babako)
    to continue to work at home or at the university later). She just has to 
    remember to  "push" the modifications to GitHub at the end of
    each work session. At some point Noe leaves the campus. 

7.  Noe arrives at home and want to continue one her laptop. 
    She "pulls" the last modifications from the "group repository"
    and continue working on her laptop.

8.  At anytime Babako can also make a "clone" of the "group repository".
    He will get the last version "pushed" by Noe. He can then work in parallel on 
    other tasks in the TODO list for instance.  
   
8.  To get the last updates from the "group repository", Noe and Babako
    "pull" the changes regularly. This allows them to incorporate modifications from each 
    other. Since they are not fluent with git they avoid to modify the same parts of the
    same file at the same time. This avoids having 
    [merge conflicts](https://help.github.com/articles/resolving-a-merge-conflict-from-the-command-line/).
    
9.  Deadline is about to arrived. Noe and Babako make sure that all their changes
    have been pushed to the "group repository" on GitHub. They also double check that
    the TODO list has been updated and that it reflects what has been done.
    
10. The deadline arrives. Nothing has to be delivered: everything is already
    in the "group repository". The work of the group is evaluated though the inspection
    of the content of the "group repository" at the deadline.
    
The following sections explain how to implement such a typical scenario.

Installing Git
--------------

To install git on your machine (if not already installed) have a look at 
the [Install the git toolkit](http://scribetools.readthedocs.org/en/latest/github/index.html#install-the-git-toolkit) 
section.

Configuring Git
---------------

You have to configure git once on each machine you use. For instance you
may want to configure your account at the university and/or your
account on your personal machine. 

**The values provided in this example MUST be replaced by actual values:**

```bash
#---- configure git -------------------------------------------------------
# Attributes with --global goes the .gitconfig file. 
# Configure the user associated with contributions (e.g. git push)
git config --global user.name "Noe ZARWIN"
git config --global user.email "noezarwin@users.noreply.github.com"
# Keep the password in memory for 2h
git config --global credential.helper "cache --timeout=7200"
# OPTIONAL: Add a proxy if your machine is behind a firewall
git config --global http.proxy http://www-cache.ujf-grenoble.fr:3128
# OPTIONAL: Configure the editor used to edit message. Depends on OS 
git config --global core.editor "gedit -w -s"  # For ubuntu
# To see current configuration you can use the "git config -l" command
```

Cloning the group repository
----------------------------

To create a local repository on your machine you have to "clone" the 
"group repository" from GitHub. This will create a local repository
on your machine where you can work.

**The values provided in this example MUST be replaced by actual values**.

```bash
#---- Clone the "group reposity" and into a "local repository" ------------
# Go to your home directory
cd # On unix
# The "group repository" is at URL like (check this when connected to GitHub)
# https://<github_account>@github.com/<school>/<school>-<class>-<group>.git
# The GitHub account is specified explicitly (noezarwin below).
# The following command will ask for the corresponding password.
# Clone it in the current directory.
git clone https://noezarwin@github.com/m2r/m2r-aeis-G12.git
# If you get a message ‘Failed to connect to github.com port 443: Time out’
# it is most probably that your machine is behind a firewall and that
# you need to define http.proxy (see the Configuration section).
#
# Enter this newly created directory
cd m2r-aeis-G12
```
You now should have an empty local repository with only the '.git' hidden directory.
Simply put, this directory contains the "local repository". This directory is
managed through git commands.

Getting assignment skeletons
----------------------------

You now have to configure your repository to get assignment skeletons 
from the "root repository". The "root repository" is maintained by teachers.
This directory contains TODO lists, directory structures, file skeletons, 
and so on.

**The values provided in this example MUST be replaced by actual values**.

```bash
#---- Declare the "root directory" and "pull" files from it ---------------
# Declare the m2r-aeis-root as a remote repository.
# You can check that you have access to this repository by logging in 
# on GitHub and visiting https://github.com/m2r/m2r-aeis-root .
# You declaration below should be done only once for each local repository.
git remote add root https://noezarwin@github.com/m2r/m2r-aeis-root.git
# If you want to see the list of remote directories use the 
# command "git remote -v". If you made a mistake in the URL and need to change
# it use the command "git remote set-url <newurl>".
#
# "Pull" the assignment skeletons from the "root directory".
# If an editor opens just enter a message like "get assignment skeletons"
git pull -e root master
# You should now have the assignment skeletons in the local repository.
# You can browse the content of the directory with "ls -la" on unix.
# There is one directory per assignment.
```

Changing the CONTRIBUTORS.md file
---------------------------------
The first action is to fill the ``CONTRIBUTORS.md`` file in the repository
and to put the information about the group using the format such as below.
Add a line for each partner in a group.
```bash
#---- Edit CONTRIBUTORS.md, commit and push the change -------------------- 
# Use your favorite editor to edit CONTRIBUTORS.md.
# Enter the data about all group members in the following format.
```
```bash
group|firstname|lastname|github_account|email
-----|---------|--------|--------------|-----
G12|Noe|ZARWIN|noezarwin|noezarwin@gmail.com
G12|Babako|ELIE SCHMIDT|eliebjoe|babakojoe@ujf-grenoble.fr
```
```bash
# Save the file.
#
# Add the modified file to the files to be saved in the next commit
git add .
# Commit (e.g. save) the changes to the local repository
git commit -a -m "Set the authors for this repository"
# Push (e.g. publish) the state of the local repository to github
git push origin master
```
The changes should now appear on GitHub "group repository". 
Log in to GitHub and go to ``https://github.com/m2r/m2r-aeis-G12``
if you want to check by yourself.

Making and pushing changes
--------------------------

Time to work and deal with assignments. The process is all about
making changes, committing these changes to the "local repository"
and pushing these changes on GitHub to the "group repository".

```bash
#---- Making changes, committing and pushing them ------------------------- 
# Make some changes.
#
# Check which files have changed.
# Use the "-s" option if you prefer a shorter format.
git status        
# Add files to be committed.
# Use "git add ." to commit the whole directory
git add <files>
# Commit the files (save them in the local repository)
# Provide a useful message.
git commit -a -m ‘<message>’
# OPTIONAL: push changes to the "group repository" on GitHub
# You must do this at the end of a working session if you
# plan to continue on another machine (at home for instance)
# or if you want other group members to "see" the changes. 
git push -e origin master 
```

Pulling changes from the group repository
-----------------------------------------
If you work on various machines or if other group members
work in parallel your local repository may not contains
the last changes available on GitHub in the group repository.
In this case you have to "pull" these changes as following.

```bash
#---- Pulling changes from the group repository on GitHub -----------------
# Before making a "pull" make sure that you have committed all changes.
# "origin" refers to the "group repository" on GitHub.
# The "pull" command download the latest changes from the "group repository"
# then it try to merge these changes with those made locally. 
git pull -e origin master
```
Pulling changes may cause some merge conflicts. 
See [resolving merge conflicts](https://help.github.com/articles/resolving-a-merge-conflict-from-the-command-line/)
in this case.

Pulling changes from the root repository
----------------------------------------
During the course new assignments may be created and/or new material
may be added into an existing assignment, for instance to bring
precision to some tasks or to add additional skeletons. These changes
will be made available through the "root repository" which contains
assignment skeletons. In order to get last updates you just have to 
pull these changes in the same way you pull changes from your
"group repository".

```bash
# Before making a "pull" make sure that you have committed all changes.
# "root" refers to the "root repository" on GitHub.
# This "remote" repository has been declared in the "Getting assignment skeletons"
# section.
git pull -e root master
```
Pulling changes may cause some merge conflicts. 
See [resolving merge conflicts](https://help.github.com/articles/resolving-a-merge-conflict-from-the-command-line/)
in this case.
