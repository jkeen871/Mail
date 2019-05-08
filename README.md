# Text based Gmail via Neomutt, offlineimap, msmtp
Clone Repository to your home directory :

	cd ~
	git clone https://github.com/jkeen871/Mail.git

Install Required Packages

	dnf install mutt neomutt w3m w3m-img offlineimap msmtp 
	
Copy dotrc files to home directory

	cp Mail/dotrc/msmtprc ~/.msmtprc
	cp Mail/dotrc/offlineimaprc ~/.offlineimaprc
	
Edit dotrc files in home directory, update with your gmail username and password

.msmtprc :

	account personal
	host smtp.gmail.com
	port 587
	protocol smtp
	auth on
	from <gmail address>
	user <gmail address>
	password <gmail password>
	tls on
	tls_nocertcheck
.offlineimaprc :

	type = Gmail
	remoteuser = <gmail address> 
	remotepass = <gmail password>
	realdelete = no
	maxconnections = 10
	sslcacertfile = /etc/ssl/certs/ca-bundle.crt
	usecompression = yes
	folderfilter = lambda folder: folder not in ['Important','Categories','Junk','[Gmail].All Mail','[Gmail].Spam']
	
	
Enable cron to download your imap mail from Gmail at intervals.  The default is every 5 minutes do a quick sync, every 8 hours do a full sync.
Edit your crontab and enter the following lines:

	*/5 * * * * ~/Mail/fetch-mail.sh -q
	10 */8 * * * ~/Mail/fetch-mail.sh -f








