---
layout: default
title: Archive
desc: Halaman Archive berisikan daftar postingan/tulisan di personal blog rifkifau yang dikelompokkan berdasarkan bulan dan tahun publikasi/uploadnya.
keywords: Archive, tulisan, postingan, bulan tahun, personal blog, rifkifau, rifki fauzi, WebGIS, Yogyakarta Indonesia, Kumpulan, Berbagi Pengalaman,  Cerita, Tutorial, cara, Foto Jepretan, Belajar
comments: false
---

<div class="post">
	<h2>Archive</h2>
	<ul>
	  {% for post in site.posts %}
	    {% unless post.next %}
	      <h3>{{ post.date | date: '%Y %b' }}</h3>
	    {% else %}
	      {% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
	      {% capture nyear %}{{ post.next.date | date: '%Y %b' }}{% endcapture %}
	      {% if year != nyear %}
	        <h3>{{ post.date | date: '%Y %b' }}</h3>
	      {% endif %}
	    {% endunless %}

	    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
	  {% endfor %}
	</ul>
</div>
