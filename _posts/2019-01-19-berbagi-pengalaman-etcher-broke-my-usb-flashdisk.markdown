---
layout: post
title:  "#BerbagiPengalaman-2: Etcher Broke my USB Flashdisk (?)"
date:   2019-01-19
tags:   [ Berbagi, Pengalaman, Software, Hardware ]
---
<p class="intro"><span class="dropcap">S</span>ore itu, sekitar habis Asar, langit Yogyakarta tampak gelap. Suara rintik hujan mulai terdengar dari dalam rumah. Ya, cukup syahdulah kalau mau ngegalau-galau ria. Tapi untungnya waktu itu tidak Ane lakukan.
</p>
<p>
Kunyalakan laptop yang sudah berada tepat di depanku. Dan Ente tau apa yang akan Ane lakukan? Yap, tepat, nonton drakor. Wkwk.
</p>
<p>
Rencananya sih waktu itu mau install Ubuntu 18.04 di laptop lawas yang emang sudah benar-benar lawas. Seperti proses install OS biasanya, setelah installer Ubuntu Desktop dan flashdisk siap, buka dulu tutorial instalasinya di Youtube. Yaa, walaupun sebenarnya instalasinya kurang lebih juga cuma next-next aja. Tapi nggak afdol rasanya kalau belum buka tutorial. Huehehe.
</p>
<p>
Nah, dari video tutorial yang Ane tonton tersebut, ada satu hal yang jujur  belum pernah Ane tau sebelumnya. Sebagai netizen yang biasa menggunakan Rufus untuk membuat bootable USB flashdisk, Ane kaget ketika di video tersebut yang dipakai adalah Etcher. Ya nama softwarenya Etcher, sebuah project opensource buatan balena. Ini nih linknya:
</p>
![berbagi pengalaman - etcher broke my usb - download dan install](https://user-images.githubusercontent.com/24805357/51428033-6c739480-1c31-11e9-906e-474c82628cc0.jpg)
<p>
Mulailah timbul ketertarikan untuk mencoba software tersebut. Ukuran file installernya nyaris 70 MB waktu itu (versi 1.4.9). Memang jauh sih kalau dibandingkan dengan Rufus yang hanya sekitar 1 MB (versi 3.4.1430). Blablabla, sampai akhirnya Etcher pun terinstall di laptop.
</p>
<p>
Kucolok flashdisk 16 GB ke laptop, lalu langsung Ane bikin bootable USB flashdisk Ubuntu dengan memanfaatkan Etcher. Hmmm…hmmmm…hmmmm… (nada Nissa Sabyan), beberapa menit kemudian proses selesai. Dan hasilnya adalah: “Flash Complete!, 1 Failed device”. Loh kok gagal?
</p>
<p>
Ane cek kemudian isi flashdisknya (emang nggak percayaan orangnya, wkwk), ternyata beneran gagal, karena isinya tidak seperti seharusnya. Ane delete dan format flashdisk, sampai kemudian tersadar total kapasitasnya berubah jadi sekitar 2 MB saja. Panik dong. Iya pasti panik dong. Masa’ nggak.
</p>
<p>
Anehnya, entah kenapa waktu itu yang terlintas dipikiran bukannya cari cara/solusi buat memperbaiki flashdisk, eh tapi malah mencoba pakai flashdisk lainnya (yang ukurannya 4 GB). Sampai nulis tulisan inipun (yang sudah dilain hari dengan kejadian) Ane masih mikir sebenarnya. Iya ya, kenapa malah nyoba lagi pakai flashdisk lain. Rodho koclok emang (bahasa jawa).
</p>
<p>
Tapi sepertinya sih waktu itu mikirnya flashdisk itu (yang 16 GB) mungkin rusak. Karena emang sudah cukup lama nggak Ane pakai.
</p>
<p>
Blablabla.
</p>
<p>
Hasil yang sama juga terjadi setelah mencoba dengan flashdisk lain (yang 4 GB).
</p>
<p>
Tambah panik dong. Sampai berungkali diformat ukurannya tetap jauh lebih kecil dari yang semestinya (hmmm, ukuran kapasitas maksudnya). Mulailah ‘menghujat’ Etcher. ****** ******, ****, ******…
</p>
<p>
Tapi, apakah benar Etcher ini software yang merusak flashdisk? Googling-googling pun dilakukan, sampai akhirnya nemu cara ini di askubuntu.com:
</p>
![berbagi pengalaman - etcher broke my usb - solusi](https://user-images.githubusercontent.com/24805357/51428048-ad6ba900-1c31-11e9-9ba6-2c0d05746252.jpg)
<p>
Setelah mencoba cara diatas, Alhamdulillah flashdisk kembali normal.
</p>
<p>
Lega rasanya.
</p>
<p>
Akhirnya memutuskan kembali ke Rufus untuk membuat bootable flashdisk.
</p>
<p>
Tapi kemudian kembali lagi ke Etcher untuk menunjukkan bukti. Hehe. Soalnya pas tragedi itu belum terpikir bikin tulisan ini dan belum sempat screenshot.
</p>
<p>
Dan berikut adalah bukti dari cerita diatas:
</p>

![berbagi pengalaman - etcher broke my usb - tampilan awal](https://user-images.githubusercontent.com/24805357/51428119-b5781880-1c32-11e9-98c0-8591037ee52b.jpg) *Ini adalah tampilan awal dari software Etcher.*

![berbagi pengalaman - etcher broke my usb - flashing](https://user-images.githubusercontent.com/24805357/51428122-b741dc00-1c32-11e9-95df-d5fc44874862.jpg) *Proses pembuatan bootable flashdisk tahap pertama: flashing.*

![berbagi pengalaman - etcher broke my usb - validating](https://user-images.githubusercontent.com/24805357/51428120-b610af00-1c32-11e9-97b0-7717e09c173c.jpg) *Proses pembuatan bootable flashdisk tahap kedua: validating.*

![berbagi pengalaman - etcher broke my usb - flash complete failed device](https://user-images.githubusercontent.com/24805357/51428121-b6a94580-1c32-11e9-9ba1-8a0557f55131.jpg) *Proses complete tapi failed.*

<center>![berbagi pengalaman - etcher broke my usb - storage berkurang](https://user-images.githubusercontent.com/24805357/51428118-b5781880-1c32-11e9-9fb8-3064f1d6f882.jpg) </center>*Setelah dicek ukuran kapasitas flashdisk tinggal segini nih.*

![berbagi pengalaman - etcher broke my usb - kembali normal](https://user-images.githubusercontent.com/24805357/51428123-b741dc00-1c32-11e9-827b-b93f8cc1e2fb.jpg) *Nah, untungnya masih bisa kembali normal.*
## Tambahan

<p>
Googling-googling tidak hanya membawa Ane pada solusi mengembalikan kapasitas flashdisk, tapi juga pada tutorial membuat bootable flashdisk tanpa software. Bisa ya? (haha gaptek emang). Dan beberapa langkah awal membuat bootable flashdisk tanpa software adalah dengan cara yang sama seperti mengembalikan kapasitas flashdisk. (Kalau bingung maksudnya silakan ulang-ulang saja membaca paragraf ini).
</p>
<p>
Setelah mencermati ulang video tutorial, ternyata didalam video tersebut tidak diperlihatkan keberhasilannya membuat bootable flashdisk menggunakan Etcher. Sial emang. Ini nih potongan videonya kalau belum percaya:
</p>
