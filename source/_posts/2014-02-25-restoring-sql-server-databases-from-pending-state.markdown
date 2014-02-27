---
layout: post
title: "Restoring SQL Server databases from Pending State"
date: 2014-02-25 22:12:58 -0300
comments: true
categories: [SQL Server, Database]
---

Today, after migrate a SQL Server 2012 server we faced a situation where all databases were in `Pending State`.


Browsing the web we found the commands needed to put databases back to online state again, the only issue was that this server has about sixteen databases and execute the script sixteen times, changing variables would be time consuming and we could type something wrong. So I wrote this very simple script that iterates over a cursor returning  databases name which is in ```Pending State```, ```Suspect``` and ```Single User``` mode.

Hope that it saves you some work hours as it saved me. :)


{% gist 9144921 %}