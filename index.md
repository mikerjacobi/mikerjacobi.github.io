---
---

I'm a learner, communicator, and doer. 
Flexible routine is the best tool we have for accomplishing goals. 
I write code for fun and work, and I like running to audio books.

{% for post in site.posts %}
  <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
  {{ post.excerpt }}
{% endfor %}
