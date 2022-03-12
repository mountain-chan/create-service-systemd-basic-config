# Set up a python script as a service through systemctl systemd

## Install systemd
```commandline
sudo apt-get install -y systemd
```

## Create file config with two option below
```
sudo nano /etc/systemd/system/<service_name>.service
```

* Basic config
```
[Unit]
Description=My test service
After=multi-user.target

[Service]
Type=simple
Restart=always
StartLimitBurst=0
ExecStart=/usr/bin/python /home/<username>/test.py

[INSTALL]
WantedBy=multi-user.target
```

* Run python with conda environment
```
[Unit]
Description=Your Description of the services
After=network.target

[Service]
Type=simple
Restart=always
StartLimitBurst=0
WorkingDirectory=/media/ubuntu/Data/jenkins/jenkins/workspace/<project_name>
Environment="PATH=/home/ubuntu/miniconda3/envs/base37/bin"
ExecStart=/home/ubuntu/miniconda3/envs/base37/bin/gunicorn --workers 2 -b 0.0.0.0:5012 manage:app

[INSTALL]
WantedBy=multi-user.target
```

## Reload systemctl and enable/start/stop/restart/status service
```
sudo systemctl daemon-reload

sudo systemctl enable/start/stop/restart/status <service_name>.service
```