# Scripts
 |  | `system.sh` | `hardware.sh` | `install.sh` | `deploy.sh` | 
 | ---- | ----- | ------ | ------ | ------ | 
 | create secret conf file | :x: | :x: | :x: | :x: | 
 | apt-get update | :heavy_check_mark: |  |  |  | 
 | apt-get dist-upgrade | :heavy_check_mark: |  |  |  | 
 | apt-get upgrade | :heavy_check_mark: |  |  |  | 
 | install supervisor git python-pip nginx | :heavy_check_mark: |  |  |  | 
 | NEXMO install build-essential libssl-dev libffi-dev python-dev | :heavy_check_mark: |  |  |  | 
 | pip install virtualenv virtualenvwrapper | :heavy_check_mark: |  |  |  | 
 | install curl | :heavy_check_mark: |  |  |  | 
 | edit /etc/modules |  | :heavy_check_mark: |  |  | 
 | edit /boot.config.txt |  | :heavy_check_mark: |  |  | 
 | **erase** /home/pi/Prod/chaudiere if exists |  |  | :heavy_check_mark: | :heavy_check_mark: | 
 | create /home/pi/Prod |  |  | :heavy_check_mark: |  | 
 | create /home/pi/Prod/chaudiere |  |  | :heavy_check_mark: |  | 
 | create /home/pi/Prod/db |  |  | :heavy_check_mark: |  | 
 | create /home/pi/Prod/log |  |  | :heavy_check_mark: |  | 
 | create /home/pi/Dev/db |  |  | :heavy_check_mark: |  | 
 | create /home/pi/Dev/log |  |  | :heavy_check_mark: |  | 
 | clone repo in Prod/chaudiere |  |  | :heavy_check_mark: | :heavy_check_mark: | 
 | **mkvirtualenv** dev and prod (overwrite) |  |  | :heavy_check_mark: |  | 
 | install requirements.txt in both env |  |  | :heavy_check_mark: |  | 
 | flask_app/manage.py **create_db in both env** |  |  | :heavy_check_mark: |  | 
 | configure nginx |  |  | :heavy_check_mark: |  | 
 | configure supervisor |  |  | :heavy_check_mark: |  | 
 | configure cron (in /etc/cron.d) |  |  | :heavy_check_mark: |  | 
 | supervisorctl start sensor gunicorn |  |  | :heavy_check_mark: | :heavy_check_mark: | 
 | sudo service nginx start |  |  | :heavy_check_mark: | :heavy_check_mark: | 
 


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
eyJoaXN0b3J5IjpbMTY2OTkwOTk4MSwtNTA1ODg0OTEzLC0xMz
gzMjA3MzI3LDIwNDUzNjE3MDMsLTE5MjE3ODY0OTcsLTE3ODU3
NDAzMzUsMTc0ODY2MTY5OV19
-->