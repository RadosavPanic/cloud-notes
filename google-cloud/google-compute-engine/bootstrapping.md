# Bootstrapping with Startup Script

**Bootstrapping**: Install OS patches or software when an VM instance is launched.

New VM instance -> Management -> Automation -> Startup script

Startup script example of setting up Web HTTP Server:

`#!/bin/bash`

`apt update`

`apt -y install apache2`

`echo "Web Server live - $(hostname) $(hostname -I)" > /var/www/html/index.html`
