# Visual language playbook

Dokumen ini menerjemahkan empat referensi di `references/visuals/` menjadi aturan keputusan. Referensi adalah bahan untuk memahami cara kerja desain, bukan template yang harus disalin.

Sumber:

```text
references/visuals/001.md
references/visuals/002.md
references/visuals/003.md
references/visuals/004.md
```

Pelajari prinsip, hubungan copy dan gambar, komposisi, hierarki, ritme, dan treatment. Jangan menyalin subjek, properti, wording, identitas kreator, metadata, atau tampilan UI platform.

Gunakan `docs/copy-composition.md` untuk baseline panjang relatif antar-block, line break, text zone, dan spacing yang diturunkan dari `_example/copy/`. Dokumen ini tetap mengatur visual family dan hubungan image dengan copy.

Jika detail referensi bertentangan dengan `SYSTEM.md`, schema, atau batas produksi V0, aturan yang lebih tinggi tetap berlaku. Contohnya, badge dekoratif pada referensi 03 tidak mengizinkan engine merencanakan graphic component baru.

---

# 1. Design DNA bersama

Keempat referensi memakai bahasa visual yang sama pada level prinsip:

```text
satu focal point yang jelas
tipografi yang punya peran visual
negative space yang disengaja
komposisi asimetris yang seimbang
palet terbatas
sedikit objek
hubungan copy dan image yang dapat dijelaskan
```

Minimal bukan berarti kosong. Satu slide boleh membawa beberapa blok copy selama setiap blok punya peran, ruang, dan hierarki yang jelas.

Image-led juga bukan berarti gambar harus selalu menjadi elemen terbesar. Pada pendekatan typography-first, foto tetap menjadi aset utama, tetapi headline boleh memimpin perhatian.

---

# 2. Empat keluarga visual

## A. Typography-first poster

Asal prinsip: referensi 01.

Gunakan ketika slide perlu terasa tegas, cepat dipahami, atau information-first.

```text
canvas terang atau bidang warna bersih
headline sebagai focal point pertama
satu cutout portrait atau objek sebagai counterweight
komposisi dua massa, biasanya text-left dan image-right
kontras tinggi
metadata sangat kecil jika memang berguna
```

Cocok untuk cover, diagnosis, pernyataan utama, angka penting, atau rangkuman yang perlu otoritas.

Jangan memakai keluarga ini pada semua slide. Jika setiap slide memakai headline raksasa, cutout kanan, dan bidang putih yang sama, variasi hilang.

## B. Lifestyle editorial

Asal prinsip: referensi 02.

Gunakan ketika gesture, situasi, atau pengalaman manusia membantu pembaca merasa dekat dengan topik.

```text
foto lingkungan sebagai canvas
satu manusia sebagai subjek utama
latar terasa dihuni tetapi tidak ramai
copy diletakkan pada tonal area yang tenang
headline editorial dapat memakai serif
body memakai sans serif netral
satu accent color
```

Cocok untuk skenario, emosi, validasi, kebiasaan, konsekuensi sehari-hari, atau momen refleksi.

Foto harus menunjukkan tindakan atau keadaan yang spesifik. Hindari pose stok seperti orang memegang kepala, menatap laptop, atau memegang dompet jika gesture tersebut tidak menambah makna.

## C. Conceptual object editorial

Asal prinsip: referensi 03.

Gunakan ketika satu objek atau kombinasi objek dapat menciptakan rasa ingin tahu tanpa membutuhkan aktor manusia.

```text
satu objek dominan dan paling banyak satu objek pendukung
scene sederhana tetapi sedikit tidak biasa
silhouette mudah dibaca dalam kurang dari satu detik
negative space besar
headline kuat dengan body yang cukup menjelaskan
komposisi text-left dan object-right atau kebalikannya
```

Cocok untuk mekanisme, perbandingan, metafora, prinsip, atau attention hook.

Jangan kembali ke simbol uang generik seperti dompet, kalkulator, koin, celengan, atau uang beterbangan kecuali objek itu melakukan pekerjaan komunikasi yang spesifik.

## D. Conceptual human cinematic

Asal prinsip: referensi 04.

Gunakan ketika slide membutuhkan curiosity, emosi, atau scale yang lebih kuat daripada skenario realistis biasa.

```text
satu manusia
satu properti dominan
paling banyak satu properti pendukung
scene mustahil atau tidak lazim tetapi langsung terbaca
landscape minimal
silhouette jelas
warna sinematik yang terkendali
ruang kosong luas untuk copy
```

Cocok untuk cover tertentu, turning point, tension, aspirasi, atau penutup reflektif.

Keanehan harus tenang dan sederhana. Jangan membuat fantasi ramai, banyak objek melayang, lighting bombastis, atau scene yang perlu dijelaskan panjang agar masuk akal.

---

# 3. Pilih berdasarkan fungsi slide

Jangan memilih keluarga visual hanya karena topiknya tentang uang. Pilih berdasarkan pekerjaan slide.

| Kebutuhan komunikasi | Pilihan awal | Alasan |
| --- | --- | --- |
| Pernyataan tegas atau authority | Typography-first poster | Copy dapat memimpin tanpa kehilangan focal image |
| Kedekatan manusia atau situasi sehari-hari | Lifestyle editorial | Gesture dan environment membawa konteks |
| Menjelaskan mekanisme dengan metafora sederhana | Conceptual object editorial | Objek dapat menyederhanakan ide tanpa pose manusia generik |
| Curiosity, tension, atau emosi yang kuat | Conceptual human cinematic | Scene tidak lazim menjadi pattern interruption |
| Langkah praktis | Lifestyle editorial atau conceptual object | Tindakan nyata atau alat utama dapat menunjukkan apa yang harus dilakukan |
| Transisi | Turunkan kompleksitas dari keluarga yang sedang dipakai | Transisi tidak perlu scene baru yang berat |

Ini titik mulai, bukan tabel otomatis. Keputusan akhir tetap mempertimbangkan message, bukti, brand, kesinambungan post, dan biaya produksi.

---

# 4. Variasi pada level carousel

Variasi tidak berarti setiap slide memakai style yang tidak berhubungan. Satu carousel harus punya satu art direction, lalu mengubah komposisi sesuai fungsi.

Sebelum merancang slide, tentukan:

```text
primary visual family
secondary visual family, jika dibutuhkan
palette behavior
type pairing
image treatment
recurring anchor
variation plan
```

Gunakan visual grammar ini sebagai working plan internal. Terapkan hasilnya langsung pada `slides[].visual`, display-copy blocks, asset prompts, dan `slides[].production_instructions`. Jangan menyalinnya ke ringkasan output terpisah.

Primary family membentuk identitas post. Secondary family hanya dipakai saat fungsi slide memang berubah. Untuk carousel 5 sampai 7 slide, satu atau dua keluarga biasanya cukup.

Pertahankan kohesi melalui paling sedikit tiga anchor:

```text
palette atau color-grade yang konsisten
type system yang konsisten
margin atau alignment logic yang konsisten
karakter, wardrobe, lokasi, atau properti berulang
image treatment yang konsisten
```

Variasikan paling sedikit tiga sumbu sepanjang carousel:

```text
skala subjek, dekat dan jauh
posisi subjek, kiri, kanan, bawah, atau tengah
rasio massa text dan image
jenis framing, cutout, full-photo, close-up, wide scene
lokasi text zone
jumlah dan ukuran copy blocks
dominasi warna terang dan gelap
```

Jangan mengubah semua sumbu sekaligus. Carousel harus bergerak, bukan pecah menjadi tujuh kampanye berbeda.

---

# 5. Ritme komposisi

Buat peta komposisi sebelum menulis prompt aset. Setiap slide harus punya siluet layout yang dapat dibedakan saat semua detail di-blur.

Contoh ritme yang valid:

```text
cover: typography-first, massa teks besar di kiri
context: full-photo, subjek besar di kanan
explanation: conceptual object kecil di bawah
turning point: bidang lebih gelap dengan copy lebih sedikit
example: close-up objek dengan body sedang
action: environment nyata dengan area langkah yang luas
close: wide scene dengan kalimat penutup
```

Contoh ini bukan urutan wajib. Yang wajib adalah adanya alasan untuk perubahan skala, framing, dan kepadatan.

Hindari pengulangan berikut kecuali menjadi motif yang disengaja:

```text
semua slide berlatar putih steril
semua subjek di kanan bawah
semua headline empat baris uppercase
semua slide memakai portrait orang yang sama dengan pose berbeda
semua visual memakai objek literal dari kata benda di copy
semua prompt meminta negative space di lokasi yang sama
```

---

# 6. Copy dan komposisi harus saling mengoreksi

Copy tidak boleh dipadatkan hanya agar cocok dengan layout pertama. Layout juga tidak boleh dipilih sebelum tahu beban penjelasan slide.

Setelah draft copy dan visual pertama tersedia, lakukan fit check:

```text
Apakah focal statement punya ruang dan skala yang pantas?
Apakah explanation masih terbaca pada lebar ponsel?
Apakah gambar membawa sebagian makna atau hanya mengulang kata-kata?
Apakah negative space benar-benar tersedia pada aset?
Apakah body copy dipecah menjadi blok yang alami?
Apakah slide terasa kosong karena copy terlalu tipis?
Apakah slide terasa sesak karena komposisi salah, bukan karena materinya terlalu banyak?
```

Jika gagal, revisi salah satu atau beberapa hal ini:

```text
copy wording
block structure
typographic hierarchy
text zone
subject scale
crop
visual family
slide split
```

Jangan langsung menghapus penjelasan yang dibutuhkan pembaca.

---

# 7. Sistem tipografi

`Anton` atau `Bebas` adalah opsi untuk statement keras, bukan default untuk setiap blok dan setiap slide.

Gunakan role-based typography:

```text
condensed bold sans: diagnosis, angka, pernyataan tegas
editorial serif: refleksi, framing, atau statement yang lebih tenang
italic serif: emphasis emosional yang pendek
neutral sans: explanation, label, langkah, metadata
```

Satu post dapat memakai paling banyak dua keluarga utama ditambah satu italic dari keluarga serif yang sama. Jangan mengganti font per slide untuk menciptakan variasi.

Emphasis sebaiknya datang dari scale, weight, style, line break, atau satu accent color. Jangan menumpuk highlight box, outline, shadow, dan warna sekaligus.

---

# 8. Palet Mantri Uang

Emerald atau forest green tetap menjadi anchor brand. Anchor tidak harus memenuhi setiap background.

Pilihan treatment yang valid:

```text
warm white + forest text + monochrome image
grayscale photo + emerald accent
forest field + warm white copy
muted cyan or cool scene + emerald or white brand cue
restrained blue-peach cinematic grade + small emerald brand cue
```

Hitam, putih, grayscale, cyan yang redup, dan warm neutral dapat menjadi bidang pendukung selama hijau tetap hadir sebagai pengikat. Jangan memaksa semua foto menjadi hijau atau semua slide memakai background putih.

---

# 9. Prompt dan aset

Prompt image generator hanya membuat aset foto. Typography, nomor slide, label, body copy, dan metadata dibuat di design tool.

## Scene coherence

Scene konseptual boleh mustahil atau tidak lazim. Namun scene tetap membutuhkan logika visual yang terbaca.

Gunakan prinsip berikut:

```text
satu keanehan utama
environment atau bidang pijakan yang jelas
skala dan perspektif yang konsisten
objek utama yang langsung dikenali
hubungan fisik antar-objek yang terlihat
sedikit properti dengan fungsi yang dapat dijelaskan
```

Setiap objek harus menjawab tiga pertanyaan:

```text
Apa benda ini?
Mengapa benda ini berada di scene tersebut?
Apa hubungan yang terlihat antara benda ini, subjek, dan message?
```

Tolak konsep jika fungsi objek hanya dapat dipahami dari `rationale`. Hindari mesin, alat ukur, tombol, jalur, atau instalasi rekaan yang mekanismenya tidak langsung terbaca. Jangan menambahkan properti acak hanya untuk mempertahankan continuity. Cohesion dapat datang dari color grade, lighting, lens behavior, material, framing, dan type system.

Surreal boleh. Arbitrer jangan. Scene yang menabrak realitas tetap harus memiliki satu dunia yang koheren.

## Observable prompt rule

Setiap prompt harus menetapkan:

```text
subject count
subject or object identity
gesture or state
scene
camera distance and angle
subject position and scale
text-safe area
background complexity
lighting
color treatment
continuity requirement
negative constraints
```

Urutkan prompt dari hal yang paling menentukan hasil:

```text
canvas dan kebutuhan text-safe area
environment
jumlah dan identitas subjek atau objek
posisi, skala, dan hubungan spasial
action, gesture, contact, atau physical state
foreground, middle ground, dan background
camera distance, angle, dan lens behavior
lighting dan color treatment
mood atau aesthetic cue
negative constraints
```

Prompt harus menerjemahkan maksud abstrak menjadi bukti yang dapat terlihat. Kata seperti `feel`, `suggest`, `symbolize`, `sensitive`, `alive`, `calm`, atau `witty` boleh menjadi arahan sekunder, tetapi tidak boleh menggantikan posisi, tindakan, ekspresi, kontak fisik, atau keadaan objek.

Contoh lemah:

```text
The balance feels sensitive to many small actions.
```

Contoh yang dapat divisualisasikan:

```text
Four hands enter from separate frame edges. Two fingertips touch opposite ends of the board. The board tilts about ten degrees and one disc has shifted close to the edge.
```

Untuk scene konseptual, jelaskan logika visualnya dalam brief. Jika hubungan image dan message tidak bisa diterangkan dalam satu atau dua kalimat, konsepnya kemungkinan terlalu kabur.

Hasil generator tidak perlu menyamai referensi. Yang harus sama adalah disiplin komposisinya.

---

# 10. Visual QA

Sebelum output, periksa keseluruhan carousel dalam satu pandangan.

```text
Apakah setiap slide punya focal point yang langsung terlihat?
Apakah keluarga visual dipilih berdasarkan fungsi slide?
Apakah carousel punya satu art direction yang jelas?
Apakah siluet layout antar-slide cukup berbeda?
Apakah ada perubahan skala dan framing?
Apakah gambar melakukan pekerjaan selain mendekorasi?
Apakah scene tetap terbaca tanpa membaca rationale?
Apakah setiap objek memiliki alasan yang terlihat untuk berada di scene?
Apakah scene hanya memiliki satu keanehan utama dan dunia di sekelilingnya tetap koheren?
Apakah ada visual stok generik atau simbol uang klise?
Apakah negative space berada di lokasi yang dibutuhkan copy?
Apakah type treatment sesuai dengan peran copy?
Apakah palet terasa sebagai sistem, bukan satu warna yang dipaksakan?
Apakah semua variasi masih bisa diproduksi dengan aset dan tool yang tersedia?
```

`PASS` untuk visual membutuhkan jawaban yang spesifik. Pernyataan seperti "variasi masih cohesive" tanpa menyebut anchor dan sumbu variasinya belum cukup.
