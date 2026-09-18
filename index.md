---
layout: default
title: "오늘의 기록"
---

{% assign current_month = site.time | date: "%m" %}
{% assign current_day = site.time | date: "%d" %}
{% assign found_posts = "" | split: "" %}

<!-- 1. 오늘 날짜(월/일)와 일치하는 포스트들만 골라냅니다 -->
{% for post in site.posts %}
  {% assign post_month = post.date | date: "%m" %}
  {% assign post_day = post.date | date: "%d" %}
  
  {% if post_month == current_month and post_day == current_day %}
    {% assign found_posts = found_posts | push: post %}
  {% endif %}
{% endfor %}

<!-- 2. 작성일시 역순(최신순: 오래된 것이 아래로)으로 정렬합니다 -->
{% assign sorted_posts = found_posts | sort: "date" | reverse %}

{% if sorted_posts.size > 0 %}
  {% for post in sorted_posts %}
    <article class="diary-entry">
      <div class="entry-meta">
        <!-- 연도 및 작성 시분초 표시 (예: 2026년 9월 18일 16:20) -->
        {{ post.date | date: "%Y년 %m월 %d일 %H:%M" }} 기록
      </div>
      <div class="entry-content">
        <!-- 제목 없이 본문 내용만 출력 -->
        {{ post.content }}
      </div>
    </article>
  {% endfor %}
{% else %}
  <div class="diary-empty">
    <p>오늘 날짜에 작성된 과거의 기록이 없습니다.</p>
    <p style="font-size: 0.9rem; margin-top: 5px;">첫 번째 이야기를 남겨보세요!</p>
  </div>
{% endif %}
