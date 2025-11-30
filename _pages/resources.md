---
layout: default
title: "资料库"
permalink: /resources/
---

# 📚 资料库

## 筛选条件
<select id="series-filter">
  <option value="">所有系列</option>
  <option value="futari_wa">ふたりはプリキュア</option>
  <option value="yes_precure_5">Yes! プリキュア5</option>
  <option value="heartcatch">ハートキャッチプリキュア!</option>
</select>

<select id="type-filter">
  <option value="">所有类型</option>
  <option value="interview">访谈</option>
  <option value="artbook">设定集</option>
  <option value="magazine">杂志</option>
</select>

## 资料列表
<div id="resource-list">
{% for resource in site.data.resources %}
<div class="resource-item" data-series="{{ resource.series | first }}" data-type="{{ resource.type }}">
  <h3>{{ resource.title }}</h3>
  <p><strong>来源:</strong> {{ resource.source }} | <strong>日期:</strong> {{ resource.publish_date }}</p>
  <p>{{ resource.excerpt }}</p>
  <a href="{{ resource.original_link }}" target="_blank">查看原文</a>
  <hr>
</div>
{% endfor %}
</div>

<script>
// 简单的筛选功能
document.getElementById('series-filter').addEventListener('change', function() {
  filterResources();
});

document.getElementById('type-filter').addEventListener('change', function() {
  filterResources();
});

function filterResources() {
  const seriesFilter = document.getElementById('series-filter').value;
  const typeFilter = document.getElementById('type-filter').value;
  const items = document.querySelectorAll('.resource-item');
  
  items.forEach(item => {
    const seriesMatch = !seriesFilter || item.dataset.series === seriesFilter;
    const typeMatch = !typeFilter || item.dataset.type === typeFilter;
    
    item.style.display = seriesMatch && typeMatch ? 'block' : 'none';
  });
}
</script>