---
layout: post
title: Build personal website with Jekyll and Github on Windows
date: 2022-11-28
categories: [website]
tags: [jekyll, personal website, github, blog]
excerpt: How to build a personal website with Jekyll and  Github on Windows
---
# What
Jekyll is a static site generator written in Ruby, so the things we need to set up: ruby, RubyGems(package manager for ruby), Jekyll.
# How
1. Download and install a Ruby+Devkit version from [RubyInstaller Downloads](https://rubyinstaller.org/downloads). Use default options for installation.

   And as the official Jekyll tutorial said, "Run the ridk install step on the last stage of the installation wizard. This is needed for installing gems with native extensions".

2. First make sure everything is ok.
   ```shell
   gem -v # my version is 3.3.26
   ```
   Open a new command prompt window, if you are in China, change the sources before gem install.
   ```shell
   gem sources --remove https://rubygems.org/ #this url can not be reached, and it should be removed, only leave usable url in sources
   gem sources --add https://gems.ruby-china.com/
   gem sources -l #check
   ```
3. Install jekyll and necessary plugins.
   > Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed. Bundler can be a great tool to use with Jekyll.
   
   Open a new cmd window as Administrator.
   ```shell
   gem install jekyll bundler jekyll-paginate
   jekyll -v #check if it's installed
   bundler -v
   ```
4. Start a new project(still in the cmd window as Administrator).
   ```shell
   jekyll new yourprojectname
   ```
   You can now write your own blog website, or just download the blog repository you like from Github then change it according to your needs.
5. The directory tree of the jekyll project:
   - _data (contents of navigation is stored in data files under this directory)
   - _includes (html codes that can be included in layouts)
   - _layouts (html files to design the layouts of website pages)
   - _posts (where you create new posts, remember name them as the pattern of ``permalink:`` you define in _config.yml)
   - _sass (saas if an extension of css in jekyll)
   - _site (generated after you first run ``jekyll build`` or ``jekyll serve``, they are html files for posts written in markdown files)
   - assests 
     - css
     - images
     - script
   - pages (static pages of the website)
   - _config.yml (website settings file)
   - Gemfile (add all plugins you want to install here, don't forget change the source according step 2 mentioned before if you're in China)
   - Gemfile.lock(generated after you use run ``bundle install`` to install the )
   - index.html (Home page html)
6. Learn how to change the default website to what you like, read [this official tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/), it's very detailed and clear.

7. Make it work.
   ```shell
   bundle exec jekyll build #build the website, and generate html files for posts written in markdown files
   bundle exec jekyll serve #make the website run in local(http://localhost:4000); "jekyll build" is a part of it
   ```
8. Upload to Github
   1. create a new repository with the name "yourgithubname.github.io"
   2. open a git bash window in you local project, then:
      ```shell
      git init
      git branch -M main
      git remote add origin git@github.com:momo4826/deep_learning_notes_fr.git
      git add .
      git commit -m "init"
      git push origin main
      ```
9. Done!