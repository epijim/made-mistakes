---
layout: work
permalink: /plots/
title: "Gallery of my posts"
short-title: "Gallery of my posts"
headline: "Gallery of my posts"
description: "Gallery of plots from my previous posts."
modified: 2014-01-06
image: 
  thumb: jimmy_logo.png
  homepage: jimmy_logo.png
category: work
homepage: true
tags: [PaperFaces, Paper by 53, iPad art, portrait, illustration]
---

PaperFaces is an [illustration project]({{ site.url }}/articles/paperfaces-ipad-portrait-project/) by designer Michael Rose --- hey that's me! Each day I draw the face of a stranger using an iPad, a stylus, and the fabulous sketching app *Paper by 53*. 

Curious how I use Paper to draw these? Check out my set of [Mastering Paper by 53 Guides]({{ site.url }}/mastering-paper/).

<div markdown="0" class="center-block"><a href="{{ site.url }}/portraits/" class="btn">Order a PaperFaces Portrait</a></div>

<ul class="oversized-recent-grid">
{% for post in site.categories.articles %}
	<li><a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}">
		<img class="load" src="{{ site.url }}/images/preload.gif" data-original="{{ site.url }}/images/{{ post.image.thumb }}" alt="" width="106" height="106">
		<noscript><img src="{{ site.url }}/images/{{ post.image.thumb }}" alt="" width="106" height="106"></noscript>
	</a></li>
{% endfor %}
</ul>