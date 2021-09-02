---
title: Database Backup via SSH
lastmod: '2021-08-30T21:04:50.612Z'
slug: database-backup-ssh
weight: 10
type: docs
---

## Manual Backup

In order to back up your database via SSH you will require 2 things:

1. SSH access to your site. You will need to check with your hosting company to see if this is available.
2. An SSH client. Most OSes have a command line SSH command. If you are not comfortable with the command line, you will nee an application such as PuTTy.

Open your SSH client and log into your website. The command line prompt you will see will vary by OS.

For most hosting companies, this will bring you into your account's home folder.

### Local MySQL

Type in the following to create a backup in the current directory:

`mysqldump --opt -Q -u dbusername -p databasename > backupname.sql`

Or to create a backup in a separate directory (signified by /path/to/) type:

`mysqldump --opt -Q -u dbusername -p databasename > /path/to/backupname.sql`

You will be prompted for the database password. Enter it and the database will backup.

### Remote MySQL 

If your hosting company has you on a remote MySQL server, such as mysql.yourhost.com, you will need to add the servername to the command line. The servername will be the same as in your config.php. The command line will be:

Current directory:

`mysqldump --opt -Q -h servername -u dbusername -p databasename > backupname.sql`

Separate directory:

`mysqldump --opt -Q -h servername -u dbusername -p databasename > /path/to/backupname.sql`

### Storage

You can then download the backup file to your home computer. You can also create a directory on the server to store multiple backups. However, it is recommended that you maintain latest backup in a location other than your web server.

You can also ZIP or GZIP your backup file before storing it. Ask your host for help with this functionality.

## Automatic Backups

The vBulletin 5.X download includes a bash script to automate the backup process. This script can be found in the `do_not_upload` folder. 

On most servers, this script will create backups with the filename format of `%dbname%-%day%-%month%-%year%.gz`. This will allow you to keep multiple backups of your database. 

Once configured, you can execute this script via the command line. However, to get the most use out of it, the server should be configured to run it automatically at a set interval.

### Uploading the backup script

On the server machine, switch to your *home* directory. If necessary, create a new subdirectory called "backups". Then upload/copy the script into this directory using SFTP, SCP, or SSH.

```
cd ~
mkdir backups
cd backups
```

### Configure vb_backup.sh

Inside the file there is one variable that needs to be updated for configuration:

```
# Please change this variable to the path to your config.php
path_to_config="/home/example/htdocs/core/includes/config.php"
```

Update the path between the quotes to point to your Core Config file (`core/includes/config.php`).

If your server does not include the paths to mysqldump and gzip within the PATH server environment, you can specify these in the script as well.

```
# If you need the full path to the mysqldump binaries or gzip binaries set below
mysqldumpcmd=mysqldump
gzipcmd=gzip
```

If neceassary, update the path on the right for each command.

Once this is done, you can upload the file to your user's *home* directory on the server.

This file should not be placed in the `public_html` or `htdocs` directories.

### Permissions

Once the server is uploaded to your web server, it needs to have permission to be executed. On linux  the command to do this would be:

`chmod +x vb_backup.sh`

This will allow the server to process the commands in the script.

### Running the script

You can run this script from the command line with this command:

`~\backups\vb_backup.sh`

If you wish to run this script automatically, you will need to configure the task scheduling tool on your server to invoke it. For example using [crontab](https://www.man7.org/linux/man-pages/man5/crontab.5.html) on a Linux system. Consult the manual/documentation for your server's operating system for help on doing this.

Example crontab configuration to run the script daily at 23:00 hours:

```
0 23 * * * ~/backups/vb_backup.sh
```