---
layout: post
title: Jekyll Archives
date: 2020-10-24
categories: jekyll
tags: [archives, liquid, tags]
excerpt:
  Using tags to create an archive page.
---

<del>In this article we learn how to create an archive page for your site using tags.</del><ins>This article has been superseded, I would refer you instead to this article, [Archive Page](/2021/03/03/archive-page/)</ins>.

<!--more-->

{% include toc.html %}

## Install the Gem
Install the gem jekyll-archives;

```ruby
gem install jekyll-archives
```

## Edit Configuration Files
Edit _config.yml to include the lines;

```yaml
plugins:
  - jekyll-archives
```

(Make sure the text is all lower case).

Edit the Gemfile to include the line

```ruby
gem "jekyll-archives", "~> 2.2.1"
```

## Configuration Options
The default configuration is

```yaml
jekyll-archives:
  enabled: []
  layout: archive
  permalinks:
    year: '/:year/'
    month: '/:year/:month/'
    day: '/:year/:month/:day/'
    tag: '/tag/:name/'
    category: '/category/:name/'
```

For advice on alternatives, please refer to [https://github.com/jekyll/jekyll-archives/blob/master/docs/configuration.md](https://github.com/jekyll/jekyll-archives/blob/master/docs/configuration.md).

## Layouts
For layout examples refer to [https://github.com/jekyll/jekyll-archives/blob/master/docs/layouts.md](https://github.com/jekyll/jekyll-archives/blob/master/docs/layouts.md).

## Archive Page
I have created archive.html, a page saved to the project root and which lists each of the tags used on my site. An example of the coding is presented below; this one will display a list of the posts that have been tagged "landscapes".

```liquid
---
layout: page
permalink: /archive/
---
<h1>Photography</h1>
  <h2>Landscapes</h2>
    <ul>
      {% raw %} {% for post in site.tags.landscapes %}
        <li>
          {{ post.date | date: "%B %d, %Y" }}: <a href="{{ post.url }}">{{ post.title }}</a>
        </li>
      {% endfor %} {% endraw %}
    </ul>
```

As an example of what is produced, take a look at my completed [archive page](/archive/).

The one downside is that you have to manually update the archive page whenever a new tag is used. Automating the process is something I will have to investigate at a later date.

24th October 2020
