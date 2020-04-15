# Some Personal Notes on setup

My setup is probably a bit perculair. 

I worked on a LOT of projects during my bootcamp, and even before that. I actually started this Github account back in 2015, before I even really know how to use Github. Now that I have the account, and using it for the past month in the Bootcamp, this is how I do it.

I already have git-bash installed, and my github account all ready to go. 

1) I go to github and create a new repo under my account called assignment7, generate a default README. You can also create a LICENSE now. AND maybe the .gitignore as well. Choose the environment you usually program in. Or just leave it out. 

2) I go ahead create a LICENSE file and pick MIT licnese

3) I go to clone or download button and get the git@..... string and copy that into clipboard 

4) Back to home PC, and this is where it gets a bit tricky. 

5) Go to your home PC's "homework" directory, where you want to do all your work. open git-bash there. 

6) From the homework directory, 

```
git clone (paste the git string wtih right-click)
```

This will create a subdir called assignment7, same name as your repo, and download the two files in the repo, LICENSE and README.md (which is mostly blank). This actually also links your current directory with the "remote repo", i.e. the one on github, that you can push to or pull from. 

7) Now, on your PC (locally), add files to this subdir, usually by copying some files you downloaded off the school gitlab server specific to this assignment, probably pre-defined tests, assignment details, sample screenshots, and so on. I prefer to keep them all in one place, and delete the extra stuff whent he project is done, but it's up to you, 

8) Once done, do

```
git add .
git commit -m "your commit message"
git push
```

To push all the changes to github repo. 

9) Verify that all the changes had been uploaded into the repo by going to github and refesh the screen . 

# Possible problems

Github is complicated, and there are many places things can go wrong. If you reversed some of the steps, above (in the wrong order), while nothing catastrophic will happen unless you force thimgs, it can get a bit frustrating. 

## You already created the local subdir

if you have already created the local subdir, then git clone will error out saying the subdir already exists. 

The easiest way would be to rename the local subdir, do the git clone, then copy the stuff you have from the local subdir and remove the renamed version. 

Or you can do it the hard way, which is way more complicated, as you have to set the remote repo manually. On the other hand, this can probably give you a bit more appreciation on how git works. 

Some TL;DR things about git... I am not going to go over git fundamentals. You can read the github rookie guide or other tutorials on the point. The basic concept is simple: you have a local repo (your subdir), and you need to sync with with a remote repo where every change can be tracked, and if necessary, reversed, merged, and so on. We're just dealing with setup the link. 

```
git remote -v
```

This views what connection your local repo has with the remote repo. If this doesn't say anything, then you hve NO connection. As you just created the directory, you wouldn't have any connections. You can also reset the connection with *git init*. There are also commands like *git remote remove ...* but let's not go into that right now. Generally, you'd want to *git init* the subdir before you make it a repo locally. 

```
git remote add assignment7 git@github.com:yourname/assignment7.git
```

where git... is that *git@github.com:yourname/assignment7.git* you copied from the repo, remember? that green button? This manually adds the connection to that repo. 

Confirm this with the *git remote -v* command again. You should now see two lines

```
assignment7 git@github.com:yourname/assignment7.git (fetch)
assignment7 git@github.com:yourname/assignment7.git (push)
```

Good, connection has been estalished both ways: fetch, and push. However, you need to do one more thing... git needs to know which BRANCH to push onto. Generally, it'd be master, UNLESS you're working off a different branch with checkout, branch, and so. As we're just setting up, it'll be master. Basically, we're saying 'merge what I got with the master and leave it as default'. 

Now we need to specify the default as origin master

```
git remote add origin git@github.com:yourname/assignment7.git
```

This means you are adding the remote repo as your "origin", i.e. root of project. (even before "master") 

Now do a 

```
git pull origin master
```

This will download any files you got in the repo, such as LICENSE and README.md, down to your local repo, and merge it with the files you have locally. 

Now you can do

```
git add .
git commit -m "YYYYMMDD Some commit message" 
git push
```

If you run into an error here, like "failed to push some refs", that means you forgot to do the pull, your subdir and the repo has conflicts and/or different versions. This often happens when you did the LICENSE thing, or edited the README.md on github directily, thus made changes in the remote, and it no longer matched the local. Usually you can fix this by doing a git pull first (i.e. grab what the remote repo has, so you have the lastest), THEN do the git push ... again.  

if that doesn't seem to work, you can always override the error message by adding "-f" parameter to that git push line. This basically tells the git push to ignore any errors, full steam ahead, oveerwrite remote with local copy. 

Verify on github that your local repo and remote repo looks the same. 

And now, your two repos are setup and in sync. You can now develop locally and periodically git add, git commit, and git push your changes to the remote repo. 
