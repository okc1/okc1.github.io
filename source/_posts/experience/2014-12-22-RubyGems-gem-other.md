---
layout: post
title: "[Ruby] RubyGems, gem, Gemfile and Bundler "
comments: true
category: experience

---

Sometme I found the different concepts in Ruby very confusing for beginners. So I write this post to explain some terminologies in ruby setup. 

### RubyGems (tool)

__[RubyGems](http://en.wikipedia.org/wiki/RubyGems)__ is a package manager for the Ruby programming language. 

It is a tool to manage the installation of gems, and a server for distributing them. 

RubyGems is very similar to apt-get, portage, and yum in functionality.

### gem (command)

'gem' command allows you to interact with RubyGems. It is used build, upload, download, and install Gem packages. 

Installation:

    gem install mygem

Uninstallation:

    gem uninstall mygem

Listing installed gems:

    gem list --local

Listing available gems, e.g.:

    gem list --remote

### Gemfile (text file)

[A Gemfile](http://bundler.io/man/gemfile.5.html) describes the gem dependencies required to execute associated Ruby code.

It is placed in the root of the directory containing the associated code. 

A Gemfile is evaluated as Ruby code, in a context which makes available a number of methods used to describe the gem requirements.

### gem (program) 

[ref1](http://stackoverflow.com/questions/5233924/what-is-a-ruby-gem), [ref2](http://guides.rubygems.org/what-is-a-gem/)

A gem is a module/Library that you can install and use in every project on your server. 

Each gem has a __name, version, and platform__. For example, __rake gem__ has a 10.3.2 version on platform Ruby.

Inside a gems are the following components: 

1. Code (including tests and supporting utilities)
1. Documentation
1. gemspec

Standard code structure:

    % tree freewill
    freewill/
    ├── bin/
    │   └── freewill
    ├── lib/
    │   └── freewill.rb
    ├── test/
    │   └── test_freewill.rb
    ├── README
    ├── Rakefile
    └── freewill.gemspec

### Bundler (dependency manager)

[ref](http://bundler.io/)

Bundler manages an application's dependencies. 

Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed. 
