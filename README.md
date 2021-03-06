
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Intro to Git and GitHub

This is a very brief introduction to the program
[git](https://git-scm.com/) and the associated
[GitHub](https://github.com/) website. The intent of this is to provide
a walk through with code you should try while getting familiar with this
software and the start of a workflow. git is incredibly powerful but
complex software. There are tons of great resources but it’s often
difficult to get started. [Happy Git and GitHub for the
useR](https://happygitwithr.com/) by Jenny Bryan is a fantastic and much
more throrough *introduction*, but still just the tip of the iceberg.

**Warning before you start** - avoid ever committing lots of data in
git. Git is just for the code and VERY small amounts of data (including
images). Add data files and folders to the `.gitignore` file. Once you
have ever committed a large file, it becomes very difficult to flush it
from the git history and can break things badly. This has ruined many a
day.

## Create a Repository

The first step is to create a repository, or repo for short, on GitHub.
This can be on your own account or on the [GARFO Organization
account](https://github.com/NOAA-Fisheries-Greater-Atlantic-Region).
Click the plus symbol in the upper right hand corner and select “new
repository”. This is where you can set the owner to be you or the
organization. For this activity, I recommend calling it something like
`sandbox_lastname` to indicate it’s just a practice, play area that can
be deleted at any time. It’s also good to initiate it with a `README.md`
file when it asks.

## Clone the Repository

You can clone the repository to get a copy on your local machine using
the command line:

    git clone https://github.com/NOAA-Fisheries-Greater-Atlantic-Region/sandbox_hocking.git

or you can use RStudio by selecting `New Project` -\> `Version Control`
-\> `Git` then pasting in the URL of the repo and telling it where on
your computer you want to put the cloned copy. It will create a new
folder with the name of the repository in the directory you select so
you don’t need to create a new folder for it.

This will copy all of the files from the repository to your computer and
set up a hidden `.git` folder that will record all of the changes your
commit over time.

## Make a change

Add a text file called `file1.txt` to the new folder. If you want to do
this via command line you can run:

    cd sandbox_lastname

to get into the folder you created, then

    nano file1.txt

to open/create the file. Then type “Initial Text” (or whatever you want)
into the file. Ctrl-x will exit the nano text editor and then type “Y”
to save and hit enter.

Now look in your file explorer to see that there is a file called
`file1.txt`. Via command line this would be `ls -alF` to view all the
files.

## Avoid big files

To avoid accidentily committing or even tracking large files I usually
open the `.gitignore` file in RStudio or your favorite text editor and
add

    *.pdf
    *.csv
    *.tif*
    *.rdata
    *.rds
    
    data/

These can be changed later to specific files or folders but it’s a good
place to start.

## Commit a change

Now that you have made this change you need to commit it. This creates a
point that you can go back to if you mess something up in the future.
First check the status of git

    git status

It will tell you that you have untracked files. You want to add these to
the git tracking system

    git add file1.txt

It’s best to only add single files or groups of related files at one
time because anything added will then be committed. If you add lots at
once then mess up just one of them it becomes very difficult to undo
just that one change and not all the other files.

    git commit -m "added first file for testing"

Each git commit needs a message. This should be informative and really
about why you made a change rather than just what was changed (which you
could see with `git diff`).

## Push to GitHub

Now that you have a local change you might want to add this to GitHub so
it’s backed up on the web and available for colleagues or even your use
on another computer.

    git push origin master

Sometimes the first time you push you have to add the flag u

    git push -u origin master

The origin is the name of the default connection to the remote
repository you set up in GitHub which you can see with

    git remote -v

## GitHub Issues

GitHub issues are a great way to keep track of decisions you make and
things you try or want to try. Go to the GitHub repo, click on issues,
and create a new issue. Call it `fastjoin` and write a message about
wanting to test a faster way to join tables.

## Create a branch

Once you have some working code, you often want to test things without
breaking the parts that do work. This can get messy when just trying to
comment things in and out of the code and sometimes you want to keep the
code working and running while you or colleagues develop additional
features. This is where branches come in. The main branch in git/GitHub
is called `master` (this is likely to change to something like `main`
soon). I highly recommend associating all branches with GitHub issues.
If you wanted to try out a way of joining data more efficiently, you
might create a branch off the master called `fastjoin` (with the
reasoning and thoughts behind it in the GitHub issue you previously
created).

    git checkout -b fastjoin master

This checks out (switches your files) to the fastjoin branch and the
flag b (`-b`) creates the branch in the process from the master. Now
create a second file called `file2.txt`, add it, and commit it (I
recently found out that if you don’t commit it, then it will follow you
from branch to branch until you commit it to one of the branches which
is not ideal).

    echo "initial text for file 2" > file2.txt
    git add file2.txt
    git commit -m "added second file to testing branch"

Now look at your files in file explorer and you should see both of these
(refresh if necessary) and/or use `ls -alF` on the command line.

## Push new branch to GitHub

Now you want to send this new branch to GitHub but not as part of the
master branch

    git push origin fastjoin

After running this code, go to the GitHub page and on the left hand side
there is a button that says “master”. Click on this and it should now
show a dropdown list that includes master and fastjoin branches.

## Merge branches

Now after some testing you decide that the fastjoin is good and you want
to merge that back into the master branch. So switch back to your master
branch

    git checkout master

If you look in your file explorer and using `ls -alF` you will see that
`file2.txt` is missing. That is because it only exists in the parallel
universe of the `fastjoin` branch. Let’s merge them now

    git merge fastjoin

**Note** - you may have to do a commit message for this and in many
command line systems it brings up vi or vim or something without
instructions for saving/exiting. In mine (Windows 10, git bash command
line) I type `:x` to exit.

Now `ls` and your file explorer (after refreshing) will show both files.
At this point it’s only local and not on GitHub. Use

    git push origin master

to send that to GitHub. You can always leave branches hanging and never
merge them. You can check what branches you have with `git branch -v`.
If you ever want to delete a branch that you don’t need or have merged
you can run `git branch -d fastjoin`.

## Closing and issue

Now that you’ve successfully made some changes with commit points to
return to if there’s a problem in the future, you want to close out the
related GitHub issue. Go to the GitHub repo and that issue. Write a new
comment celebrating your amazing new success then “comment and close”
the issue.

**Congratulations you did it\!\!\!**
