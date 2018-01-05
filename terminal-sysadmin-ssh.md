# ssh (secure shell)

	ssh -p 333 user@server.com 

## ssh specifying identity file key


	ssh -i ~/.ssh/id_rsa user@server.com
    
Or can set identity file in ~/.ssh/config as follows:

	vi ~/.ssh/config

Add both host names and their identity file as follows:

    Host server1.com
      IdentityFile ~/.ssh/id_dsa_server1
    Host server2.com
      IdentityFile ~/.ssh/id_dsa_server2

## ssh over qnap

 	ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no admin@nasqnap.com

