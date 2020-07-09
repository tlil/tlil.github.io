---
layout: default
section: blog
excerpt: "Latest blog posts"
footer_nav: true
---
<div class="home">
    <div class="post-list">
    {% for post in site.posts limit: 5 %}
    <section>
        <h1><a class="post-link" href="{% if post.stuburl %}{{ post.stuburl }}{% else %}{{ post.url | prepend: site.baseurl }}{% endif %}">{{ post.title }}</a></h1>
        <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
        <article class="post-content excerpt">
            {{ post.excerpt }}
            <a class="excerpt-link" href="{% if post.stuburl %}{{ post.stuburl }}{% else %}{{ post.url | prepend: site.baseurl }}{% endif %}">Read more ...</a>
        </article>
    </section>
    {% endfor %}
    </div>
</div>
