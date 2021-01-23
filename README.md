Django file manager
===================

We have few servers for sharing files easily. One is called 
public.futurice.com, which is accessible from everywhere.

Earlier, sftp was the only way to upload files, which is a little bit 
cumbersome. Server usage is rather versatile: some content is for 
customers, some for colleagues, and some for everyone.

To make sharing and configuring permissions easier, we made small Django 
application for managing files and folder access rules.

This service is built on [Django](http://djangoproject.com) 
[jQuery-File-Upload](https://github.com/blueimp/jQuery-File-Upload) and 
[Bootstrap](http://twitter.github.com/bootstrap/).

Setting up
==========

* Run grep to find references to Futurice (some static files here and there):

```
grep -R -i futurice *
```

* Install latest Django (1.4), django_compressor and yui-compressor
* Configure authentication for application URL
* Start fastcgi server (*./bin/restart.sh*)
* Configure apache2 & fastcgi (or wsgi). We use following configuration:

```
RewriteEngine on
RewriteRule ^/filemanager/static/(.*)$ /home/filemanager/static/$1 [QSA,L]
FastCGIExternalServer /var/www/filemanager.fcgi -socket /home/filemanager/filemanager.sock
RewriteRule ^/filemanager/(.*)$ /filemanager.fcgi/$1 [QSA,L]
```


Assumptions in the code (feel free to change, just good to know):

* Run *python manage.py collectstatic* and *python manage.py compress* when you change static files.
* URL is */filemanager/* (mainly for static files, majority of URLs are generated automatically)
* */home/u/username/* style home folders
* *~/public_html* accessible over http
* *~/public_ssl* accessible over https
* *~/upload* not accessible over web server
* *.htaccess* enabled
* [pubtkt](https://neon1.net/mod_auth_pubtkt/install.html) configured on the server
* Write access to everyone's home folder
* Sudo access without password to */root/safe_chown.py*


Licensing
=========

See LICENSE.txt

jQuery-File-Upload
------------------

[MIT license](http://www.opensource.org/licenses/MIT)

Bootstrap
---------

[Apache license](https://github.com/twitter/bootstrap/blob/master/LICENSE)


