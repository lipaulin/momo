---
layout: home
title: もも
---


<div class="row">
{% assign intro_post = site.posts.last %}
{% include functions/card_post.html post=intro_post note=nil %}

{% assign postsByDay = site.posts | group_by_exp:"post", "post.date | date: '%F'" %}
{% for i in (1..17) %}
{% assign delta = i | minus: 1 | times: 86400 %}
{% assign fmt_date = "March 11, 2019" | date: "%b %d, %y" | date:'%s' | plus:delta | date:"%F" %}
{% assign day_post = postsByDay | where: "name", fmt_date | first %}

{% if day_post == nil %}
    {% include functions/card.html url=nil thumbnail_path=nil location='???' title='???' date=fmt_date note=nil %}
{% else %}
    {% assign linked_post =  day_post.items | first %}
    {% include functions/card_post.html post=linked_post note=nil %}
{% endif %}

{% endfor %}
</div>
