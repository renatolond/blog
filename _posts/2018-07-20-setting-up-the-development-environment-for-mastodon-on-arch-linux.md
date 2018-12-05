---
layout: post
title: Setting up the development environment for Mastodon on Arch Linux
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

Well, on the last post I described [how to run a mastodon instance using Arch Linux](/2018/07/13/running-a-mastodon-instance-using-archlinux). But what if you wanted to contribute to Mastodon also?

I still plan to write maybe a small demo on how to get your hands dirty on Mastodon's codebase, maybe fixing a small bug, but before that we need to have the development environment up and working!

Now, as it's the case with the guide on [how to run your instance](/2018/07/13/running-a-mastodon-instance-using-archlinux), this guide is very similar to the {% external_link { "text":"official guide", "link": "https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Development-guide.md"} %}, and when in doubt, you should double check the official guide because it's more likely to be up-to-date. This guide is also very similar to how to run an instance, I mean, it's the same software, right?

There is also an {% external_link {"text": "official guide to setting up your environment using vagrant", "link": "https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Vagrant-guide.md"} %} which might be easier if you have enough resources for a VM running side-by-side with your environment and/or does not run Linux.

This guide is focused on Mastodon, but most of the setup done here will work for other ruby on rails projects you might want to contribute to.

---

<h3>Note on the choices made in this guide</h3>

The official guide recommends {% external_link {"text":"rbenv", "link":"http://rbenv.org/"} %}, but I'm more used to {% external_link {"text":"rvm", "link":"https://rvm.io/"} %}. `rbenv` is likely to be more lightweight. So if you don't have any preferences, you might want to stick to {% external_link {"text":"rbenv and ruby-build", "link":"https://wiki.archlinux.org/index.php/Rbenv"} %} when installing ruby.

Since this is a development setup, I'm not mentioning any security concerns. \\
⚠️ Do not use this guide for running a production instance. ⚠️ \\
Refer to [how to run a mastodon instance using Arch Linux](/2018/07/13/running-a-mastodon-instance-using-archlinux) instead.

Questions are super welcome, you can contact me using any of the methods listed in the [about page](/about). Also if you notice that something doesn't seem right, don't hesitate to hit me up.

As with the other guide, I tested the steps on this guide on a virtual machine and they should work if you copy-paste them. Things might not work well if your computer has less than 2GB of ram.

---

<nav markdown="1">
  <h3 class="toc_title">On this page</h3>
  1. test
  {:toc}
</nav>

---

### General Mastodon development tips

From the official guide:

> You can use a localhost->world tunneling service like {% external_link {"text": "ngrok", "link": "https://ngrok.com/"} %} if you want to test federation, **however** that should not be your primary mode of operation. If you want to have a permanently federating server, set up a proper instance on a VPS with a domain name, and simply keep it up to date with your own fork of the project while doing development on localhost.
>
> Ngrok and similar services give you a random domain on each start up. This is good enough to test how the code you're working on handles real-world situations. But as soon as your domain changes, for everybody else concerned you're a different instance than before.
>
> Generally, federation bits are tricky to work on for exactly this reason - it's hard to test. And when you are testing with a disposable instance you are polluting the databases of the real servers you're testing against, usually not a big deal but can be annoying. The way I have handled this so far was thus: I have used ngrok for one session, and recorded the exchanges from its web interface to create fixtures and test suites. From then on I've been working with those rather than live servers.
>
> I advise to study the existing code and the RFCs before trying to implement any federation-related changes. It's not *that* difficult, but I think "here be dragons" applies because it's easy to break.
>
> If your development environment is running remotely (e.g. on a VPS or virtual machine), setting the `REMOTE_DEV` environment variable will swap your instance from using "letter opener" (which launches a local browser) to "letter opener web" (which collects emails and displays them at /letter_opener ).

When trying to fix a bug or implement a new feature, it is a good idea to branch off the `master` branch with a new branch and then submit your pull request using that branch.

A good way to see that your environment is working as it should is to check out the latest stable release (for instance, at the time of writing the latest stable release is `v2.4.3`) and then run tests as suggested in the [tests](#tests) session. They should all pass because the tests in stable releases should always be working.

---

### Dependencies

Since we're trying to run the same software as in the production guide, we'll need mostly the same dependencies, this is what we'll need:

- `postgresql`: The SQL database used by Mastodon
- `redis`: Used by mastodon for in-memory data store
- `ffmpeg`: Used by mastodon for conversion of GIFs to MP4s.
- `imagemagick`: Used by mastodon for image related operations
- `protobuf`: Used by mastodon for language detection
- `git`: Used for version control.
- `python2`: Used by gyp, a node tool that builds native addons modules for node.js

Besides those, it's a good idea to install the `base-devel` group, since it comes with `gcc` and some ruby modules need to compile native extensions.

Now, you can install those with:

```
sudo pacman -S postgresql redis ffmpeg imagemagick protobuf git python2 base-devel
```

---

### PostgreSQL configuration

Take a look at {% external_link {"text":"Arch Linux's wiki about PostgreSQL", "link":"https://wiki.archlinux.org/index.php/PostgreSQL"} %}.
The first thing to do is to initialize the database cluster. This is done by doing:

```
sudo -u postgres initdb --locale en_US.UTF-8 -E UTF8 -D '/var/lib/postgres/data'
```

If you want to use a different language, there's no problem.

After this completes, you can then do
```
sudo systemctl start postgresql # will start postgresql
```

You will need to start postgresql every time you want to use it for development. You could also `enable` it so it starts with your system if you prefer, but it will be running and using resources even when you don't need it.

Now that postgresql is running, we can create your user in postgresql:

```
# Launch psql as the postgres user
sudo -u postgres psql
```

In the prompt that opens, you need to do the command below replacing the username you use on your setup.
``` SQL
-- Creates user with SUPERUSER permission level
CREATE USER <your username here> SUPERUSER;
```

The `SUPERUSER` level will let you do anything without having to change users. With great powers...

---

### Redis

We also need to start redis. Same as postgresql:

```
sudo systemctl start redis # will start redis
```

As with postgres, you can `enable` it too to make it start with the system, but personally I prefer to start on demand.

---

### Setting up ruby and node

This part is very similar to the production guide, so I'll copy and paste a bit:

First step is that we install `rvm` that will be used for configuring ruby. For that we'll follow the instructions at {% external_link {"text":"rvm.io", "link":"https://rvm.io/"} %}. Before doing the following command, visit {% external_link {"text":"rvm.io", "link":"https://rvm.io/"} %} and check which keys need to be added with `gpg --keyserver hkp://keys.gnupg.net --recv-keys`.

```
\curl -sSL https://get.rvm.io | bash -s stable
```

After that, we'll have rvm. You will see that to use rvm in the same session you need to execute additional commands:

```
source $HOME/.rvm/scripts/rvm
```

With `rvm` installed, we can then install the ruby version that Mastodon uses:

```
rvm install 2.5.1
```

Now, this will take some time, drink some water, stretch and come back.

Similarly, we will install nvm for managing which node version we'll use.

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

Refer to {% external_link {"text":"nvm github", "link":"https://github.com/creationix/nvm"} %} for the latest version.

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

While we're at it, we also need to install bundler:

```
gem install bundler
```

And with that we have ruby and npm dependencies ready to go.

---

### Cloning the repo and installing dependencies

You need to clone the repo somewhere on your computer. I usually clone my projects in a `source` folder in my home directory, if you do different, change the following instructions accordingly.

```
cd ~/source
git clone https://github.com/tootsuite/mastodon.git
```

And then, `cd ~/source/mastodon` and we will install the dependencies of the project:

```
bundle install # install ruby dependencies
yarn install --pure-lockfile # install node dependencies
```

This will also take a while, try to relax a bit, have you listened to your favorite song today? 🎶

Since we created the postgres user before, we can setup the development database using:

```
bundle exec rails db:setup
```

This will use the default development configuration to setup the database. Which means: no password, same user as your username, using a database named `mastodon_development` in localhost.

In development mode the database is setup with an admin account for you to test with. The email address will be `admin@YOURDOMAIN` (e.g. admin@localhost:3000) and the password will be `mastodonadmin`.

Now, you have two options.

---

#### Run each service separately

If you checked out the guide to run an instance, you probably noticed that mastodon has three parts: A web service, a sidekiq service to run background jobs and a streaming service. In development you need those three components too, plus the webpack development server, which will compile assets (javascript, css) as needed. In production we don't need webpack running all the time because we compile the assets only once after we update Mastodon.

To run those separately, you will need one window for each, since each of those holds your terminal while it's running.

To run the web server:

```
bundle exec puma -C config/puma.rb
```

To run sidekiq:

```
bundle exec sidekiq
```

To run the streaming service:

```
PORT=4000 yarn run start
```

And to run webpack:

```
./bin/webpack-dev-server --listen-host 0.0.0.0
```

All of those should start immediately, except for the webpack server, which compiles the assets before starting.

To check that everything is working as expected, if you open your browser window at `http://localhost:3000` you should see Mastodon landing page!

---

#### Run everything using Foreman

Now, most of the time this method is more practical. Running each service by itself is good if one is not starting to see what is the error, but most of the time you'll want to start everything so that you can start coding away. In which case, first you'll want to install foreman

```
gem install foreman
```

And then, when you need to start your dev environment you can do:

```
foreman start -f Procfile.dev
```

---

### Working on master

When working on master, the steps are similar to when updating an instance, but they happen much more frequently since master changes much more frequently.

This means, every time you pull changes into your computer (for instance, when you do `git pull origin master`), you might need to:

```
# Update any gems that were changed
bundle install
# Update any node packages that were changed
yarn install --pure-lockfile
# Update the database to the latest version
bin/rails db:migrate RAILS_ENV=development
```

Now, you don't need to run them all the time, you will notice if one of them is not working as it should. How?

Bundler complains like this:

```
Could not find proper version of railties (5.2.0) in any of the sources
Run `bundle install` to install missing gems.
```

The name of the gem and version will change, but this means that one of your dependencies is not up to date and you need to run `bundle install` again.

If the database is missing a migration, rails will complain with:

```
ActiveRecord::PendingMigrationError - Migrations are pending. To resolve this issue, run:

        bin/rails db:migrate RAILS_ENV=development
```

This will appear on your console, but also on your browser.

If the ruby being used in the project is updated, you will also see some complaints from rvm (in this example, with a hypothetical ruby 2.5.2):

```
$ cd .
Required ruby-2.5.2 is not installed.
To install do: 'rvm install "ruby-2.5.2"'
```

In that case we need to do the same as we did to install it the first time, that is:

```
rvm install 2.5.2
```

And since rvm manages gems by ruby version, you'll need to install the dependencies again using `bundle install`.

---

### Tests

Tests in the mastodon project live in the `spec` folder. Tests also use migrations, so if the database was updated since you last ran tests, you will need to run something like this:

```
bin/rails db:migrate RAILS_ENV=test
```

But when you try to run tests with a database missing migrations, you'll get an error from Rails that will explain exactly that.

To run all the tests, you need to do:

```
rspec
```

To run only one test, you can run it like so:

```
rspec spec/validators/status_length_validator_spec.rb
```

---

### Other useful commands

If you add a new string that needs to be translated, you can run

```
yarn manage:translations
```

To update the localization files. This is needed so that {% external_link {"text": "weblate", "link": "https://weblate.joinmastodon.org" } %} can inform translators that there are new strings to be translated in other languages.

You can check code quality using

```
rubocop
```

Have in mind that it might complain about code violations that you did not introduce, but you should always try not to introduce new violations.

---

### Troubleshooting

#### RVM says it's not a function

Follow recommended instructions at {% external_link {"text": "https://rvm.io/integration/gnome-terminal", "link": "https://rvm.io/integration/gnome-terminal"} %}

#### Mastodon has no css
If mastodon has no css and you see something like `#<Errno::ECONNREFUSED: Failed to open TCP connection to localhost:3035 (Connection refused - connect(2) for "::1" port 3035)>` in your console, the issue is where webpacker is trying to connect. You can fix it by changing `config/webpacker.yml`.
Instead of

```
  dev_server:
    host: localhost
```

Use

```
  dev_server:
    host: 127.0.0.1
```
