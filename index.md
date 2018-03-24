---
layout: default
title: Home
---
{% assign homepagetype = site.homepagetype %}
{% capture homepagetypestring %}home-{{homepagetype | trim}}.html{%endcapture%}
{% include {{homepagetypestring}} %}

<div class="container">
    
</div>