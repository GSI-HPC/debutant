Debianization of LSI Megaraid SNMP agents
=========================================

Quick howto
-----------

1. Download the Megaraid Storage Manager tarball from Broadcom
   eg. <https://www.broadcom.com/support/download-search/?pg=Storage+Adapters,+Controllers,+and+ICs&pf=RAID+Controller+Cards&pn=MegaRAID+SAS+9271-4i>
2. Unpack the tarball:
   `tar xvfz …_Linux-64_MSM.gz`
3. Enter the `disc` subdir
   `cd ./disc` 
4. call debutant with the sas-snmp RPM as argument:
   `debutant lsi-sas-snmp sas_snmp-….x86_64.rpm`
   sas-snmp_….deb will be built in the current directory
5. Install the sas-snmp_….deb package
   Add it to /etc/snmp/snmpd.conf
   ```
   pass .1.3.6.1.4.1.3582 /usr/sbin/lsi_mrdsnmpmain
   ```

How it works
------------

The package contains two binaries:
1. `/usr/sbin/lsi_mrdsnmpmain` called by snmpd
2. `/usr/sbin/lsi_mrdsnmpagent` runs daemonized (see systemd unit)

Both communicate via shared memory and have to run with root privileges.

The original RPM configures snmpd to run with root privileges too.
This packages sets the suid bit on /usr/sbin/lsi_mrdsnmpmain instead,
allowing snmpd to run with its dedicated userid (Debian default).

Here is a Nagios/Icinga check to monitor machines with Megaraid adapters with sas-snmp:
https://github.com/willixix/WL-NagiosPlugins/blob/master/check_snmp_raid.pl
