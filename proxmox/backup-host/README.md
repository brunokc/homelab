# Backup Host

Uses proxmox-backup-client to backup a proxmox (PVE) host

## Installation

Copy the files in this directory to your host starting from the root (/):

```bash
cp -aruv . /
```

Adjust settings in /etc/default/pbs-host-backup

## Configuration

You'll need to create a new token, specifically to give this script access to 
creating backup on your backup server.

### From the UI

Assuming your have the backup store already registered in your proxmox server:

1. On your backup server (PBS), click on the Configuration -> Access Control node
2. Click on the API Token tab and then on the Add button
3. Add a new token with a suggestive name (e.g.: pve01Backup) and description 
(e.g.: Token used to create backups for host pve01)
   1. Make note of the Token ID and Secret to be used later (this is your only 
      opportunity to save the Secret)
4. Now click on the Permissions tab and click the Add button and choose API 
   Token Permission
   1. Select /datastore or /datastore/<name> under Path
   2. Select your recently create token under API Token
   3. Under Role, select DatabaseBackup
   4. Select the Propagate checkbox, especially if you have selected /datastore
      under Path, so the script will have access to any datastore.
   5. Take note of the token (copy it) to be used in the next step
5. Back on your host, create (or edit) file /usr/local/etc/pbs-host-backup-token
   and paste the token (the Secret from step 3.1 above) as the first line of that
   file.
6. Reload systemd so it will see the new host backup service you just installed:
   `systemctl daemon-reload`

You're done!
