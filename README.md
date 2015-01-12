# procurve-watch
Creating backups of and monitoring changes on HP Procurve switches through SSH.

You will have a folder for each switch containing its current and previous configuration.
You will receive an email if a change is detected.

### Purpose of this script

1. to backup the configuration of Procurve switches through secure shell (No Telknet or TFTP),
2. to keep track of changess. Changes are emailed and logged.

### Audience

Anyone who may want to backup and keep track of the configuration of some HP procurve
 switches but doesn't have the resources to implement the bigger network management tools. 
Please note that this tool does not allow you control the switches (send commands).

### Security
 
procurve-watch uses sshpass to pass the switch password to the scp command.
The password will be stored in a text file in etc/procurve-watch.conf. 

If your switches are configured to use ssh keys for authentication, you can set 'USESSHKEYS=False' to True.

Procurve-watch does not need any special privileges and can be run by an unprivileged user.

### How do I get started?

#### Requirements

1. the ssh public key of the switches must be present in the 'known_hosts' file (maybe use ssh-keyscan),
2. you need to enable ssh file transfers with 'ip ssh filetransfer'.

#### Action plan

1. clone this project,
2. install 'sshpass' (like apt-get install sshpass),
3. set username password, email address and other settings in etc/procurve-watch.conf,
4. edit switches/(somefilename) and add the domain name or IP-address of your switches (one per line),
5. run 'procurve-watch'. 

**Security**: make sure that the entire procurve-watch folder structure is not accessible to other users.
Consider applying a chmod -R 600 on ./etc, ./configs and ./switches.

### Organising your switches

You can create a directory structure under the 'switches' folder. For example, you can create folders
for different sites. The folder structure you create here will be mimicked in the configs folder so 
you can quickly navigate to the appropriate switch configuration backup.

### Monitor changes

Just setup a cron job that runs procurve-watch every x hours or any interval you like.
Make sure to redirect the output of procurve-watch to some log file like this:

	0 * * * * /usr/local/procurve-watch/procurve-watch >> /var/log/procurve-watch
	
Make sure that the log file is writable by the user running procurve-watch. 

