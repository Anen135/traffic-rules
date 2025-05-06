---
layout: default
title: Выбор раздела правил
---

<div class="container pt-6 pb-6">
  <h1 class="mb-4 text-center">Выберите раздел правил ПДД</h1>
  <div class="row justify-content-center">
    {% for rule in site.rules %}
    <div class="col-12 col-md-6 col-lg-4 mb-3">
      <div class="card p-3 h-100">
        <h2 class="h5 mb-2">
          <a href="{{ rule.url | relative_url }}">{{ rule.title }}</a>
        </h2>
        <p>{{ rule.excerpt | markdownify | strip_html | truncate: 120 }}</p>
        <a class="button button-secondary mt-2" href="{{ rule.url | relative_url }}">Перейти</a>
      </div>
    </div>
    {% endfor %}
  </div>
</div>
