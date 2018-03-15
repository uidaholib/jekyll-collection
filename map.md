---
title: Map of Documents
layout: default
permalink: /map/
mapcenter: 45.67269023984288, -116.78261356184085
zoom: 6
---
{%- assign items = site.data.metadata -%}
<style>
    #map { height: 650px; z-index: 98; }
    .leaflet-popup-content img { max-width: 100%;}
    b { font-weight: bold; }
</style>
<link rel="stylesheet" href="{{ "/assets/leaflet/leaflet.css" | relative_url }}">
<link rel="stylesheet" href="{{ "/assets/leaflet/leaflet.fusesearch.css" | relative_url }}">

<div id="map"></div>

<script src="{{ "/assets/leaflet/leaflet.js" | relative_url }}"></script>
<script src="{{ "/assets/leaflet/fuse.min.js" | relative_url }}"></script>
<script src="{{ "/assets/leaflet/leaflet.fusesearch.js" | relative_url }}"></script>

<!-- add collection map data -->
<script>
    var geodata = { "type": "FeatureCollection", "features": [ 
{% for item in items %}{% if item.lat-long %}
{%- assign long-lat = item.lat-long | split: ";" | first | split: "," | reverse | join: "," -%}
    { "type":"Feature", "geometry":{ "type":"Point", "coordinates":[{{ long-lat }}] }, "properties":{ "title": {{ item.title | jsonify }}, "creator": {{ item.creator | jsonify }}, "date": {{ item.date | jsonify }}, "subject": {{ item.subject | jsonify}}, "id": {{ item.resource-identifier | jsonify }} } }{% if forloop.last == false %}, {% endif %}{% endif %}{% endfor %}
    ]};
</script>

<script>
    /* init and set zoom */
    var map = L.map('map').setView([{{page.mapcenter}}], {{page.zoom}});
    /* load map layer */ 
    L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/NatGeo_World_Map/MapServer/tile/{z}/{y}/{x}', {
    attribution: 'Tiles &copy; Esri &mdash; National Geographic, Esri, DeLorme, NAVTEQ, UNEP-WCMC, USGS, NASA, ESA, METI, NRCAN, GEBCO, NOAA, iPC',
    maxZoom: 24
    }).addTo(map);
    /* add search, https://github.com/naomap/leaflet-fusesearch */
    var options = {
        title: 'Search documents',
        placeholder: 'Search documents...',
        threshold: 0.35 // 1 = anything, 0 = exact match
    };
    var searchCtrl = L.control.fuseSearch(options);
    searchCtrl.addTo(map);
    searchCtrl.indexFeatures(geodata.features, ['title', 'subject']);
    /* add geojson marker and popup */
    L.geoJson(geodata, {
        pointToLayer: function(feature,latlng){
            var marker = L.marker(latlng);
            marker.bindPopup('<h3>' + feature.properties.title + '</h3><p>Authors: '+ feature.properties.creator + '<br>Date: ' + feature.properties.date + '<br>Subjects: ' + feature.properties.subject + '<br>Identifier: ' + feature.properties.id + '</p><h4><a href="{{ site.baseurl }}/docs/'+feature.properties.id+'.html" >View Document</a><h4>');
            return marker;
        }, 
        onEachFeature: function (feature, layer) {
            feature.layer = layer;
        }
    }).addTo(map);
</script>