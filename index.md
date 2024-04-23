---
#
# By default, content added below the "---" mark will appear in the home page
# between the top bar and the list of recent posts.
# To change the home page layout, edit the _layouts/home.html file.
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
#
layout: home
---
text btwnn top bar abd recent posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

pages:

<ul>
  {% for a_page in site.pages %}
    <li>
      <a href="{{ a_page.url }}">{{ a_page.title }}</a>
    </li>
  {% endfor %}
</ul>

...