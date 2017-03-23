---
layout: post
title: "octpress hole"
date: 2014-09-12 12:43
comments: true
categories: takeiteasy
---


###octopress & ruby
1. octopress use ruby 1.9.3-p0

###octopress on macos
* ####install ruby.
   
   for this ruby will show the error about gcc error(use rvm install). 
   
   here is solution: [RVM ruby Installation error on Mac](http://www.quora.com/Mostafa-Ali-Elganainy/Posts/RVM-ruby-Installation-error-on-Mac)

* ####DO NOT use sudo to install ruby or about about ruby.

   if not, your will need sudo every thing about ruby.

   AND

   search how to use ruby without root for a long time.
   
   AND
   
   the search result is : uninstall.

* ####file .ruby-version
  ```bash
  ruby-1.9.3-p0 is not installed.
  To install do: 'rvm install ruby-1.9.3-p0'
  ```
  modify file .ruby-version

  ruby-1.9.3-p0 ====> ruby-1.9.3-p547

  ![RUBY VERSION SWITCH](/assets/photos/20140915octopress_rvm.png)

  then use 
  ```bash
  rvm --default your_ruby_version.
  ```

* ####rake new_post not work under z shell.
   
   try this: rake "new_post[your post]"

* ####review your markdown post easily

   chrome app store: [markdown preview plus](https://chrome.google.com/webstore/detail/markdown-preview-plus/febilkbfcbhebfnokafefeacimjdckgl). (support github format)
   
   i use it with emacs editor.

* ####got rake abort erro
   
   sometimes you got this:

   You have already activated rake 0.9.6, but your Gemfile requires rake 0.9.2.2. Prepending `bundle exec` to your command may solve this.

   to solve see this [octopress setup rvm](http://octopress.org/docs/setup/rvm/)
   
   command : rvm use 1.9.3


that's all.