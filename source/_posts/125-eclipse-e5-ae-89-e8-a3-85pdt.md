---
title: eclipse 安装pdt
tags:
  - php
url: 125.html
id: 125
categories:
  - 'NULL'
date: 2007-12-20 14:12:00
---

安装PDT  
如果决定不使用Xdebug for PDT的话，那么在这里就可以采用自订的线上安装，步骤如下：  
  
选择功能表上的「 Help / Software Updates / Find and Install... 」。  
  
在Feature Updates视窗中，选择「 Search for new features to install 」后按「 Next 」。  
  
按下「 New Remote Site 」，在New Update Site视窗中的Name栏位输入「 PDT (可以随便填) 」，而URL栏位则填入「 [http://download.eclipse.org/tools/php/](http://download.eclipse.org/tools/php/) updates/ 」。  
  
回到Feature Updates视窗后，「 Site to include in search 」栏中应该会多出一个已经被勾选的「 PDT 」项目。这时除了「 PDT 」外，请取消勾选其他项目，然后再按下「 Finish 」。  
  
接下来的步骤就和上面必要套件安装步骤是一样的，这里略过。  
  
如果想使用Xdebug for PDT ，那么这边PDT就要改用本地安装的方式来安装，步骤如下：  
  
解开PDT 0.7 RC2 ( org.eclipse.php\_feature-S20070130\_RC2.zip ) ，假设这里我解开到「 D:\\Temp\\PDT\\eclipse 」。  
  
选择功能表上的「 Help / Software Updates / Find and Install... 」。  
  
在Feature Updates视窗中，选择「 Search for new features to install 」后按「 Next 」。  
  
按下「 New Local Site 」，这时安装程式会要我们选择一个资料夹，这里就选「 D:\\Temp\\PDT\\eclipse 」。  
  
在Edit Local Site视窗中的Name栏位输入「 PDT (可以随便填) 」。  
  
回到Feature Updates视窗后，「 Site to include in search 」栏中应该会多出一个已经被勾选的「 PDT 」项目。这时除了「 PDT 」外，请取消勾选其他项目，然后再按下「 Finish 」。  
  

humen1 Tech