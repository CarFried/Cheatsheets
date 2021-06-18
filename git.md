####Cheatsheet Git 
######1. How to get going?

Everything starts with a repository weather you create one locally or you clone an existing repository from the remote server. 

locally: ``git init <reponame>``
remote: ``git clone <repoUrl>``

######2. I do have a local repository how can I add a remote one?

The best way is to create a remote repository on the GUI of git and add the newly created repo to the local repository

``git remote add origin <repoUrl>``

In case you would like to change the URL afterwards: 

``git remote set-url <repoURL>``

To see the list of your rempote repositories

``git remote -v``

######3.How can I set the correct remote branch to merge to?

Usually the feature branch will be the branch to push to. To set the branch in this case you can simply just push the feature branch and the remote feature branch will be created. 

``git push -u origin <nameoffeaturebranch>``

or 

`` git push --set-upstream <remote> <featurebranch>``

If you would like to switch the remote branch you can use: 


``git push <remote> <branch with new changes>:<branch you are pushing to> ``


######4.Upstream, downstream, tracking - how is it all linked?

upstream (further ahead the git stream) is basically source from where you pull/clone your code to you. Therefore you are downstream (further down the git stream). The upstream branch is tracked by your local branch. 

######5. What is the difference between rebase and merge? 

Both commands integrate certain changes from a different branch BUT rebase changes the current head of the branch and changes the commit history whereas merge the two branches merges with a merge commit. 

Rebase: 
   git rebase checks for a upstream commit and adds again all following commits which were submitted  on the current branch (and changes the commit history by). Basically you put your work on top of the current changes from others. 
    ``git rebase <upstream>``
   to abort: 
    ``git rebase --abort``

   to select specific commits make use of the interactive history option
   ``git rebase -i <upstream>``
  
   to adjust the history you can use the following commands in the editor: 

     #  p, pick = use commit
     #  r, reword = use commit, but edit the commit message
     #  e, edit = use commit, but stop for amending
     #  s, squash = use commit, but meld into previous commit
     #  f, fixup = like "squash", but discard this commit's log message ```

 DO NOT REBASE ON PUBLIC BRANCHES

Merge: 
    git merge adds changes from another branch by merging the two branches together. Usually you want to integrate a feature branch into the master branch. To do so  we need to be on the branch that we are merging into.

    For example if you would like to merge into master you need to checkout to master and then add: 

    ``git merge <featurebranch/branch you would like to merge with current branch>``

    git will create a merge commmit. 

######Is Cherrypicking a fruit?

With cherrypicking you can interate a specific commit into another branch. You would have to search for the specific commit via ``git log`` and then checkout to the branch where you would like to integrate the change. To add the commit type: 
``git commit cherry-pick <commitid>``

flags: 

git will ask for commit message: 

``-edit``

git won't ask for commit message and simply transfers the target commit to the current branch's commit history:

``--nocommit``

adding a signoff line after the cherry-pick commit: 

``--signoff``

#######How do I switch between branches? 

``git checkout <branch>``
``git switch <branch>``

if you want to checkout to the previous branch: 
``git checkout -``

######I've forgot some stuff in my commit/commit -message how can I fix that?

You can use git commit --amend to add your staged changes to the previous commit and/or change the commit message. The current commit is hence overwritten by your changes. 

To correct the message: 

``git commit --amend -m"new message"``

To add forgotten changes to the current commit without changing the message: 

``git commit --amend --no-edit``

##### I want to get a remote branch to work with locally. What should I do?

To add a remote branch first list all the remote branches

``git branch -r``

or to see remote & local branches 

``git branch -a``

pick the remote branch you want to work with and and check it out with setting branch to track. 

``git checkout --track origin/<remotebranchname>``

or 

``git checkout -b <remotebranchname> origin/<remotebranchname>``

#####Shit! Detached head - what now? 

Do you have any changes in the detached head state which you want to keep?
1. NO 
    just checkout to a new branch - your "detached head" will be deleted 
    ``git checkout <previousbranch>``
    ``git switch   <previousbranch>``
2. YES 
   commit your changes and checkout a new branch your changes will be saved:
   ``git checkout -b <newbranch>``
   run:

   ``git log`` to verify that your commits are there
    
#####Stash is cash 

Assume you have to work on several branches and changes parallel which means you most likely switch branches but don't want to commit the current messy state. In order to save your working directory & index state you can use git stash.

run ``git stash`` to save the current work before switching branches 

run ``git stash list``to see the current WIP on your branches 

run ``git stash apply``to apply the latest stash on your branch or specifiy with ``git stash apply stash@{x}``which stash you would like to apply 

run ``git stash drop``to drop stashes

##### Ahh - My remote branches are still visible after completing a pull request (and deleting the remote source branch)

run ``git config --global remote.origin.prune true``

##### I don't want to add my untracked file and want to get rid of them

run ``git clean -<flag>``

available flags: -f (forced); -n (overview over untracked files) -f -d (include directories which are ignored by default)
            
