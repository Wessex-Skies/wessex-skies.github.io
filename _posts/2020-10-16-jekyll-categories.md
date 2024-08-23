---
layout: single
title: Jekyll Categories
date: 2020-10-16
tags: [categories, frontmatter, liquid]
synopsis:
  So how do we implement and make use of categories when building a website with Jekyll?
---

So how do we implement and make use of categories? Once again I am indebted to [https://blog.webjeda.com/jekyll-categories/](https://blog.webjeda.com/jekyll-categories/) for providing the solution to this problem.

The front matter on each of my posts appears in the following format;

```
---
layout: post
title: my-post-title
permalink: /my-post-title/
categories: [Category1, Category2]
---
```

I have created an html page for each category, and inserted the following code. Remember to replace `category-name` with the name of your desired category.

<!--more-->

```liquid
{% raw %} ---
layout: page
title: Title
permalink: /category-name/
---
<div id="archives">
  {% for post in site.categories.category-name %}
   <li><span>{{ post.date | date: '%Y-%m-%d' }}</span> &nbsp; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</div> {% endraw %}
```

To have the category type display on each post, place the following code wherever you want it to appear in the post. Alternatively, and as I have done, paste it into `layouts/post.html`.

```liquid
{% raw %}
<div class="post-categories">
 {% if post %}
   {% assign categories = post.categories %}
 {% else %}
   {% assign categories = page.categories %}
 {% endif %}
 {% for category in categories %}
 <p>Post Categories: <a href="{{site.baseurl}}/{{category|slugize}}">{{category}}</a></p>
 {% unless forloop.last %}&nbsp;{% endunless %}
 {% endfor %}
</div>
{% endraw %}
```

16th October 2020
