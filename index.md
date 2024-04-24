---
#
# By default, content added below the "---" mark will appear in the home page
# between the top bar and the list of recent posts.
# To change the home page layout, edit the _layouts/home.html file.
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
#
layout: home
---


### [GreenForecast.au](http://greenforecast.au)
7-Day Outlook of Renewable Electricity and Power Price in the National Electricity Market
- [Introduction](/greenforecast)

### [Healthcare needs trustworthy LLMs: Deterministic Quoting can help](/deterministic-quoting)

### [Front Path Piano](/front-path-piano)

--- 

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <!-- {{ post.excerpt }} -->
    </li>
  {% endfor %}
</ul>

pages:

<ul>
  {% for a_page in site.pages %}
    <li>
      <a href="{{ a_page.url }}">{{ a_page.title }}</a>
      <!-- {{ a_page.excerpt }} -->
    </li>
  {% endfor %}
</ul>

...