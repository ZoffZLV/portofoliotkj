+++
author = "lee.so"
title = "Static Routing"
date = "2024-04-09"
description = "Lorem Ipsum Dolor Si Amet"
tags = [
    "markdown",
    "text",
]
weight = 10
+++

Static routing adalah mekanisme dimana seorang administrator jaringan menambahkan rute secara manual kedalam tabel routing pada setiap router, static routing sangat cocok diimplementasikan pada jaringan skala kecil, pada jaringan skala besar, jika tetap menggunakan static routing , maka akan sangat membuang waktu administrator jaringan untuk melakukan update table routing.

Mikrotik secara default akan menambahkan jalur routing secara otomatis ketika menambahkan IP Address  pada interface, lalu kenapa memerlukan static routing? Karena untuk menghubungkan perangkat network yang memilik IP segment (subnet) yang berbeda memerlukan sebuah perangkat yang mampu melakukan proses routing.

## Cara Konfigurasi static routing mikrotik
Untuk memudahkan teman-teman memahami konfigurasi static routing saya akan menggunakan topologi sedehana dengan menggunakan dua router.

## Topologi

![alt text](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgRt2Up0nbx00Hwr5ReU4DymG9gSOsXPVTdkNxrWpD47PrTRo-pkeM8hu8WQHRSoMewFLF2HmXhKyoLoYtblNyI4AO-TpdZFHxLfsqw_Ij6Ahss9DTdvpFfSKbahyphenhyphen02ebjMRBdK-qckjgY/s557/topologi.PNG "Topologi Static Routing")


Dari gambar diatas terdapat dua router (Mikrotik A dan Mikrotik B) yang saling terhubung menggunakan kabel LAN melalui ether5. Di ether2 pada Mikrotik A dan Mikrotik B terhubung dengan PC.

Sebelum melakukan konfigurasi static routing, setiap router sudah dilakukan konfigurasi IP Address untuk setiap interfacenya.

Mikrotik A : Ether 5 = 10.10.10.1/30 dan Ether 2 = 192.168.1.1/24

Mikrotik B : Ether 5 = 10.10.10.2/30 dan Ether 2 = 192.168.2.1/24

Yang perlu dipahami sebelum memulai konfigurasi static routing adalah gateway yang akan digunakan untuk saling terhubung.

Perhatikan pada tabel routing setiap router, setelah sudah dilakukan konfigurasi IP Address.

![alt text](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh47VPjg6M7kDXEPoKw87yziqGJf4aHtgL3891IKNE-B0pXCGlHGVttpqqujT_tBY0U4vm4EyP9Aua5J4csOp0-p7iXJ1IbIuBnA-bRwhswqcMFXDu6ZNcYadWa0nvq5AaNtVE0FSpQBdQ/s331/IP+address+Mikrotik+A.PNG "Topologi Static Routing")
![alt text](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgL22TlUGJ2DlNDRmMvFWcRSkp4FO5F-8jxY9w63a5MGzEC6z1FM-7KIrTqeMV_uCeBMn_1faE279FcyG-iTz8PLlHnVHu8WIuv0fCZ0grzRSQWQbHYmtHga-o_zmcO0NqSevCYEanvT5Q/s598/IP+Route+Mikrotik+A.PNG "Topologi Static Routing")

Pada saat PC yang ada di LAN 1 (192.168.1.x) melakukan PING ke PC yang ada di LAN 2 (192.168.2.x) akan Timeot dikarenakan pada table routing tidak terdapat IP Address yang di minta dan tidak ada petunjuk untuk ke tujuan IP Address yang di minta.

Untuk mengatasi Timeout tersebut maka disetiap router harus ditambahkan static routing untuk setiap IP Address Tujuan.

## Konfigurasi Static Routing

Tambahkan static routing setiap router pada menu IP->Routes Klik tambah (+)

Konfigurasi Mikrotik A
![alt text](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi5vbB5JMBq8UfLWgLA3kGn0Prf-945Zjau1fi_y_sRuVsnlaoUshkyXqtyVx-FnIFqGtIkUg2KYPuBLywTRe9e4iPa_P7kt9MfClnQVpSMhMgqNrEyWGAdG-aPnPaxrUCCHezjXxRKl6U/s724/IP+Route+Mikrotik+A+dst+LAN+2.PNG "Topologi Static Routing")

Konfigurasi Mikrotik B
![alt text](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgfGmg-bVF316fuOTGlJHhG-h7j2SL7LrmtMTEVny65LLCPd_lAgHv4AdVk1DH4JsL-vNbYC4PUvuXvFONtrP3GeCWgyAMA7R7034K6prtswZUR6jdIn9pj8LKTD8BTgLg78Go76ZcYnXE/s724/IP+Route+Mikrotik+B+dst+LAN+1.PNG "Topologi Static Routing")

Parameter yang harus diisi adalah dst-address dan gateway, Dst-address adalah IP Address yang akan dituju sedangkan Gateway  adalah IP Address yang digunakan sebagai jalur (gerbang jaringan) atau IP address router tetangganya.

Setelah menambahkan static routing untuk setiap router maka LAN 1 dapat saling terhubung dengan LAN 2 begitu juga sebaliknya.

## Pengujian


![alt text](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiVqtK1mAeHiDrCYz0EnseohLso8g8pePPFdRMhruFbcv1RjsncTaKvdea6zL_puvmOFEt7_ELcZPTqLSJLx2JB_CMH9h8AS0IU1Qg8K2R_pp_WQECVSx6Vj9SqZ8x3SdbVg2ZSyNkGwDA/w400-h89/pengujian+Dari+LAN+1.PNG "Topologi Static Routing")
![alt text](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjx24NDNySuJIFmpREm4x2SBfT5A_2mdjLOgriBkRPxsFSzUfTHhWi1LjzLUF1nhqj-awKsgL2HCp8EkPCVBE_CTsZON2IPvzGungdE00n0_vZSml0rbcjrsGIk8fT5SaSd5LmfQWfu2ro/w400-h94/pengujian+Dari+LAN+2.PNG "Topologi Static Routing")

Dari pengujian diatas PC yang ada di LAN 1 dapat melakukan ping ke PC yang ada di LAN 2.

## Kesimpulan
Static Routing diperlukan ketika jaringan kita sudah lebih kompleks dan memiliki router lebih dari satu. Static Routing dibuat dengan menentukan IP tujuan dan gateway yang akan dilalui, setiap ada perubahan topologi atau jalur maka harus ditambahkan routing yang baru. Static Routing. 

## [Source](https://www.coka.web.id/2020/09/konfigurasi-static-routing-mikrotik.html)


{{< css.inline >}}

<style>
.canon { background: white; width: 100%; height: auto; }
</style>

{{< /css.inline >}}
