---
layout: post
title: "Use Jykyll to build your blog"
description: "This article will outline specifically how to use jekyll to build your blog."
category: jekyll
tagline: "--my first blog"
tags: [jekyll, blog, install, gem, ruby, rake, post]
---
{% include JB/setup %}

This article will outline specifically how to use jekyll to build your blog, summary how to use git to manage source code.

## Environment ##

        ubuntu 12.04 LTS

## Configure Jekyll ##

        $ sudo apt-get install ruby1.9.1-dev    # Install Ruby
        $ sudo gem install jekyll               # Install Jekyll
        $ sudo apt-get install rake             # Install Rake

## The Jekyll Application Base Format

Jekyll expects your website directory to be laid out like so:

    .
    |-- _config.yml                             # Stores configuration data.
    |-- _includes                               # partial views
    |-- _layouts                                # main templates
    |   |-- default.html
    |   |-- post.html
    |-- _posts                                  # dynamic content/posts
    |   |-- 2011-04-26-hello-world.md
    |-- _site                                   # the generated site
    |-- index.html
    |-- assets                                  # not standard jekyll structure
        |-- css
            |-- style.css
        |-- javascripts

(read more: <https://github.com/mojombo/jekyll/wiki/Usage>)

## Configure GitHub ##

        $ ssh-keygen -t rsa -C "your_email@example.com"
        # Create a new ssh key (press Enter while need to type a passphrase)

        $ sudo apt-get install xclip
        # Install xclip

        $ xclip -sel clip < ~/.ssh/id_rsa.pub               
        # Copy the contents to clipboard, add to github account setting.

        $ ssh -T git@github.com
        # Showing 'Hi username!' means you've successfully authenticated.

        (Read more: <https://help.github.com/articles/generating-ssh-keys>)

        $ sudo apt-get install git git-core git-gui git-doc
        # Install git

        $ git config --global user.name "Your Name Here"
        # Set the default name for git to use when you commit

        $ git config --global user.email "your_email@example.com"
        # Set the email associated with your GitHub account

        $ git config --global credential.helper 'cache --timeout=3600'
        # Set the cache to timeout after 1 hour (setting is in seconds)

## Create Jekyll Blog ##

Step1.Create a new repository named USERNAME.github.com
        
Step2.Install Jekyll-Bootstrap

        $ git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.com
        $ cd USERNAME.github.com
        $ git remote set-url origin git@github.com:USERNAME/USERNAME.github.com.git
        $ git push origin master

Step3.Profit

Blog will be publicly available at <http://USERNAME.github.com>

        $ git clone https://github.com/USERNAME/USERNAME.github.com.git
        $ cd USERNAME.github.com
        $ jekyll --server

See it in action at <http://localhost:4000>

Step4.Rake post & page

        $ rake post title="Hello World"     # create a new post
        $ rake page name="about.md"         # create a new page
        $ rake page name="pages/about.md"   # create a new nested page
        $ rake page name="pages/about"      # create a page: ./pages/about/index.html

## Github Release commands ##

        $ git clone git@github.com:USERNAME/USERNAME.github.com.git # grap a complete copy
        $ cd USERNAME.github.com        # locate to blog
        $ git pull origin master        # fetch remote origin and merge it into local master
        $ git status                    # see the state of the project
        $ git add .                     # add unexisting files into remote
        $ git commit * -m "add comment" # add a comment
        $ git push origin master        # update to remote

(Read more: <https://help.github.com/articles/fetching-a-remote>)

        git clone URL                           # grab a complete copy of user's repository
        git://github.com/user/repo.git          # a read-only URL
        https://github.com/user/repo.git        # an HTTPS write-able URL
        git@github.com:user/repo.git            # a private SSH URL
        https://user@github.com/user/repo.git   # a private HTTPS URL

        git pull <REMOTENAME> <BRANCHNAME>      # fetch a specific branch and merge it into current local branch.

## Q & A ##

**Q1.gem install jekyll error**

        ERROR: Loading command:install(LoadError)
        no such file to load -- zlib

**A1:**
    download [ruby source code](http://archive.ubuntu.com/ubuntu/pool/universe/r/ruby1.9.1/ruby1.9.1_1.9.1.378.orig.tar.gz) and install zlib package.

        $ tar -zxvf ruby1.9.1_1.9.1.378.orig.tar.gz
        $ cd ext/zlib
        $ ruby ./extconf.rb
        $ make
        $ make install

  For more details to see [gem install error](http://www.linuxidc.com/Linux/2012-06/62073.htm)

## Refrences ##

- [Jekyll Install] (https://github.com/mojombo/jekyll/wiki/Install)

- [Jekyll Introduction](http://jekyllbootstrap.com/lessons/jekyll-introduction.html)

- [The Quickest Way to Blog with Jekyll.](http://jekyllbootstrap.com/)

- [使用github+jekyll搭建blog环境，完美替代wordpress](http://www.heiniuhaha.com/lessons/2012/08/09/use-jekyll-build-blog/)

