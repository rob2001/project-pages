---
layout: page
title: "Projects"
description: "A Short List of Projects"
---


{% for page in site.pages %}{% if page.url contains "projects/" and page.url != "/projects/" %}{% if page.title %}

### [{{ page.title }}]({{site.baseurl}}{{page.url}})

{{ page.description }}

{% endif %}{% endif %}{% endfor %}

