---
layout: post
title: "[Ruby] Endless error with gem dependencies "
comments: true
category: experience

---

### The problem

In setting up the octopress environment, we need to install dependencies like this: 

    gem install bundler
    bundle install

First line simply installs bundler (a Ruby dependency manager). The second line is where you might face problems:

> bundle install
>
> [Install the dependencies](http://bundler.io/man/bundle-install.1.html) specified in your Gemfile

Look at the Gemfile in your octopress folder, it looks like [this](https://github.com/imathis/octopress/blob/master/Gemfile): 

    source "https://rubygems.org"

    group :development do
      gem 'rake', '~> 10.0'
      gem 'jekyll', '~> 2.0'
      gem 'octopress-hooks', '~> 2.2'
      gem 'octopress-date-format', '~> 2.0'
      gem 'jekyll-sitemap'
      gem 'rdiscount', '~> 2.0'
      gem 'RedCloth', '~> 4.2.9'
      gem 'haml', '~> 4.0'
      gem 'compass', '~> 1.0.1'
      gem 'sass-globbing', '~> 1.0.0'
      gem 'rubypants', '~> 0.2.0'
      gem 'rb-fsevent', '~> 0.9'
      gem 'stringex', '~> 1.4.0'
    end

    gem 'sinatra', '~> 1.4.2'

When I do 'bundle install': 

    $ bundle install
    Fetching gem metadata from https://rubygems.org/........
    Resolving dependencies...

    Gem::RemoteFetcher::FetchError: SSL_connect returned=1 errno=0 state=SSLv3 read
    server certificate B: certificate verify failed (https://rubygems.org/gems/rake-
    10.4.2.gem)
    An error occurred while installing rake (10.4.2), and Bundler cannot continue.
    Make sure that `gem install rake -v '10.4.2'` succeeds before bundling.

It shows the gem 'rake' is missing. So I did as I was instrcucted to. I type __gem install rake -v '10.4.2'__ into command line, and execute. Again, I was told another gem missing. I kept doing this, until I found this is an endless procedure: 

    $ bundle install
    Fetching gem metadata from https://rubygems.org/.......
    Using rake 10.3.2
    Using RedCloth 4.2.9
    Using blankslate 2.1.2.4

    Gem::RemoteFetcher::FetchError: SSL_connect returned=1 errno=0 state=SSLv3 read
    server certificate B: certificate verify failed (https://rubygems.org/gems/timer
    s-1.1.0.gem)
    An error occurred while installing timers (1.1.0), and Bundler cannot continue.
    Make sure that `gem install timers -v '1.1.0'` succeeds before bundling.

Something is very wrong with the execution of 'bundle install'. 

### The solution

Until I found [this post](http://stackoverflow.com/questions/15529451/octopress-installation-stops-during-bundle-install), I was hopelessly searching and learning Ruby gems and related things. 

I fact, I just deleted 1 letter by changing __source "https://rubygems.org"__ to __source "http://rubygems.org"__ at line 1 of Gemfile in octopress folder. 

Then, everything is fine: 

    $ bundle install
    Fetching gem metadata from http://rubygems.org/........
    Resolving dependencies....
    Installing rake 10.4.2
    Using RedCloth 4.2.9
    Using blankslate 2.1.2.4
    Installing hitimes 1.2.2
    Installing timers 4.0.1
    Installing celluloid 0.16.0
    Installing chunky_png 1.3.3
    Installing fast-stemmer 1.0.2
    Installing classifier-reborn 2.0.2
    Installing coffee-script-source 1.8.0
    Installing execjs 2.2.2
    Installing coffee-script 2.3.0
    Installing colorator 0.1
    Installing multi_json 1.10.1
    Installing sass 3.4.9
    Installing compass-core 1.0.1
    Installing compass-import-once 1.0.5
    Installing rb-fsevent 0.9.4
    Installing ffi 1.9.6
    Installing rb-inotify 0.9.5
    Installing compass 1.0.1
    Installing tilt 1.4.1
    Installing haml 4.0.6
    Installing jekyll-coffeescript 1.0.1
    Installing jekyll-gist 1.1.0
    Installing jekyll-paginate 1.1.0
    Installing jekyll-sass-converter 1.3.0
    Installing listen 2.8.4
    Installing jekyll-watch 1.2.0
    Installing kramdown 1.5.0
    Installing liquid 2.6.1
    Installing mercenary 0.3.5
    Installing posix-spawn 0.3.9
    Installing yajl-ruby 1.1.0
    Installing pygments.rb 0.6.0
    Installing redcarpet 3.2.2
    Installing safe_yaml 1.0.4
    Installing parslet 1.5.0
    Installing toml 0.1.2
    Installing jekyll 2.5.3
    Installing jekyll-sitemap 0.7.0
    Installing octopress-hooks 2.2.3
    Installing octopress-date-format 2.0.2
    Installing rack 1.6.0
    Installing rack-protection 1.5.3
    Installing rdiscount 2.1.7.1
    Installing rubypants 0.2.0
    Installing sass-globbing 1.0.0
    Installing sinatra 1.4.5
    Installing stringex 1.4.0
    Using bundler 1.7.9
    Your bundle is complete!
    Use `bundle show [gemname]` to see where a bundled gem is installed.
    Post-install message from compass:
        Compass is charityware. If you love it, please donate on our behalf at http:
    //umdf.org/compass Thanks!
    Post-install message from haml:

    HEADS UP! Haml 4.0 has many improvements, but also has changes that may break
    your application:

    * Support for Ruby 1.8.6 dropped
    * Support for Rails 2 dropped
    * Sass filter now always outputs <style> tags
    * Data attributes are now hyphenated, not underscored
    * html2haml utility moved to the html2haml gem
    * Textile and Maruku filters moved to the haml-contrib gem

    For more info see:

    http://rubydoc.info/github/haml/haml/file/CHANGELOG.md

I guess this is because my network security settings, but I do not know. If you are facing the same issue, I hope my solution helped. Or if you know the reason, please tell me by leaving a comment below. Thanks! 
