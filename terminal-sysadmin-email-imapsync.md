# imapsync

imapsync.noarch : Tool to migrate email between IMAP servers

	dnf install imapsync

example of command for sync two mails server using imap


	imapsync --host1 imap.gmail.com --port1 993 --user1 you@gmail.com --password1 ****** --ssl1 
    		--host2 imap.gmail.com --port2 993 --user2 you@domain.com --password2 ****** --ssl2 
            --syncinternaldates --split1 100 --split2 100 
            --authmech1 LOGIN --authmech2 LOGIN --allowsizemismatch --useheader Message-ID
