---
---

<h2> About </h2>

I'm a learner, communicator, and doer. 
Flexible routine is the best tool we have for accomplishing goals. 
I write code for fun and work, and I like running to audio books.

<h2> Posts </h2>

<h3><a href="https://docs.google.com/document/d/e/2PACX-1vRclLtq0B1IrL4J2FnUBwDKyXIrLEbtc5vXhHZhN9XE7BO0isGeGYluB4Jqdc4InFXxuYxUDpYNj2Y9/pub">3D Model Search</a></h3>
This post walks through quality tuning on a 3D model search system. 

<h3><a href="https://docs.google.com/document/d/e/2PACX-1vQaOh3ttV9X9lHhuJnQybO4XQKtDo6jz8aQRSmDmzMRwVBX_JQO9P8QlkokypmHOgfhHHQwYM8G6a92/pub">Blastro</a></h3>
Blastro is a top-down 2D space shooter I made in Godot. 

<h3><a href="https://docs.google.com/document/d/e/2PACX-1vRg6M_ai5aTALKyhL1eyOBewfaIXp-fawCRHlyM59c4KVpJdtYz4ToghrpJPrTE5WsVZvpXJVMdygIG/pub">Seattle Times GPT</a></h3>
Seattle Times GPT is an experiment with the OpenAI Assistants API. 

{% for post in site.posts %}
  <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
  {{ post.excerpt }}
{% endfor %}
