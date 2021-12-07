---
layout: post 
title:  "Face Detection di OpenMV"
author: odeng 
categories: [OpenMV]
tags: [openmv, micropython]
image: assets/images/2021/12/06.png 
featured: true
---

Bismillah,  
Saya akan melanjutnya cerita dari postingan [sebelumnya](2021-12-05-konfigurasi-openmv-di-macOS.md) yaitu masih kaitannya dengan perangkat OpenMV, 
seperti yang telah saya sebutkan bahwa OpenMV telah menyediakan banyak sekali contoh kode program yang bisa kita manfaatkan.
Sebagai contoh adalah untuk face detection yaitu untuk melakukan deteksi wajah menggunakan metode yang cukup terkenal yaitu **Haar Cascade**.
Agar alur tulisan saya tersusun dengan rapih saya akan buat point-point sebagai berikut

* [Intro](#Intro)
* [Penjelasan Kode Program](#Penjelasan-Kode-Program)
* [Run Code](#Run-Code)
* [Kesimpulan](#Kesimpulan)
* [Referensi](#Referensi)<figure class="wp-block-image">

#### Intro {#Intro}

OpenMV IDE layaknya Arduino IDE, yang mana sudah menyediakan contoh program yang siap untuk digunakan baik untuk kebutuhan 
computer vision ataupun mengontrol komponen atau perangkat baik sensor serta aktuator yang menempel pada OpenMV.
Unfortunately, ketika kita mau memanfaatkan perangkat/hardware kita harus order dulu yang satu platform dengan OpenMV dan
apesnya harganya tidak murah, serta import juga.

Ya sudah kita mencoba saja yang tidak perlu menggunakan perangkat/komponen, pada tulisan ini saya akan mencoba untuk
menunjukkan face detection menggunakan perangkat OpenMV. Sebelum melakukan ini, pastikan terlebih dahulu sudah terinstall
OpenMV IDE dan sudah install driver atau depedensi yang dibutuhkan.

Silakan buka OpenMV IDE dari laptop/komputer Anda, dari menu `File - Examples - OpenMV - Face Detection - face-detection.py`.
Atau untuk lebih jelasnya dapat melihat pada gambar di bawah ini

<div class="wp-block-image">
  <figure class="aligncenter"><img src="/assets/images/2021/12/04.png" alt="" class="wp-image-140" />
    <figcaption>Open Face Detection</figcaption></figure>
</div>

Setelah langkah di atas dilakukan seharusnya pada jendela editor akan terbuka kode program untuk face detection.

#### Penjelasan Kode Program {#Penjelasan-Kode-Program}

Jika lihat dari kode program yang terbuka pada OpenMV sepertinya tidak terlalu banyak dan terlalu sulit untuk dimengerti,
saya akan mencoba untuk menjelaskan kode program untuk masing-masing fungsinya.
<pre class="wp-block-code">
<code>
import sensor, time, image

# Reset sensor
sensor.reset()

# Sensor settings
sensor.set_contrast(3)
sensor.set_gainceiling(16)
# HQVGA and GRAYSCALE are the best for face tracking.
sensor.set_framesize(sensor.HQVGA)
sensor.set_pixformat(sensor.GRAYSCALE)

# Load Haar Cascade
# By default this will use all stages, lower satges is faster but less accurate.
face_cascade = image.HaarCascade("frontalface", stages=25)
print(face_cascade)

# FPS clock
clock = time.clock()
</code>
</pre>

Kode program yang paling atas sudah sangat jelas, yaitu untuk memanfaatkan class yang telah disediakan oleh OpenMV yaitu
`sensor, time, dan image` masing-masing karena kita memanfaatkan kamera, class time untuk kebutuhan fps, dan image karena
kita ingin meload model dari Haar Cascasde.

Dilanjutnya dengan melaukan konfigurasi sensor kamera yaitu mengatur tingkat kecerahan, mengatur ukuran frame menjadi 240x160, dan
mengubah gambar menjadi abu-abu. Perlu diperhatikan bahwa khusus ukuran frame dan jenis gambar sangat penting karena akan 
mempengaruhi waktu pemrosesan selanjutnya. Semakin besar ukuran frame dan semakin padat tingkat kerapatan pada sebuah citra
tentunya akan semakin lama waktu yang dibutuhkan untuk melakukan pengolahan dan fps akan drop.

Baris yang selanjutnya digunakan untuk meload model HaarCascade agar nanti bisa mengenali wajah berdasarkan fitur yang telah
disedikan oleh HaarCascade itu sendiri.

<pre class="wp-block-code">
<code>
while (True):
    clock.tick()

    # Capture snapshot
    img = sensor.snapshot()

    # Find objects.
    # Note: Lower scale factor scales-down the image more and detects smaller objects.
    # Higher threshold results in a higher detection rate, with more false positives.
    objects = img.find_features(face_cascade, threshold=0.75, scale_factor=1.25)

    # Draw objects
    for r in objects:
        img.draw_rectangle(r)

    # Print FPS.
    # Note: Actual FPS is higher, streaming the FB makes it slower.
    print(clock.fps())
</code>
</pre>

Beberapa baris terakhir di atas akan melakukan perulangan terus-menerus dengan mengambil waktu saat ini, mengambil gambar,
serta dideteksi dengan cara mencari fitur apakah termasuk gambar wajah. Ketika dideteksi objek wajah maka wajah tersebut akan
ditampilkan. Beberapa paramter yang perlu disesuaikan pada waktu pencarian fitur untuk mengoptimalkan proses deteksi wajah misalkan
threshold ataupun scale_factor, semakin rendah nilai scale factor mengakibatkan objek yang dideteksi akan semakin kecil
sedangkan semkin tinggi tingkat threshold mengakibatkan detection rate yang lebih tinggi.

#### Run Code {#Run-Code}

Hasil dari kode program di atas bisa dijalankan dengan klik tombol segitiga di pojok kiri bawah, normalny berwarna hijau
sehingga tombol tersebut berwarna abu-abu berarti OpenMV belum terhubung ke laptop/komputer Anda. Jika dijalankan hasilnya
dapat dilihat seperti pada gambar di bawah ini

<div class="wp-block-image">
  <figure class="aligncenter"><img src="/assets/images/2021/12/05.png" alt="" class="wp-image-140" />
    <figcaption>Face Detected</figcaption></figure>
</div>

Dari gambar di atas terlihat citra gambar akan tampil abu-abu dan ketika wajah terdeteksi akan ditandai dengan bentuk square
pada bagian wajah pada panel sebelah kanan OpenMV IDE Anda.

#### Kesimpulan {#Kesimpulan}

Dari tulisan sedikit di atas, semoga sudah ada gambaran ketika kita inginkan memanfaatkan kode program yang telah disediakan
oleh OpenMV. Contoh-contoh yang lain kurang lebih sama pemanfaatannya, selanjutnya kita bisa memodifikasi sesuai kebutuhan
yang kita inginkan. Selanjutnya timbul pertanyaan, gimana jika kita inginkan memanfaatkan model yang telah kita buat? 
Pertanyaan tersebut menjadi pekerjaan rumah bersama ya. :)

#### Referensi {#Referensi}

* <https://docs.openmv.io/library/omv.sensor.html#module-sensor>
* <https://docs.openmv.io/library/omv.image.html>