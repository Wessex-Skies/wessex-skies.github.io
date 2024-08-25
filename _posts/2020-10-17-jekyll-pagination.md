---
title: Jekyll Pagination
date: 2020-10-17
categories: jekyll
tags: [liquid, paginate]
synopsis:
  If you have a lot of posts, then pagination is essential.
---

If you have a lot of posts, then pagination is essential. From within my project directory, I began by installing `jekyll-paginate`;

```ruby
gem install jekyll-paginate
```

I then struggled to get the process working, but I was helped through the shadows of my ignorance with the aid of [https://blog.webjeda.com/jekyll-pagination/](https://blog.webjeda.com/jekyll-pagination/).

The above guide also provides snippets of code which allows you to display and style the pagination.

The following is added to `config.yml`.

```yaml
plugins:
  - jekyll-paginate

paginate: 8
paginate_path: /page:num/
```

Then add the following to `index.html`, the home page located at the root of the project;

```liquid
{% raw %}<!-- post list -->
<ul>
  {% for post in paginator.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>

<!-- pagination -->
{% if paginator.total_pages > 1 %}
<div class="pagination">
  {% if paginator.previous_page %}
    <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&laquo; Prev</a>
  {% else %}
    <span>&laquo; Prev</span>
  {% endif %}

  {% for page in (1..paginator.total_pages) %}
    {% if page == paginator.page %}
      <span>{{ page }}</span>
    {% elsif page == 1 %}
      <a href="/">{{ page }}</a>
    {% else %}
      <a href="{{ site.paginate_path | prepend: site.baseurl | replace: '//', '/' | replace: ':num', page }}">{{ page }}</a>
    {% endif %}
  {% endfor %}

  {% if paginator.next_page %}
    <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">Next &raquo;</a>
  {% else %}
    <span>Next &raquo;</span>
  {% endif %}
</div>
{% endif %}{% endraw %}
```

