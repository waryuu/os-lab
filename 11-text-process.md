---
title: Pencarian dan Pemrosesan Teks
author: Praktikum Sistem Operasi
institute: Ilmu Komputer IPB
date: 2019
theme: Dresden
linkcolor: .
header-includes:
    - \renewcommand{\figurename}{Gambar}
---

# Pencarian

## `man`
Menampilkan manual suatu program, fungsi, dan lain-lain.
```bash
man [SECTION] PAGE
```
- `q`: *quit*; keluar
- `/`: pencarian kata
    - `n`: *next*; lanjutkan pencarian kata
    - `N`: *next-reverse*; lanjutkan pencarian kata mundur

---

![Bagian halaman manual](img/man.png)

## `which`
Mencari lokasi *file* program.
```bash
which COMMAND
```


## `locate`
Mencari *file* berdasarkan namanya.
```bash
locate [OPTION] 'PATTERN'
```
- `-c`: *count*; tampilkan jumlah *file* yang ditemukan
- `-i`: *ignore-case*

## `find`
Mencari *file* pada sebuah hierarki direktori.
```bash
find [PATH] [TEST]...
```
- `-name  'PATTERN' `
- `-iname 'PATTERN' `
- `-size  [+-]N[kMG]`
- `-atime [+-]N     `
- `-mtime [+-]N     `
- `-empty           `
- `-type  [dfl]     `

## `xargs`
Mengubah tiap baris masukan menjadi argumen suatu perintah.
```bash
... | xargs COMMAND
```

### Contoh

```bash
# temukan semua file backup (.bak), lalu hapus
find . -name '*.bak' | xargs rm
```

# Editor Teks

## `pager` (`less`)
Menampilkan *file* teks per halaman layar.
```bash
pager [FILE]...
```
- `q`: *quit*; keluar
- `/`: pencarian kata
    - `n`: *next*; lanjutkan pencarian kata
    - `N`: *next-reverse*; lanjutkan pencarian kata mundur

## `editor` (`nano`)
Membuat dan mengedit *file* teks.
```bash
editor [OPTION] [FILE]...
```
- `-i`: *indent*; indentasi otomatis
- `-u`: *undo*; aktifkan fitur *undo*
- `^O`: *write-out*; simpan *file*
- `^X`: *exit*

<!--
## `micro`
Editor teks yang intuitif dan mudah dipakai, penerus '`nano`'.
```bash
micro [FILE]...
```
- `^X`, `^C`, `^V`: *cut*, *copy*, *paste*
- `^Z`: *undo*
- `^S`: *save*
- `^Q`: *quit*
-->

## `vi`
Editor teks untuk *programmer*.
```bash
vi [OPTION] [FILE]...
```

---

![Petunjuk singkat `vi`](img/vi_bell.jpg)

---

![*Editor wars*](img/real_programmers.png)


# Pemrosesan Teks

## `cat`
Menggabungkan *file* dan menampilkan isinya ke layar.
```bash
cat [FILE]...
```

## `split`
Memecah *file* menjadi beberapa bagian.
```bash
split [OPTION] FILE [PREFIX]
```
- `-b`: *bytes*; pecah per sekian *byte*
- `-l`: *lines*; pecah per sekian baris

## `head`
Menampilkan bagian awal *file* (*default*: 10 baris).
```bash
head [OPTION] [FILE]
```
- `-c`: *chars*; tampilkan sekian karakter pertama
- `-n`: *lines*; tampilkan sekian baris pertama

## `tail`
Menampilkan bagian akhir *file* (*default*: 10 baris).
```bash
tail [OPTION] [FILE]
```
- `-c`: *chars*; tampilkan sekian karakter terakhir
- `-n`: *lines*; tampilkan sekian baris terakhir

<!--
- `-f`: *follow*; ikuti penambahan isi *file*

---

![`tail -f`](img/tail.png)
-->

## `sort`
Mengurutkan baris teks pada *file*.
```bash
sort [OPTION] [FILE]
```
- `-n`: *numeric*; urutkan secara numerik
- `-r`: *reverse*; urutkan terbalik
- `-k`: *key*; urutkan berdasarkan kolom ke-sekian
- `-t`: karakter pemisah antarkolom


## `uniq`
Menghilangkan baris teks yang berulang.
```bash
uniq [OPTION] [FILE]
```
- `-c`: *count*; tampilkan jumlah kemunculan
- `-i`: *ignore-case*

## `tr`
Translasi karakter dari set pertama ke set kedua.

```bash
tr [OPTION] SET1 [SET2]
```
- `-d`: *delete*; hapus karakter pada *SET1*
- `-s`: *squeeze*; hapus karakter yang berulang pada *SET1*

## `grep`
Mencetak baris teks yang cocok dengan suatu pola.
```bash
grep [OPTION] 'PATTERN' FILE
```
- `-c`: *count*; tampilkan jumlah baris
- `-i`: *ignore-case*
- `-r`: rekursif
- `-v`: *invert*; kebalikan dari pola yang diberikan
- `-E`: *extended regex*

## `sed`
*Stream editor*, manipulasi baris teks dengan *regular expression*.
```bash
sed [OPTION] 's/SEARCH/REPLACE/' [FILE]
```
- `-e`: *execute*; tambahkan perintah untuk dieksekusi
- `-i`: *in-place*; edit *file* langsung
- `-E`: *extended regex*

## `cut`
Mengambil karakter/kolom tertentu dari tiap baris teks.
```bash
cut OPTION [FILE]
```
- `-c`: *char*; cetak karakter ke-sekian
- `-f`: *field*; cetak kolom ke-sekian
- `-d`: *delimiter*; pemisah antarkolom

## `paste`
Menggabungkan tiap baris dari beberapa *file* per kolom.
```bash
paste [OPTION] [FILE...]
```
- `-d`: *delimiter*; pemisah antarkolom
- `-s`: *serial*; gabungkan isi *file* menjadi sebaris

## `join`
Menggabungkan baris dari dua *file* berdasarkan satu kolom *join*.
```bash
join [OPTION] FILE1 FILE2
```
- `-1`: nomor kolom *join* untuk *FILE1*
- `-2`: nomor kolom *join* untuk *FILE2*
- `-t`: karakter pemisah antarkolom

## `diff`
Membandingkan antara dua *file* per baris.
```bash
diff [OPTION] FILE1 FILE2
```
- `-u`: *unified*; keluaran beserta konteks
- `-y`: *side-by-side*; keluaran dua kolom

## `wc`
Mencetak jumlah baris, kata, dan karakter dari suatu *file*.
```bash
wc [OPTION] [FILE...]
```
- `-c`: *char*; cetak jumlah karakter
- `-l`: *line*; cetak jumlah baris
- `-w`: *word*; cetak jumlah kata


# Ekspresi Reguler

## Ekspresi Reguler (Regex)

Regex adalah susunan karakter yang merupakan pola pencarian.
Regex digunakan untuk mencari *string* tertentu pada teks.

Misal, ekspresi reguler `/G64\d{6}/` dapat mencocokkan NIM semua mahasiswa S1 Ilmu Komputer IPB.

Untuk informasi dan latihan lebih lanjut, *lihat* <http://regexr.com>.


## Referensi Singkat

- Karakter

    `.`
    : karakter apapun selain *newline*

    `[abc]`
    : karakter `a`, `b`, atau `c`

    `[^abc]`
    : bukan karakter `a`, `b`, atau `c`

    `[a-g]`
    : karakter antara `a` sampai `g`

- Kelas karakter

    `\w`
    : kata, `[A-Za-z0-9_]`

    `\d`
    : digit, `[0-9]`

    `\s`
    : *whitespace*

- *Anchor*

    `^`
    : awal baris

    `$`
    : akhir baris


## Referensi Singkat

- Jumlah

    `*`
    : 0 atau lebih

    `+`
    : 1 atau lebih

    `?`
    : 0 atau 1

    `{3}`
    : tepat 3

    `{3,}`
    : 3 atau lebih

    `{3,5}`
    : antara 3 sampai 5

- Grup

    `(...)`
    : membuat grup

    `\n`
    : referensi balik grup ke-*n*

---

![*Regex saves the day*](img/regular_expressions.png)

## Tugas

UNIX Text Processing Contest 2019^[<https://www.hackerrank.com/unix-text-processing-2019>]

Nilai maksimum: **120**
