#git & github
---
GIT Commands:

- Make changes to file in text editor
- Add changes view Gitbash/command line
- Commit changes to git
- Continuous integration, adding code into master on a continual basis to eliminate massive changes.

- Use git help for help directory
- Use cd ~ to go to root
- Use cd /c/... to arrive at files
- Use mv and then file name to move files
- Use git init to track a project in whatever directory
- Use ls -la to see directory of files
- Use git add .(or add file name) to add an entire project to track
- Use git add -A for adding anything and everything like magic
- Use git commit -m "message goes here" to commit the add files
- Use git log to see a log of file changes and commit
- Use git status to see what files are not commited
- Use git diff to see changes to files that are in the working files
- Use git diff --staged to see changes in the add stage
- Use git rm <file> to remove file followed by git commit to remove the file into the staging area then to the trash. (File is saved in repository)
- Use git checkout to change modified files back to the repository change (use git checkout -- <file>  to just change one file)
- Use git reset HEAD <file> to take a file off the add and back to working file
- Use git commit --amend -m "message here" to amend a commit
- Use git revert (first ten digits of sha #) to revert a commit change on a particular file.

Git Workflow for Collaboration:

- git checkout master
- git clone

    - git clone https://github.com/USERNAME/REPOSITORY.git
    - # Clones a repository to your computer

- git fetch

    - git fetch remotename
    - # Fetches updates made to a remote repository

- git merge origin/master

    - git merge remotename/branchname
    - # Merges updates made online with your local work

- git checkout -b (new branch for day's work)
- git add dayswork.html
- git commit -m "Added a new page"
- git fetch (make sure Im up to date)
- git push -u origin new_branch
- git pull is a convenient shortcut for completing both git fetch and git mergein the same command

    - git pull remotename branchname
    - # Grabs online updates and merges them with your local work

Fetch (pull) before you work. Fetch before you push! Fetch often! Then merge!

[Github.com forking a repo:](https://help.github.com/articles/fork-a-repo/)

[Github.com syncing a fork:](https://help.github.com/articles/syncing-a-fork/)

[Github.com pushing to remote:](https://help.github.com/articles/pushing-to-a-remote/)
