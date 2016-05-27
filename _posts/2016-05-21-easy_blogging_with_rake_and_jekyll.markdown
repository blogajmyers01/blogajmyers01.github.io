---
layout: post
title: Easy Blogging with Rake and Jekyll
date: 2016-05-21  0:44:43
tags: "Rake, Jekyll, Blogging"
category: "Jekyll"
---

So while building this blog I decided to use Jekyll since github so
kindly hosts it for free on their servers.

I wanted to share the RakeFile I use to create posts.

```
# Ask for title
def ask message
  print message
  STDIN.gets.chomp
end
title = ask('Title: ')

#Create new a post
desc "Default 'rake' command creates a new post"
task :default do
  filename = "#{Time.now.strftime('%Y-%m-%d')}-#{title.gsub(/\s/, '_').downcase}.markdown"
  path = File.join("_posts", filename)
  if File.exist? path; raise RuntimeError.new("File exists #{path}"); end
  File.open(path, 'w') do |file|
    file.write <<-EOS
---
layout: post
title: #{title}
date: #{Time.now.strftime('%Y-%m-%d %k:%M:%S')}
---

Content goes here
    EOS
  end

  # open the file in vim
  sh "vim #{path}"

end
```

Then to create a new blog post you just run:

```
rake
```

<div> 
  {% tweet_button %}
  {% facebook_like_button %}
  {% gplus_share_button %}
</div>

{% facebook_comments %}
