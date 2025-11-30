---
layout: default
title: "资料库" 
permalink: /resources/  # 确保有斜杠
---

# 📚 资料库

<!-- 筛选条件 -->
<div class="filters">
    <select id="series-filter">
        <option value="">所有系列</option>
        {% for series in site.data.series %}
        <option value="{{ series.id }}">{{ series.title }}</option>
        {% endfor %}
    </select>

    <select id="type-filter">
        <option value="">所有类型</option>
        <option value="interview">访谈</option>
        <option value="artbook">设定集</option>
        <option value="magazine">杂志</option>
    </select>
</div>

<!-- 资料列表 -->
<div id="resource-list">
{% for resource in site.data.resources %}
<div class="resource-item" data-series="{{ resource.series | first }}" data-type="{{ resource.type }}">
    <h3>{{ resource.title }}</h3>
    <p><strong>来源:</strong> {{ resource.source }} | <strong>日期:</strong> {{ resource.publish_date }}</p>
    {% if resource.excerpt %}
    <p>{{ resource.excerpt }}</p>
    {% endif %}
    <a href="{{ resource.original_link }}" target="_blank" class="btn">查看原文</a>
    <hr>
</div>
{% endfor %}
</div>

<script>
// 筛选功能
document.addEventListener('DOMContentLoaded', function() {
    const seriesFilter = document.getElementById('series-filter');
    const typeFilter = document.getElementById('type-filter');
    
    function filterResources() {
        const seriesValue = seriesFilter.value;
        const typeValue = typeFilter.value;
        const items = document.querySelectorAll('.resource-item');
        
        items.forEach(item => {
            const seriesMatch = !seriesValue || item.dataset.series === seriesValue;
            const typeMatch = !typeValue || item.dataset.type === typeValue;
            
            item.style.display = seriesMatch && typeMatch ? 'block' : 'none';
        });
    }
    
    seriesFilter.addEventListener('change', filterResources);
    typeFilter.addEventListener('change', filterResources);
});
</script>