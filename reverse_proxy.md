# Reverse Proxy

### What is it?
- redirect IPs
- use it to do load balancing
- get something from port 80 and redirect to a development server
- you don't want people to be on development port

### When needed?
- If your page lands on the nginx homepage
- you will also need to restart nginx after:
$ sudo systemctl reload nginx

### commands
- remove default config file in sites_enabled and sites_available
- create a new config file and recreate symlink between sites_enabled and sites_available

$ rm /etc/nginx/sites-available/default
$ rm /etc/nginx/sites-enabled/default
$ cp /home/ubuntu/default.conf /etc/nginx/sites-available/default.conf
$ ln -s /etc/nginx/sites-available/default.conf /etc/nginx/sites-enabled/default.conf
