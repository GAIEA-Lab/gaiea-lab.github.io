---
title: "Publications"
layout: publications
excerpt: "Publications."
sitemap: false
permalink: /publications
---
<!-- Custom CSS -->
<style>
  .hanging-indent {
    margin-left: 20px;
    text-indent: -20px;
  }
  .btn-xs {
    padding: 2px 5px;
    font-size: 9px;
    line-height: 1.5;
    border-radius: 3px;
    border: none;
    box-shadow: none;
    background-color: #0059b3; /* Bootstrap primary color */
    color: white;
  }
  .btn-xs:hover, .btn-xs:focus, .btn-xs:active {
    background-color: #011f4b; /* Darker shade of primary color */
    box-shadow: none;
  }
</style>

<!-- START OF PAGE -->
# Publications

Comprehensive list from Semantic Scholar (Last updated {{ site.data.publications_meta.updated }}).
{% if site.google_scholar_url.size > 0 %}See <a href="{{ site.google_scholar_url }}">Google Scholar</a> for the most up-to-date publications. {% endif %}More information on {{ site.title }} projects can be found on the [Projects page]({{ site.url }}{{ site.baseurl }}/projects).

---

<!-- Display all publications -->
{% for pub in site.data.publications %}
<!-- Citations -->
<div class="publication-item">
  <p class="hanging-indent">
    {% if pub.url %} [{{ pub.title }}]({{ pub.url }}). {% else %} {{ pub.title }}. {% endif %}{{ pub.authors }}. *{{ pub.journal }}*{% if pub.volume %} {{ pub.volume }}{% if pub.issue %}({{ pub.issue }}){% endif %},{% endif %}{% if pub.pages %} {{ pub.pages }}{% endif %}. ({{ pub.year }})
    {% if pub.doi %} DOI: {{ pub.doi }} {% elsif pub.preprint %} *preprint: {{ pub.preprint }}*{% endif %}
  </p>
  <!-- Buttons and tags -->
  {% if pub.preprint_url %}
  <p style="margin-left: 20px; margin-top: -11px">
    {% if pub.preprint_url %}<a href="{{ pub.preprint_url }}" class="btn btn-xs btn-primary">Preprint</a>{% endif %}
  </p>
  {% endif %}
</div>
{% endfor %}
