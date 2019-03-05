---
layout:	#post 또는 공백
title: "Jekyll 기본 알아두기"
tags:
categories: Jekyll
---

This post is used for testing tag plugins. See [docs](http://zespia.tw/hexo/docs/tag-plugins.html) for more info.

## Jekyll 기본 알아두기

### 머릿말
```
---
layout:	post 또는 공백
title: "Jekyll 기본 알아두기"
tags:
- consectetur
categories: jeklly
or
categories: 
- jeklly
- jeklly2
link: #제목을 클릭하면 해당 링크로 자동이동
---
```

### Normal code block

```
#```
코드블럭: # 제거 후 사용
#```
```

````
#````
글상자: # 제거 후 사용
#```
```

### Highlight code block

```python
print "Hello world"
```
{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}

### Image Test

```
![](http://ww1.sinaimg.cn/mw690/81b78497jw1emfgwkasznj21hc0u0qb7.jpg)
```
![](http://ww1.sinaimg.cn/mw690/81b78497jw1emfgwkasznj21hc0u0qb7.jpg)

```
![Caption](http://ww3.sinaimg.cn/mw690/81b78497jw1emfgwjrh2pj21hc0u01g3.jpg)
```
![Caption](http://ww3.sinaimg.cn/mw690/81b78497jw1emfgwjrh2pj21hc0u01g3.jpg)

```
![Small Picture](http://placehold.it/350x150.jpg)
```
![Small Picture](http://placehold.it/350x150.jpg)

### Emoji Test
```
:bowtie::smile::laughing::blush::smiley::relaxed::smirk:
:heart_eyes::kissing_heart::kissing_closed_eyes::flushed::relieved::satisfied::grin:
```
:bowtie::smile::laughing::blush::smiley::relaxed::smirk:
:heart_eyes::kissing_heart::kissing_closed_eyes::flushed::relieved::satisfied::grin:



