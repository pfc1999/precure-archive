---
layout: default
title: "系列总览"
permalink: /series/  # 确保有斜杠
---

# ✨ 系列总览

{% for series in site.data.series %}
<div class="series-card">
    <h2>{{ series.title }} ({{ series.year }})</h2>
    <p>{{ series.description }}</p>
    <a href="{{ site.baseurl }}/resources/?series={{ series.id }}">查看相关资料</a>
</div>
<hr>
{% endfor %}