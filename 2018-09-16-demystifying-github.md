---
#layout: post
title: Demystifying Github
dark: False
#image:
#      url: /media/2018-09-16-demystifying-github/cover.jpg
---
## Intro:  
This post doesn't need an intro, the title says it all :smiley:


## Motivation:  
This might be a bold statement, but I would argue that anyone who ever had to use Github would have experienced the following emotions - :hushed: :weary: :cold_sweat: :rage: :confused: :expressionless:  
So this is my attempt to translate Github from Computer Science language to English. I don't pretend do be an expert, far from it, just hope to make someone's Git-journey a little easier than mine was...

## What is Github?
In simple words, it is a way to keep a copy of your documents (most commonly codes (Jupyter notebooks, python / R files, etc.)). It makes it easy to manage different versions of documents or share them with your team. It is perfect for keeping track of changes to documents related to a project being worked on by multiple people.
Think of it this way, if you wanted to make changes to your CV / Resume, you could use GitHub to store the best version on a master branch and whenever making changes, work on a copy of it, on a different branch. Once you're happy with the results, you would "merge" the two branches and the updated CV / Resume would become your new best version.

## How does it work?


## Must-Know Commands:

git clone
git add *file_names or "." for everything*
git commit -m "*your message*"
git push
git pull
git pull origin master
git stash
git checkout *branch_name*
git checkout -b *branch_name*

check what branches exist in the repo:
	git branch


**use with caution**
To go back one step before the last commit:
	git reset --hard HEAD~1

To merge the changes on git if on the non-master branch:
	git merge master


To merge the changes on git if on the master branch:
  git merge *branch_name*

to delete a branch:
git branch -D branch_name

**nice to knows**
rename branch

	1. If you are on the branch you want to rename:
	git branch -m new-name

	2. If you are on a different branch:
	git branch -m old-name new-name

	3. Delete the old-name remote branch and push the new-name local branch
	git push origin :old-name new-name

	4. Reset upstream branch for the new-name local branch
git push origin -u new-name

Pulling master changes to my own branch

	git remote -v
	git remote add upstream metis_repo_url
git pull upstream master
