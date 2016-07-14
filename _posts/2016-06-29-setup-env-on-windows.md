---
layout: post
title: "Setup development environment on Windows 7 碎碎念"
date: 2016-06-29 23:58:00 +0800
categories: others
---


# Setup development environment on Windows 7 碎碎念

自从有了mac，我的windows本早已沦为游戏机。鉴于这次只带了windows小本回国，于是只好开始在windows电脑上配置开发环境。

### Preparation:
Upload wip code onto Github

### Tools:
* Cygwin64
* SourceTree
* Lantern vpn (in order to access Google...)

### Install Cygwin64
1. Download Cygwin64 from https://cygwin.com/install.html
2. Run the execution file to install.
3. Select 'download and install'
4. Choose a download url
5. Select packages want to install, such as git, python, php etc...
6. Done

### Install Node:
1. Download node from https://nodejs.org/
2. Run the installer and follow instructions
3. Open command prompt, check 'node -v' and 'npm -v'

### Install MongoDB
1. Download MongoDB from https://www.mongodb.com/download-center?jmp=nav#community. I choose Windows Vista without SSL support.
2. Run the installer. By default it will be installed to C:\Mongodb
3. Create folder **data** under Mongodb and create folder **db** under folder data.
4. Navigate to bin folder under Mongodb. Run 'mongod --dbpath "c:\MongoDB\data\db" --storageEngine=mmapv1' and check if it successfully starts mongodb.

Note: Only get it working using command prompt. When using Cygwin64, it throws error 'cannot find command mongod'.