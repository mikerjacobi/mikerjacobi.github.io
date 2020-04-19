---
---

<h2> About </h2>

I'm a learner and a communicator. 
I believe that dedicated routine is the best tool available for accomplishing goals. 
I try to be process oriented in what I do, and flexible in how I do it. 
I write code for fun and professionally. 
I like to run while listening to audio books/podcasts, and I find an outlet in writing and gaming.

<h2> Posts </h2>

{% for post in site.posts %}
  <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
  {{ post.excerpt }}
{% endfor %}
