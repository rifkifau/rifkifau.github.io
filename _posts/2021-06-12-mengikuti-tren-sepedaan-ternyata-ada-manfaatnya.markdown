---
layout: post
title:  "Mengikuti Tren Sepedaan, Ternyata Ada Manfaatnya"
date:   2021-06-12
tags:   [ Tren, Sepeda, Manfaat, Visualisasi, Data, Track ]
---
<p class="intro"><span class="dropcap">S</span>ebelum genap seminggu di Jakarta* adalah target yang mesti Ane kejar untuk menyelesaikan tulisan ini. Kalau tidak dipaksa emang terbawa suasana males terus. Lha wong ini aja pelarian karena bingung dan males mau ngisi apa lagi di blog <a href="https://spasialkan.com" title="spasialkan.com" target="_blank">spasialkan.com</a>, di <a href="https://www.instagram.com/webgisindonesia" title="Instagram WebGIS Indonesia" target="_blank">Instagram WebGIS Indonesia</a>, di <a href="https://www.youtube.com/marispasialkan" title="channel youtube Mari Spasialkan" target="_blank">channel youtube Mari Spasialkan</a>, dan beberapa media lainnya. Kebanyakan media tapi <em>update</em> <em>mood-mood</em>an.
</p>
<sup>
*Ane emang baru diminggu awal Juni ini kembali ke Jakarta setelah WFH di kampung halaman selama hampir dua bulan lamanya.
</sup>
<hr>
<p>
Sekitar pertengahan bulan Agustus 2020 lalu Ane memutuskan untuk membeli sepeda lipat. Sempat menjadi bahan omongan teman-teman karena warnanya yang kuning ngejreng. Bagi yang kepo, fotonya Ane lampirkan di bawah ini yak.
</p>
![sepeda-ecosmo-9-rifkifau](../../images/manfaat-sepedaan/sepeda-ecosmo-9-rifkifau.jpg)
<sup>
Gimana menurut kalian, keren nggak? Untung nggak ada Ane di dalam foto, kalau ada bisa basah dah. (lho eh, haha).
</sup>
<p>
Disamping karena tren, sebenarnya sudah cukup lama juga kepengen beli sepeda. Awalnya tertarik karena merasa bakal membantu mobilitas dari kost ke tempat kerja. Kalau dihitung-hitung nih, secara jarak tergolong nanggung. Ngojol kok lumayan dekat, tapi kalau jauh kok jalan. Eh, kalau jalan kok jauh maksudnya.
</p>
<p>
Selain beberapa kali Ane pakai untuk pergi-pulang kerja, diperiode awal beli, semangat tuh sepedaan muter-muter. Seminggu bisa dua kali. Tapi namanya juga manusia ya (haha), makin lama makin males dong.
</p>
<p>
Terlepas dari semua itu, fyi, sepedaan yang Ane lakukan bukanlah sepedaan pada umumnya. Ya, karena Ane sepedaan sendiri terus. Temenin dong. Hihi, meskipun itu ada benernya, namun bukan itu maksudnya. Mengapa disebut nggak umum (tidak berarti cuma Ane sendiri yang melakukan yak), karena Ane <em>record</em> rute sepedaan menggunakan aplikasi di <em>smartphone</em>. Aplikasi yang Ane pakai namanya Strava. Alasan memilih Strava cukup simpel, karena sepertinya ada teman yang menggunakan juga. Jadi, sangat dimungkinkan banyak aplikasi serupa yang lebih <em>recommended</em>.
</p>
<p>
Dari Strava ini, kalian bisa <em>download</em> rute sepedaan (lari, jalan, renang, dan beberapa aktivitas lain juga sebenarnya) dalam format <em>file</em> *.gpx. Terkait cara mengunduhnya, kalian bisa lakukan dengan login dulu ke strava[.]com, lalu masuk ke halaman "Activities".
</p>
<p>
Nah, mulai dari sinilah sebenarnya inti tulisan ini. Memanfaatkan data hasil <em>track</em> sepedaan menjadi sesuatu.
</p>
<p>
Sebelum masuk kepembahasan mengenai visualisasi seperti apa yang bisa kita buat dengan mengolah <em>file</em> yang berformat *.gpx tadi. Pertama perlu Ane jelaskan dulu <em>software</em> yang bisa digunakan untuk pengolahan awal. Di sini Ane menggunakan QGIS.
</p>
<p>
Kalau kalian buka data *.gpx <em>tracks</em> Strava akan muncul kurang lebih 5 <em>layer</em> sebagaimana gambar di bawah, dan yang bisa kalian manfaatkan tentu yang ada <em>features</em>nya. Lebih spesifik, yang Ane pakai adalah data tracks saja. Meskipun data atribut <em>layer</em> tracks kosong semua kecuali kolom ‘name’, tetap aman karena Ane hanya butuh geometrinya. Bagi kalian yang butuh <em>attribute data</em> lebih lengkap bisa cek pada <em>layer</em> track_points. Di situ terdapat informasi elevasi dan waktu juga.
</p>
![isi-file-gpx-dari-strava_tracks-dan-routes](../../images/manfaat-sepedaan/isi-file-gpx-dari-strava_tracks-dan-routes.jpg)
<p>
Dari data track_points, kalian sebenarnya bisa belajar (bagi yang belum tahu yak) menghitung sudut perubahan tiap titik. Caranya menggunakan QGIS Expression, ya mirip-mirip dengan tulisan Ane di <a href="https://spasialkan.com" title="spasialkan.com" target="_blank">spasialkan.com</a>, yang sampe Ane buat series jadi empat tulisan. Hehe. Ke sini dulu yak kalau mau baca-baca: <a href="https://spasialkan.com/category/qgis-expressions" title="Series QGIS Expression Spasialkan.COM" target="_blank">Series QGIS Expression Spasialkan.COM</a>.
</p>
<p>
Seperti ini kurang lebih expression-nya:
</p>
<code>
degrees( azimuth( start_point( $geometry ), end_point( geometry( get_feature( 'nama-layer', 'track_seg_point_id',  "track_seg_point_id"+1  )))))
</code>
<hr>
<p>
Okay, lanjut terkait visualisasi data <em>track</em>nya. Pertama yang Ane lakukan adalah meng<em>export</em> data <em>track</em> menjadi format *.geojson. Setelah itu, baru kemudian mengedit data geojson <em>track</em> tersebut. Apa aja bentuk edit yang dilakukan? (i) mengapus beberapa bagian awal dan akhir dari <em>track</em>, ya biar nggak begitu ketahuan posisi pasti kost-kostan Ane, (ii) menghapus beberapa <em>track</em> bagian tujuan sepedaan, karena ada yang tujuannya adalah kost teman, jadi ada baiknya dihilangkan biar tidak banyak orang tau, (iii) menghapus, menambah dan menggeser <em>vertex</em>/<em>node</em>, terutama di beberapa area yang <em>track</em>nya tidak terakam atau terekam awut-awutan (bisa karena pas sepedaan salah jalan, istirahat sejenak, atau lainnya), seperti ini nih maksudnya (kiri sebelum diedit; kanan setelah diedit):
</p>
![perbaikan-dan-edit-tracks](../../images/manfaat-sepedaan/perbaikan-dan-edit-tracks.jpg)
<p>
Sekilas info, total ada 11 <em>tracks</em> yang tersimpan diakun Strava Ane. Adapun jarak total yang terekam adalah 254.2 km, dengan <em>track</em> terpanjang adalah 28.1 km.
</p>
<p>
<em>Software</em> berikutnya yang Ane gunakan adalah Visual Studio Code dan Browser Chrome. Keduanya digunakan untuk membuat visualisasi dalam bentuk WebGIS dengan memanfaatkan <em>library</em> Javascript yang cukup populer. Yak, Leaflet JS.
</p>
<p>
Di sini tidak akan Ane bahas rinci terkait <em>script</em>nya seperti apa, tapi gambaran kasar saja mengenai struktur data dan <em>plugin</em> Leaflet yang digunakan. Dari 11 data <em>track</em> yang sudah berformat *.geojson, Ane ambil bagian “coordinates”, kemudian membuatnya menjadi array object. Oh ya, pada saat <em>export</em> data dari layer *.gpx menjadi *.geojson, opsi ‘Geometry type’nya Ane ganti ‘LineString’ sekaligus <em>uncheck</em> bagian ‘Include z-dimension’. Dengan menghilangkan z-dimension ini, maka isi “coordinates” dalam file geojson hanya [x, y] saja, bukan lagi [x, y, z]. Berikut adalah struktur dari array object rute sepeda yang Ane simpan dalam variable.
</p>
![array-of-object-data-track-sepedaan](../../images/manfaat-sepedaan/array-of-object-data-track-sepedaan.jpg)
<p>
Terdapat empat plugin LeafletJS yang Ane gunakan, berikut daftarnya:
  <ul>
    <li>Leaflet StyledLayerControl, digunakan untuk membuat <em>layer control</em> yang terdiri dari beberapa <em>group</em> (dalam konteks ini grup berdasarkan nama <em>track</em>),</li>
    <li>Leaflet Polyline SnakeAnim, digunakan untuk membuat animasi <em>track</em> menyerupai ular yang sedang merayap, karena itulah <em>layer</em> hasil animasinya Ane namakan “Slithering Snake”,</li>
    <li>Leaflet Ant Path, digunakan untuk membuat animasi <em>track</em> seperti jalur semut atau semut yang jalan berbaris gitu,</li>
    <li>Leaflet MovingMarker, digunakan untuk membuat animasi <em>marker</em> (anggap saja sepeda) yang bergerak sesuai/mengikuti <em>track</em>.</li>
  </ul>
</p>
<p>
Nah, terakhir, berikut adalah hasil akhir dari visualisasi <em>track</em> sepedaan Ane:
</p>
 <iframe src="https://rifkifau.github.io/visualisasi-animasi-track-sepeda" height="500px" width="100%" frameborder="0"></a></iframe>
<sub>
Entah penting atau tidak bagi kalian, btw misi merampungkan tulisan ini sebelum genap seminggu di Jakarta dinyatakan berhasil, berhasil, berhasil hore.
</sub>
