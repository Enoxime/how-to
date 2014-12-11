local-fakeimg
=============

How to get a fakeimg.pl working on your localhost when you don't have internet access and need it to work.

Notes:
* Tested on a Ubuntu 14.04
* It works only if you start the application.

Requirements:
* apache2.4.*
* mod_proxy activated
* mod_proxy_http activated
* python
* Flask
* Pillow
* Superuser access (with sudo)
* A beer :-D (not for under 18 and 21 in case you are in states)

## Cloning the git repository
Go to the root directory of your server.  
`$ cd /var/www`  
Clone here the repository  
`$ sudo git clone https://github.com/Rydgel/Fake-images-please.git`  
Change the owner and group owner to you 
`$ sudo chown -R $USER:$USER Fake-images-please`  
Make it executable  
`$ sudo chmod +x -R Fake-images-please`  
Test it  
`$ cd Fake-images-please`  
`$ python tests.py`  
Start it  
`$ python app.py`  
Then open your browser and go to address "0.0.0.0:8000" to test if it works.

## Redirect fakeimg.pl url to your internal server
Open hosts file with super user access  
`$ sudo nano /etc/hosts`  
Then add this line  
`0.0.0.0  fakeimg.pl`  
There you go! Save it.

## Pointing fakeimg.pl to the right port
Create a new VirtualHost  
`$ sudo nano /etc/apache2/sites-available/fakeimg.conf`  
Add the following lines and save  
```
<VirtualHost *:80>
  ServerName fakeimg.pl
  ProxyPass			/ http://0.0.0.0:8000/
  ProxyPassReverse	/ http://0.0.0.0:8000/
</VirtualHost>
```
Enable the new VirtualHost  
`$ sudo a2ensite fakeimg.conf`  
Then restart the server
`$ sudo service apache2 restart`  
Disconnect yourself from the internet access and test this address "fakeimg.pl" you should see the original fakeimg website but working in your internal server.

## The last thing
Now that it's done, you can drink this beer which has been awayting for you.
