# Usage
This docker extends the great docker https://hub.docker.com/r/muccg/pgbackup/, which in its turn is based on https://wiki.postgresql.org/wiki/Automated_Backup_on_Linux.

The script automatically rotates logs. Defaults are to keep 7 daily logs before deleting the oldest one, keep one per week (defaults to the one on Friday) and keep one per month (by default the one made on the first of the month).

Basic usage:

	docker run -it -v /data/pgbackup:/data -e PGUSER=someuser -e PGPASSWORD=somepass -e PGHOST=postgresql pgbackup backup

which will dump all available databases into the shared volume.

To keep the docker running whilst making a daily backup, just add the daily word:

	docker run -it -v /data/pgbackup:/data -e PGUSER=someuser -e PGPASSWORD=somepass -e PGHOST=postgresql pgbackup backup daily

In this case the script starts by making a backup and then sleeps for 24 hours.

Encrypting the backup can be done by adding environment variable ENCRYPT and set it to 'yes' with the password set in the ENCRYPT_PASSWORD environment variable.


	docker run -it -v /data/pgbackup:/data -e PGUSER=someuser -e PGPASSWORD=somepass -e PGHOST=postgresql -e ENCRYPT=yes -e ENCRYPT_PASSWORD=some_secret pgbackup backup
