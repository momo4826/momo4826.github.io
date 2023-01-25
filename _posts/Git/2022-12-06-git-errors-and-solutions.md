---
layout: post
title: Git errors and solutions
date: 2022-12-02
categories: [Git]
tags: [Git]
excerpt: Record of git errors I met and relevant solutions.
---
1. `ssh: connect to host github.com port 22: Connection refused`

   It worked well before, however, all of a sudden, I got this error when I tried to push codes to github.com.

    Because the error is ssh-relevant, so first I generated a new ssh key and added it to github. However, the problem wasn't solved.

    If this error can't give me enough information, why not get more errors to find clues? So I tried `git clone`, and got error `ssh: connect to host github.com port 22: Connection refused`. I googled this error, and got the solution as below:
    
    The reason why we suddenly got this error might be 22 port is blocked by firewall, so try to connect 443 port of github.
    Execute `ssh -T -p 443 git@ssh.github.com` in Git Bash, then everything is fine for me!


# Resources
1. Oh, shit! Git[https://ohshitgit.com/]