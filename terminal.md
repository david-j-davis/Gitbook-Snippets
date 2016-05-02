# Terminal

####Export / Import Large Database from MAMP using Terminal
---
MAMP is a great tool for running servers locally, however, when you must export that site you have been developing locally and your database is huge, then you could have some problems with PHPMyAdmin.
One solution is to use terminal. The reason that I am writing this post is so that I can reference it in the future. It always takes me more that 10 minutes to figure this out since I never use terminal, so I thought someone else may find this of some use.

I understand there are probably many ways to do this, but this works for me, so… try out the code below.

Step One:

Open a new terminal window
Step Two:

Navigate to the MAMP install by entering the following line in terminal
cd /applications/MAMP/library/bin
Hit the enter key
Step Three:

Write the dump command
./mysqldump -u [USERNAME] -p [DATA_BASENAME] > [PATH_TO_FILE]
Hit the enter key
Example:
./mysqldump -u root -p wp_database > /Applications/MAMP/htdocs/symposium10_wp/wp_db_onezero.sql
Quick tip: to navigate to a folder quickly you can drag the folder into the terminal window and it will write the location of the folder. It was a great day when someone showed me this.
Step Four:

This line of text should appear after you hit enter
Enter password:
So guess what, type your password, keep in mind that the letters will not appear, but they are there
Hit the enter key
Step Five:

Check the location of where you stored your file, if it is there, SUCCESS
Now you can import the database, which will be outlined next.

IMPORT DATABASE INTO MAMP
Step One:

Open a new terminal window
CAREFUL: This will replace all tables in the database you specify!
Step Two:

/applications/MAMP/library/bin/mysql -u [USERNAME] -p [DATABASE_NAME] < [PATH_TO_SQL_FILE]
Hit the Enter Key
Example:
/applications/MAMP/library/bin/mysql -u root -p wordpress_db < /Applications/MAMP/htdocs/backupDB.sql
Quick Tip: Don’t forget that you can simply drag the file into the terminal window and it will enter the location of the file for you.
Step Three:

You should be prompted with the following line:
Enter password:
Type your password, keep in mind that the letters will not appear, but they are there
Hit the enter key
Step Four:

Check if you database was successfully imported
Navigate to phpMyAdmin in a browser
http://localhost:8888/MAMP/
I hope this helps, please let me know if anyone has any errors, questions or comments.