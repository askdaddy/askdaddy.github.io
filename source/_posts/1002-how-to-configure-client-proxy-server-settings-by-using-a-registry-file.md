---
title: How to configure client proxy server settings by using a registry file
tags:
  - proxy
url: 1002.html
id: 1002
categories:
  - Windows
date: 2016-11-10 09:01:45
---

SUMMARY This article describes how to create a Windows registry file to configure the proxy server settings on a client computer that is running Microsoft Internet Explorer or Windows Internet Explorer.

##### MORE INFORMATION

You can automatically configure the proxy server settings on a client computer by updating the client computer registry. To do this, create a registry file that contains the registry settings you want to update, and then distribute it to the client computer by using a batch file or logon script. Important This section, method, or task contains steps that tell you how to modify the registry. However, serious problems might occur if you modify the registry incorrectly. Therefore, make sure that you follow these steps carefully. For added protection, back up the registry before you modify it. Then, you can restore the registry if a problem occurs. For more information about how to back up and restore the registry, click the following article number to view the article in the Microsoft Knowledge Base: [322756](https://support.microsoft.com/en-us/kb/322756) How to back up and restore the registry in Windows To configure the proxy server settings on a client computer, create the following .reg file to populate the registry with the proxy server information:

    Regedit4
    
    [HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings]
    "MigrateProxy"=dword:00000001
    "ProxyEnable"=dword:00000001
    "ProxyHttp1.1"=dword:00000000
    "ProxyServer"="http://ProxyServername:80"
    "ProxyOverride"="<local>"
    

In this file, ProxyServername is the name of your proxy server. You can also use the Internet Explorer Administration Kit (IEAK) to configure proxy server settings on client computers. For additional information about IEAK, visit the following Microsoft Web site: [http://technet.microsoft.com/en-us/ie/bb219520.aspx](http://technet.microsoft.com/en-us/ie/bb219520.aspx)

            Properties
    

Article ID: 819961 - Last Review: 09/11/2011 07:27:00 - Revision: 2.0

        <span>Applies to</span>
        <p>
            Windows 7 Enterprise, Windows 7 Enterprise N, Windows 7 Home Basic, Windows 7 Home Premium, Windows 7 Home Premium N, Windows 7 Professional, Windows 7 Professional N, Windows 7 Starter, Windows 7 Starter N, Windows 7 Ultimate, Windows 7 Ultimate N, Windows Internet Explorer 8, Microsoft Internet Explorer 6.0, Windows Internet Explorer 7 for Windows XP, Windows Internet Explorer 7 for Windows Server 2003
    
    
    
        <span>Keywords: </span>
        <ul><li>
                kbisa2004yes kbinfo KB819961 
            </li></ul>
    
    
        <h5>Feedback</h5>
    
    
    
                <span>Was this information helpful?</span>
    
            </p>