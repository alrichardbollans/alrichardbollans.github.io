---
layout: page
title: Guides
permalink: /guides/
---

[//]: # (As per https://stackoverflow.com/questions/31017554/jekyll-post-links-not-including-base-url, include base url in linnks)

If you have any questions or comments on any information on this site, please start
a [discussion](https://github.com/alrichardbollans/scratch/discussions).

{% for g in site.guides %}
<h2>
<a href="{{ g.url | relative_url }}">
{{ g.title }}
</a>
</h2>
  <p>{{ g.snippet | markdownify }}</p>
{% endfor %}
