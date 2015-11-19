Using GitHub
============
To learn more about GitHub/Git have a look at 
[Git(Hub) section](http://scribetools.readthedocs.org/en/latest/github/index.html)
of <http://http://scribetools.readthedocs.org>. This section explain how to use
git/gitHub in the context of the course. 

Installing Git
--------------

To install git on your machine (if not already installed) have a look at 
the [Install the git toolkit](http://scribetools.readthedocs.org/en/latest/github/index.html#install-the-git-toolkit) 
section.

Configuring Git
---------------

THIS SECTION WILL BE COMMENTED

```bash
cd

#---- configure git-------------------------------------------------------------------------
git config --global user.name "Noe ZARWIN"
git config --global user.email "noezarwin@users.noreply.github.com"
git config --global credential.helper "cache --timeout=3600"

#---- Clone your repository  m2r-aeis-G00.git -----------------------------------------------
git clone https://noezarwin@github.com/m2cci/m2r-aeis-G00.git

#---- Configure your local repository -------------------------------------------------------
cd m2r-aeis-G00
git remote add root https://noezarwin@github.com/m2cci/m2r-aeis-root.git
git pull -e root master
ls -la
```

Working with Git
----------------
TO BE COMPLETED

```bash
git status
git add <file>
git commit -a -m ‘<message>’
git push origin master 
```
