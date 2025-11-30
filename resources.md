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
        {% assign all_series_ids = "" | split: "" %}
        {% for resource in site.data.resources %}
          {% for series_item in resource.series %}
            {% assign all_series_ids = all_series_ids | push: series_item %}
          {% endfor %}
        {% endfor %}
        {% assign unique_series_ids = all_series_ids | uniq %}
        
        {% comment %} 创建包含年份信息的系列数组 {% endcomment %}
        {% assign series_with_years = "" | split: "" %}
        {% for series_id in unique_series_ids %}
          {% assign series_info = site.data.series | where: "id", series_id | first %}
          {% if series_info %}
            {% capture series_data %}{{ series_info.year }}|{{ series_id }}|{{ series_info.title }}{% endcapture %}
            {% assign series_with_years = series_with_years | push: series_data %}
          {% endif %}
        {% endfor %}
        
        {% comment %} 按年份排序 {% endcomment %}
        {% assign sorted_series = series_with_years | sort %}
        
        {% comment %} 生成排序后的选项 {% endcomment %}
        {% for series_data in sorted_series %}
          {% assign parts = series_data | split: "|" %}
          {% assign series_id = parts[1] %}
          {% assign series_title = parts[2] %}
          <option value="{{ series_id }}">{{ series_title }}</option>
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