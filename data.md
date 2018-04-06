---
layout: table
title: Data
permalink: /data/
---
{% assign items = site.data[site.csvtitle] %}
{% include datadownload.html %}
<!-- currently downloaded version of datatables is bundled with bootstrap and responsive and csv download extensions -->
<style>.description{min-width:400px;"}</style>
## Collection Data 

The table below provides sorting and basic search of the archive contents. Use the download button at the top right to download the entire metadata spreadsheet building the collection. Use the "CSV" button below to download the metadata you see on the page.  
<table id="item-table">
    <thead>
        <tr>
        {% assign tableheaders = site.datatable | split:',' %}
        {% for header in tableheaders %}
            <th class="{{header}}">{{header | capitalize}}</th>
          {%endfor%}
          <th>Download</th>
        </tr>
    </thead>
    <tbody>{% for item in items %}<tr>{% for header in tableheaders %}{% if forloop.first %}<td><a href="{% include item-link.html %}" target="_blank" title="link to item">{{item[header]}}</a>{% if item.format contains "pdf" %}<br/><br/><a target="_blank" href="{% include download/pdf.html %}" style="font-size:11px;">Download PDF</a>{% endif%}</td>
         {% else %}
            <td class="{{header}}">{{item[header]}}</td>
            {% endif%}
          {%endfor%}
        <td><a class="btn btn-secondary btn-sm" target="_blank" {% if item.format contains "pdf" %} href="{% include download/pdf.html %}">Download<br/>PDF</a>{% elsif item.format contains "image" %}href="{% include download/image.html %}">Download<br/>Image</a>{% elsif item.format contains "mp3" %} href="{% include download/mp3.html %}">Download<br/>MP3</a>{% else %}{% endif %}
     </td>
        </tr>
{% endfor %}
    </tbody>
</table>
