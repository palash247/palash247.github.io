---
layout: page
title: About
permalink: /about/
---

This is the about page. You can edit this file to add information about yourself or your blog.

## About the Author

{{ site.author.name }} is the author of this blog. {{ site.author.bio }}

Feel free to connect with me on social media:

{% if site.social.twitter %}
- [X](https://x.com/{{ site.social.x }})
{% endif %}
{% if site.social.github %}
- [GitHub](https://github.com/{{ site.social.github }})
{% endif %}
{% if site.social.linkedin %}
- [LinkedIn](https://www.linkedin.com/in/{{ site.social.linkedin }})
{% endif %}

