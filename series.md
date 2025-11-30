---
layout: default
title: "系列总览"
permalink: /series/  # 确保有斜杠
---

# ✨ 系列总览

{% for series in site.data.series %}
<div class="series-card">
    <div class="series-header">
        {% if series.logo %}
        <img src="{{ site.baseurl }}/assets/logos/{{ series.logo }}" alt="{{ series.title }} Logo" class="series-logo">
        {% endif %}
        <div class="series-info">
            <h2>{{ series.title }} ({{ series.year }})</h2>
            <p>{{ series.description }}</p>
        </div>
    </div>
    <a href="{{ site.baseurl }}/resources/?series={{ series.id }}" class="btn">查看相关资料</a>
</div>
{% unless forloop.last %}<hr>{% endunless %}
{% endfor %}

<style>
.series-card {
    padding: 20px;
    margin: 20px 0;
}

.series-header {
    display: flex;
    align-items: flex-start;
    gap: 20px;
    margin-bottom: 15px;
}

.series-logo {
    width: 120px;
    height: auto;
    border-radius: 8px;
}

.series-info {
    flex: 1;
}

.series-info h2 {
    margin: 0 0 10px 0;
    color: #333;
}

.series-info p {
    margin: 0;
    color: #666;
    line-height: 1.5;
}

.btn {
    display: inline-block;
    padding: 8px 16px;
    background-color: #007bff;
    color: white;
    text-decoration: none;
    border-radius: 4px;
    transition: background-color 0.3s;
}

.btn:hover {
    background-color: #0056b3;
}

@media (max-width: 768px) {
    .series-header {
        flex-direction: column;
        align-items: center;
        text-align: center;
    }
    
    .series-logo {
        width: 100px;
    }
}
</style>
