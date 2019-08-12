---
layout: post
title: How to Setup Automatic Backup for your Ghost Blog
featured: true
image: assets/images/ghostbak.jpg
---
Data loss can happen any where, yet we can't afford losing data. We have to be prepared one way or the other. We can avoid this using our webhost's backup plans but it'll cost us some bucks.

We can do it on our own for free using Google drive as our backup host. I've developed an easy to use command line interface to automate this task. You can find the [source code](https://github.com/dkarthe/ghost-backup) on GitHub.

## How it works
* Schedules a daily task on your blog server.
* Task runs daily and pushes backup archives to your Google Drive without your consent or intervention (Initial authentication required).
* You'll also get daily notification on Telegram about backup status if you want.

## Setup
Setup will be simple and straight forward. Whole setup process will be interactive. You just have to run following two commands on your blog server.

```
git clone https://github.com/dkarthe/ghost-backup && cd ghost-backup
python3 setup.py
```
After executing the above two commands, you'll be welcomed by an interactive command line interface. There will be on screen instructions. Still, I'll walk you through each step.

The whole purpose of this post is taking daily backup of your blog database. But, you can also backup your images & themes along with DB.

It stores the backup files as `.tar.gz` archives inside the folder `Ghost Backup`. It overwrites the previous file daily. But, we can get upto last 30 revisions. To get the previous version of the backup right click the file on Google Drive and select Mange versions....

**Note:** Whenever you provide invalid input, command line will ask for your input again.

* If you want to backup your images or themes or both give yes when prompted and give the absolute path where images or themes directory resides.
* When asked for your DB details like username, password, host, database name give the details correctly else you've to rerun the setup.
* Wait till the external dependencies download completion.
* Now, you'll be asked to visit a URL to obtain authorization code.
* Visit that URL and choose the Google account on which you want to save the backup files.
* Copy the authorization code you see on browser & paste it on the terminal.
* That's it Google Drive setup is done.
* It is highly recommended to setup Telegram notifications as you'll get to know about the status of daily backup or about the errors occurred in the process.

## Backup file Name format
```
Example: `20180115172329.tar.gz`
1-4 digits `2018` -> Year
5-6 digits `01` -> Month
7-8 digits `15` -> Date
From 9th digit `172329` -> Time, represents `7:23:29`
```
Read - Create a nice AMP template for your Ghost blog.

## When the Backup will happen
Backup task will be scheduled to run at midnight (i.e) 12 in the night. Timezone will be of your blog server. To change the timezone or to change the time at which the task runs daily you can run the following command.

```
sudo dpkg-reconfigure tzdata
```

After changing your timezone, you've to restart cron to make the changes take effect.

```
sudo service cron restart
```

## How to Restore Backup
Download the archive from your Google Drive. Use scp to transfer the files from your local machine to server. To unpack the archive use the below command.

```
tar -xvzf filename.tar.gz
```

Finally, dump the .sql file to your database.

```
mysql -hhostname -uroot -ppassword dbname < filename.sql
```
Replace the `hostname`, `root`, `password`, `dbname` with what is appropriate for you.

## Troubleshooting
This section will deal with the possible issues you'll face during setup or backup process.

## Permission denied error
Sometimes the logged in user will not have access to copy the script files to the `/opt` directory. In that case run the following command to eliminate the issue. This happens during setup.

```
sudo setfacl -R -m u:$(whoami):rwx /opt
```

```
setfacl: command not found
```

If you get the above error, install acl utility.

```
sudo apt install acl
```

If you had setup backup for images or themes, When you don't have write access to the images or themes directory, you'll get exception during the execution of backup script. In that case run the following command.

```
sudo setfacl -R -m u:$(whoami):rwx /var/www/ghost/content
```
Replace the marked path with yours if you have different installation path. Permission denied is the most common error during setup. If you get this error anywhere during the process, replace the marked path with the path reported by the error.

## Privacy Policy
The app 'Ghost Blog Backup' is free to use and it doesn't collect or use or share any user info. However authorization code is obtained from you just to authenticate your access to Google Drive. All the required tokens are stored on your blog server.
