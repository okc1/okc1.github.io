---
layout: post
title: "[Octopress] Clone Octopress Blog From A Different Computer "
comments: true
category: experience

---

__Ruby/gem/bundler setup (on a new machine) has always been a hassle to me__. Not only that, I've had some confusions about developing Octopress blog on 2 different computers. 

Now that I've had enough failures and success, I would like write a long post to summarize it. 

### Install Ruby

Well first of all, we must install __Ruby__ and __Development Kit__. Simply go this [this page](http://rubyinstaller.org/downloads/) and download: 

1. Ruby 1.9.3
1. DevKit for Ruby 1.9.3

__Installing Ruby__ is straight-forward, only remember to check "Add Ruby to your PATH". Otherwise you need to manually set the __Ruby directory__ (eg. C:\Ruby193\bin) in __System Variables Settings__. 

{% img middle /assets/images/install-ruby-193.png %}

__Ruby DevKit is a self-extracting archive__. After extracting the files, we should [initialize the DevKit](http://jekyll-windows.juthilo.com/1-ruby-and-devkit/) like this: 

    cd C:/RubyDevKit
    ruby dk.rb init
    ruby dk.rb install

### Clone octopress 

__clone the source branch to the local octopress folder__

> using HTTPS
>
> git clone -b source https://github.com/okckd/okckd.github.io.git octopress

> or using SSH
>
> git clone -b source git@github.com:okckd/okckd.github.io.git octopress

I would recommend using SSH over HTTPS, because __using HTTPS, you will need to type your username and password everytime you push__. 

To correct 'HTTPS' to 'SSH', follow [this instruction](http://stackoverflow.com/a/6565661): 

> git remote set-url origin git@github.com:username/repo.git

More info about HTTPS and SSH is [available](https://help.github.com/articles/which-remote-url-should-i-use/). 

### Install dependencies

Follow [this instruction](http://www.techelex.org/setup-octopress-windows7/) and install bundler and dependencies. 

    cd c:/github/octopress
    gem install bundler
    rbenv rehash    # optional, unless you are using rbenv
    bundle install

If you see endless dependency errors here, please refer to my other post: __[[Ruby] Endless error with gem dependencies]({% post_url /experience/2014-12-23-Endless-error-gem-dependencies %})__. 

If you are confused with some concepts in Ruby, read __[[Ruby] RubyGems, gem, Gemfile and Bundler]({% post_url /experience/2014-12-22-RubyGems-gem-other %})__. 

### Now, start octopress

You can use either of the commands below to start octopress. I can't remember clearly but you can simply follow [this guide](http://octopress.org/docs/setup/).

> rake setup_github_pages
>
> when prompted, enter this url: git@github.com:okckd/okckd.github.io.git
>
> rake install

### Commit your changes

You can do 'rake gen_deploy' to deploy to master branch. Do 'git commit", "git push origin source' to update blog source. [reference](http://blog.zerosharp.com/clone-your-octopress-to-blog-from-two-places/)

At this step, congratulations you are all set! 

### Last word

Setting 'rake' up is found to be a great hassle for many, for example, [someone spent 7 hours on it](http://hamaluik.com/posts/switching-to-octopress/). 

Wish this post can help! 
