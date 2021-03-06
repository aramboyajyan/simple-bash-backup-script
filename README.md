# Simple bash script for backing up website files and the database

This is a very simple bash script used for backing up the files and the database of your website. You can use it through cronjob. It uses [`mysqldump`](https://dev.mysql.com/doc/refman/5.5/en/mysqldump.html) command for exporting the database, so it should work with larger databases without problems as well.

The script is not system specific. This means that you can use it for backing up CMS-based websites (WordPress, Drupal, Joomla), custom websites, APIs, etc.

## Setup

1. Copy the `sample.cfg` to `backup.cfg`.
2. Open the `backup.cfg` and set the following items:
    - `project_name` - this will be used for generating the filenames. It should not contain spaces or special characters.
    - `date` - date string that will also be used in filenames. You don't have to change this.
    - `website` - path to the website files.
    - `backup_directory` - path to the backup directory.
    - `db_name` - name of the database.
    - `db_user` - username used for accessing the database (*).
    - `db_pass` - password used for accessing the database (*).
3. Make sure that the `backup.sh` is executable: `chmod +x backup.sh`.
4. Use the script. You can either:
    1. Run it manually from terminal: `./backup.sh`.
    2. Run it through a cronjob: `bash /path/to/this/script/backup.sh >/dev/null 2>&1`

(*) Ideally, you would not include database credentials in configuration, but add them to the `.my.cnf` file in the home directory of your user instead. This is for added security. Here's an example:

    [client]
    user="YOUR_USER"
    password="YOUR_PASSWORD"

You can read more about end-user guidelines for MySQL password security [here](https://dev.mysql.com/doc/mysql-security-excerpt/5.7/en/password-security-user.html).

The script will generate 3 compressed files:

1. `[date]-[project-name]-files.zip` which contains the complete target directory.
2. `[date]-[project-name]-database.zip` which contains the export of target database.
3. `[date]-[project-name]-output.zip` which contains all output messages printed from the `zip` command.

## Contributing

All contributions are welcome! Just clone the repo, make the changes and submit a merge request with explanation of the changes. I'll have a look as soon as I can.
