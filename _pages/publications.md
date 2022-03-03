---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

Please see my <u><a href="https://hansriess.com/files/cv.pdf">CV</a>.</u>. You can also find my articles on <u><a href="https://scholar.google.com/citations?hl=en&user=lkdryGgAAAAJ">my Google Scholar profile</a>.</u>


{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}