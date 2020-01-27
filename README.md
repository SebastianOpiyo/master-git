*Master-git
Becoming an expert in git.

*What to Learn  

    *The git commands to learn by heart
    *Branches
    *Doing the imports
    *Learning `Markdown`
    *Additional Hacks

*The Git Commands to learn by heart
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1. $ git init ~ initializes a local git repo and does introduce a .git file
2. $ git status ~ check the status of the working tree
3. $ git add <file(s)> ~ Add file(s) to index
4. $ git commit ~ Commit changes in the index
5. $ git push ~ push the chages from the local repo to the remote repo
6. $ git pull ~ pull the changes made. crutial in team development.
7. $ git clone ~ copy a project into your local folder for dev 
8. $ git remote -v ~ give the status of the branch you are working on.
9. $ git fetch ~ used to update a branch by comparing it to the remote changes
10. $ git rm ~ remove file or folder(use recursive option)
11. $ git log~ list the log info of the commits

*Branches*
// Name branched
$ git branch

// create a branch
$ git branch <branch_name>

// switch to a branch
$ git checkout <branch_name>

// To create a branch and switch to it immediately
$ git checkout -b <branch_name>


// delete branch locally
$ git branch -d <local_branch_name>

// delete branch remotely
$ git push origin --delete <name_of_the_remote_branch>

*Doing the Imports*

*Learning `Markdown`*

*Additional Hacks to set me aside.*
>> It begins with avoiding the use of the git GUI.
>> Use of the cmd ensures you learn a lot.
>> Avoid the username and password prompt by setting up the ssh
