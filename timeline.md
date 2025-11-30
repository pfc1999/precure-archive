---
layout: default
title: "时间线"
permalink: /timeline/
---

# 📅 时间线

{% for series in site.data.series %}
<div class="timeline-item">
    <h2>{{ series.year }} - {{ series.title }}</h2>
    <p>{{ series.description }}</p>
    
    {% assign series_resources = site.data.resources | where: "series", series.id %}
    {% if series_resources.size > 0 %}
    <h4>相关资源 ({{ series_resources.size }}):</h4>
    <ul>
        {% for resource in series_resources limit:3 %}
        <li>
            <a href="{{ resource.original_link }}" target="_blank">{{ resource.title }}</a>
            ({{ resource.publish_date }})
        </li>
        {% endfor %}
    </ul>
    {% endif %}
</div>
<hr>
{% endfor %}