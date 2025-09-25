---
title: Run an Ubuntu server
created: 2025-09-20
---
# Run an [Ubuntu](https://ubuntu.com/server) server

```bash
# WIP

vi ~/.ssh/authorized_keys

# PasswordAuthentication **no**
vi /etc/ssh/sshd_config

sudo apt update && sudo apt upgrade

ssh -NL 1111:localhost:5432 server

sudo adduser -m username
```