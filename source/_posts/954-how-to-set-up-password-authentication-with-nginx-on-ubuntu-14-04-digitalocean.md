---
title: >-
  How To Set Up Password Authentication with Nginx on Ubuntu 14.04 |
  DigitalOcean
tags:
  - htpasswd
  - nginx
  - 密码
url: 954.html
id: 954
categories:
  - linux server
date: 2016-03-05 00:57:09
---

> sudo sh -c "echo -n 'sammy:' >> /etc/nginx/.htpasswd"Next, add an encrypted password entry for the username by typing:sudo sh -c "openssl passwd -apr1 >> /etc/nginx/.htpasswd"

来源： _[How To Set Up Password Authentication with Nginx on Ubuntu 14.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-nginx-on-ubuntu-14-04)_