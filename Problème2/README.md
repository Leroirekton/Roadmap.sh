Log Archiver

A simple Bash tool to archive log directories by compressing their contents into a timestamped tar.gz file. This is useful for system maintenance, freeing up space while keeping old logs for future reference.

Features

Command-Line Interface: Easy to use from the terminal.
Flexible Target: Accepts any log directory as an argument.
Timestamped Archives: Creates unique archives named with the date and time (e.g., logs_archive_20240816_100648.tar.gz).
Centralized Storage: Stores all archives in a dedicated directory (/var/log-archives by default).
Activity Logging: Logs all archive operations to a central log file (/var/log-archives/archive.log).
Error Handling: Includes checks for permissions, directory existence, and empty directories.
Requirements

A Linux-based operating system.
Root or sudo privileges (required to access common log directories like /var/log and to create archives in /var/log-archives).
Standard Linux utilities: tar, date, mkdir, du, grep, awk.
Installation

Save the script code above as log-archive.sh.
Make the script executable:
bash
chmod +x log-archive.sh
(Optional) Move the script to a directory in your PATH for easier access, e.g., /usr/local/bin/:
bash
sudo mv log-archive.sh /usr/local/bin/log-archive
Usage

Run the script with sudo and provide the path to the log directory you want to archive.

Basic Syntax

bash
sudo log-archive.sh <path-to-log-directory>
Example

To archive the logs for a custom application located at /var/log/myapp:

bash
sudo log-archive.sh /var/log/myapp
Output:

Starting archive process for directory: /var/log/myapp
Compressing logs to /var/log-archives/logs_archive_20240816_101530.tar.gz...
Archive created successfully: /var/log-archives/logs_archive_20240816_101530.tar.gz
Archive process complete.
A log entry will also be created in /var/log-archives/archive.log:

2024-08-16 10:15:30 - Successfully archived '/var/log/myapp' to '/var/log-archives/logs_archive_20240816_101530.tar.gz'. Size: 12M.
Configuration

You can change the default archive directory by setting the ARCHIVE_DIR environment variable before running the script.

bash
sudo ARCHIVE_DIR=/mnt/backups/logs ./log-archive.sh /var/log/myapp
Stretch Goals & Advanced Ideas

This project can be extended with more advanced features:

Automated Scheduling: Use cron to run the script automatically. For example, to archive logs every Sunday at 3 AM:
bash
# Edit the crontab
sudo crontab -e

# Add the following line
0 3 * * 0 /usr/local/bin/log-archive.sh /var/log/myapp > /dev/null 2>&1
Email Notifications: Pipe the output or use the mail command to send an email upon completion or failure.
Remote Transfer: Use scp or rsync to transfer the completed archive to a remote server or cloud storage (like AWS S3).
Log Rotation: Modify the script to delete archives older than a certain number of days to manage disk space on the archive server itself.
License

This project is open-source and available under the MIT License.
