---
layout: post
title: "Jekyll, gh-pages y el directorio _data"
tags: Jekyll gh-pages
categories: misc
---

# El directorio _data en Jekyll

Pues eso, que se pueden poner datos en YAML, JSON o incluso CSV y luego usarlos en las plantillas

# Ejemplo con listado de productos de gestión de APIs

{% for producto in site.data.apim.listado-productos %}
- Sobre el producto {{ producto.nombre }}, puedo decir
  - {{ producto.descripcion }}
{% endfor %}

# Prueba liquid

{{ page.title }}