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

I still plan to write maybe a small demo on how to put hands on Mastodon codebase, maybe fixing a small bug, but before that we need to have the development environment up and working!

Now, as it's the case with the guide on [how to run your instance](/2018/07/13/running-a-mastodon-instance-using-archlinux), this guide is very similar to the [official guide](https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Development-guide.md), and when in doubt, you should double check the official guide because it's more likely to be up-to-date.

There is also an [official guide to setting up your environment using vagrant](https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Vagrant-guide.md) which might be easier if you have enough resources for a VM running side-by-side with your environment.

## Note on the choices made in this guide

The official guide recommends [rbenv](http://rbenv.org/){:target="_blank"}, but I'm more used to [rvm](https://rvm.io/){:target="_blank"}. `rbenv` is likely to be more lightweight. So if you don't have any preferences, you might want to stick to [rbenv and ruby-build](https://wiki.archlinux.org/index.php/Rbenv){:target="_blank"} when installing ruby.

## Dependencies

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

## Setting up ruby and node

This part is very similar to the production guide, so I'll copy and paste a bit:

First step is that we install `rvm` that will be used for configuring ruby. For that we'll follow the instructions at [rvm.io](https://rvm.io/){:target="_blank"}. Before doing the following command, visit [rvm.io](https://rvm.io/){:target="_blank"} and check which keys need to be added with `gpg --keyserver hkp://keys.gnupg.net --recv-keys`.

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

While we're at it, we also need to install bundler:

```
gem install bundler
```

And with that we have ruby and npm dependencies ready to go.

## Cloning the repo and installing dependencies

You need to clone the repo somewhere on your computer. I usually clone my projects in a `source` folder in my home directory, if you do different, change the following instructions accordingly.

```
cd ~/source
# Clone the mastodon git repository
git clone https://github.com/tootsuite/mastodon.git
```

And then, we will install the dependencies of the project:

```
bundle install # install ruby dependencies
yarn install --pure-lockfile # install node dependencies
```
