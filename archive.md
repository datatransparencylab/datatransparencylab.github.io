---
layout: default
title: Archive
---

<h3> The DTL Blog </h3>

{% for post in site.posts %}
<div class="divider-line"></div>
<div class="container-fluid">
  <div class="row">
   <div class="col-sm-4 date"><em>{{ post.date | date_to_string }}</em></div>
   <div class="col-sm-8 left-aligned"> 
     <h4> {{ post.title}}<a href="{{ post.url }}"><i class="fa fa-external-link fa-1x" style="color:#424242;"></i></a></h4>
   </div>
 </div>
</div>
{% endfor %}
