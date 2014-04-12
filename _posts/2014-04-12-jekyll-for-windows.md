---
layout: post
title: Jekyll在windows下的本地环境搭建
tags: jekyll windows
year: 2014
month: 4
day: 12
published: true
---

##安装Ruby和DevKit
推荐在win7下使用的版本

* [Ruby 1.9.3-p448](http://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-1.9.3-p448.exe?direct)
* [DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe](https://github.com/downloads/oneclick/rubyinstaller/DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe)

`rubyinstaller-1.9.3-p448.exe`直接安装即可，安装路径不要含有空格。

DevKit解压到`C:\devkit`下，依次执行下面的命令安装

{% highlight bash %}
$ cd /D C:\devkit
$ ruby dk.rb init
$ ruby dk.rb install
{% endhighlight %}

##安装Jekyll

**1. 修改rubygems源**

使用淘宝(<http://ruby.taobao.org/>)的rubygems源

{% highlight bash %}
$ gem sources --remove https://rubygems.org/
$ gem sources -a http://ruby.taobao.org/
$ gem sources -l
*** CURRENT SOURCES ***

http://ruby.taobao.org
# 请确保只有 ruby.taobao.org
$ gem install rails
{% endhighlight %}

**2. 安装Jekyll**

{% highlight bash %}
$ gem install jekyll
{% endhighlight %}

查看Jekyll版本

{% highlight bash %}
jekyll -v
{% endhighlight %}

**3. 启动Jekyll服务器**

{% highlight bash %}
jekyll serve
{% endhighlight %}

启动服务器后，浏览器输入 <http://127.0.0.1:4000/> 访问搭建的博客。

##若干错误的解决

**1. Jekyll serve "Error: Invalid argument"错误**

降级Jekyll版本到1.4.2

{% highlight bash %}
$ gem uninstall jekyll
$ gem install jekyll --version "=1.4.2"
{% endhighlight %}

**2. Jekyll serve "invalid byte sequence in GBK"**

中文编码问题

找到jekyll安装目录，修改`convertible.rb`文件

`C:\Ruby193\lib\ruby\gems\1.9.1\gems\jekyll-1.4.2\lib\jekyll\convertible.rb`

第38行

{% highlight ruby %}
self.content = File.read_with_options(File.join(base, name), merged_file_read_opts(opts))
{% endhighlight %}

替换为下面内容

{% highlight ruby %}
self.content = File.read_with_options(File.join(base, name), :encoding => "utf-8")
{% endhighlight %}

##参考链接
1. [Windows 安装 Jekyll 若干问题的解决](http://dannyli.net/notes/fix-problems-of-jekyll-on-windows/)
2. [jekyll本地环境搭建(Windows)](http://www.cnblogs.com/yevon/p/3308158.html)
3. [Jekyll serve “Error: Invalid argument” issue](http://stackoverflow.com/questions/21164557/jekyll-serve-error-invalid-argument-issue)
4. [在 Windows 上安装 Jekyll](http://cn.yizeng.me/2013/05/10/setup-jekyll-on-windows/)
5. [Jekyll 笔记](http://huangxc.com/jekyll/)
6. [Jekyll在github上构建免费的Web应用](http://blog.fens.me/jekyll-bootstarp-github/)
