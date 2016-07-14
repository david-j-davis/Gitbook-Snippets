How to ssh into your server for github deployment:

ssh into the server with terminal commands:

```ssh root@23.253.69.109
3D53F19k6GAp0809If1G
cd / (brings you to the root)
cd var/www/live
ls (displays contents in that folder)```

I then did terminal commands (disregard this):

```git init
```touch .gitignore
```touch README.md
```git remote set-url origin git@github.com:axcloud/axcientdotcom.git

I then opened up another terminal window and ssh'd into the server again:

```cd .ssh
```cat ~/.ssh/id_rsa.pub (to display ssh key)

Copy and paste the following ssh key into my github account under settings > SSH & GPG Keys
```ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCgQ3SqvGtoAG1+y+c85PAk4KeXc4XmSLmHIos1qj8zRbpCg5b6v+0gaDQKjCiT4dWSlhDOriRiQNet2FSx09PgvTl+ZrqpT6u4djAXwLj15fCYqjAascq6lG5hAtsSg31QtJw2Ov8ch+TrTNNZwwJO+j44K14S00i2DBHFPK6yuuYHORW7gKwdHRi0D4ZMFbhBXulABitnYQpwvBMkIohrl8AQey12eb+1ICorYIN0SdiUf7WSUNuJqHV6F6pImFiWZQ3CVcsDyMiwEa4mDA37ONELPFFErhNMf7u4GeRoDL8H/F/nsWbNQkGTyAWC64TyselP1M2KIAACOWXElzMv root@axcient.com

Now push and pull away:

 ```git push -u origin master
 ```git pull -u origin master

 ```exit (to close ssh connection)
