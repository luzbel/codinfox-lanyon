---
layout: post
title: "Jekyll, gh-pages y los emoji"
tags: Jekyll gh-pages emoji
categories: misc
---

# El problema

¿quién pone todavía [emoticonos](https://es.wikipedia.org/wiki/Emoticono)? Eso es cosa del pasado, ahora si no usas [emojis](https://es.wikipedia.org/wiki/Emoji) no eres nadie.

# Esta vez parece de fácil solución

Un poco de google (tengo que empezar a usar más [DuckDuckGo](https://duckduckgo.com/)) y encontramos las [instrucciones](https://help.github.com/articles/emoji-on-github-pages/)

Vamos, que añadimos al _config.yml 

{% highlight yaml %}
# emoji
gems:
  - jemoji
{% endhighlight %}

reiniciamos, y listo :smiley:

# No tan fácil :confused: , problemas pendientes

1. <del>Cada vez que pongo un emoji, sale en la siguiente línea y no en la misma :confused: </del>
  - `[2016-11-13]` Veo el CSS de este [blog](http://blog.iansinnott.com/using-emoji-in-excerpts-on-github-pages) y modifico _scss/component/_post.scss añadiendo al final
  - {% highlight css %}
.post img.emoji {
  display: inline-block;
  vertical-align: middle;
  margin: 0;
}
{% endhighlight %}
2. <del>No salen los emojis en la página recopilatoria del [blog]({{ site.baseurl }}{{ site.nav.Blog[0] }})</del>
  - `[2016-11-13]` Me baso en el mismo [blog](http://blog.iansinnott.com/using-emoji-in-excerpts-on-github-pages) anterior y añado al _config.yml
    - {% highlight yaml %}
# como alternativa a excerpt, mientras no genera bien los emojis 
excerpt_length: 100
{% endhighlight %}
    - y modifico la parte del resumen del artículo en  blog/index.html 
    - {% highlight html %}
{% raw %}
    <article>
      <!-- {{ post.excerpt | markdownify }} -->
      {{ post.content | truncatewords: site.excerpt_length | markdownify }}
    <article>
{% endraw %}
{% endhighlight %}



