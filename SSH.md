How to ssh into your server for github deployment:

ssh into the server with terminal commands:

```ssh root@example.com

cd / (brings you to the root)
cd var/www/live
ls (displays contents in that folder)```

I then did terminal commands (disregard this):

```git init
```touch .gitignore
```touch README.md
```git remote set-url origin git@github.com:your/repo.git

I then opened up another terminal window and ssh'd into the server again:

```cd .ssh
```cat ~/.ssh/id_rsa.pub (to display ssh key)

Copy and paste the ssh key into my github account under settings > SSH & GPG Keys

Now push and pull away:

 ```git push -u origin master
 ```git pull -u origin master

 ```exit (to close ssh connection)
