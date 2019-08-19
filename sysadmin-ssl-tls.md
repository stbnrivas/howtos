SSL - Secure Socket Layer
TLS - Tranport Layer Security

handshake

OCSP	Online Certificate Status Protocol







# certificates from terminal utils

```bash
# generate an self-signed
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365
# generate .crt from pem
openssl x509 -outform der -in cert.pem -out cert.crt



# generate for an script without propmpt
sudo openssl req -x509 -days 365 -nodes -newkey rsa:2048 -keyout /etc/nginx/ssl/self.key -out /etc/nginx/ssl/self.crt -subj "/C=ES/ST=Madrid/L=Madrid/O=Global Security/OU=IT Department/CN=parkingverde.com"



# 
openssl verify cert.pem

openssl verify -untrusted ca-bundle cert.pem

-CApath or -CAfile

openssl verify -verbose -x509_strict -CAfile ca.pem -CApath nosuchdir cert_chain.pem
```




### example at http://www.ft.com


dig ft.com any

```
;; QUESTION SECTION:
;ft.com.		IN	ANY

;; ANSWER SECTION:
ft.com.	86357	IN	TXT	"v=pf1 a mx a:host2.labkarmon.com ~all"
ft.com.	86357	IN	TXT	"google-site-verification=thunderstuck"
ft.com.	86281	IN	NS	dns1.interdominios.com.
ft.com.	86281	IN	NS	dns2.interdominios.com.
ft.com.	84724	IN	A	89.248.107.77
ft.com.	86208	IN	MX	10 mail.ft.com.

;; ADDITIONAL SECTION:
dns2.interdominios.com.	44879	IN	A	89.248.97.3
dns1.interdominios.com.	44887	IN	A	93.174.4.16
```




# download certificates

```
echo | openssl s_client -servername NAME -connect HOST:PORT |\
  sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > certificate.crt


echo | openssl s_client -servername google.com -connect google.com:443 |\
  sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > certificate.crt

echo | openssl s_client -servername TEST -connect test.sc.rs.com:1026 |\
  sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > sc.rs.com.crt
```




# ssl using certbot

```bash
sudo dnf install certbot certbot-nginx

# try write into /etc/nginx.conf
sudo certbot --nginx
# use this
sudo certbot certonly --nginx

echo "0 0,12 * * * root python -c 'import random; import time; time.sleep(random.random() * 3600)' && certbot renew" | sudo tee -a /etc/crontab > /dev/null
```


# ssl using certbot from a container

```bash
docker run --rm -d nginx:1.17.2
docker exec -it $continer /bin/bash

apt-get install certbot python-certbot-nginx
```

```bash
cat /etc/letsencrypt/options-ssl-nginx.conf 
```






```bash
docker cp <containerId>:/file/path/within/container /host/path/target




sudo certbot certonly --nginx


```