---
title: 'Exchange 2016: External Email Cache'
published: true
date: '08-12-2018 23:05'
taxonomy:
    category:
        - blog
    tag:
        - exchange
visible: true
hide_git_sync_repo_link: false
---

This is a placeholder post to replace a post from my old blog platform which has been deleted. I will see if I can recover the post.

The basic concept of setting up an external cache in front of exchange is to find a VPS provider which allows you to receive mail on port 25, get a VPS, and setup postfix. I used Digital Ocean for this in the past.

Once you have postfix configured to receive email and forward it to Exchange, you can point your MX records at the VPS IP, and it will forward all incoming email to Exchange, and cache email if your Exchange server is unreachable.

Note that you do not have to send email through the VPS, you can configure your Exchange server to use a service like SendGrid to send email, which will use port 587.

You could setup Exchange to use the VPS to send email, and cut out SendGrid, but then you have to worry about getting on spam lists and whatnot.