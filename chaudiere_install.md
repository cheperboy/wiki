---


---

<h1 id="os-installation-and-configuration">OS installation and configuration</h1>
<h2 id="install-and-configure-raspbian">Install and configure Raspbian</h2>
<ol>
<li>Format SD card FAT32</li>
<li>Download <a href="https://www.raspberrypi.org/downloads/raspbian/">Raspbian</a> image</li>
<li>Flash image with <a href="https://www.balena.io/etcher/">Etcher</a></li>
</ol>
<h2 id="hardware-setup">Hardware setup</h2>
<p>Create a file boot/ssh to enable ssh after boot</p>
<p>Add at the end of boot/config.txt</p>
<h6 id="mj-enable-the-kernel-module-allowing-1-wire-communication-on-gpio-4"># mj Enable the kernel module allowing 1-wire communication on GPIO-4</h6>
<h6 id="dtoverlayw1-gpio">dtoverlay=w1-gpio</h6>
<h6 id="mj-enable-i2c-for-adc-ads1115"># mj enable i2C (for ADC ADS1115)</h6>
<h6 id="dtparami2c1on">dtparam=i2c1=on</h6>
<p>Reboot and edit /etc/modules</p>
<h6 id="w1-gpio">w1-gpio</h6>
<h6 id="w1-therm">w1-therm</h6>
<h2 id="wifi-setup">3_ Wifi setup</h2>
<p><a href="https://howchoo.com/g/ndy1zte2yjn/how-to-set-up-wifi-on-your-raspberry-pi-without-ethernet">help</a></p>
<p>This must be done before first boot.</p>
<p>From Windows PC with Notepad++ in SD card in partition “boot”</p>
<ol>
<li>
<p>Create file boot/wpa_supplicant.conf (Raspbian will move it in /etc/wpa_supplicant/ when the system is booted)</p>
</li>
<li>
<p>In Notepad++“Edit” &gt; “EOL Conversion” &gt; “UNIX/OSX Format”. “UNIX” is then shown in the status bar.</p>
</li>
<li>
<p>Add content:</p>
</li>
</ol>
<h6 id="countryfr--your-2-digit-country-code">country=FR # Your 2-digit country code</h6>
<h6 id="ctrl_interfacedirvarrunwpa_supplicant-groupnetdev">ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev</h6>
<h6 id="network">network={</h6>
<h6 id="ssidyour_network_name">ssid=“YOUR_NETWORK_NAME”</h6>
<h6 id="pskyour_password">psk=“YOUR_PASSWORD”</h6>
<h6 id="key_mgmtwpa-psk">key_mgmt=WPA-PSK</h6>
<h6 id="section">}</h6>
<p>If conf is done after first boot, edit wpa_supplicant.conf</p>
<p>sudo nano /etc/wpa_supplicant/wpa_supplicant.conf</p>
<h6 id="network-1">network={</h6>
<h6 id="ssidyour_network_name-1">ssid=“YOUR_NETWORK_NAME”</h6>
<h6 id="pskyour_password-1">psk=“YOUR_PASSWORD”</h6>
<h6 id="key_mgmtwpa-psk-1">key_mgmt=WPA-PSK</h6>
<h6 id="section-1">}</h6>
<h1 id="admin-configuration">Admin configuration</h1>
<p>Default username/password is pi/raspberry.</p>
<ol>
<li>
<p>Modify hostname, Edit /etc/hostname. Set to chaudiere</p>
</li>
<li>
<p>Modify pi password type terminal sudo passwd pi</p>
</li>
<li>
<p>Edit ~/.bashrc</p>
</li>
</ol>
<h6 id="ls-alias"># ls alias</h6>
<h6 id="alias-llls--l">alias ll=‘ls -l’</h6>
<h6 id="alias-lals--a">alias la=‘ls -A’</h6>
<h6 id="alias-llals--la">alias lla=‘ls -la’</h6>
<h6 id="alias-lls--cf">alias l=‘ls -CF’</h6>
<h6 id="supervisor-alias"># supervisor alias</h6>
<h6 id="alias-restart_allsudo-supervisorctl-restart-all">alias restart_all=‘sudo supervisorctl restart all’</h6>
<h6 id="alias-statussudo-supervisorctl-status">alias status=‘sudo supervisorctl status’</h6>
<h6 id="alias-start_scriptsudo-supervisorctl-start-script">alias start_script=‘sudo supervisorctl start script’</h6>
<h6 id="alias-stop_scriptsudo-supervisorctl-stop-script">alias stop_script=‘sudo supervisorctl stop script’</h6>
<h6 id="other-alias"># other alias</h6>
<h6 id="alias-devcd-homepidevchaudiere">alias dev=‘cd /home/pi/Dev/chaudiere/’</h6>
<h6 id="alias-prodcd-homepiprodchaudiere">alias prod=‘cd /home/pi/Prod/chaudiere/’</h6>
<h6 id="load-virtualenvwrapper-for-python-after-custom-paths"># load virtualenvwrapper for python (after custom PATHs)</h6>
<h6 id="export-workon_homeenvs">export WORKON_HOME=~/Envs</h6>
<h6 id="source-homepi.localbinvirtualenvwrapper.sh">source /home/pi/.local/bin/virtualenvwrapper.sh</h6>
<h6 id="workon-dev">workon dev</h6>
<h1 id="install-packages-apt-get">Install packages (apt-get)</h1>
<ol>
<li>Update/upgrade system and existing packages</li>
</ol>
<p>sudo apt-get update met à jour la liste des dépôts<br>
sudo apt-get dist-upgrade -y met à jour tous les paquets installés vers les dernières versions en installant de nouveaux paquets si nécessaire</p>
<p>sudo apt-get upgrade -y met à jour tous les paquets installés sur le système</p>
<ol start="2">
<li>Install packages</li>
</ol>
<p>sudo apt-get -y install supervisor</p>
<p>sudo apt-get -y install git</p>
<p>sudo apt-get -y install python-pip</p>
<p>sudo apt-get -y install nginx</p>
<ol start="3">
<li>Install packages (specific to Chaudiere application)</li>
</ol>
<p>sudo apt-get install curl</p>
<p>NEXMO need cryptographie and cffi</p>
<p>sudo apt-get install build-essential libssl-dev libffi-dev python-dev</p>
<p>sudo apt-get clean  supprime les paquets téléchargés et stockés sur carte SD</p>
<h1 id="home-directory-configuration">Home directory Configuration</h1>
<ol>
<li>
<p>mkdir ~/Dev</p>
</li>
<li>
<p>mkdir ~/Dev/log</p>
</li>
<li>
<p>mkdir ~/Dev/db</p>
</li>
<li>
<p>mkdir ~/Prod</p>
</li>
<li>
<p>mkdir ~/Prod/log</p>
</li>
<li>
<p>mkdir ~/CONFIG_CHAUDIERE</p>
</li>
<li>
<p>Copy secret conf file ~/CONFIG_CHAUDIERE/chaudiere_secret_config.py</p>
</li>
</ol>
<h1 id="install-virtualenvwrapper-for-python">Install virtualenvwrapper (for python)</h1>
<p><a href="https://virtualenvwrapper.readthedocs.io/en/latest/install.html">Tuto</a></p>
<h6 id="pip-install-virtualenv-virtualenvwrapper">pip install virtualenv virtualenvwrapper</h6>
<h1 id="install-python-modules">Install python modules</h1>
<h6 id="mkvirtualenv-dev">mkvirtualenv dev</h6>
<h6 id="pip-install--r-requirements.txt">pip install -r requirements.txt</h6>
<p>Idem for env prod</p>
<h1 id="todo">TODO</h1>
<p>Add nexmo to requirements.txt</p>
<p>Add a template of chaudiere_secret_config.py in repository</p>
<h1 id="debug">Debug</h1>
<p>Run server</p>
<h6 id="devchaudiereflask_app--python-main.py">~/Dev/chaudiere/flask_app $ python <a href="http://main.py">main.py</a></h6>
<h1 id="create-database">Create Database</h1>
<p>python <a href="http://manage.py">manage.py</a> create_db</p>
<h1 id="configure-nginx">Configure nginx</h1>
<h2 id="install">Install</h2>
<h2 id="config">Config</h2>
<h2 id="edit-a-new-conf-file-and-copy-the-content-of-this-template-conf-file">Edit a new conf file and copy the content of this template conf file</h2>
<h2 id="sudo-nano-etcnginxsites-availablechaudiere">sudo nano /etc/nginx/sites-available/chaudiere</h2>
<h2 id="sudo-ln--s-etcnginxsites-availablechaudiere-etcnginxsites-enabled">sudo ln -s /etc/nginx/sites-available/chaudiere /etc/nginx/sites-enabled</h2>
<h2 id="remove-the-sym-link-to-default-conf-file-otherwise-it-causes-errors">Remove the sym link to default conf file (otherwise it causes errors)</h2>
<h2 id="sudo-rm-etcnginxsites-enableddefault">sudo rm /etc/nginx/sites-enabled/default</h2>
<h2 id="to-test-configuration">To test configuration:</h2>
<h2 id="sudo-nginx--t">sudo nginx -t</h2>
<h2 id="restart-nginx">Restart nginx</h2>
<h2 id="sudo-service-nginx-restart">sudo service nginx restart</h2>
<h2 id="usefull-cmmands">Usefull Cmmands</h2>
<h2 id="sudo-systemctl-status-nginx">sudo systemctl status nginx</h2>
<h2 id="sudo-service-nginx-restart-1">sudo service nginx restart</h2>
<h1 id="configure-supervisor">Configure supervisor</h1>
<p>Sudo nano /etc/supervisor/conf.d/supervisor_chaudiere.conf</p>
<h1 id="configuration-variables">Configuration variables</h1>
<p>file</p>
<p>line</p>
<p>value</p>
<p>/etc/nginx/sites-available/chaudiere</p>
<p>server_name 81.56.250.29;</p>
<p>Public IP of the network</p>
<p>chaudiere_secret_config.py</p>
<p>“URL” : “<a href="http://montlevic.hd.free.fr">http://montlevic.hd.free.fr</a>:”,</p>
<p>Public IP of the network</p>
<p>flask_app/app/constantes.py</p>
<p>InputDb = {</p>
<p>TEMP_CHAUDIERE : ‘temp0’,</p>
<p>TEMP_FUMEE : ‘temp1’,</p>
<p>TEMP_RETOUR : ‘temp2’,</p>
<p>VENT_SECONDAIRE : ‘watt0’,</p>
<p>ALLUMAGE : ‘watt1’,</p>
<p>VENT_PRIMAIRE : ‘watt2’,</p>
<p>ALIMENTATION : ‘watt3’,</p>
<p>PHASE : ‘phase’</p>
<p>}</p>
<h1 id="physical-inputs---database-fields">Physical inputs -&gt; database fields</h1>
<h1 id="edit-this-dictionary-to-allocate-physicalsoftware-interface">Edit this dictionary to allocate physical/software interface</h1>
<p>Architecture du programme</p>
<h1 id="base-de-données">Base de données</h1>
<p>Table</p>
<p>Contenu</p>
<p>Chaudiere</p>
<p>1 entrée à chaque appel du script sensor/create_data.py (toutes les 3 à 5 secondes)</p>
<p>ChaudiereMinute</p>
<p>1 entrée par minute (moyenne des données de la table Chaudiere)</p>
<p>Pour simplifier le code, les deux tables ont la même structure et les mêmes champs. Le champ ‘phase’ n’est pas utilisé dans la table Chaudiere.</p>
<h1 id="principes-de-base">Principes de base</h1>
<p>Le script sensor/create_data.py tourne en tâche de fond géré par supervisor. Il récupère les données des capteur (températures et moteurs) et les enregistre dans la table Chaudiere toutes les 3 à 5 secondes environ.</p>
<p>Le script flask_app/script/archive_minute.py est appelé toutes les deux minutes (cron).</p>
<p>Si de nouvelles données sont présentent dans la table Chaudiere, alors il crée une/plusieurs entrées dans la table ChaudiereMinute (une entrée pour chaque minute).</p>
<p>La valeur température est la moyenne des températures (sur une minute) de la table Chaudiere</p>
<p>La valeur des moteur est un booléen qui vaut vrai si au moins une entrée (sur une minute) est vraie.</p>
<p>En mode production, deux minutes sont traitées à chaque appel</p>
<p>Le script flask_app/script/process_phase.py est appelé toutes les deux minutes (cron). Si de nouvelles entrées sont à traiter dans la table ChaudiereMinute alors il exécute un algorithme pour déterminer la phase de fonctionnement de la chaudière au cours de chaque minute qu’il traite.</p>
<p>En mode production, deux minutes sont traitées à chaque appel</p>
<p>Si la température de l’eau de la chaudiere (temp0) passe sous la consigne, alors une alerte mail/sms est générée. Aucun mail/sms n’est envoyé si une alerte à déja été générée dans les 10 minutes précédentes.</p>

