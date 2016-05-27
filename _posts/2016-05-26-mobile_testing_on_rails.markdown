---
layout: post
title: Mobile Testing on Rails
date: 2016-05-26  9:31:22
tags: "Rails, Mobile"
category: "Rails"
---

If you have worked on making a website that isn't complete garbage, you
have probably worried about what it looks on mobile. So I'll show you
the real quick and easy way to connect to your local server from your
mobile device.

 * Ensure both devices are on the same network

 * Then start your rails server using the following command

```bash
rails s -b 0.0.0.0
```

### Mac

 * Open Network preferences and find your local IP

![](https://dl.dropboxusercontent.com/spa/l2plmwrbl136qhn/jhi0pys8.png)

### Linux

To find your Local IP

Use ifconfig to find your inet address.

```bash
ifconfig
```

or if you're lazy you can use this command that gets rid of the stuff that
doesn't matter in this case.

```bash
ifconfig | grep 'inet addr:' | cut -d: -f2 | awk '{ print $1}' `
```

### Windows

LOL ... plz.
![](http://www.reactiongifs.com/lol/OIXrp.gif)

### Finally 
Then open your mobile browser and go to YOUR_IP:3000

<div> 
  {% tweet_button %}
  {% facebook_like_button %}
  {% gplus_share_button %}
</div>

{% facebook_comments %}
