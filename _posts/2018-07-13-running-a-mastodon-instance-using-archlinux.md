---
layout: post
title: Running a Mastodon instance using Arch Linux
tags:
  - Mastodon
  - Arch Linux
  - Redes sociais
  - Descentralização
  - Código aberto
  - Decentralization
  - Open Source
  - Twitter
  - Social Network
  - Linux
---

It's been a while now that I've been running [masto.donte.com.br](https://masto.donte.com.br){:target="_blank"} using Arch Linux and since the [official guide](https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Production-guide.md){:target="_blank"} recommends using Ubuntu 16.04, I figured that describing what I did could help someone out there. If in doubt, use the official guide instructions instead, since they're more likely to be up to date.

<h2>Notes about some choices made in this guide</h2>

The official guide recommends [rbenv](http://rbenv.org/){:target="_blank"}, but I'm more used to [rvm](https://rvm.io/){:target="_blank"}. `rbenv` is likely to be more lightweight. So if you don't have any preferences, you might want to stick to [rbenv and ruby-build](https://wiki.archlinux.org/index.php/Rbenv){:target="_blank"} when installing ruby.

There's also choices made regarding firewall. You do not need to follow those exact ones if you already have another firewall on your server or if you want to use a different one. However, do use some firewall. :)

Like the official guide, this guide assumes you're using Let's Encrypt for the certificates. If it's not the case, you can ignore let's encrypt references and configure your own certificate in Nginx.

Also note that the SSL configurations for `nginx` are slightly different than the ones in the official guide. They are aimed at being compatible with older android phones and were generated using [Mozilla SSL Configuration Generator](https://mozilla.github.io/server-side-tls/ssl-config-generator/?server=nginx-1.14.0&openssl=1.1.0h&hsts=yes&profile=intermediate){:target="_blank"} with the intermediate configuration and [HSTS](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security){:target="_blank"} enabled. Have in mind that HSTS disables non-secure traffic and gets cached on the client side, so if you are unsure, generate a new configuration without HSTS.

Questions are super welcome, you can contact me using any of the methods listed in the [about page](/about). Also if you notice that something doesn't seem right, don't hesitate to hit me up.

I tested this guide using a digital ocean droplet with 1GB memory and 1vCPU. I had to enable swap to be able to compile the assets. There's more information about this in the relevant section.

---

<nav markdown="1">
  <h3 class="toc_title">On this page</h3>
  1. test
  {:toc}
</nav>

---

### Before starting the guide

You need:
- A server running at least a base install of [Arch Linux](https://wiki.archlinux.org/index.php/installation_guide){:target="_blank"}
- Root access
- A domain or sub-domain to use for the instance.

What is assumed:
- There's no service running in the same ports as Mastodon. If that's the case, adjustments will need to be made throughout the guide.
- You're not using root as your base user. That you have another user configured with sudo access.

---

### What you should have by the end of this

You should have an instance running with a basic firewall, a valid https certificate and prepared to be upgraded when needed. All the services needed will be on the same machine. Basic monitoring to know if your instance is up or not.

---

### General suggestions

If you have no experience with Linux systems administrations, it's a good idea to [read a bit about it](https://wiki.archlinux.org/index.php/security){:target="_blank"}. You will need to keep this system up to date since it will be facing the internet.

Do not reuse [passwords](https://wiki.archlinux.org/index.php/security#Passwords){:target="_blank"} and [force public key](https://wiki.archlinux.org/index.php/Secure_Shell#Force_public_key_authentication){:target="_blank"} for your SSH user. Use [sudo instead of running everything as root](https://wiki.archlinux.org/index.php/security#Use_sudo_instead_of_su){:target="_blank"} and [disable root login over ssh](https://wiki.archlinux.org/index.php/Secure_Shell#Deny){:target="_blank"}.

The official guide already recommends this, but I'll go one step further:
Always use `tmux` or `screen` when doing operations on your server. You will need to learn the [basic commands](https://tmuxcheatsheet.com/){:target="_blank"} but it's well worth it to avoid losing things if your connection go down and also for long operations in which you can disconnect and leave it running.

If you have 1GB it's quite likely that asset compilation will fail. Remember to setup a swap partition or use [systemd-swap](https://wiki.archlinux.org/index.php/swap#systemd-swap)

---

### DNS

The domain you're planning to use should have DNS records pointing to your server. If your server has a IPv6 address, you should configure an AAAA record, otherwise, only the A record should be enough.

Now, this guide will not get into [serving a different domain](https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Serving_a_different_domain.md){:target="_blank"}. Just have in mind that:
- The domain will be part of the identifier of your instance users. Once it's defined, you cannot change it anymore or you'll get all kinds of federation weirdness.
- Because of that, avoid using "temporary" domains, like the ones coming from ngrok or similar.

---

### Dependencies
- `ufw`: An easy-to-use firewall
- `certbot` and `certbox-nginx`: used for generating the certificates from Let's Encrypt.
- `nginx`: Frontend web server that will be used in this setup
- `jemalloc`: Different memory management library that improves memory usage for this setup.
- `postgresql`: The SQL database used by Mastodon
- `redis`: Used by mastodon for in-memory data store
- `ffmpeg`: Used by mastodon for conversion of GIFs to MP4s.
- `imagemagick`: Used by mastodon for image related operations
- `protobuf`: Used by mastodon for language detection
- `git`: Used for version control.
- `python2`: Used by gyp, a node tool that builds native addons modules for node.js
- `libxslt`, `libyaml`: I don't know. They were in the official guide so I'm installing them, but I have to say: I do not have they installed in other instances and never noticed an issue 🤷🏽‍♂️

Besides those, it's a good idea to install the `base-devel` group. It comes with `sudo` and other tools which might come in handy.

Now, you can install those with:
```
sudo pacman -S ufw certbot nginx jemalloc postgresql redis ffmpeg imagemagick protobuf git base-devel python2 libxslt libyaml
sudo pacman -S --asdeps certbot-nginx
```

---

### Configuring ufw

🛑**WARNING**: Configuring a firewall is quite important, but if something goes wrong you might lose connectivity to your server. Make sure you have other ways of reaching your server if something goes wrong. 🛑

Now, Mastodon runs a couple of different services and to support it we will be running different services too, but since we will have everything in the same server, the only ports that should be available for the outside world are the HTTP/HTTPS ports that will be used to connect to the instance. Also, we want the SSH port open so that we can connect remotely to the server.

You should read into [Arch Linux's wiki about ufw](https://wiki.archlinux.org/index.php/Uncomplicated_Firewall){:target="_blank"}. For this guide what you want is to do:

```
sudo ufw allow SSH # this allows SSH traffic to your server
sudo ufw allow WWW # this allows traffic on port 80 to your server
sudo ufw allow "WWW Secure" # this allows traffic on port 443 to your server
```

And then you can do:
```
sudo ufw enable
sudo systemctl enable ufw # Enables ufw to be started at startup
sudo systemctl start ufw # starts ufw
```

And with this the firewall should be up :)

---

### Configuring Nginx

You should read into [Arch Linux's wiki about nginx](https://wiki.archlinux.org/index.php/Nginx){:target="_blank"}, but again, what you want to do is something along these lines:

First, you want to edit `nginx.conf`.
To remove the "welcome to nginx" page, you want to change the beginning of your `server` block to something like this:
```
    server {
        listen       80 default_server;
        server_name  '';

        return 444;
```

And at the very end of the `http` block, add:
```
    types_hash_max_size 4096; # sets the maximum size of the types hash tables
    include sites-enabled/*; # Includes any configuration located in /etc/nginx/sites-enabled
```

And then create these two directories:

```
sudo mkdir /etc/nginx/sites-available # All domain configurations will live here
sudo mkdir /etc/nginx/sites-enabled # The enabled ones will be linked here
```

Now, let's say we're using `my.instance.com` as the instance domain/sub-domain. You will need to replace this accordingly throughout this next steps.

Create a new file `/etc/nginx/sites-available/my.instance.com.conf`, replacing `my.instance.com` by your domain, and then add to it the following content:

```
map $http_upgrade $connection_upgrade {
  default upgrade;
  ''      close;
}

server {
  listen 80;
  listen [::]:80;
  server_name my.instance.com;
  root /home/mastodon/live/public;
  # Useful for Let's Encrypt
  location /.well-known/acme-challenge/ { allow all; }
  location / { return 301 https://$host$request_uri; }
}

server {
  listen 443 ssl http2;
  listen [::]:443 ssl http2;
  server_name my.instance.com;

  ssl_certificate     /etc/letsencrypt/live/my.instance.com/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/my.instance.com/privkey.pem;
  ssl_session_timeout 1d;
  ssl_session_cache shared:SSL:10m;
  ssl_session_tickets off;

  ssl_dhparam /etc/ssl/certs/dhparam.pem;

  ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
  ssl_ciphers 'ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS';
  ssl_prefer_server_ciphers on;

  add_header Strict-Transport-Security max-age=15768000;

  ssl_stapling on;
  ssl_stapling_verify on;

  ssl_trusted_certificate /etc/letsencrypt/live/my.instance.com/chain.pem;

  resolver 8.8.8.8 8.8.4.4 valid=300s;
  resolver_timeout 5s;

  keepalive_timeout    70;
  sendfile             on;
  client_max_body_size 8m;

  root /home/mastodon/live/public;

  gzip on;
  gzip_disable "msie6";
  gzip_vary on;
  gzip_proxied any;
  gzip_comp_level 6;
  gzip_buffers 16 8k;
  gzip_http_version 1.1;
  gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

  add_header Strict-Transport-Security "max-age=31536000";

  location / {
    try_files $uri @proxy;
  }

  location ~ ^/(emoji|packs|system/accounts/avatars|system/media_attachments/files) {
    add_header Cache-Control "public, max-age=31536000, immutable";
    try_files $uri @proxy;
  }

  location /sw.js {
    add_header Cache-Control "public, max-age=0";
    try_files $uri @proxy;
  }

  location @proxy {
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto https;
    proxy_set_header Proxy "";
    proxy_pass_header Server;

    proxy_pass http://127.0.0.1:3000;
    proxy_buffering off;
    proxy_redirect off;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $connection_upgrade;

    tcp_nodelay on;
  }

  location /api/v1/streaming {
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto https;
    proxy_set_header Proxy "";

    proxy_pass http://127.0.0.1:4000;
    proxy_buffering off;
    proxy_redirect off;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $connection_upgrade;

    tcp_nodelay on;
  }

  error_page 500 501 502 503 504 /500.html;
}
```

⚠️ It's a good idea to take a look if something changed in relation to the [official guide](https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Production-guide.md#nginx-configuration){:target="_blank"} ⚠️

At this point `nginx` still doesn't know about our instance (because we're including files from `/etc/nginx/sites-enabled` and we created the file in `/etc/nginx/sites-available`), however, we should be able to start `nginx` already.

For that, we need to do:

```
sudo systemctl start nginx # Starts the nginx service
sudo systemctl enable nginx # Makes the service start automatically at boot
```

If you do `curl -v <your server ip>` now, you should see something like this:

```
$ curl -v <your server's ip>
* Rebuilt URL to: <your server's ip>/
*   Trying <your server's ip>...
* TCP_NODELAY set
* Connected to <your server's ip> (<your server's ip>) port 80 (#0)
> GET / HTTP/1.1
> Host: <your server's ip>
> User-Agent: curl/7.60.0
> Accept: */*
>
* Empty reply from server
* Connection #0 to host <your server's ip> left intact
curl: (52) Empty reply from server
```

And that means `nginx` was correctly started and that `ufw` is allowing connections as expected. We will now get our certificates from Let's Encrypt before jumping back to nginx configuration

---

### Intermission: Configuring Let's Encrypt

Now, for Let's Encrypt we will use certbot that we installed previously. For more information about it you can take a look at [Arch Linux's wiki about Certbot](https://wiki.archlinux.org/index.php/Certbot){:target="_blank"}. For this guide, you need to run the following command:

```
sudo certbot --nginx certonly -d my.instance.com
```

As usual, remind to change the url to the url for your actual instance. You will need to follow the instructions on screen.

```
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator nginx, Installer nginx
Enter email address (used for urgent renewal and security notices) (Enter 'c' to
cancel):

-------------------------------------------------------------------------------
Please read the Terms of Service at
https://letsencrypt.org/documents/LE-SA-v1.2-November-15-2017.pdf. You must
agree in order to register with the ACME server at
https://acme-v01.api.letsencrypt.org/directory
-------------------------------------------------------------------------------
(A)gree/(C)ancel:

-------------------------------------------------------------------------------
Would you be willing to share your email address with the Electronic Frontier
Foundation, a founding partner of the Let's Encrypt project and the non-profit
organization that develops Certbot? We'd like to send you email about our work
encrypting the web, EFF news, campaigns, and ways to support digital freedom.
-------------------------------------------------------------------------------
(Y)es/(N)o:
Obtaining a new certificate
Performing the following challenges:
http-01 challenge for my.instance.com
Using default address 80 for authentication.
2018/07/13 18:28:47 [notice] 4617#4617: signal process started
Waiting for verification...
Cleaning up challenges
2018/07/13 18:28:53 [notice] 4619#4619: signal process started
```

If everything goes as expected, you should see something like this:

```
IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/my.instance.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/my.instance.com/privkey.pem
   Your cert will expire on 2018-10-11. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot
   again. To non-interactively renew *all* of your certificates, run
   "certbot renew"
```

This means that now we have a valid certificate and that we can go back to nginx. Double check that the path informed by certbot (in this example `/etc/letsencrypt/live/my.instance.com/fullchain.pem`) matches the one in your nginx file.

Let's Encrypt certificates only last for 90 days, so we will still come back to this. But for now, let's go back to nginx.

If you have an error like
```
Saving debug log to /var/log/letsencrypt/letsencrypt.log
An unexpected error occurred:
UnicodeDecodeError: 'ascii' codec can't decode byte 0xc2 in position 10453: ordinal not in range(128)
Please see the logfiles in /var/log/letsencrypt for more details.
```
Check that you have set up correctly your locale! If your locale is set to `C`, certbot will fail.

---

### Finishing off nginx configuration

At this point the certificate should be working. Since this configuration is using HSTS, we also need to generate a [dhparam](https://security.stackexchange.com/questions/38206/can-someone-explain-what-exactly-is-accomplished-by-generation-of-dh-parameters){:target="_blank"}. You can do that by doing (might take a little while!)

```
openssl dhparam -out dhparam.pem 2048
sudo mv dhparam.pem /etc/ssl/certs/dhparam.pem
```

What is left for us to do is to enable the instance configuration and reload nginx. We should do this (remember to replace with your instance config!):

```
sudo ln -s /etc/nginx/sites-available/my.instance.com.conf /etc/nginx/sites-enabled/ # creates a softlink of the configuration we created previously to the enabled sites directory
sudo systemctl reload nginx
```

Now, if everything went fine, your nginx should reload. Otherwise, it will throw some error like this:

``` shell
$ sudo systemctl reload nginx
Job for nginx.service failed because the control process exited with error code.
See "systemctl status nginx.service" and "journalctl -xe" for details.
```

In that case, you need to execute one of the commands and try to see what went wrong.

However, if everything went right until now, if you do `curl -v my.instance.com` replacing for your domain, you should see something like this:

```
$ curl -v my.instance.com
* Rebuilt URL to: my.instance.com/
*   Trying <your server's ip>...
* TCP_NODELAY set
* Connected to my.instance.com (<your server's ip>) port 80 (#0)
> GET / HTTP/1.1
> Host: my.instance.com
> User-Agent: curl/7.60.0
> Accept: */*
>
< HTTP/1.1 301 Moved Permanently
< Server: nginx/1.14.0
< Date: Fri, 13 Jul 2018 18:41:17 GMT
< Content-Type: text/html
< Content-Length: 185
< Connection: keep-alive
< Location: https://my.instance.com/
<
<html>
<head><title>301 Moved Permanently</title></head>
<body bgcolor="white">
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx/1.14.0</center>
</body>
</html>
* Connection #0 to host my.instance.com left intact
```

And if you curl or visit the https address you should get a `502 Bad Gateway`.

---

### Mastodon user setup

We need to create the Mastodon user:

```
sudo useradd -m mastodon # create the user
```

Then, we will start using this user for the following commands:
```
sudo su - mastodon
```

First step is that we install `rvm` that will be used for configuring ruby. For that we'll follow the instructions at [rvm.io](https://rvm.io/){:target="_blank"}. Before doing the following command, visit [rvm.io](https://rvm.io/){:target="_blank"} and check which keys need to be added with `gpg --keyserver hkp://keys.gnupg.net --recv-keys`.

```
\curl -sSL https://get.rvm.io | bash -s stable
```

After that, we'll have rvm. You will see that to use rvm in the same session you need to execute additional commands:

```
source /home/mastodon/.rvm/scripts/rvm
```

With `rvm` installed, we can then install the ruby version that Mastodon uses:

```
rvm install 2.5.1 -C --with-jemalloc
```

Note that the `-C --with-jemalloc` parameter is there so that we use jemalloc instead the standard memory allocation library, since it's more efficient in Mastodon's case. Now, this will take some time, drink some water, stretch and come back.

Similarly, we will install nvm for managing which node version we'll use.

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

Refer to [nvm github](https://github.com/creationix/nvm){:target="_blank"} for the latest version.

You will also need to run
```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

And add these same lines to `~/.bash_profile`

And then to install the node version we're using:

```
nvm install 8.11.3
```

And to install yarn:

```
npm install -g yarn
```

And with that we have our mastodon user ready.

---

### Cloning mastodon repository and installing dependencies

For these next instructions we still need to be logged in Mastodon's user. First, we will clone the repo:

```
# Return to mastodon user's home directory
cd ~
# Clone the mastodon git repository into ~/live
git clone https://github.com/tootsuite/mastodon.git live
```

Now, it's highly recommended to run a stable release. That means the latest on [tootsuite's releases](https://github.com/tootsuite/mastodon/releases/){:target="_blank"}. At the time of writing the latest one is `v2.4.3`.
With that in mind, we will do:

```
# Change directory to ~/live
cd ~/live
# Checkout to the latest stable branch
git checkout v2.4.3
```

And then, we will install the dependencies of the project:

```
# Install bundler
gem install bundler
# Use bundler to install the rest of the Ruby dependencies
bundle install -j$(getconf _NPROCESSORS_ONLN) --without development test
# Use yarn to install node.js dependencies
yarn install --pure-lockfile
```

After this finishes you can go back to the user you were using before. This will also take a while, try to relax a bit, have you listened to your favorite song today? 🎶

---

### PostgreSQL configuration

Now, once more, check out [Arch Linux's wiki about PostgreSQL](https://wiki.archlinux.org/index.php/PostgreSQL){:target="_blank"}.
The first thing to do is to initialize the database cluster. This is done by doing:

```
sudo -u postgres initdb --locale en_US.UTF-8 -E UTF8 -D '/var/lib/postgres/data'
```

If you want to use a different language, there's no problem.

After this completes, you can then do
```
sudo systemctl enable postgresql # will enable postgresql to start together with the system
sudo systemctl start postgresql # will start postgresql
```

Now that postgresql is running, we can create mastodon's user in postgresql:

```
# Launch psql as the postgres user
sudo -u postgres psql
```

In the prompt that opens, create the mastodon user with:
``` SQL
-- Creates mastodon user with CREATEDB permission level
CREATE USER mastodon CREATEDB;
```

Okay, after this we're done with postgresql. Let's move on!

---

### Redis configuration

The last service we need to start is `redis`. Check out [Arch Linux's wiki about Redis](https://wiki.archlinux.org/index.php/redis){:target="_blank"}.

We need to start redis and enable it on initialization:
```
sudo systemctl enable redis
sudo systemctl start redis
```

---

### Mastodon application configuration

We're approaching the end, I promise!

We need to go back to Mastodon user:

```
sudo su - mastodon
```

Then we change to the live directory and run the setup wizard:

```
cd ~/live
RAILS_ENV=production bundle exec rake mastodon:setup
```

This will do the instance setup: ask you about some options, generate needed secrets, setup the database and precompile the assets.

For PostgreSQL host, port and etc, you can just press enter and it will use default values. The same goes for redis. For email options, refer to the [email section](#email). You will want to allow the setup to prepare the database and compile the assets.

Precompiling the assets will take a little while! Also, pay attention to the output. It might output:

```
That failed! Maybe you need swap space?

All done! You can now power on the Mastodon server 🐘
```

Which means the asset compilation failed and you will need to try again with more memory. You can try again using `RAILS_ENV=production bundle exec rails assets:precompile`

---

### Intermission: Mastodon directory permissions

The mastodon user folder cannot be accessed by nginx. The `/home/mastodon/live/public` needs to be accessed by nginx because it's where images and css is served from.

You have some options, the one I chose for this guide is:

```
sudo chmod 751 /home/mastodon/ # Makes mastodon home folder executable by all users in the server and readable and executable by the user group
sudo chmod 755 /home/mastodon/live/public # Makes mastodon public folder readable and executable by all users in the server
sudo chmod 640 /home/mastodon/live/.env.production # Gives read access only to the user/group for the file with production secrets
```

Other subfolders will also be readable by other users if they know what to search for.

---

### Mastodon systemd service files

Now, you can go back to your user and we'll create service files for Mastodon. You again should compare with the [official guide](https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Production-guide.md#mastodon-systemd-service-files){:target="_blank"} to see if something changed, but have in mind that since we're using `rvm` and `nvm` in this guide the final result will be a bit different.

This is what our services will look like, first the one in `/etc/systemd/system/mastodon-web.service`, responsible for Mastodon's frontend and API:

```
[Unit]
Description=mastodon-web
After=network.target

[Service]
Type=simple
User=mastodon
WorkingDirectory=/home/mastodon/live
Environment="RAILS_ENV=production"
Environment="PORT=3000"
Environment="WEB_CONCURRENCY=3"
ExecStart=/bin/bash -lc "bundle exec puma -C config/puma.rb"
ExecReload=/bin/kill -SIGUSR1 $MAINPID
TimeoutSec=15
Restart=always

[Install]
WantedBy=multi-user.target
```

Then, the one in `/etc/systemd/system/mastodon-sidekiq.service`, responsible for running background jobs:

```
[Unit]
Description=mastodon-sidekiq
After=network.target

[Service]
Type=simple
User=mastodon
WorkingDirectory=/home/mastodon/live
Environment="RAILS_ENV=production"
Environment="DB_POOL=5"
ExecStart=/bin/bash -lc "bundle exec sidekiq -c 5 -q default -q mailers -q pull -q push"
TimeoutSec=15
Restart=always

[Install]
WantedBy=multi-user.target
```

Lastly, the one in `/etc/systemd/system/mastodon-streaming.service`, responsible for sending new content to users in real time:

```
[Unit]
Description=mastodon-streaming
After=network.target

[Service]
Type=simple
User=mastodon
WorkingDirectory=/home/mastodon/live
Environment="NODE_ENV=production"
Environment="PORT=4000"
ExecStart=/bin/bash -lc "npm run start"
TimeoutSec=15
Restart=always

[Install]
WantedBy=multi-user.target
```

Now, you can enable these services using:

```
sudo systemctl enable /etc/systemd/system/mastodon-*.service
```

And then run them using
```
sudo systemctl start mastodon-*.service
```

Check that they are running as they should using:
```
systemctl status mastodon-*.service
```


At this point, if everything is as it should, going to `https://my.instance.com` should give you the Mastodon landing page! 🐘

---
<a name="email"></a>

### Emails
Now, you'll probably want to send emails, since new users get an email to confirm their emails.

You should really follow the [official guide](https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Production-guide.md#email-service){:target="_blank"} on this one, because there's no difference in this case.

---

### Monitoring with uptime robot

I'm giving an example with Uptime Robot because they have a free tier, but you can use other services if you prefer. The idea is just to be pinged if your instance goes down and also to have an independent page where your users can be sure if everything is working as expected.

After creating an UptimeRobot account, you can create a HTTP(s) type monitor pointing to your instance full url: `https://my.instance.com`, don't forget to change accordingly.

If you have IPv6, you should also create another monitor with the Ping type, in which you should use your server's IPv6 as the IP.

Now, in the settings page, you can click on "add public status page", then you select for selected monitors and you select the ones you just created. You can create a CNAME DNS, so that for instance `status.my.instance.com` would show the this new status page.

Now if your instance goes down or your IPv6 stops working, you should get an email.

---

### Remote media attachment cache cleanup

Mastodon downloads media from other instances and caches them locally. If you don't clean this from time to time, this will only keep growing. Using mastodon user, you can add a cron job that cleans it up daily using `crontab -e` and adding:

```
0 2 * * * /bin/bash -lc "cd live; RAILS_ENV=production bundle exec rake mastodon:media:remove_remote" 2>&1 /home/mastodon/remove_media.output
```

If you don't have any cron installed in your server, you need to take a look in [Arch Linux's wiki page about cron](https://wiki.archlinux.org/index.php/cron){:target="_blank"}.

---

### Renew Let's Encrypt certificates

The best way for this is to follow [Arch Linux's wiki about Certbot automatic renewal](https://wiki.archlinux.org/index.php/certbot#Automatic_renewal){:target="_blank"}, which is:

Create a file `/etc/systemd/system/certbot.service`:

```
[Unit]
Description=Let's Encrypt renewal

[Service]
Type=oneshot
ExecStart=/usr/bin/certbot renew --quiet --agree-tos
```

The nginx plugin should take care of making sure the server is reloaded automatically after renewal.

Then, create a second file `/etc/systemd/system/certbot.timer`:

```
[Unit]
Description=Daily renewal of Let's Encrypt's certificates

[Timer]
OnCalendar=03:00:00
RandomizedDelaySec=1h
Persistent=true

[Install]
WantedBy=timers.target
```

Now, enable and start the timer service:
```
sudo systemctl start certbot.timer
sudo systemctl enable certbot.timer
```

---

### Updating between Mastodon versions

Okay, you set it all up, everything is running and then Mastodon `v2.5.0` comes out. What do you do?

Do not despair, dear reader, all is well.

Remember our tip about `tmux`? When updating is always a good idea to be running `tmux`. Database migrations can take some time and `tmux` will help to avoid losing data if your connection fails in the meantime.

First, we will go to the Mastodon user once again:
```
sudo su - mastodon
```

Okay, first things first, let's go into the live directory and get the new version:

```
cd ~/live
git fetch origin --tags
git checkout v2.5.0
cd . # This is to force rvm to check if we're in the right ruby version
```

Now, suppose the ruby version changed, since the last time you were here and instead of `2.5.1` is now `2.5.2`. After you do `cd .`, rvm will complain:

```
$ cd .
Required ruby-2.5.2 is not installed.
To install do: 'rvm install "ruby-2.5.2"'
```

In this case, we will need to use rvm to install the new version. The command is the same as last time:

```
rvm install 2.5.2 -C --with-jemalloc
```

Everything will take some time and at the end you will be ready to follow through. Notice that this won't happen very often.

Now, you'll always want to make sure that you look at the releases notes for the release you're going to. Sometimes there's special tasks that need to be done before following.

If there was dependencies updated, you need to do:
```
bundle install --without development test # if you need to update ruby dependencies or if you installed a new ruby
yarn install --pure-lockfile # if you need to update node dependencies
```

In most of the updates you will need to update the assets:
```
RAILS_ENV=production bundle exec rails assets:precompile
```

For comparison: in the digital ocean droplet I tested this guide on, compiling assets on v2.4.3 took around 5 minutes.

If the update includes database migrations that you'll need to do:
```
RAILS_ENV=production bundle exec rails db:migrate
```

Sometimes database migrations will change the database in a way that the instance will stop working for a little bit until you restart the services, that's why I usually leave them for last to reduce downtime.

⚠️ Backup your database regularly ⚠️

After the migration is finished running, you can leave the mastodon user and then restart the services:

```
sudo systemctl restart mastodon-sidekiq
sudo systemctl restart mastodon-streaming
sudo systemctl reload mastodon-web
```

Now, if there was some database changes you need to `restart mastodon-web` instead of `reload`.

Alrite, you should be in the last version of Mastodon now!

---

### Upgrading Arch Linux

Some special notes about upgrading Arch Linux itself. If you haven't yet, read through the [Arch Linux's wiki on Upgrading the system](https://wiki.archlinux.org/index.php/System_maintenance#Upgrading_the_system){:target="_blank"}. Since Arch Linux is rolling, there's some differences if you're coming from other distros.

Ruby uses native modules in some of the gems, that is, modules compiled against local libraries. This means that if your system changes radically from one version to the other, you might have issues starting services.

However, to make your life a bit easier, you can re-compile native modules by doing (using mastodon user):

```
cd ~/live
bundle pristine
```

This will take a little while but will recompile needed gems. When in doubt, do that after a system upgrade.

Now, second thing to take note: [Postgresql minor version](https://www.postgresql.org/support/versioning/){:target="_blank"} are compatible between themselves. This means that 9.6.8 is compatible with 9.6.9 and after version 10 they adopted a two number versioning, which means that 10.3 is compatible with 10.4. However, 9.6 is not compatible with 10. And 10 will not be compatible with 11. This means that: when upgrading from 10 to 11 you need to follow the [official documentation](https://www.postgresql.org/docs/current/static/upgrading.html){:target="_blank"} and [Arch Linux's wiki orientation](https://wiki.archlinux.org/index.php/PostgreSQL#Upgrading_PostgreSQL){:target="_blank"}. With that in mind, be careful when upgrading.

🛑 Upgrading wrongly may cause data loss. 🛑

---

### (Optional) Adding elasticsearch for searching authorized statuses

Since Mastodon v2.3.0, you can enable full text search for authorized statuses. That means toots you have written, boosted, favourited or were mentioned in. For this functionality, Mastodon uses Elasticsearch. As usual, you should take a look in [Arch Linux's wiki about Elasticsearch](https://wiki.archlinux.org/index.php/Elasticsearch){:target="_blank"}.

Note: I was able to run elasticsearch on my test instance using the 1GB/1vCPU droplet from Digital Ocean with 1GB of Swap by using the memory configurations suggested at the [Arch Linux's wiki about Elasticsearch](https://wiki.archlinux.org/index.php/Elasticsearch#Configuration){:target="_blank"}, that is, `-Xms128m -Xmx512m`. However, I don't have any load and I don't know how the system would behave with more real loads.

To install elasticsearch do:
```
sudo pacman -S elasticsearch
```

Pacman then will ask which version of jdk you want to use. After installed, you can start Elasticsearch by doing:

```
sudo systemctl enable elasticsearch # Enables elasticsearch to be started at startup
sudo systemctl start elasticsearch # starts elasticsearch
```

Then you need to switch to Mastodon user, `cd ~/live` and edit `.env.production`, to add configuration related to Elasticsearch, look for the commented configs and change them:

```
ES_ENABLED=true
ES_HOST=localhost
ES_PORT=9200
```

Then, you need to build the index. This might take a while if your database is big!

```
RAILS_ENV=production bundle exec rails chewy:deploy
```

When this is finished, you need to restart all mastodon services.

The [official docs](https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Elasticsearch-guide.md#advanced-elasticsearch-configuration-optional){:target="_blank"} have some tips on how to tune Elasticsearch.
