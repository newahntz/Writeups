

Scenario: We had a MSP come in to install some new software who, upon assessing our systems, has determined that Apache and Active Directory are both configured in an insecure manner. We have been directed to refer to STIGS (Security Technical Implementation Guides) by the Defense Information Systems Agency for remediation. Our primary focuses will be on Prod-Joomla and Domain-Controller for STIG compliance. 

Our colleague has too much on their plate right now so we have been tasked with heading up this project. They have been kind enough to provide us reference materials at /home/playerone/Desktop/STIGs and have directed us to focus on STIG CAT I. 

STIG CAT I is the highest level in the STIG outline, covering settings that are most at risk for exploitation. These settings have the highest impact on the wider network if exploited and are likely to directly lead to data breaches or LoS (Loss of Service). These are high severity and should be resolved first.


Apache hardening

1) Open the STIG viewer
	1) java -jar STIGViewer_1.2.jar
2) Import from zip U_Apache_2-2_UNIX_V1R9_STIG.zip
3) Filter by CAT I keyword
4) Per STIG WG190 A22: Web server software must be a vendor-supported version.
	1) sudo apt install --only-update apache2
		1) this produces an error on apache2 restart due to authz and mpm conflicts
		2) sudo a2dismod authz_default
		3) ls /etc/apache2/mods-available | grep mpm
		4) sudo a2enmod mpm_prefork
		5) sudo a2enmod authz_core
	2) Upon fixing the above issues, the page was unable to render PHP output
		1) sudo apt install php libapache2-mod-php
5) Per STIG WG200 A22: Administrators must be the only users allowed to access the directory tree, the shell, or other operating system functions and utilities.
	1) sudo vim /etc/apache2/sites-enabled/joomla.conf
	2) change Options to -Index
6) Per STIG WA000-WWA054 A22: Server side includes (SSIs) must run with execution capability disabled.
	1) while in joomla.conf, add -IncludesNoExec
7) Per STIG WG290 A22: Web client access to the content directories must be restricted to read and execute
	1) cd /var/www/html
	2) find /var/www/html -type d -exec chmod 755 {} \;



AD hardening

1) With STIG viewer already open from apache hardening:
	1) Import from zip U_Active_Directory_Domain_V2R9_STIG.zip
2) Logged onto domain-controller
3) Per STIG AD.0001: Membership to the Enterprise Admins group must be restricted to accounts used only to manage the Active Directory Forest. 
	1) Removed all users other than specific admin privileged accounts from Enterprise Admins group
4) Per STIG AD.0002: Membership to the Domain Admins group must be restricted to account used only to manage the Active Directory domain and domain controllers.
	1) Created playeroneadmin account
	2) Switched user to playeroneadmin
	3) Added playeroneadmin account to Domain Admins group
	4) removed playerone user account from Domain Admins group
5) Per STIG AD.0005: Delegation of privileged accounts must be prohibited.
	1) Under individual user properties for "Ashley Steele Admin" and "playeroneadmin"
		1) ticked account option "Account is sensitive and cannot be delegated"

AD hardened per STIG CAT I standards