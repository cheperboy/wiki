# Directories
```
mkdir ~/Dev
mkdir ~/Dev/log
mkdir ~/Dev/db
mkdir ~/Prod
mkdir ~/Prod/log
mkdir ~/Prod/db
mkdir ~/CONFIG_CHAUDIERE
```

# Production
```
cd  ~/Prod
git clone https://github.com/cheperboy/chaudiere.git
```

## nginx
Edit a new conf file and copy the content of this template conf file
```
# sudo nano /etc/nginx/sites-available/chaudiere
sudo cp ~/Prod/chaudiere/config/prod/nginx_chaudiere_conf /etc/nginx/sites-available/

sudo ln -s /etc/nginx/sites-available/nginx_chaudiere_conf /etc/nginx/sites-enabled
```
Remove the sym link to default conf file (otherwise it causes errors)
`sudo rm /etc/nginx/sites-enabled/default`

To test configuration:

`sudo nginx -t`

Restart nginx

`sudo service nginx restart`

## Usefull Cmmands
sudo systemctl status nginx
sudo service nginx restart


# Secret conf file 

`nano ~/CONFIG_CHAUDIERE/chaudiere_secret_config.py`


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgwMzk2ODA3XX0=
-->