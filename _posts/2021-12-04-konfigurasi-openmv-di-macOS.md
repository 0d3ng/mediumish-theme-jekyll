---
layout: post title:  "Konfigurasi OpenMV di MacOS"
author: odeng categories: [OpenMV]
tags: [openmv, micropython]
image: assets/images/2021/12/03.jpg description: "My review of Inception movie. Acting, plot and something else in this short
description."
featured: true hidden: true rating: 0
---

Bismillah,  
Hah, sampai lupa punya blog. Hari ini saya ada perangkat baru namanya OpenMV, yang mana perangkat tersebut merupakan
sebuah microprocessor yang sudah dibekali untuk kebutuhan computer vision. Sebenarnya mirip dengan arduino dan
sejenisnya tetapi memang fungsi diperluas include modul kamera. Untuk lebih jelasnya silakan mengunjungi di website
resminya di [sini](https://openmv.io/collections/cams/products/openmv-cam-h7-r2).
Ada beberapa bagian yang akan saya tulis seperti di bawah ini

* [Download OpenMV IDE](#Konfigurasi-Spring-Boot)
* [Install libusb](#Install-libusb)
* [Hello world](#Hello-world)
* [Kesimpulan](#Kesimpulan)
* [Referensi](#Referensi)<figure class="wp-block-image">

#### Download OpenMV IDE {#Download-OpenMV-IDE}

OpenMV datang tidak hanya hardware tetapi mereka juga menawarkan dengan kode editor yang bisa kita gunakan secara
gratis, OpenMV bisa diimplementasikan menggunakan C++ dan Python. Langkah awal yang bisa kita lakukan yaitu dengan
download di halaman [ini](https://openmv.io/pages/download), selanjutnya silakan lakukan installasi seperti pada
software pada umumnya di MacOS. File hasil download berukuran kurang lebih 170Mb, versi terakhir yang saya gunakan
adalah v2.8.1.

<div class="wp-block-image">
  <figure class="aligncenter"><img src="/assets/images/2021/12/01.png" alt="" class="wp-image-140" />
    <figcaption>OpenMV IDE</figcaption></figure>
</div>

Dari gambar di atas terdapat 2 jendela yaitu kiri dan kanan, kiri tempat kita untuk mengetik kode program sedangkan bagian
kanan adalah menampilkan gambar dan statistik dari gambar tersebut.

#### Install libusb {#Install-libusb}

OpenMV tidak bisa lakukan sebelum melakukan installasi lib-usb, library ini digunakan untuk komunikasi OpenMV
menggunakan USB pada laptop kita. Beberapa perintah yang bisa digunakan adalah sebagai beikut, bisa menggunakan MacPorts
atau HomeBrew. Untuk MacPort menggunakan perintah di bawah ini
<pre class="wp-block-code"><code>
sudo port install libusb py-pip
sudo pip install pyusb
</code></pre>
Sedangkan untuk perintah brew bisa paste 2 baris perintah di bawah ini
<pre class="wp-block-code">
<code>
sudo brew install libusb python
sudo pip install pyusb
</code>
</pre>
Setelah kedua perintah di atas berhasil dijalankan, selanjutnya hubungkan OpenMV pada MacOS Anda. Saya menggunakan
MacBook Pro mid 2012 dengan sistem operasi Mojave bisa berjalan dengan normal dan tidak terjadi masalah ketika melakukan
konfigurasi ini.

<blockquote class="wp-block-quote">
  <p>
    Kalau misalkan sudah install python, nggak perlu install lagi nggak masalah tetapi isntall libusb saja.
  </p>
</blockquote>

#### Hello world {#Hello-world}

Setelah OpenMV editor telah dipasang pada MacBook dan depedency juga sudah diinstall dengan, kemudian silakan hubungkan
OpenMV pada laptop menggunakan USB. Jika muncul untuk dilakukan ugrade firmware dan software pendukung silakan dilakukan
update terlebih dahulu.

<div class="wp-block-image">
  <figure class="aligncenter"><img src="/assets/images/2021/12/02.png" alt="" class="wp-image-140" />
    <figcaption>Hello world</figcaption></figure>
</div>

Contoh kode program untuk menampilkan gambar, sederhana sekali jika dilihat dari kode program yang digunakan.

<blockquote class="wp-block-quote">
  <p>
    Alhamdulillah, OpenMV menyediakan banyak sekali contoh kode program yang bisa kita gunakan dari yang sederhana sampai
dengan yang advance seperti face recognition. Contoh kode program tersebut dapat diakses melalui menu `File-Example-OpenMV`.
  </p>
</blockquote>

#### Kesimpulan {#Kesimpulan}

Dari tulisan sedikit di atas, jika Anda misalkan akan belajar computer vision dengan perangkat yang murah bisa menggunakan 
OpenMV karena sudah disediakan media input berupa kamera dan dokumentasi yang lengkap, serta contoh kode program untuk
mengawali menggunakan OpenMV.

#### Referensi {#Referensi}

* <https://openmv.io/collections/cams/products/openmv-cam-h7-r2>
* <https://openmv.io/pages/download>
* <https://docs.openmv.io/openmvcam/tutorial/software_setup.html>