---
layout: post
title: Best way to check if assets exist.
date: 2016-05-31 19:32:01
tags:
category:
---

  So if you have ever had to check if an asset exists in rails, you may
have overlooked the fact that Rails assets compile in production.

  I found this out the hard way, luckily it was just the first deploy so
it didn't affect any customers. So I thought I would share the solution I
created. Just drop this bad boy in a helper and you can then use them througout your Rails app.

```rb
def asset_exist?(path)
  if Rails.configuration.assets.compile
    Rails.application.precompiled_assets.include? path
  else
    Rails.application.assets_manifest.assets[path].present?
  end
end
```

Then in your view or controller:

```rb
if asset_exist?('test.png')
  puts "Asset found!"
else
  puts "Asset not found!"
end
```

There you have it!

![](https://m.popkey.co/991451/kMlYw.gif)

<div>
  {% tweet_button %}
  {% facebook_like_button %}
  {% gplus_share_button %}
</div>

{% facebook_comments %}
