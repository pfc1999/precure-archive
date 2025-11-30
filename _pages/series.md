---
layout: default  
title: "系列总览"
permalink: /series/
---

# ✨ 系列总览

{% for series in site.data.series %}
## {{ series.title }} ({{ series.year }})
{{ series.description }}

[查看相关资料](/resources?series={{ series.id }})

---
{% endfor %}