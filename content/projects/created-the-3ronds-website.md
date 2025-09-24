---
title: Created the 3ronds.net website.
created: 2025-09-20
tags:
  - web
---
# Tools & Methods I used 

I used a [github-action workflow](https://github.com/chamaloriz/cult-of-the-done/blob/main/.github/workflows/website.yml) to generate the website using [quartz](https://github.com/jackyzha0/quartz).
The website it hosted on my server running Ubuntu and here are the steps.

> [!info] Preliminary steps
> At this step you already have a server configured but if not refer to [[run-an-ubuntu-server]] and to [[setup-caddy-on-a-webserver]] to serve the files
## The server setup

Once on the server using you admin account you can setup a user using the following commands.

```bash

# I first created a user on my ubuntu server
# The -m is used to generate the home folder of that user /home/3ronds/
# We will use the home of that user to publish the website
sudo useradd -m 3ronds

# Then I generated a ssh-key for that user using this command
# First I enter the 3ronds user bash console
sudo -u 3ronds bash
# or use this if sudo is not available
su - 3ronds -s /bin/bash

# And generate the key for that user
# I just press enter we don't need a password for this key
ssh-keygen -t ed25519 -C "3ronds server"

# I then add the generated public key to the users authorized_keys file, to do that.
# First copy the public_key, to print it in the console you can use the tail command
# The default name for that key should be id_ed25519.pub 
tail ~/.ssh/id_ed25519.pub
# I use the 'vi' command but you can use the 'nano' editor instead
# The authorized_keys file is located in the ~/.ssh of the user but you need to create it, it does not exist by default in a new user.
vi ~/.ssh/authorized_keys

# then print the private key and copy it to the clipboard
tail ~/.ssh/id_ed25519

# then delete both of the keys we wont need them on the server
rm ~/.ssh/id_ed25519
rm ~/.ssh/id_ed25519.pub

```

now that you have a private key in you clipboard go to github and create a new repository once you created it [you can add a SECRET](https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets) in it named **PRIVATE_KEY** and paste that key in it.

## The repo setup

On the repo I followed the structure described in the Quartz documentation, but I did not copy the entire Quartz project files into my repo, [I just copied the 2 files needed to configure the project](https://github.com/chamaloriz/cult-of-the-done/tree/main/quartz-config). And I created a `content` folder to store the Markdown files for the website. to publish it to the server, I use the workflow called [website](https://github.com/chamaloriz/cult-of-the-done/blob/main/.github/workflows/website.yml) in the first step, it builds the Quartz files and in the second and last step, it pushed the files to the server using the private key we created in the previous step.

> [!info] Info
> Now that the files are on the server you can use [Caddy](https://caddyserver.com/) to serve the files to the client, check the article about it here : [[setup-caddy-on-a-webserver]]

## the caddy config

```bash

# You need to make caddy part of the project user group so that caddy can see into the /home/3ronds folder.
sudo usermod -a -G 3ronds caddy

```

```bash
3ronds.net {
    tls /home/caddy/certs/3ronds.net.pem /home/caddy/certs/3ronds.net.key
    # fix for the folder structure of Quartz
    try_files {path} {uri}.html
    # the generated folder
    root * /home/3ronds/public
    file_server
}
```