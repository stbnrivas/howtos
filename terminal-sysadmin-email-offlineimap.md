# offlineimap

http://www.offlineimap.org/documentation.html


This example shows you how to set up OfflineIMAP to synchronize multiple accounts with the mutt mail reader. Start by creating a directory to hold your folders by running mkdir ~/Mail. Then, in your ~/.offlineimaprc, specify:

cat /home/user/.offlineimaprc

    [general]
    accounts = GMail 
    maxsyncaccounts = 3

    [Account GMail]
    localrepository = Local
    remoterepository = Remote

    [Repository Local]
    type = Maildir
    localfolders = /media/store/backups/clientname/email@domain.com

    [Repository Remote]
    type = IMAP
    remotehost = mail.domain.com
    remoteuser = email.domain.com
    remotepass = supersecret
    ssl = yes
    cert_fingerprint = 9a9aff619c423.......
    maxconnections = 1
