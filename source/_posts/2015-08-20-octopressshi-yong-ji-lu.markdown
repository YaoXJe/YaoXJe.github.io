---
layout: post
title: "Octopress使用记录"
date: 2015-08-20 14:43:50 +0800
comments: true
categories: 
---

##*rubyGems*配置
1. **执行以下命令替换ruby源**


	```shell
	$ gem sources --remove https://rubygems.org/
	$ gem sources -a https://ruby.taobao.org/
    $ gem sources -l
    *** CURRENT SOURCES ***
    
    https://ruby.taobao.org
	    # 请确保只有 ruby.taobao.org
	```

2. **执行以下命令修改Gemfile文件** 
 
    `$ vi Gemfile`然后将第一行的  
	`source 'https://rubygems.org/'`  
	改成  
	`source 'https://rubygems.org/'`  
	`:wq`保存并退出Vim


##上传顺序
1. **更新静态网页并上传**  

	```shell
	$ rake generate
	$ rake deploy
		
	```
2. 	**上传源文件**


	```
	$ git add .
	$ git commit -m 'your message'
	$ git push origin source
	```

##多终端合作时
+ **如果本地已经配置过octopress，只是把octopress删掉重装**
	1. 首先将博客的源文件clone到本地的octopress文件夹内
		
		```shell
		$ git clone -b source git@github.com:username/username.github.com.git octopress
		```
	2. 将博客文件clone到octopress的_deploy文件夹内
	
		```shell
		$ cd octopress  
		$ git clone git@github.com:username/username.github.com.git _deploy
		```		
+ **如果是重新在一台全新的电脑上要和服务器上的进行同步**  
	1. 执行以上2步
    2. 重新*install bundle*
    
    	```shell
    	cd octopress  
		ruby --version # Should report Ruby 1.9.2  
		gem install bundler  
		bundle install
    	``` 	
+ **如果几台电脑上面都配置好了Otcopress，要在其中一台上写博客**  	
	1. 更新*source*仓库
	
		```shell
		$ cd octopress  
		$ git pull origin source  # update the local source branch  
		$ cd ./_deploy  
		$ git pull origin master  # update the local master branch	
		```
	2. 按*上传顺序*执行
