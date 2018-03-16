---
layout: table
title: Items
permalink: /items/
---
{% assign items = site.data.metadata %}

<!-- currently downloaded version of datatables is bundled with bootstrap and responsive and csv download extensions -->
## Browse Items

This table provides sorting and basic search of the archive contents. 
Click on the "Read" link to see the full document.

<table id="item-table">
    <thead>
        <tr>
            <th>Title</th>
            <th>Date</th>
            <th>Subjects</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
{% for item in items %}        
        <tr>
        {%if site.repo-url%}
       <td><a href="{{ site.repo-url }}{{ site.repo-collection-pdfdownload }}{{ item.cdmid }}/filename/{{ item.title }}.pdf">{{ item.title }}</a></td>
        {%else%}
        <td><a href="{{ site.baseurl }}/items/{{ item.identifier | downcase }}.html">{{ item.title }}</a></td>
        {%endif%}
            
            <td>{{ item.date }}</td>
            <td>{{ item.subjects }}</td>
            <td>{{ item.description | truncatewords: 15 }} <a href="{{ site.baseurl }}/items/{{ item.identifier | downcase }}.html">Read</a></td>
        </tr>
{% endfor %}
    </tbody>
</table>
