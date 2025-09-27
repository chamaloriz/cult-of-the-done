---
title: Host a simple python script with systemd on ubuntu
created: 2025-09-27
---
# Host a simple python script with [systemd](https://www.man7.org/linux/man-pages/man1/systemd.1.html) on ubuntu

> [!warning] Work In Progress

```bash
sudo useradd -m simple-script

sudo -u simple-script bash

ssh-keygen -t ed25519 -C “simple-script”

tail ~/.ssh/id_ed25519.pub
```

```bash
# after adding the key to the deploykey section of github
git clone git@github.com:user/simple_script.git

```

> [!info] Difference between folders
> the user folder is simple-script with a "-" and the project forlder has a "_" instead

```bash
cd /home/simple-script/simple_script/

# test you script
python3 -m venv venv

source venv/bin/activate

pip3 install -r requirement.txt

python3 main.py

```

```bash
# execute this with the host admin user
sudo nano /etc/systemd/system/simple-script.service
```

```bash
# systemd service file
[Unit]
Description=bot-vendor daemon
After=network.target

[Service]
User=bot-vendor
Group=bot-vendor
WorkingDirectory=/home/simple-script/simple_script/
ExecStart=/home/simple-script/simple_script/venv/bin/python3 main.py

[Install]
WantedBy=multi-user.target
```

```bash
# execute this with the host admin user
sudo systemctl start simple-script.service

# check if everything is running correctly
sudo systemctl status simple-script.service

# make it start when you restart the server
sudo systemctl enable simple-script.service
```