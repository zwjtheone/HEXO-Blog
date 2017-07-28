title: Ruby gems更换source的时候 certificate verify failed
date: 2016-11-30 10:01:08
update: 2016-11-30 10:08:08
tags:
	- Ruby
	- Sass
---


安装Ruby后，安装sass，jekkly会遇到错误，按照 https://gems.ruby-china.org/ ,的方式更换Ruby源，会遇到错误

>gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
>Error fetching https://ruby.taobao.org/:
>SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://rubygems-china.oss-cn-hangzhou.aliyuncs.com/specs.4.8.gz)

其实 `gem sources --add http://gems.ruby-china.org/` 是 **http**。 就可以了。坑啊- -。
