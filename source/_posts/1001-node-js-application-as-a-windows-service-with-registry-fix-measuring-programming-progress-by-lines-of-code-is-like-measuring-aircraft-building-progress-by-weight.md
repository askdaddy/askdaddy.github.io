---
title: >-
  Node.js Application as a Windows Service (With registry fix) - Measuring
  programming progress by lines of code is like measuring aircraft building
  progress by weight.
tags:
  - Javascript
  - js
url: 1001.html
id: 1001
categories:
  - nodejs
  - Windows
date: 2016-11-09 05:27:52
---

 [![](/uploads/2016/11/1a0cba83fdad21dce044f8961f3333b1.png)](http://www.likeaboss.lt/wp-content/uploads/2013/07/3.png) npm install In my case, command nssm install MyWebService… was unsuccessful, the problem was that app.js can’t find config.json file.

### First you will need:

1.  Node.js application (project) which you want to run as a Windows Service
2.  [Node.js](http://nodejs.org/download/)
3.  [NSSM](http://nssm.cc/)

### 1 step: Set your Node.js application as Windows Service

Download **nssm.exe** and put file into you node.js project folder [![](/uploads/2016/11/fecaf3aed7d3669485524a7db3b4aab5.png) ](http://www.likeaboss.lt/wp-content/uploads/2013/07/1.png) Put nssm.exe file into you node.js project folder Run Windows Command Processor (cmd.exe) **as administrator** and go to your node.js project folder [ ![](/uploads/2016/11/0976029aec4ae482da0427b650cf515a.png) ](http://www.likeaboss.lt/wp-content/uploads/2013/07/2.png) Your node.js project folder Run command _**npm install**_ [ ![](/uploads/2016/11/1a0cba83fdad21dce044f8961f3333b1.png) ](http://www.likeaboss.lt/wp-content/uploads/2013/07/3.png) npm install Run command _**node src\\app.js**_ and allow access through Windows firewall [ ![](/uploads/2016/11/8223266b33faf4beeecb06882e9c0b21.png) ](http://www.likeaboss.lt/wp-content/uploads/2013/07/7.png) Allow access through Windows firewall Run these two commands _**nssm.exe install MyWebService "C:\\Program Files\\nodejs\\node.exe" "C:\\Service\\src\\app.js"**_ _**net start MyWebService**_ [ ![](/uploads/2016/11/2baac63b917c8c9c5f5e8cca5f5d56f5.png) ](http://www.likeaboss.lt/wp-content/uploads/2013/07/4.png) net start MyWebService Now we need to fix this error.

### 2 step: Edit registry

Open registry editor (regedit.exe) and go to **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\MyWebService\\Parameters** [![](/uploads/2016/11/2d3c176bc47d1338ab42cd4ef628d133.png) ](http://www.likeaboss.lt/wp-content/uploads/2013/07/5.png) HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\MyWebService\\Parameters Now we need to change AppDirectory from C:\\Program Files\\nodejs to C:\\Service [ ![](/uploads/2016/11/547ca86931b2cd51a4e642eb6923dd95.png) ](http://www.likeaboss.lt/wp-content/uploads/2013/07/6.png) Change AppDirectory from C:\\Program Files\\nodejs to C:\\Service Restart computer and don’t forget to run Apache, MySQL or any other necessary servers for your project after restart. [ ![](/uploads/2016/11/5c97418a8735dda6d916b7a558f42edd.png) ](http://www.likeaboss.lt/wp-content/uploads/2013/07/9.png) Node.js Application as a Windows Service