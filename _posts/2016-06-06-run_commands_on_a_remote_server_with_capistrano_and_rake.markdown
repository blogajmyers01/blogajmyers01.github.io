---
layout: post
title: Run Rake tasks on a server with Capistrano and Rake
date: 2016-06-06 22:54:26
tags:
category:
---

I ran into the issue the other day of getting my Jenkins to be able to
run rake tasks on a remote server. So I decided to write a rake task
that allowed it to offload the connection to the remote box onto
Capistrano. This nifty little Rake task will allow you to run Rake tasks
in a production environment on a remote server using the Dynamic Duo of
Capistrano 3 and Rake.

```rb
desc "Easily Run rake task on a remote server"
  task :server_side_rake do
    on roles(:app), in: :sequence, wait: 5 do
      within release_path do
      with rails_env: :production do
      execute :rake, ENV['task'], "RAILS_ENV=production"
      end
    end
  end
end
```

Then you can run your one off rake task with the following command:

`cap production server_side_rake task=one_time_rake_task --trace`

Easy as that!

![](https://media.giphy.com/media/XreQmk7ETCak0/giphy.gif)

<div> 
  {% tweet_button %}
  {% gplus_share_button %}
</div>

{% facebook_comments %}
