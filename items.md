---
layout: page
title: Items
permalink: /items/
---
{% assign items = site.data.metadata %}

<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.16/css/jquery.dataTables.min.css">
<script type="text/javascript" language="javascript" src="https://code.jquery.com/jquery-1.12.4.js"></script>
<script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.10.16/js/jquery.dataTables.min.js"></script>
    
<h2>Browse Items</h2>

<p>This table provides sorting and basic search of the archive contents. 
Click on the "Read" link to see the full document.</p>

<table id="doc-table" class="display">
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
            <td><a href="{{ site.baseurl }}/docs/{{ item.resource-identifier | downcase }}.html">{{ item.title }}</a></td>
            <td>{{ item.date }}</td>
            <td>{{ item.subject }}</td>
            <td>{{ item.description | truncatewords: 15 }} <a href="{{ site.baseurl }}/docs/{{ item.resource-identifier | downcase }}.html">Read</a></td>
        </tr>
{% endfor %}
    </tbody>
</table>

<script>
$(document).ready(function() {
    $('#doc-table').DataTable();
} );
</script>
