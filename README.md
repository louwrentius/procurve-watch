# procurve-watch
Creating backups and monitoring changes on HP Procurve switches through SSH

You will have a folder for each switch containing its current and previous configurations that differ from the current.

# Purpose of this script

1. To backup the configuration of Procurve switches through secure shell (No Telknet or TFTP)
2. To keep track of changes in the configuration files. Changes are emailed and logged.

# Security
 
procurve-watch uses sshpass to pass the switch password to the scp command.
The password will be stored in a text file in etc/procurve-watch.cfg. 

If your switches are configured to use ssh keys for authentication, you can set 'USESSHKEYS=False' to True.

# How do I get started?

- Requirements

1. The ssh public key of the switches must be present in the known_hosts file
2. You need to enable ssh file transfers with 'ip ssh filetransfer'

- Action plan:

1. Clone this project
2. install 'sshpass' (like apt-get install sshpass)
3. set username password, email address and other settings in etc/procurve-watch.conf
4. edit switches/<somefilename>.txt and add the domain name or IP-address of your switches (one per line)
5. run 'procurve-watch' 

# Example of file containing switches

sw01.company.local
sw02
192.168.10.21
192.168.10.22

# Monitor changes

Just setup a cron job that runs procurve-watch every x hours or any interval you like.

