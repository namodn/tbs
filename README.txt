Aeronet Backup
---

This file explains how to perform useful administrative functions with the
Aeronet backup scripts. Contact Rob Helmer <robert@namodn.com> with questions/
problems/suggestions.


--
ACCESSING BACKUPS 
--
Backups are available in the backup user's home directory, sorted by date
in archive/ ( by default the full path is /home/backup/archive/ ).

Backups are also available to allowed hosts only via a web interface.


--
ADDING/REMOVING NEW HOSTS AND BACKUP PATHS
--
To add a new host to back up from ( for example, "hubert" ), you would create 
a file in the backup user's home directory called "hubert.nightly".

NOTE: this must be a hostname, not an IP address. Add an entry in /etc/hosts
if neccessary, or use DNS.

The ".nightly" part of the filename is the "frequency". It is whatever you
pass to the scheduler.

Put an alias and an entry for each path on "hubert" that you would like 
backed up inside the "hubert.backup" file.

Example hubert.backup :
---
etc:/etc
home:/home
confidential:/home/secret/stuff
--

To remove a path, delete the line from the "hubert.backup" file. To remove
hubert from the list of backed up hosts, delete the "hubert.backup" file.


--
ADDING/REMOVING EMAIL ADDRESS FOR NOTIFICATION
--
Email notification uses the standard Sendmail ~/.forward mechanism. Edit the
backup user's ~/.forward file to add or remove users from the notification
list.


--
CHANGING SCHEDULE
--
The backup system uses the standard Unix cron mechanism for scheduling 
backups and for purging old files.

Run "crontab -e" as the backup user to adjust these schedules. To schedule
a backup time, run "$HOME/bin/scheduler $FREQUENCY" and to schedule a purge 
time run "$HOME/bin/purge".

See "man cron" for more information on the Cron mechanism. It is also possible
to run "scheduler" by hand when logged in as the backup user, or use the Unix 
at mechanism to schedule a one-time backup ( see "man at" for more information )

--
EXAMPLES
( NOTE - These examples will back up ALL hosts and paths specified in the 
hostname.backup files in the backup user's home directory. Move these files
around as neccessary ).
--

EXAMPLE OF A SCHEDULED ONE-TIME BACKUP 
( logged in as backup user )
--
at 5:00pm ( Enter )
at> scheduler ( Enter )
at> ( Ctrl-D )

EXAMPLE OF AN UNSCHEDULED ONE-TIME BACKUP
( logged in as backup user )
--
scheduler ( Enter )
