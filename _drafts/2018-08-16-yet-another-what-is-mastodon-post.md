---
layout: post
title: Yet another 'What is Mastodon' post
date: 2018-08-16 11:51 +0200
---

Everytime a social network fucks up (and that happens quite often) there's a lot of talk about Mastodon (the social network, not the band). It happens in waves, sometimes because of Twitter, sometimes it's Tumblr or yet another reveal of Facebook dirty schemes.

One of the last times that happened, I wrote a thread on Twitter trying to explain most of the doubts that arise with Mastodon and decided to turn into a blog post so that it can be found more easily by people that maybe are not in Twitter to begin with.

## What is Mastodon?

Mastodon was created in the beginning of 2016, but it started to get some more attention in the beginning of 2017 amidst some other Twitter shitstorm. It has then followed several waves of users registering in it and a part of them bouncing back to Twitter, while a part of them remains in the service. The [whole network](#fediverse) had around 1.43 million users by the end of July, 2018[⁽¹⁾](#mnm) and the numbers keep growing.

Mastodon is intended as a Twitter replacement. It accepts 500 characters instead of 280, but other than that it has a similar format. In Mastodon you can follow, retweet (it's called boost over there) and @ people just like in Twitter. Tweets are called Toots over there (apparently in some parts of the US toots are how small kids call farts, and there's a lot of US people that seems to get really unhappy about this choice of name 🤷🏽‍♂️).

Mastodon's default interface is close to tweetdeck, with one main panel for tweets by people you follow, one for notifications and a third one with links to extra things you can do (More on that later). However, there's also other web apps to access it, one of them [mimmicking twitter](https://itter.photog.social), the other an [original app which is very pleasant to use](https://pinafore.social).

However, Mastodon is _decentralized_. And that's achieved with instances.

<!-- Even though Mastodon has lots of [instances](#instances) -- more on that later -- each instance can talk to each other, unless one purposedly blocks the other. Instances work a lot like email servers. In Mastodon you are identified by your @ + your instance domain. i.e @renatolond@masto.donte.com.br or @gargron@mastodon.social -->

<a name='instances'></a>
## Instances

There's no direct equivalent to the concept of instance in traditional social networks, however, there are two systems which are quite known and have the same structure: E-mail and Telephone networks.

When you sign up on Gmail, you can still send e-mails to users of protonmail or tutanota, or even to the private server of your company. When you sign up with your mobile telecom, you can still call your friend that uses a different telecom, or even someone from another country.

Mastodon instances are more close to e-mail providers, you sign up with a username, and you get a full instance identifier which is like @renatolond@masto.donte.com.br or @gargron@mastodon.social.

Also, just like e-mails, Mastodon instances are *connected*. No matter which instance you sign in, you can follow and talk with people in other instances (unless your instance has blocked theirs, or vice-versa).

This leads to the second part: instances work a bit like a "shared block/mute list". When a moderator of an instance blocks/mutes a user or another instance, this block/mute is shared by the instance users. However, you can still block/mute users by yourself. Your list of blocked/muted users is a combination of users you blocked and the ones your instance blocked.

Migrating instances is possible, but is not automatic yet. For now you can export all your data (followers, follows, blocks, mutes and toots), but you can only import follows, blocks and mutes. There's [discussion on how to make this more automatic](https://github.com/tootsuite/mastodon/issues/177), but it might still take some time.

Because of this, Mastodon is not "like reddit". Sub-reddits are more disconnected than Mastodon, each one operating by itself and with popular posts reaching front page, while when you post (publicly) on Mastodon your post will reach all instances which you have followers on. It's not like IRC either, even though IRC has several servers, servers are independent and have further divisions inside (the channels).

## Features

Mastodon has apps for both iOS and Android. They are not "official" apps, but much like Twitterrific or Tweetbot exist for Twitter, the apps that exist for Mastodon work just as good (or even better, depending on the app) than the official interface.

Mastodon has custom emojis, like Discord or Slack. The emojis are customized by the instance admins, which means each instance has their own set. i.e https://emojos.in/masto.donte.com.br

Mastodon has protected accounts like Twitter, but Mastodon posts (called toots) can be posted as followers-only, unlisted or public. Unlisted is like posting on Twitter in an account that's not protected. Public toots are posted on two special timelines that Mastodon has.

Mastodon has two special timelines: local and federated. Local has public toots by everyone that's on the same server as you and Federated has public toots by everyone that your server knows about.

Mastodon is part of a bigger network called the "Fediverse". The Fediverse is comprised of different social network softwares that are able to talk to each other seamlessly. There's softwares for youtube and instagram, for instance.

You don't really need to know about the Fediverse, but it allows for some cool stuff, like being able to see and comment in a PeerTube video from your Mastodon account. Or being able to share a cool Pixelfed photo from your Mastodon account.

Mastodon is not the only Twitter replacement in the Fediverse nor is the first one. Before Mastodon there was GNU Social and there's Pleroma too. And they all talk to each other, meaning you can follow people from any of them. The difference is mostly interface/features.

Okay, links time!

Guides: https://medium.com/@GinnyMcQueen/toot-how-to-intro-to-mastodon-e5655bfa87d2 https://hackernoon.com/what-i-wish-i-knew-before-joining-mastodon-7a17e7f12a2b

Project page: https://joinmastodon.org

Alternative web clients: https://pinafore.social/ or https://itter.photog.social/ (twitter-like one)

Some apps for Android: https://tuskyapp.github.io/ https://play.google.com/store/apps/details?id=org.mariotaku.twidere (you can use it for twitter and mastodon at the same time!)

Some apps for iOS: https://itunes.apple.com/us/app/amaroq-for-mastodon/id1214116200 https://itunes.apple.com/us/app/id1229555793

Tools to post from Twitter to Mastodon and/or vice-versa: http://crossposter.masto.donte.com.br http://moa.party https://chrome.google.com/webstore/detail/birdsite/lfmfhaopllgidldpmifdcjdckdggdjaj?q=speedtracer (chrome extension)

<a name='mnm'></a>[1]: Data from [Mastodon Network Overview](https://dashboards.mnm.social/d/000000001/mastodon-network-overview?refresh=1h&orgId=1)

