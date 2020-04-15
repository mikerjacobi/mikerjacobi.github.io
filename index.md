---
---
I'm a learner and a communicator. 
I believe that dedicated routine is the best tool we have to accomplish our goals. 
I try to be process oriented in what I do, and casual in how I do it. 
I write code for fun and professionally. 
I'm a fan of jogging while listening to audio books/podcasts because it's so efficient. 
I find an outlet in writing and gaming.

<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>

