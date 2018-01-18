## apache2 + php 5.6
```
# add ppa since it is not default involved
sudo add-apt-repository ppa:ondrej/php
sudo apt update

sudo apt-get install -y php5.6 apache2 php5.6-xml libapache2-mod-php5.6

# open ssl mod
sudo a2enmod ssl
sudo a2ensite default-ssl.conf

# For Ubuntu 16.04
sudo systemctl restart apache2.service 

# For Ubuntu 14.04
sudo /etc/init.d/apache2 restart

# copy your webpage to correct directory
move your webpage to /var/www/html & 
check permissions (e.g. you folder should be rw-r--r-x)

# remove Options Indexes
cp ~/apache2.conf /etc/apache2/apache2.conf

# Remember to restart
sudo systemctl restart apache2.service 

```
## SSL
```
sudo apt install letsencrypt

letsencrypt certonly --webroot -w /var/www/html/ -m $YourMail@gmail.com --agree-tos --rsa-key-size 4096 -d $YourDomain

cp ~/default-ssl.conf /etc/apache2/sites-enabled/default-ssl.conf
cp ~/ssl.conf /etc/apache2/mods-enabled/default-ssl.conf
```

## Confs

* apache2.conf
```
<Directory /var/www/>
    Options FollowSymLinks
    AllowOverride None
    Require all granted
</Directory>
```

* ssl.conf
```
SSLCipherSuite ECDH+AESGCM:ECDH+AES256:ECDH+AES128:!MD5:!aNULL
```


* default-ssl.conf
```
SSLCertificateFile	/etc/letsencrypt/live/$YourDomain/cert.pem
SSLCertificateKeyFile /etc/letsencrypt/live/$YourDomain/privkey.pem
SSLCertificateChainFile /etc/letsencrypt/live/$YourDomain/chain.pem
```

## For VM
```
Remember to forward 80 port & 443 port
```
