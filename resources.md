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
        {% assign all_series = "" | split: "" %}
        {% for resource in site.data.resources %}
          {% for series_item in resource.series %}
            {% assign all_series = all_series | push: series_item %}
          {% endfor %}
        {% endfor %}
        {% assign unique_series = all_series | uniq | sort %}
        {% for series in unique_series %}
        <option value="{{ series }}">{{ series }}</option>
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
<div class="resource-container" data-series="{{ resource.series | join: ',' }}" data-type="{{ resource.type }}">
    <div class="resource-item">
        <h3>{{ resource.title }}</h3>
        <p><strong>来源:</strong> {{ resource.source }} | <strong>日期:</strong> {{ resource.publish_date }}</p>
        {% if resource.excerpt %}
        <p>{{ resource.excerpt }}</p>
        {% endif %}
        <a href="{{ resource.original_link }}" target="_blank" class="btn">查看原文</a>
    </div>
    {% unless forloop.last %}<hr>{% endunless %}
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
        const containers = document.querySelectorAll('.resource-container');
        let visibleCount = 0;
        
        containers.forEach(container => {
            const seriesData = container.dataset.series.split(',');
            const typeMatch = !typeValue || container.dataset.type === typeValue;
            const seriesMatch = !seriesValue || seriesData.includes(seriesValue);
            
            const isVisible = seriesMatch && typeMatch;
            
            container.style.display = isVisible ? 'block' : 'none';
            
            if (isVisible) {
                visibleCount++;
            }
        });
        
        // 隐藏最后一个容器的分隔线
        const visibleContainers = Array.from(containers).filter(container => 
            container.style.display !== 'none'
        );
        
        visibleContainers.forEach((container, index) => {
            const hr = container.querySelector('hr');
            if (hr) {
                hr.style.display = index === visibleContainers.length - 1 ? 'none' : 'block';
            }
        });
    }
    
    seriesFilter.addEventListener('change', filterResources);
    typeFilter.addEventListener('change', filterResources);
});
</script>