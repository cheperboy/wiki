# Scripts
| Effect | `install_system.sh` | `install_chaudiere.sh` | `install_system.sh` |
| ---- | ----- |------|------|
|  | `"URL" : "http://xxx.hd.free.fr:",`| Public IP of the network| 
| `flask_app/app/constantes.py` |`InputDb = {TEMP_CHAUDIERE : 'temp0', ...}` | Edit to map Physical inputs to database fields 


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

# Production tools
```
cd  ~/Prod
git clone https://github.com/cheperboy/chaudiere.git
```

## nginx
Create a chaudiere conf file and sym link
```
# sudo nano /etc/nginx/sites-available/chaudiere
sudo cp ~/Prod/chaudiere/config/prod/nginx_chaudiere_conf /etc/nginx/sites-available/

sudo ln -s /etc/nginx/sites-available/nginx_chaudiere_conf /etc/nginx/sites-enabled
```
Remove the sym link to default conf file (otherwise it causes errors)
`sudo rm /etc/nginx/sites-enabled/default`

To test configuration `sudo nginx -t`

To Restart nginx `sudo service nginx restart`

## Supervisor
```
sudo supervisorctl stop all
sudo cp ~/Prod/chaudiere/config/prod/supervisor_chaudiere.conf /etc/supervisor/conf.d/
sudo supervisorctl reread
sudo supervisorctl reload
sudo supervisorctl start sensor gunicorn
```

## Edit config variable

| File | Content | Value |
| ---- | ----- |------|
| `chaudiere_secret_config.py` | `"URL" : "http://xxx.hd.free.fr:",`| Public IP of the network| 
| `flask_app/app/constantes.py` |`InputDb = {TEMP_CHAUDIERE : 'temp0', ...}` | Edit to map Physical inputs to database fields 



# Secret conf file 

`nano ~/CONFIG_CHAUDIERE/chaudiere_secret_config.py`


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NDI0ODg1MywtMTkyMTc4NjQ5NywtMT
c4NTc0MDMzNSwxNzQ4NjYxNjk5XX0=
-->