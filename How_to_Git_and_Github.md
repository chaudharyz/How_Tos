# git and github with cmd line
Following https://youtu.be/DnwEaa5QtpI?si=XRFCqeU2oLHBXB-3
## Configuration
To make it work, check if you have git in your computer
```
git --version
```

Add user details as below:
```
git config --global user.name "Sidhant Chaudhary"
git config --global user.email "s.chaudhary619@gmail.com"
```

To add github user account name, make an account on Github first and get username. connect using:

```
git config --global github.user "chaudharyz"
```

Some defaults to setup:
```
git config --global core.autocrlf input
git config --global core.editor "code --wait"
```

## Workflow
5 commands in general will work for 95% of work with git and github. These are: 
1. `git status`: check the current status of files, can be used at various stages, 
2. `git add`: to add or stage a change, 
3. `git commit`: to commit our staged change, 
4. `git push`: to push the files to github, 
5. `git pull`: to pull the latest uploaded version from github

The workflow in general is: 
1. **Start a new repository** 

when in the right main directory, 
```
git init .
 ```

2. **Adding and staging to git repo**
First the file is always added in git repo

```
git add <dir/file>
```

3. **Committing a file**

The added file is then followed by committing as below:

```
git commit <dir/file> -m "add commit message here"
```

You should check the status of your files at various stages using: 

```
git status <dir/file>
```

It also allows a possibility to undo.

4. **Upload/push on github**

First, make a repo online, ideally with the same name as the computer repository. 
*git source control* in VS code helps. 

To do it manually: (As done here: https://youtu.be/DnwEaa5QtpI?si=apLEzrK9dChBggYw&t=1394)
* go online, make repo, 
* copy html from code
* use following in command line
```
git remote add origin https://github.com/<your_github_account>/<your_github_repo>.git


```

Fetch Remote Content

Fetch the remote content to synchronize your local repository with the remote one.

```
git fetch origin
```
Merge Remote Changes

Merge the remote changes into your local repository. This step ensures that your local repository is up to date with the remote repository.

```
git merge origin/main --allow-unrelated-histories
```

If there are conflicts, you will need to resolve them. Git will provide instructions on how to do this.

After merging the changes, you can push your local commits to the remote repository.
```
git push -u origin master OR main
```

if the first 3 steps are fulfilled, now the selected files can be synced with github server using the following: 

```
git push
```

Sometimes, when multiple people are working on the same github repo, they might have made some changes that you want to sync locally before continue to work. To do so, 
```
git pull 
```
command should be used first.

**Not everything we have in our repository is wanted to be synced with github. We only want to sync mainly the code and the files we are changing. That means that the data and the output is not necessary to be in synch constantly.** 

To drop files which are big from repository `.gitignore` file comes in handy. Create the file using:

```
code .gitignore
# or 
nano .gitignore 
``` 

Add the directories or files in .gitignore to avoid them from syncing in the github repo. 

### How to access the old version of files from github?
1. Search the old versions using:
```
git log <file/dir>
```

2. Copy the commit hash code and run to see the version, file will open in nano: 


```
# file opens in nano
git show <commit-hash>:<file>

# to open in VScode reader
git show <commit-hash>:<file> | code -
```

3. to compare old version and the current version
Install git lens in VS code and then the current version of the file can be opened and compared using a button on top right

or

```
git log --follow -p -- <file>
```

Some other options with `git diff` are also available which I am unfamiliar to at this point. 

But Git lens feature in VS code works the best. 

### How to restore the old version from Git?
commit code is called **sha** for some reason

```
git checkout <sha> -- <file>
```

#### git flow
https://riffomonas.org/code_club/2020-07-09-github-flow 

1. Create an issue in your repository’s issue tracker on GitHub
2. Create and check out a branch in your local repository
git branch issue_1
git branch
git checkout issue_1
git branch
git status

3. Work on the issue. As you go through the issue, feel free to add to the thread for the issue on GitHub

4. Commit the change when you are done with the issue. In the commit message, include the statement “closes #[issue_number]”

5. Checkout your master branch
git checkout master

6. Merge your issue branch into the master branch. If you have conflicts, open the offending files and resolve the conflict and commit the change.

git merge issue_1

7. Push to your remote repository
git push

8. Refresh the issue and see that it has closed or close it yourself

