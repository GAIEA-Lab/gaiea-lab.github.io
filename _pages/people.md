---
title: "People"
layout: gridlay
excerpt: ""
sitemap: false
permalink: /people
---

# People

<!-- Group photo(s): put files in /images/grouppic/ and list them in _data/group_photos.yml -->
{% for photo in site.data.group_photos %}
<div class="col-sm-12 clearfix" style="text-align: center; ">
<div style="display: flex; justify-content: center;">
<img class="group-pic" src="{{ site.url }}{{ site.baseurl }}/images/grouppic/{{ photo.name }}" alt="Group photo"/>
</div>
<i>{{ photo.description }}</i>
</div>
{% endfor %}

<!-- PI(s), postdocs, and grad students, in that order. Photos go in /images/teampic/ -->
{% assign member_groups = "pi,postdocs,grad_students" | split: "," %}
{% for group in member_groups %}
{% for member in site.data[group] %}
<div class="row" style="margin-bottom: 10px; padding: 15px 0;">
<div class="col-sm-2" style="display: flex; justify-content: center;">
<div class="image-cropper">
{% if member.photo %}<img class="person-pic" src="{{ site.url }}{{ site.baseurl }}/images/teampic/{{ member.photo }}" alt="{{ member.name }} photo"/>{% endif %}
</div>
</div>
<div class="col-sm-10" style="display: flex; flex-direction: column;">
<h4 class="person-name">{{ member.name }}</h4>
{% if member.info %}<p class="person-title">{{ member.info }}</p>{% endif %}
<p class="person-bio">{{ member.description }}</p>
<div class="person-links" style="display: flex; gap: 8px;">
{% if member.website %}<a href="{{ member.website }}" title="Website" aria-label="{{ member.name }} website"><i class="mdi mdi-web"></i></a>{% endif %}
{% if member.google_scholar %}<a href="{{ member.google_scholar }}" title="Google Scholar" aria-label="{{ member.name }} Google Scholar"><i class="mdi mdi-school"></i></a>{% endif %}
{% if member.github %}<a href="{{ member.github }}" title="GitHub" aria-label="{{ member.name }} GitHub"><i class="mdi mdi-github"></i></a>{% endif %}
{% if member.email %}<a href="mailto:{{ member.email }}" title="Email" aria-label="Email {{ member.name }}"><i class="mdi mdi-email"></i></a>{% endif %}
{% if member.linkedin %}<a href="{{ member.linkedin }}" title="LinkedIn" aria-label="{{ member.name }} LinkedIn"><i class="mdi mdi-linkedin"></i></a>{% endif %}
{% if member.twitter %}<a href="{{ member.twitter }}" title="Twitter" aria-label="{{ member.name }} Twitter"><i class="mdi mdi-twitter"></i></a>{% endif %}
{% if member.youtube %}<a href="{{ member.youtube }}" title="YouTube" aria-label="{{ member.name }} YouTube"><i class="mdi mdi-youtube"></i></a>{% endif %}
{% if member.instagram %}<a href="{{ member.instagram }}" title="Instagram" aria-label="{{ member.name }} Instagram"><i class="mdi mdi-instagram"></i></a>{% endif %}
</div>
</div>
</div>
{% endfor %}
{% endfor %}

{% if site.data.msvisit.size > 0 %}
---
<h2 style="padding: 20px 0 10px">Masters & Visiting Students</h2>
<ul style="list-style: none; padding: 0;">
{% for member in site.data.msvisit %}
  <li style="margin-bottom: 8px;">
    <span style="font-size: 1.1em;">{{ member.name }}</span>
    {% if member.info %}<br><span style="color: #666; font-size: 0.9em;">{{ member.info }}</span>{% endif %}
  </li>
{% endfor %}
</ul>
{% endif %}

{% if site.data.undergrads.size > 0 %}
---
<h2 style="padding: 20px 0 10px">Undergraduates</h2>
<ul style="list-style: none; padding: 0;">
{% for member in site.data.undergrads %}
  <li style="margin-bottom: 8px;">
    <span style="font-size: 1.1em;">{{ member.name }}</span>
    {% if member.info %}<br><span style="color: #666; font-size: 0.9em;">{{ member.info }}</span>{% endif %}
  </li>
{% endfor %}
</ul>
{% endif %}

{% if site.data.alumni.size > 0 %}
---
<h2 style="padding: 20px 0 10px">Lab Alumni</h2>
<ul style="list-style: none; padding: 0;">
{% for member in site.data.alumni %}
  <li style="margin-bottom: 8px;">
    {% if member.link %}
      <a href="{{ member.link | escape }}" style="font-size: 1.1em; color: inherit; text-decoration: underline; text-decoration-color: #bbb; text-underline-offset: 0.15em;">{{ member.name }}</a>
    {% else %}
      <span style="font-size: 1.1em;">{{ member.name }}</span>
    {% endif %}
    <span style="color: #666; font-size: 0.9em;">({{ member.previous }}){% if member.current %} &rarr; {{ member.current }}{% endif %}</span>
  </li>
{% endfor %}
</ul>
{% endif %}
