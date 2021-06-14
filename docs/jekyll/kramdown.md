---
title: Kramdown
---


## 属性付加

```md
> A nice blockquote
{: title="Blockquote title"}

こんちわclass
{: .class1 .class2}

こんばんわid
{: #id-nyan}
```

## code block line numbers

参考

- https://www.richwerden.com/2017/line-numbers-in-jekyll-code.html

### method 1: use liquid tag

```liquid
{% highlight javascript linenos %}
  function some(code) { /*goes here*/ }
  let x = 21;
{% endhighlight %}
```

### method 2: _config.yml

```yml
kramdown:
  highlighter: rouge
  syntax_highlighter_opts:
    block:
      line_numbers: true
```

マークダウン；

````md
```
  function some(code) { /*goes here*/ }
  let x = 21;
```
````

