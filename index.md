---
layout: home
title: もも
---

<div class="container">

{% assign postsByDay = 
site.posts | group_by_exp:"post", "post.date | date: '%F'" %}
<div class="row">


{% for i in (1..18) %}
{% assign delta = i | minus: 1 | times: 86400 %}
{% assign fmt_date = "March 11, 2019" | date: "%b %d, %y" | date:'%s' | plus:delta | date:"%F" %}
{% assign day_post = postsByDay | where: "name", fmt_date | first %}

{% if day_post == nil %}
{% assign thumbnail = site.static_files | where: "image", true | where_exp:"item", "item.name  == 'placeholder.jpg'" | first%}
<div class="col d3 card">
<img src="{{ site.baseurl }}{{ thumbnail.path }}" class="_blur _width100 " height="100px">
<div class="-content _alignCenter">
Japan
<p>
{{ fmt_date }}<br>
</p>
</div>
</div>

{% else %}
<div class="col d3 card">
{% assign linked_post =  day_post.items | first %}
<a href="{{ site.baseurl }}{{ linked_post.url }}">
{% assign thumbnail = site.static_files | where: "image", true | where_exp:"item", "item.path contains fmt_date" | first%}
{% if thumbnail == nil %}
    {% assign thumbnail = site.static_files | where: "image", true | where_exp:"item", "item.name  == 'default.jpg'" | first%}
{% endif %}
<img src="{{ site.baseurl }}{{ thumbnail.path }}" class="_width100" height="100px">
</a>
<div class="-content _alignCenter">
{% assign location = linked_post.location %}
{% if location == nil %}
    {% assign location = "Japan" %}
{% endif %}
<strong>{{ location }}</strong>
<p>
{{ fmt_date }}
</p>
</div>
</div>

{% endif %}

{% assign indexmod = forloop.index | modulo: 4 %}
{% if indexmod == 0 %}</div><div class="row">{% endif %}
{% endfor %}
</div>

</div>
