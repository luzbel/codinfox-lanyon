---
layout: post
title: "IFTTT and Jekyll"
tags: Jekyll gh-pages IFTTT
categories: misc
---

# El problema

Una vez montada una forma rápida de publicar, el siguiente paso es automatizar que cada vez que publico algo, el contenido se distribuya por diversas redes sociales.
Como no todo lo que pienso publicar es relevante, es necesario un mecanismo para decidir cuando publicar y cuando no, al ser meras notas personales.

# Un burdo intento

Mi primera aproximación consistió en usar el disparador ["New feed item matches"](https://ifttt.com/create/if-new-feed-item-matches?sid=2) de IFTTT.
Obviamente no quería tener que poner un texto oculto en todos los mensajes, así que probé a generar en el 'feed' un nuevo campo 'trigger' (en un espacio de nombres 'ignore' inventado)

{% highlight liquid %}
{% raw %}
<?xml version="1.0" encoding="utf-8"?>
<feed xmlns="http://www.w3.org/2005/Atom" xmlns:ignore="http://www.example.com/">

 <title>{{ site.title }}</title>
 ...
 {% for post in site.posts %}
 <entry>
   <title>{{ post.title }}</title> 
   ...
    <content type="html">{{ post.content | xml_escape }}</content>
   <ignore:trigger>{{ post.trigger }}</ignore:trigger>
 </entry>
 {% endfor %}

</feed>
{% endraw %}
{% endhighlight %}

de modo que pudiera poner en el 'Front matter' de cada entrada, si quería publicar. Algo así:

{% highlight yaml %}
---
layout: post
title: "Titulo"
trigger: IFTTT-TRIGGER
---

Artículo a publicar
{% endhighlight %}

De este modo, el RSS resultante tendría este aspecto

{% highlight xml %}
<feed xmlns="http://www.w3.org/2005/Atom" xmlns:ignore="http://www.example.com/">
<title>Titulo del RSS</title>
...
<entry>
<title>Título de la entrada</title>
...
<content type="html">
Texto de la entrada
</content>
<ignore:trigger>IFTTT-TRIGGER</ignore:trigger>
</entry>
...
</feed>
{% endhighlight %}

Desafortunadamente, parece que el lector RSS de IFTTT ignora los campos que no entiende, y la acción nunca se ejecutaba :disappointed:

# Copy&paste

Afortunadamente, siempre hay quien ya ha [solucionado](https://eduardoboucas.com/blog/2015/04/28/sharing-jekyll-posts-on-social-media-using-front-matter-and-ifttt.html) el mismo problema y puedo probar su misma solución.