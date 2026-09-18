---
layout: default
title: "홈"
---

<h2>📖 오늘의 다이어리 (On This Day)</h2>

{% assign current_month = site.time | date: "%m" %}
{% assign current_day = site.time | date: "%d" %}
{% assign current_year = site.time | date: "%Y" | plus: 0 %}

<ul class="diary-list">
  {% assign found = false %}
  {% for post in site.posts %}
    {% assign post_month = post.date | date: "%m" %}
    {% assign post_day = post.date | date: "%d" %}
    {% assign post_year = post.date | date: "%Y" | plus: 0 %}
    
    {% if post_month == current_month and post_day == current_day %}
      {% assign found = true %}
      <li class="diary-item">
        <span class="diary-year">{{ post_year }}년</span>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        <div class="diary-excerpt">
          {{ post.excerpt | strip_html | truncate: 100 }}
        </div>
      </li>
    {% endif %}
  {% endfor %}
  
  {% if found == false %}
    <p>오늘 날짜에 작성된 과거의 기록이 아직 없습니다. 첫 글을 작성해 보세요!</p>
  {% endif %}
</ul>
