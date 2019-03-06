---
layout: home
title: News
---

<div class="container">
{% assign post_list = site.posts | group_by_exp: "item", "item.last_updated_at | default: item.date | date:'%F'" %}
{% for date_post in post_list %}
    {% for post in date_post.items %}
        {% assign note = 'nouveau' %}
        {% if post.last_updated_at %}
            {% assign note = 'changement' %}
        {% endif %}
        {% include functions/card_post.html post=post note=note %}
    {% endfor%}
{% endfor%}
</div>

