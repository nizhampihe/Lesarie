---
layout: default
title: Tetris
description: Tutorial bikin Tetris
---

[Beranda](https://nizhampihe.github.io/Lesarie) / [Posts](https://nizhampihe.github.io/Lesarie/posts) / [Pemrograman](https://nizhampihe.github.io/Lesarie/posts/pemrograman) / tetris

> Kata Kunci: [Pemrograman](https://nizhampihe.github.io/Lesarie/posts/pemrograman), Web, Game, Tetris

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

- Tetromino
- Shape
  - Bentuk I
    ```
    y\x   0   1   2   3
        +---+---+---+---+
     0  |   |   |   |   |
        +---+---+---+---+
     1  | 0 | 1 | 2 | 3 |
        +---+---+---+---+
    ```
    sehingga jika dibuat dalam bentuk `Array` yang berisi koordinat `[x, y]` sebagai elemennya akan menjadi seperti berikut
    ```javascript
    [[0, 1], [1, 1], [2, 1], [3, 1]]
    ```
  - Bentuk J
    ```
    y\x   0   1   2   3
        +---+---+---+---+
     0  | 3 |   |   |   |
        +---+---+---+---+
     1  | 0 | 1 | 2 |   |
        +---+---+---+---+
    ```
    sehingga jika dibuat dalam bentuk `Array` yang berisi koordinat `[x, y]` sebagai elemennya akan menjadi seperti berikut
    ```javascript
    [[0, 1], [1, 1], [2, 1], [0, 0]]
    ```
  - Bentuk L
    ```
    y\x   0   1   2   3
        +---+---+---+---+
     0  |   |   | 3 |   |
        +---+---+---+---+
     1  | 0 | 1 | 2 |   |
        +---+---+---+---+
    ```
    sehingga jika dibuat dalam bentuk `Array` yang berisi koordinat `[x, y]` sebagai elemennya akan menjadi seperti berikut
    ```javascript
    [[0, 1], [1, 1], [2, 1], [2, 0]]
    ```
  - Bentuk O
    ```
    y\x   0   1   2   3
        +---+---+---+---+
     0  |   | 0 | 2 |   |
        +---+---+---+---+
     1  |   | 1 | 3 |   |
        +---+---+---+---+
    ```
    sehingga jika dibuat dalam bentuk `Array` yang berisi koordinat `[x, y]` sebagai elemennya akan menjadi seperti berikut
    ```javascript
    [[1, 0], [1, 1], [2, 0], [2, 1]]
    ```
  - Bentuk S
    ```
    y\x   0   1   2   3
        +---+---+---+---+
     0  |   | 2 | 3 |   |
        +---+---+---+---+
     1  | 0 | 1 |   |   |
        +---+---+---+---+
    ```
    sehingga jika dibuat dalam bentuk `Array` yang berisi koordinat `[x, y]` sebagai elemennya akan menjadi seperti berikut
    ```javascript
    [[0, 1], [1, 1], [1, 0], [2, 0]]
    ```
  - Bentuk T
    ```
    y\x   0   1   2   3
        +---+---+---+---+
     0  |   | 3 |   |   |
        +---+---+---+---+
     1  | 0 | 1 | 2 |   |
        +---+---+---+---+
    ```
    sehingga jika dibuat dalam bentuk `Array` yang berisi koordinat `[x, y]` sebagai elemennya akan menjadi seperti berikut
    ```javascript
    [[0, 1], [1, 1], [2, 1], [1, 0]]
    ```
  - Bentuk Z
    ```
    y\x   0   1   2   3
        +---+---+---+---+
     0  | 0 | 1 |   |   |
        +---+---+---+---+
     1  |   | 2 | 3 |   |
        +---+---+---+---+
    ```
    sehingga jika dibuat dalam bentuk `Array` yang berisi koordinat `[x, y]` sebagai elemennya akan menjadi seperti berikut
    ```javascript
    [[0, 0], [1, 1], [1, 0], [2, 1]]
    ```
  ```javascript
  const SHAPES = [
    [[0, 1], [1, 1], [2, 1], [3, 1]], // Bentuk I
    [[0, 1], [1, 1], [2, 1], [0, 0]], // Bentuk J
    [[0, 1], [1, 1], [2, 1], [2, 0]], // Bentuk L
    [[1, 0], [1, 1], [2, 0], [2, 1]], // Bentuk O
    [[0, 1], [1, 1], [1, 0], [2, 0]], // Bentuk S
    [[0, 1], [1, 1], [2, 1], [1, 0]], // Bentuk T
    [[0, 0], [1, 1], [1, 0], [2, 1]], // Bentuk Z
  ];
  ```
  ```javascript
  function tetromino(shape = Math.floor(Math.random() * 7)) {
    return { ...SHAPES[shape], length: 4, color: shape + 1 };
  }
  ```
- Check
  - yaitu fungsi untuk mengecek apakah tetrimino akan bertabrakan dengan balok lain atau pun keluar papan permainan
  - menggunakan method `Array.from()` untuk membuat array dari tetromino
  - menggunakan method `every()` untuk mengecek tiap elemen pada array
  - membuat _Arrow Function_ `() => {}`sebagai argumen dari method `every()` yang memliki parameter _Array Destructor_ `([x, y]) => {}` dari elemen array tersebut untuk mendapatkan koordinat **x** dan **y**
  ```javascript
  function check(temp) {
    return Array.from(temp).every(([x, y]) => {
      if (x < 0 || x >= width) return false;
      if (y < 0 || y >= height) return false;
      if (board[y][x] > 0) return false;
      return true;
    });
  }
  ```
- Trans
  - yaitu fungsi untuk mentransformasi ataupun mentranslasi tetromino
  ```javascript
  function trans(method) {
    let temp = Array.from(piece).map(method);
    return check(temp) ? ((piece = { ...temp, length: 4, color: piece.color }), true) : false;
  }
  ```
- Add
  - yaitu fungsi untuk menambahkan tetromino kedalam papan permainan
  ```javascript
  function addPiece() {
    Array.from(piece).forEach(([x, y]) => (board[y][x] = piece.color));
  }
  ```

## Action

- Display
  - yaitu fungsi untuk menampilkan tetrimino dan papan permainan kedalam elemen div#board
  ```javascript
  function display() {
    [...document.getElementById("board").children].forEach((a, i) => (a.classList = "block " + " IJLOSTZ"[board[Math.floor(i / width)][i % width]]));
    Array.from(piece).forEach(([x, y]) => document.getElementById("board").children[x + y * width].classList.add(" IJLOSTZ"[piece.color]));
    document.getElementById("score").textContent = score;
    return true;
  }
  ```
- Fall
  - yaitu fungsi untuk menggerakan tetromino ke bawah
  ```javascript
  function fall() {
    return trans(([x, y]) => [x, y + 1]);
  }
  ```
- Right
  - yaitu fungsi untuk menggerakan tetromino ke kanan
  ```javascript
  function right() {
    if (trans(([x, y]) => [x + 1, y])) display();
  }
  ```
- Left
  - yaitu fungsi untuk menggerakan tetromino ke kiri
  ```javascript
  function left() {
    if (trans(([x, y]) => [x - 1, y])) display();
  }
  ```
- Drop
  - yaitu fungsi untuk menjatuhkan tetromino ke paling bawah yang dapat ditempati tetromino
  ```javascript
  function drop() {
    while (fall());
    display();
  }
  ```
- Rotate
  - yaitu fungsi untuk memutar tetromino 
  ```javascript
  function rotate() {
    let [cx, cy] = piece[1];
    if (trans(([x, y]) => [cx - (y - cy), cy + (x - cx)])) display();
  }
  ```
- Event
  - yaitu untuk menambahkan keyboard event agar tetromino dapat dikendalikan menggunakan tombol panah pada keyboard
  ```javascript
  let input = {
    ArrowUp: () => rotate(),
    ArrowDown: () => drop(),
    ArrowLeft: () => left(),
    ArrowRight: () => right(),
  };
  document.addEventListener("keydown", e => {
    if (input[e.key] == undefined) return console.log(e.key);
    input[e.key]();
  });
  ```

## Game Loop

- Center
  - yaitu fungsi untuk memindahkan tetromino ke tengah
  ```javascript
  function center() {
    return trans(([x, y]) => [x + Math.floor(width / 2) - 2, y]) ? display() : false;
  }
  ```
- Phase
  ```javascript
  function phase() {
    piece = tetromino();
    if (!center()) return false;
    return display();
  }
  ```
- Line
  - yaitu fungsi untuk menghapus baris yang sudah penuh
  ```javascript
  function row() {
    return board.reduce((count, row, line) => row.every(block => block > 0) ? (board.unshift(board.splice(line, 1)[0].fill(0)), ++count) : count, 0);
  }
  ```
- Over
  - yaitu fungsi untuk mengakhiri permainan
  ```javascript
  function over() {
    clearInterval(runer);
    runer = null;
    console.log("game over");
  }
  ```
- Loop
  - yaitu fungsi yang akan diulang terus menerus selama permainan berlangsung
  ```javascript
  function loop() {
    if (fall()) return display();
    addPiece();
    score += [0, 10, 30, 50, 80][row()];
    if (phase()) return;
    over();
  }
  ```
- Play
  - yaitu fungsi untuk memulai permainan
  ```javascript
  function play() {
    if (runer) return;
    score = 0;
    board = Array(height).fill().map(() => Array(width).fill(0));
    phase();
    runer = setInterval(() => loop(), 1000);
  }
  ```

## Conclution

[Kembali ke Atas>](#)