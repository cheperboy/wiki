# Install with scripts
1. Install raspbian
2. configure wifi (edit  `/etc/wpa_supplicant/wpa_supplicant.conf`)
3. set hostname to chaudiere (edit  `/etc/hostname`. raspberry will be accessible via *chaudiere.local*)
4. `mkdir /home/pi/Dev && cd /home/pi/Dev` 
5. `git clone https://github.com/cheperboy/chaudiere.git`
6. Secret config 
i.  `mkdir /home/pi/CONFIG_CHAUDIERE`
8. `. install_system.sh |& tee install_system.sh.log`
9. `sudo /bin/bash hardware.sh`
10. `. install_chaudiere.sh |& tee install_chaudiere.sh.log`


# Scripts
 |  | `system.sh` | `hardware.sh` | `install.sh` | `deploy.sh` | 
 | ---- | :-----: | :-----: | :-----: | :-----: | 
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
eyJoaXN0b3J5IjpbLTMyMjQ4MzE3LDEyNjcwMzU5NiwyMDYxNj
A0MzA4LC01MDU4ODQ5MTMsLTEzODMyMDczMjcsMjA0NTM2MTcw
MywtMTkyMTc4NjQ5NywtMTc4NTc0MDMzNSwxNzQ4NjYxNjk5XX
0=
-->