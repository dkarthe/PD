---
layout: post
title: How to Install Ghost on Ubuntu 
image: https://res.cloudinary.com/kd/image/upload/v1556866498/KD/qbvohcxc8pi7ndkvnbcl.jpg
kayword: ghost,ubuntu,install
---

A full guide for installing, configuring and running Ghost on your Ubuntu 16.04 or 18.04 server, for use in production.

## Overview

This the official guide for self-hosting Ghost using our recommended stack of Ubuntu 16.04 or 18.04. If you're comfortable installing, maintaining and updating your own software, this is the place for you. By the end of this guide you'll have a fully configured Ghost install running in production using MySQL.

## Prerequisites
The officially recommended production installation requires the following stack:

* Ubuntu 16.04 or Ubuntu 18.04
* NGINX (minimum of 1.9.5 for SSL)
* A supported version of [Node.js](https://nodejs.org/)
* MySQL 5.5, 5.6, or 5.7 (not >= 8.0)
* Systemd
* A server with at least 1GB memory
* A registered domain name

Before getting started you should set an **A record** from the domain you plan to use, pointing at the server’s IP address and ensure that it's resolving correctly. This must be done in advance so that SSL can be properly configured during setup.

## Server Setup
This part of the guide will ensure all prerequisites are met for installing the Ghost-CLI.

### Create a new user 
Open up your terminal and login to your new server as the root user:
```
 # Login via SSH
ssh root@your_server_ip

 # Create a new user and follow prompts
adduser <user>
```
> Note: Using the user name `ghost` causes conflicts with the Ghost-CLI, so it’s important to use an alternative name.

```
# Add user to superuser group to unlock admin privileges
usermod -aG sudo <user>

# Then log in as the new user
su - <user>
```
## Update packages
Ensure package lists and installed packages are up to date.
```
# Update package lists
sudo apt-get update

# Update installed packages
sudo apt-get upgrade
```
Follow any prompts to enter the password you just created in the previous step.

## Install NGINX
Ghost uses an NGINX server and the SSL configuration requires NGINX 1.9.5 or higher.
```
# Install NGINX
sudo apt-get install nginx
```

If `ufw` was activated, the firewall allows HTTP and HTTPS connections. Open Firewall:
```
sudo ufw allow 'Nginx Full'
```
## Install MySQL
Next, you'll need to install MySQL to be used as the production database.
```
# Install MySQL
sudo apt-get install mysql-server
```
## MySQL on Ubuntu 18.04
If you’re running Ubuntu 18.04, a password is required to ensure MySQL is compatible with Ghost-CLI. This requires a few extra steps!
```
# To set a password, run
sudo mysql

# Now update your user with this password
# Replace 'password' with your password, but keep the quote marks!
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

# Then exit MySQL
quit

# and login to your Ubuntu user again
su - <user>
```
## Install Node.js
You will need to have a supported version of Node installed system-wide in the manner described below. If you have a different setup, you may encounter problems.
```
# Add the NodeSource APT repository for Node 8
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash

# Install Node.js
sudo apt-get install -y nodejs
```
## Install Ghost-CLI
Ghost-CLI is a commandline tool to help you get Ghost installed and configured for use, quickly and easily. The npm module can be installed with `npm` or `yarn`.
```
sudo npm install ghost-cli@latest -g
```
Once installed, you can always run ghost help to see a list of available commands.

## Install Ghost
Once your server is correctly setup and the `ghost-cli` is installed, you can install Ghost. The following steps are the recommended setup. If you would prefer more fine-grained control, the CLI has flags and options that allow you to break down the steps and customise exactly what they do.

>Note: Installing Ghost in the `/root` or `home/<user>` directories results in a broken setup. Always use a custom directory with properly configured permissions.

## Create a directory
Create a directory for your installation, then set the owner and permissions.
```
# We'll name ours 'ghost' in this example; you can use whatever you want
sudo mkdir -p /var/www/ghost

# Replace <user> with the name of your user who will own this directory
sudo chown <user>:<user> /var/www/ghost

# Set the correct permissions
sudo chmod 775 /var/www/ghost

# Then navigate into it
cd /var/www/ghost
```
## Run the install process
Now you've made it this far, it's time to install Ghost with a single command 😀
```
ghost install
```

## Install questions
During install, the CLI will ask a number of questions to configure your site.

### Blog URL
Enter the exact URL your publication will be available at and include the protocol for HTTP or HTTPS. For example, `https://example.com`. If you use HTTPS, Ghost-CLI will offer to set up SSL for you. Using IP addresses will cause errors.

### MySQL hostname
This determines where your MySQL database can be accessed from. When MySQL is installed on the same server, use `localhost` (press **Enter** to use the default value). If MySQL is installed on another server, enter the name manually.

### MySQL username / password
If you already have an existing MySQL database enter the the username. Otherwise, enter `root`. Then supply the password for your user.

### Ghost database name
Enter the name of your database. It will be automatically set up for you, unless you're using a **non**-root MySQL user/pass. In that case the database must already exist and have the correct permissions.

### Set up a ghost MySQL user? (Recommended)
If you provided your root MySQL user, Ghost-CLI can create a custom MySQL user that can only access/edit your new Ghost database and nothing else.

### Set up NGINX? (Recommended)
Sets NGINX up automatically enabling your site to be viewed by the outside world. Setting up NGINX manually is possible, but why would you choose a hard life?

### Set up SSL? (Recommended)
If you used an `https` Blog URL and have already pointed your domain to the right place, Ghost-CLI can automatically set up SSL for you using Let's Encrypt. Alternatively you do this later by running `ghost setup ssl` at any time.

### Enter your email
SSL certification setup requires an email address so that you can be kept informed if there is any issue with your certificate, including during renewal.

### Set up systemd? (Recommended)
`systemd` is the recommended process manager tool to keep Ghost running smoothly. We recommend choosing `yes` but it’s possible to set up your own process management.

### Start Ghost?
Choosing `yes` runs Ghost, and makes your site work.

Once Ghost is properly set up it's important to keep it properly maintained and up to date.
