# SSL Certificates



## generation

- Generating a self-signed certificate pair (PEM) from [https://core.telegram.org/bots/self-signed](https://core.telegram.org/bots/self-signed)


```
openssl req -newkey rsa:2048 -sha256 -nodes -keyout YOURPRIVATE.key -x509 -days 365 -out YOURPUBLIC.pem -subj "/C=ES/ST=$CCAA/L=$PROVINCE/O=COMPANY /CN=YOURDOMAIN.EXAMPLE"
```

YOURPUBLIC.pem has to be used as input for setting the self-signed webhook.

You can inspect the generated certificate with:
```
openssl x509 -text -noout -in YOURPUBLIC.pem
```

Converting from a previously generated DER:
```
openssl x509 -inform der -in YOURDER.der -out YOURPEM.pem
```

Converting from a previously generated PKCS12:
```
openssl pkcs12 -in YOURPKCS.p12 -out YOURPEM.pem
```

## validate a ssl certificate from a server

```bash
openssl s_client -connect server.yourwebhoster.eu:443 -servername mail.domain.com
```

## download a certificate using curl


```bash
openssl s_client -showcerts -connect {HOSTNAME}:{PORT} :443 </dev/null 2>/dev/null|openssl x509 -outform PEM > output.pem
```

## adding to generate to a server

debian:

```bash
sudo mkdir /usr/local/share/ca-certificates/extra
sudo cp new.crt /usr/local/share/ca-certificates/extra
sudo update-ca-certificates
```



redhat:

```bash
ls /etc/pki/ca-trust/source/anchors/
cp certificate.pem /etc/pki/ca-trust/source/anchors/
sudo ln -s /etc/ssl/your-cert.pem /etc/pki/ca-trust/source/anchors/your-cert.pem
update-ca-trust
```



## packages related to CA certificates


redhat:

```bash
yum install -y ca-certificates
update-ca-trust force-enable
```
