# libvirt_vm_backup
##At a glance
This script is a wrapper around the [virt-backup.pl](http://gitweb.firewall-services.com/?p=virt-backup;a=blob_plain;f=virt-backup;hb=HEAD) script by Daniel Berteaud. It adds the ability to retain more than one backup per time, stored in tar archives.

It's a shell script whos dependancies are:
* virt-backup.pl (already stored in this repo)
* tar (usually already there in your distro)
* a properly configured mail/sendmail program (optional for emailing)
* pbzip2: a parallel implementation of the bzip2 algo (usually available in your repos, maybe EPEL in CentOS)

On its turn, virt-backup.pl requires:
* Perl (of course)
* the XML::Simple perl package
* the Sys::Virt perl package

All of these are available in the statndard CentOS repo as well as in standard repo from Debian and Ubuntu

It _is_ rude and it _is not expected_ to be really elegant, but you should be able to edit it quickly to get your backups done.
If you do not want to make use of pbzip2, you can easely change the --compress option to fit your needs, but having a parallel zip utility is really useful to reduce backup timings
## Usage
My standard usage is:

1. make a copy of the prototype
2. edit the initial variables:
  * **VMS**: a space separated list of VM names as shown by 'virsh list'
  * **MAILTO**: a comma separated list with dest mail to send the backup log to (NO SPACES)
  * **KEEP**: how many backups would you like to keep? must be >= 1
3. copy the script into one of the cron.* folders to get a backup at given scheduled times.

_OR_

3a. add some entries in crontab to get more fine-tuned control over backup scheduling
##Testing
I'm currently using this script to define backups of a number of production VMs running on a CentOS7 libvirt/KVM host
 
