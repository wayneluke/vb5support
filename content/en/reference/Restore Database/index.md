---
title: Restoring Your Database
slug: restoring-database
lastmod: '2021-08-30T23:37:54.917Z'
weight: 20
type: docs
---


In order to restore your database via SSH you will require 2 things:

1. SSH access to your site. You will need to check with your hosting company to see if this is available.
2. An SSH Client, such as PuTTy.

{{% alert title="Note:" color="info" %}}
If your database backup resides on your home computer, you will first have to upload it via SFTP to your website
{{% /alert %}}


Open your SSH client and log into your website. The command line prompt you will see will vary by OS. For most hosting companies, this will bring you into the SFTP root folder.

You can either change directoties to wherever the backup is located and type in the following:

`mysql -u dbusername -p databasename < backupname.sql`

Or if you do not want to change directories and you know the path to where the backup is located, type in the following:

`mysql -u dbusername -p databasename < /path/to/backupname.sql`

You will be prompted for the database password. Enter it and the database will backup.

If your hosting company has you on a remote MySQL server, such as mysql.yourhost.com, you will need to add the servername to the command line. The servername will be the same as in your config.php. The command line will be:

`mysql -h servername -u dbusername -p databasename < backupname.sql`

Or:

`mysql -h servername -u dbusername -p databasename < /path/to/backupname.sql `
