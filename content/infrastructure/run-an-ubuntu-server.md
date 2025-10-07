---
title: Run an Ubuntu server
created: 2025-09-20
---
# Run an [Ubuntu](https://ubuntu.com/server) server

> [!warning] Work In Progress

```bash
vi ~/.ssh/authorized_keys

# PasswordAuthentication **no**
vi /etc/ssh/sshd_config

sudo apt update && sudo apt upgrade

sudo adduser -m username

sudo systemctl start app.service

sudo systemctl status app.service

sudo journalctl -u app.service
```