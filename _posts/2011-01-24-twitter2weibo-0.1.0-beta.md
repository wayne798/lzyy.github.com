---
layout: post
title: twitter2weibo 0.1.0 beta release
category: tech
tag: 技术
---

经过1个多月断断续续的调试和优化，twitter2weibo终于迎来了0.1.0 beta版。此版本修正了不少bug，也添加了些新特性。感谢大家的反馈，因为此脚本而给您带来的麻烦，我表示非常抱歉。

重新研究了一下weibo的登录机制，发现依旧可以通过登录微博，然后同步的方式来避开使用新浪apikey。为了保险起见，设置了个fallback，当登录失败时，通过apikey正规渠道来同步。

### 特性

* 支持多用户(在config.php里配置)
* 多线程同步(只支持linux)
* 保存用户cookie，避免多次读取
* 用户删除某条/某些tweet后，不会出现异常同步

### 0.1.0 beta 新特性

* 完善的日志(如果出现异常，会记录到data/log)
* 先通过"非正规"方式登录微博，然后同步。如果失败，再通过正规的apikey方法来同步
* 使用curl代替file_get_contents

data/log demo

{% highlight console %}
2011-01-24 14:20:08: 同步到新浪微博出错，错误信息：{"code":"M18003","info":"同步太频繁","email":"xxx@qq.com","pwd":"111111","tweet":"yyy","apikey":"123456789"}

2011-01-24 14:21:52: 使用apikey同步失败：{"request":"/statuses/update.json","error_code":"400","error":"40028:发微博太多啦，休息一会儿吧","email":"xxx@qq.com","pwd":"111111","tweet":"yyy","apikey":"123456789"}
{% endhighlight %}

### 0.1.0 beta 修复的bug

* 重复同步的问题(当时没有考虑到这个问题的严重性，给大家添麻烦了)
* 对pcntl_fork方法的判断(之前需要手工修改，现在自动判断)

### 下载/更新

旧版本用户可以通过此命令行更新

{% highlight bash %}
wget -N -O twitter2weibo.php --no-check-certificate https://github.com/lzyy/twitter2weibo/raw/master/twitter2weibo.php
{% endhighlight %}

新用户请到github下载: <a href="https://github.com/lzyy/twitter2weibo">https://github.com/lzyy/twitter2weibo</a>

水平有限，bug难免，您若有心，欢迎反馈
