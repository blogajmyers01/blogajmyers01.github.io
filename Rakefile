#Sources:
# http://jasonseifer.com/2010/04/06/rake-tutorial
# http://elia.wordpress.com/2008/11/07/get-input-in-rake-tasks/
# http://www.layouts-the.me/rake/2011/04/23/rake_tasks_for_jekyll/

#Create new a post
desc "Default 'rake' command creates a new post"
task :blog do

  # Asking for title
  def ask message
    print message
    STDIN.gets.chomp
  end
  title = ask('Title: ')

  filename = "#{Time.now.strftime('%Y-%m-%d')}-#{title.gsub(/\s/, '_').downcase}.markdown"
  path = File.join("_posts", filename)
  if File.exist? path; raise RuntimeError.new("File exists #{path}"); end
  File.open(path, 'w') do |file|
    file.write <<-EOS
---
layout: post
title: #{title}
date: #{Time.now.strftime('%Y-%m-%d %k:%M:%S')}
tags:
category:
---

Content goes here

<div> 
  {% tweet_button %}
  {% facebook_like_button %}
  {% gplus_share_button %}
</div>

{% facebook_comments %}
    EOS
  end

  # invoke Textmate to edit file
  sh "vim #{path}"

end

require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"


#Change your GitHub reponame
GITHUB_REPONAME = "blogajmyers01/blogajmyers01.github.io"


desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end


desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
  Dir.mktmpdir do |tmp|
    cp_r "_site/.", tmp

    pwd = Dir.pwd
    Dir.chdir tmp

    system "git init"
    system "touch CNAME"
    system "echo 'blog.alexmyers.net' >> CNAME"
    system "git add ."
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m #{message.inspect}"
    system "git remote add origin git@github.com:#{GITHUB_REPONAME}.git"
    system "git push origin master --force"

    Dir.chdir pwd
  end
end

