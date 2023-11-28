---
---

<h2> About </h2>

I'm a learner, communicator, and doer. 
Flexible routine is the best tool we have for accomplishing goals. 
I write code for fun and work, and I like running to audio books.

<h2> Posts </h2>

<h3><a href="https://docs.google.com/document/d/e/2PACX-1vQaOh3ttV9X9lHhuJnQybO4XQKtDo6jz8aQRSmDmzMRwVBX_JQO9P8QlkokypmHOgfhHHQwYM8G6a92/pub">Blastro</a></h3>
Blastro is a top-down 2D space shooter I made in Godot. 

{% for post in site.posts %}
  <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
  {{ post.excerpt }}
{% endfor %}
