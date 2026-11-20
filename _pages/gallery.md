---
permalink: /gallery/
title: "Gallery"
author_profile: true
---

<!--
  Sections are listed in _data/gallery.yml. Photos go in images/gallery/<folder>/
  and are shown in filename order.
-->
<style>
  .gallery-section h2 { margin-top: 1.5em; }
  .gallery { display: flex; flex-wrap: wrap; gap: 12px; margin-top: 0.75em; }
  .gallery a { display: block; max-width: 100%; }
  .gallery img { display: block; height: 240px; width: auto; max-width: 100%; object-fit: contain; border-radius: 6px; transition: opacity 0.2s; }
  .gallery img:hover { opacity: 0.85; }
</style>

{% assign photos = site.static_files | where_exp: "f", "f.path contains '/images/gallery/'" | sort: "path" %}

{% for section in site.data.gallery %}
  {% assign prefix = "/images/gallery/" | append: section.folder | append: "/" %}
<div class="gallery-section" id="{{ section.folder }}">
  <h2>{{ section.title }}</h2>
  {% if section.description %}<p>{{ section.description }}</p>{% endif %}
  <div class="gallery">
  {% for photo in photos %}
    {% assign start = photo.path | slice: 0, prefix.size %}
    {% assign ext = photo.extname | downcase %}
    {% if start == prefix %}
      {% if ext == ".jpg" or ext == ".jpeg" or ext == ".png" or ext == ".webp" or ext == ".gif" %}
    <a href="{{ photo.path | relative_url }}" target="_blank"><img src="{{ photo.path | relative_url }}" alt="{{ section.title }}" loading="lazy"></a>
      {% endif %}
    {% endif %}
  {% endfor %}
  </div>
</div>
{% endfor %}

[← Back to home](/)
