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







# 
openssl verify cert.pem

openssl verify -untrusted ca-bundle cert.pem

-CApath or -CAfile

openssl verify -verbose -x509_strict -CAfile ca.pem -CApath nosuchdir cert_chain.pem
```




### example at http://www.forumtropic.com


dig forumtropic.com any

```
;; QUESTION SECTION:
;forumtropic.com.		IN	ANY

;; ANSWER SECTION:
forumtropic.com.	86357	IN	TXT	"v=spf1 a mx a:host2.labkarmon.com ~all"
forumtropic.com.	86357	IN	TXT	"google-site-verification=tgXQwmp2Y5JGRqee7DcYDALzG4NFJniiQHGJ1ZpaMZs"
forumtropic.com.	86281	IN	NS	dns1.interdominios.com.
forumtropic.com.	86281	IN	NS	dns2.interdominios.com.
forumtropic.com.	84724	IN	A	89.248.107.77
forumtropic.com.	86208	IN	MX	10 mail.forumtropic.com.

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

echo | openssl s_client -servername TEST -connect test.synchronicity.ridespark.com:1026 |\
  sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > synchronicity.ridespark.com.crt  
```