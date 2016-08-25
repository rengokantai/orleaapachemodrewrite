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
```
${SERVER_NAME}
%{HOST}
%{REQUEST_URI}
%{QUERY_STRING}
%{HTTP_POST}
%{HTTP_REFERER}
%{SSL_PROTOCOL}
```
[see cheatsheet](http://www.askapache.com/htaccess/mod_rewrite-variables-cheatsheet.html)  
another .htaccess: [L] = last rewrite rule.
```
RewriteEngine On
RewriteRule ^index\.html$ http://ke.com [L]
```
#######RewriteRule Directive
```
RewriteEngine
RewriteRule
```
others:
```
RewriteCond
RewriteOptions
RewriteBase
RewriteMap
Flags
```
example:use another folder's file
```
RewriteRule ^boats/1$ ../ke.com/boats/1 [L]
```
use backreference
```
RewriteRule ^boats/([0-9]+)$ http://ke.com/boats/$1 [L]
```
######RewriteCond Directive - Part 1
```
RewriteCond %{HTTP_HOST} ^www\.my(\w+)\.com$ [NC]  //case insensitive
RewriteCond %1 !^boats$
RewriteCond %{REQUEST_FILENAME} /index\.html$ [NC]
RewriteRule ^([a-zA-Z]+)/(\d+)$ http://myke.com/prod/$1/$2 [C]
```
error page. If a file is not file or not dict, then 404 page
```
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule .* /404.html [L]
```
######RewriteCond Directive - Part 2
blocking -403
```
RewriteCond %[HTTP_USER_AGENT} ^Bot.*$ [OR]
RewriteCond %[HTTP_USER_AGENT} ^mailto:bad@bot.com$ [OR]
RewriteCond %[HTTP_USER_AGENT} .....   //allowed
RewriteRule .* - [F]
```
######RewriteBase And Options
```
RewriteBase /subfolder
RrewriteRule ^index\.html$ /ke.html [L]
```
same as
```
RrewriteRule ^index\.html$ /subfolder/ke.html [L]
```



#####Advanced Rewriting Solutions
######Rewrite Logging
.htaccess
```
RewriteEngine On
LogLevel elert rewrite:trace3
```
level:  
emerg>alert>crit>error>warn>notice>info>debug  
