---
layout: post
title: php程序员是否该学习python
category: tech
tag: 技术
---

p(date). 2010-09-08

其实标题可以变为"xx程序员是否该学习yy"，xx和yy可以是任何编程语言，而答案总是"应该"。因为我本身跟php打了不少年的交道，同时python也学习了一段时间，所以就把这两种语言串起来了。

php和python上手都很容易，php基本上是"大把函数任你抓，抓来就能做项目"，python是"大把模块任你选，事半功倍全靠它"。双方都有强大的第三方扩展，很少需要自己费力去写一个，除非进行二次封装。

先来看看PHP比较爽的几个特性

### array

php的<a href="http://php.net/manual/en/language.types.array.php">数组</a>几乎是所有语言中最强大的，同时扮演了list, dictionary, stack, queue甚至更多(相信这也是许多人喜欢PHP的一个重要原因)。而且使用还挺方便，提供了<a href="http://cn2.php.net/manual/en/ref.array.php">77个数组相关方法</a>(这也不可避免地产生了另一个问题，下面会提到)。

### 与html的亲密结合

这也是其他语言少有的特性，php本身就是一个模板引擎，可以与html天然融合。不过也有弊端，如html不应该包含复杂的业务逻辑，而且php与html混杂实在不够美观。

### 齐全的函数和丰富的第三方类库

函数是php的核心，这也是php容易上手的一个重要原因。要完成什么功能，只要找到该函数即可，从这个方面来说，php更适合脚本化编程(貌似这也是php的初衷)。随着php的流行，第三方类库也开始丰富起来，甚至可以为php写插件来增强php的功能。

### 对OOP的完美支持

php4虽然也可以进行oop编程，但语言本身不给力，只能努力往OOP方向去靠。到了php5，情况就有了很大的好转，支持PPP(private, protected, public) method和property，以及static/final等语法。php5.3还支持LSB(late static bindings)，虽然我觉得支持得很不到位。

### 魔术方法

<pre>__get/__set/__call/__toString</pre>等等，这些魔术方法给类带来了很大的便利，随便找个流行的框架，查看源码都会发现这些魔术方法的影踪，仿佛一下子变得无所不能。

再来看看PHP几个让人不爽的地方

### 变量被赋值，但却不使用

不太好理解，写段代码就知道了

{% highlight php %}
<?php
error_reporting(-1);
$str = 'hello world';
// 下面这段代码会报NOTICE ERROR，但事实上$str_arr已经被赋值，只是current方法没有使用这个变量
// 这段代码的运行过程是执行explode方法，然后将结果赋给$str_arr，然后将结果作为参数传递给current方法
// 也就是说整个过程没$str_arr什么事，$str_arr收到结果后就被踢走了
// 但有时候，只能使用变量而不能使用函数的返回值，如empty
$hello = current($str_arr = explode(' ', $str));
{% endhighlight %}

### 不能在函数/方法后跟[]

还是不太好理解，继续上代码

{% highlight php %}
<?php
function arr() {
	return array('hello', 'world');
}

// 会报错，于是只能先把结果赋给变量，再从这个变量去获取相应值，用完之后再unset该变量
echo arr()[0];
{% endhighlight %}

### 混乱的命名

上面说的几点只是小问题，这个就严重了。php的命名几乎没有规律可循，随便举几个例子

{% highlight php %}
<?php
// 其中一个单词缩写，中间没有分割符
strpos();
tempnam();

// 两个单词没有缩写，其中有一个分割符
str_repeat();
file_exists();

// 驼峰命名
__toString();

// 下划线连接
__set_state();

// 这个太恐怖了，强烈怀疑是酒后编程
mysql_real_escape_string()
{% endhighlight %}

### 难记的参数

这个是很要命的，有些方法，我是用一次，看一次手册，比如strpos/in_array/basename/...，完全没有套路可循。有些把$needle放到前面，$haystack放到后面(如explode)，有些正好倒过来(如strpos)，太影响写程序的效率了。怪不得写PHP的基本都需要一个强大的IDE(如Zend/NetBeans)。

### 命名空间的缺失

就好像一大堆能人异士挤在一个房子里，要用到什么功能了，就抓一个出来，如果要往这个房间加人的话，还得保证不能跟已有的重名。如果有命名空间的话，就方便了，新建一个屋子，只要这个屋子不跟别的屋子重名就行，屋子里的人爱起什么名起什么名，完全不用担心冲突。好在php5.3加入了命名空间，虽然用起来还是挺别扭。

下面来说说python吧，其实python的职能是跨平台软件开发，但也可以用做web开发，而且出现了不少优秀的web框架，所以就不可避免地与php正面交锋(php虽然也可以用来开发gui软件，但多少有点旁门左道的感觉)。

python给我的感觉是简洁，强大且优雅。

### 简洁

* 半个单词能搞定的就不用整个单词，如def/elif/iter
* 一行能搞定的就不用多行
{% highlight python %}
#generator expressions
sum(i*i for i in range(10))
{% endhighlight %}

* 同时对多个变量赋值
{% highlight python %}
a, b = ('hello', 'world')
{% endhighlight %}

### 强大

* 内置了3种常用数据结构：tuple/list/dictionary
* 支持匿名函数
* 多线程
* 函数的参数(可以不按顺序传参，这是个亮点)
* ...(php有的，python基本也少不了)

### 优雅

* 一切皆对象
* 一切皆引用
* 模块机制
* 独特的书写风格(这个因人而异吧，觉得换行+tab很别扭的也大有人在)
* 自我说明(docstring+pydoc)

当然python也非完美，不爽的地方也挺多的，如参数的默认值如果是mutable(可变的)，只会在第一次调用时初始化；class的方法至少要传一个self参数等等。但瑕不掩瑜，php程序员还是应该了解一下python，即使不是全面转向python。

对了，使用python还有一个很重要的原因是：GAE(我知道有SAE，但~~~)

参考：
* http://ioreader.com/2007/08/19/12-things-you-should-dislike-about-php/
* http://ioreader.com/2007/08/17/11-cool-things-about-php-that-most-people-overlook
* http://wiki.python.org/moin/PythonVsPhp
* http://stackoverflow.com/questions/1486608/is-switching-from-php-to-python-worth-the-trouble
* http://stackoverflow.com/questions/3319261/php-devs-that-moved-to-python-is-the-experience-better
