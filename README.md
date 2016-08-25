#### orleaapachemodrewrite
#####Getting Started With mod_rewrite
######Getting Started With 
```
cd /etc/apache2
a2enmod rewrite
```
######Adjusting Configuration
```
<directory /var/www/html/>
  AllowOverride All
</directory>
```
restart
```
service apache2 restart
```
git rid of fqdn error
```
vim apache2.conf
```
edit
```
ServerName ke
```
htaccess file: for directory level.try:
```
cd /var/www/html
vim .htaccess
```
edit
```
RewriteEngine On
RewriteRule ^index.html$ test.html   //redirect index.html to test.html
```
######Module mod_rewrite Usage
If only redirect, use alias
```
a2enmod alias
```
in .htaccess
```
Redirect www.ke.com ke.com
```


#####Rewrite Directives
######vHost Setup
```
cd /etc/apache2/sites-avaliable
a2ensite ke.com.conf
```
then change hosts file.

###### mod_rewrite Variables
