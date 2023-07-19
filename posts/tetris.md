---
layout: default
title: Tetris
description: Tutorial bikin Tetris
---

[Halaman Utama](https://nizhampihe.github.io/Lesarie) / [posts](https://nizhampihe.github.io/Lesarie/posts) / tetris

# Tetris

Kali ini saya akan menunjukan cara untuk membuat permainan Tetris di dalam suatu Browser, meskipun saya bilang akan membuatnya di dalam Browser namun sebenarnya untuk membuatnya tidak membutuhkan koneksi internet sama sekali dan hanya mengandalkan fitur Developer Tools yang terdapat pada Browser.

## Prerequisites

Hal yang perlu disiapkan untuk membuat permainan Tetris yaitu diantaranya adalah.

- Desktop (Laptop/PC/Komputer)

  Saya sarankan untuk tidak menggunkakan perangkat HP/Smartphone karena akan sulit untuk kedepannya.

- Sistem Operasi (OS)

  Saya sarankan untuk tidak menggunkakan Sistem Operasi android karena Browser pada Sistem Operasi tersebut biasanya tidak memiliki fitur Developer Tools.

- Browser

  Saya menyarankan untuk menggunakan Google Chrome karena itu Browser yang saya gunakan dalam pembahasan ini.

## Prelude

Sebelum memulai membuat permainanya mari pahami dulu kosep dari permainan itu sendiri ->

dengan menerapkan salah satu konsep dari Computational Thinking yaitu Decomposition saya akan membagi pembahasan menjadi 4 bagian yaitu

- Layouting
- Object
- Action
- Loop

## Layouting

Tujuan dari tahapan ini yaitu untuk membuat tata letak antarmuka pengguna yang terdiri dari kolom skor dan papan permainan. Papan permainan yang akan dibuat memiliki ukuran yang umum untuk permainan Tetris yaitu memiliki tinggi **20** _petak_ dan lebar **10** _petak_. -> 

Adapun tahapan untuk membuat nya yaitu adalah sebagai berikut

- Pertama silahkan buka terlebih dahulu Browser yang digunakan kemudian ketikan alamat berikut pada kolom URL kemudian tekan `Enter`.
  ```
  about:blank
  ```
  Setelah itu Browser akan mengarahkan ke suatu halaman kosong yang mana akan menjadi wadah untuk dapat membuat permainan Tetris.
- Berikutnya silahkan klik kanan menggunakan mouse lalu pilih `Inspect` atau tekan tombol `Ctrl` + `Shift` + `I` pada keyboard secara bersamaan. Kemudian Browser akan memunculkan panel Developer Tools yang akan didgunaakan untuk memanipulasi halaman.
- Selanjutnya bukan tab `Element` disana terdapat kode **HTML**, silahkan klik kanan pada kode `<body></body>` kemudian pilih `Edit as HTML`, Kemudian ketikan kode berikut
  ```html
  Score: <span id="score"></span><div id="board"></div>
  ```
  sehingga kodenya menjadi
  ```html
  <html>
    <head></head>
    <body>
      "Score: "
      <span id="score"></span>
      <div id="board"></div>
    </body>
  </html>
  ```
- Lalu berikutnya klik pada kode `<div id="board"></div>`, kemudian pada bagian bawah pada tab `Styles` tuliskan kode **CSS** pada blok `element.style` yang kemudian diisi dengan beberapa kode untuk _styling_ papan permainan yaitu diantaranya adalah sebagai berikut
  - yang pertama yaitu adalah ukuran dari papan 
  
  berikut sehingga kodenya menjadi
  ```css
  element.style {
    width: 200px;
    height: 400px;
    display: flex;
    flex-wrap: wrap;
    box-sizing: border-box;
    border: 10px solid black;
  }
  ```
## Object

## Action

## Game Loop

## Conclution

[Kembali ke Atas>](#tetris)