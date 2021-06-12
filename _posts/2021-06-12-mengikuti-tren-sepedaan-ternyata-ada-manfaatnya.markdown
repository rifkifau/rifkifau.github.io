---
layout: post
title:  "Mengikuti Tren Sepedaan, Ternyata Ada Manfaatnya"
date:   2021-06-12
tags:   [ Tren, Sepeda, Manfaat, Visualisasi, Data, Track ]
---
<p class="intro"><span class="dropcap">S</span>ebelum genap seminggu di Jakarta* adalah target yang mesti Ane kejar untuk menyelesaikan tulisan ini. Kalau tidak dipaksa emang terbawa suasana males terus. Lha wong ini aja pelarian karena bingung dan males mau ngisi apa lagi di blog spasialkan.com, di Instagram WebGIS Indonesia, di channel youtube Mari Spasialkan, dan beberapa media lainnya. Kebanyakan media tapi update e mood-mood-an.
</p>

*Ane emang baru diminggu awal Juni ini kembali ke Jakarta setelah WFH di kampung halaman selama hampir dua bulan lamanya.

-----
Sekitar pertengahan bulan Agustus 2020 lalu Ane memutuskan untuk membeli sepeda lipat. Sempat menjadi bahan omongan temen karena warnanya yang kuning. Fotonya aku lampirkan dibawah yak.

![sepeda-ecosmo-9-rifkifau](../../images/manfaat-sepedaan/sepeda-ecosmo-9-rifkifau.jpg)

Selain karena tren, sebenarnya sudah cukup lama juga kepengen beli sepeda. Awalnya tertarik karena merasa bakal membantu mobilitas dari kost ke tempat kerja. Kalau dihitung-hitung nih, secara jarak tergolong nanggung. Ngojol kok lumayan dekat, tapi kalau jauh kok jalan. Eh kalau jalan kok jauh maksudnya.

Selain beberapa kali Ane pakai pergi-pulang kerja, periode awal beli semangat tuh sepedaan muter-muter. Seminggu bisa dua kali. Tapi namanya juga manusia ya (haha), makin lama makin males dong.

Terlepas dari semua itu, sepedaan yang Ane lakukan bukanlah sepedaan pada umumnya. Ya, karena Ane sepedaan sendiri terus. Temenin dong. Hihi, meskipun itu ada benernya, namun bukan itu maksudnya. Kenapa Ane sebut nggak umum (tidak berarti cuma aku sendiri yang melakukan yak), karena aku record rute sepedaanku menggunakan aplikasi di smartphone. Aplikasi yang aku pakai namanya Strava. Mengapa pakai itu, simple, karena sepertinya ada teman yang menggunakan juga. Jadi, sangat dimungkinkan banyak yang lebih recommended yak.

Dari Strava ini, kalian bisa download rute sepedaan (lari, jalan, renang, dan beberapa aktivitas lain juga sebenarnya) dalam format file *.gpx. Terkait cara mengunduhnya, kalian bisa lakukan dengan login dulu ke www.strava.com.

Nah dari sinilah sebenarnya inti tulisan ini. Memanfaatkan data hasil track sepedaan menjadi sesuatu.
Sebelum masuk kepembahasan mengenai visualisasi seperti apa yang bisa kita buat dengan mengolah file yang berformat *.gpx tadi. Pertama perlu Ane jelaskan dulu software yang bisa digunakan untuk pengolahan awal. Di sini Ane menggunakan QGIS.

Kalau kalian buka data *.gpx-nya akan muncul kurang lebih 5 layer berikut, dan yang bisa kalian manfaatkan tentu yang ada featuresnya. Lebih spesifik, yang Ane pakai adalah data tracks saja. Meskipun data atributnya kosong semua kecuali kolom ‘name’ tetap aman karena Ane hanya butuh geometrinya. Bagi kalian yang butuh attribute data lebih lengkap bisa cek pada layer track_points. Di situ terdapat informasi elevasi dan waktu juga.

![isi-file-gpx-dari-strava_tracks-dan-routes](../../images/manfaat-sepedaan/isi-file-gpx-dari-strava_tracks-dan-routes.jpg)

Dari data track_points, kalian sebenarnya juga bisa belajar (bagi yang belum tahu yak) menghitung sudut perubahan tiap titik. Caranya menggunakan QGIS Expression, ya mirip-mirip dengan tulisan Ane di Spasialkan.Com, yang sampe Ane buat series jadi empat tulisan. Hehe.

Seperti ini kurang lebih expression-nya:

degrees(azimuth(start_point($geometry), end_point(geometry(get_feature('nama-layer', 'track_seg_point_id',  "track_seg_point_id"+1  )))))

---
Okay, lanjut terkait visualisasi data track-nya. Pertama yang Ane lakukan adalah mengexport data track menjadi format *.geojson. Baru kemudian mengedit data geojson track tersebut. Apa aja bentuk edit yang dilakukan? (i) mengapus beberapa bagian awal dan akhir dari track, ya biar nggak begitu ketahuan posisi pasti kost-kostan Ane, (ii) menghapus beberapa track bagian tujuan sepedaan, karena ada yang tujuannya adalah kost teman, jadi ada baiknya dihilangkan biar tidak banyak orang tau, (iii) menghapus, nenambah dan menggeser vertex/node, terutama di beberapa area yang tracknya tidak terakam atau terekam awut-awutan (bisa karena pas sepedaan salah jalan, istirahat sejenak, atau lainnya), seperti ini nih maksudnya:

![perbaikan-dan-edit-tracks](../../images/manfaat-sepedaan/perbaikan-dan-edit-tracks.png)

Total ada 11 tracks yang tersimpan diakun Strava Ane. Adapun jarak total yang terekam adalah 254.2 km, dengan track terpanjang adalah 28.1 km.

Software berikutnya yang Ane gunakan adalah Visual Studio Code dan Browser Chrome. Keduanya digunakan untuk membuat visualisasi dalam bentuk WebGIS dengan memanfaatkan library Javascript yang cukup popular. Yak, Leaflet JS.

Di sini tidak akan Ane bahas rinci terkait scriptnya seperti apa, tapi gambaran kasar saja mengenai struktur data dan plugin Leaflet yang digunakan. Dari 11 data track yang sudah berformat *.geojson, Ane ambil bagian “coordinates”, kemudian membuatnya menjadi array object. Oh ya, pada saat export data dari layer *.gpx menjadi *.geojson, opsi ‘Geometry type’nya Ane ganti ‘LineString’ sekaligus uncheck bagian ‘Include z-dimension’. Dengan menghilangkan z-dimension ini, maka isi “coordinates” dalam file geojson hanya [x,y] saja, bukan lagi [x, y, z]. Berikut adalah struktur dari array obyek rute sepeda yang Ane simpan dalam variable.

![array-of-object-data-track-sepedaan](../../images/array-of-object-data-track-sepedaan.jpg)

Terdapat empat plugin leaflet yang Ane gunakan, berikut daftarnya:
•	Leaflet StyledLayerControl, digunakan untuk membuat layer control yang terdiri dari beberapa group (dalam konteks ini grup berdasarkan nama track),
•	Leaflet Polyline SnakeAnim, digunakan untuk membuat animasi track menyerupai ular yang sedang merayap, karena itulah nama layer hasil animasinya Ane namakan “Slithering Snake”,
•	Leaflet Ant Path, digunakan untuk membuat animasi track seperti jalur semut atau semut yang jalan berbaris gitu,
•	Leaflet MovingMarker, digunakan untuk membuat animasi marker (anggap saja sepeda) yang bergerak sesuai/mengikuti track.

Nah, terakhir, berikut adalah hasil akhir dari visualisasi track sepedaan Ane:

