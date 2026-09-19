# Expected Behavior â€” Carousel Brief Engine

Folder ini mendefinisikan behavior yang diharapkan dari engine ketika menjalankan fixtures.

Expected behavior bukan golden output.

File di folder ini tidak menentukan:

- display-copy wording exact;
- copy exact;
- visual exact;
- angle exact;
- jumlah slide exact, kecuali memang diperlukan oleh test;
- prompt exact.

Sebaliknya, file ini menentukan properties yang harus atau tidak boleh muncul pada behavior engine.

---

## Purpose

Tujuan expected behavior adalah membuat evaluation standard sebelum melihat output model.

Dengan demikian, kualitas engine tidak dinilai berdasarkan:

> "Output ini kelihatannya bagus."

Tetapi berdasarkan:

> "Apakah engine menunjukkan behavior yang sebelumnya sudah kita sepakati?"

---

## Evaluation Categories

Setiap test dapat memeriksa:

### Status

Apakah engine seharusnya menghasilkan:

```text
NEEDS_REVIEW
````

atau:

```text
BLOCKED
```

### MUST

Behavior yang wajib terjadi.

Jika tidak terjadi, run dianggap gagal.

### MUST_NOT

Behavior yang tidak boleh terjadi.

Jika terjadi, run dianggap gagal.

### SHOULD

Behavior yang sangat diharapkan tetapi masih dapat dinilai secara kontekstual.

### FLEXIBLE

Area yang sengaja dibiarkan untuk kreativitas model.

---

## Important Principle

Expected behavior harus mengevaluasi:

```text
behavior
```

bukan:

```text
wording
```

Contoh yang baik:

```text
Engine harus membedakan diskon Rp80.000 sebagai nilai yang dapat diturunkan dari input.
```

Contoh yang terlalu rigid:

```text
Slide 3 harus berbunyi:
"Kamu hemat Rp80 ribu?"
```

---

## Fixture Stability

Jangan mengubah expected behavior hanya karena suatu model gagal memenuhi test.

Jika output model buruk:

```text
investigate engine
```

sebelum:

```text
change expectation
```

Expected behavior hanya berubah jika:

* system principles berubah;
* contract berubah;
* fixture ternyata salah dirancang;
* keputusan product berubah.


## Image + Text Regression Checks

Assertion visual/asset/production pada empat fixture NEEDS_REVIEW adalah MUST/MUST_NOT, bukan golden wording. Semua pilihan `flexible` tetap tunduk pada contract ini. Validasi output memakai schema 0.3.0; input fixtures tetap 0.1.0. Kasus BLOCKED tetap diuji atas evidence/scope dan tidak perlu menghasilkan visual atau asset.

Schema validator memeriksa enum dan struktur. Evaluator juga wajib membaca makna primary visual, requirements, prompts, dan instruksi Canva: label AI_GENERATED tidak membuat rencana infographic menjadi valid. Manusia boleh menambahkan graphic embellishment di tahap desain atas inisiatif sendiri, tetapi engine tidak merencanakannya, bahkan sebagai opsi.

Untuk pemeriksaan regresi, gunakan variasi terkontrol dari fixture simple tanpa mengubah material/objective:

- Tanpa `context.visual`: default AI-generated visual tetap photorealistic.
- Dengan `context.visual.data.direction` secara eksplisit meminta watercolor illustration: style tersebut boleh pada image AI_GENERATED; engine tetap image + text dan tidak merencanakan komponen Canva. Pengecualian style tidak boleh digeneralisasi ke fixture tanpa permintaan itu.
- Dengan visual context meminta foto dokumenter laptop nyata yang dijelaskan mat_03: prioritaskan REAL_ASSET dengan sourcing requirements; jangan menghasilkan foto AI seolah dokumentasi laptop tersebut.
- Dengan visual context meminta kombinasi foto laptop nyata dan AI-generated background: HYBRID_COMPOSITE boleh, registry memuat image real dan AI dengan prompt, dan editing terbatas pada compositing ringan.

Pemeriksaan negatif schema: strategy GRAPHIC_ONLY, asset type GRAPHIC_COMPONENT/OTHER, output schema_version lama, field copy `headline`/`supporting`, dan visual `fallback` harus ditolak. Ketiga strategy, kedua image asset type, dan ordered display-copy blocks harus diterima pada struktur yang valid. Pemeriksaan semantik harus menolak rencana icon/shape/diagram yang disamarkan sebagai image. Tidak perlu menjalankan atau mengubah arsip manual runs lama untuk melakukan pemeriksaan contract ini.

## Copy sufficiency regression checks

Evaluator harus memeriksa dua arah density. Output gagal jika terlalu padat, tetapi juga gagal jika explanation, comparison, example, atau action slide hanya menyisakan slogan.

MUST:

- display copy pada slide informasional dapat dipahami tanpa membaca `core_message`, caption, atau production notes;
- hook dan transition boleh lebih pendek daripada slide yang membawa reasoning;
- penjelasan mempertahankan bridge yang diperlukan, seperti alasan, mekanisme, implication, contoh, kontras, atau langkah;
- ritme panjang copy bervariasi mengikuti fungsi slide.

MUST_NOT:

- menilai copy baik hanya karena jumlah katanya rendah;
- memaksa semua slide ke panjang cover;
- memindahkan reasoning penting ke caption;
- menambah filler untuk mengejar rentang kata.

Rentang kata dalam `docs/principles.md` adalah alarm untuk review, bukan assertion numerik kaku.

## Visual language regression checks

Evaluator harus membaca carousel sebagai satu sistem, bukan menilai tiap prompt secara terpisah.

MUST:

- global production `SETUP` menyebut primary visual family, optional secondary family, cohesion anchors, dan variation axes;
- keluarga visual dipilih berdasarkan fungsi komunikasi slide;
- sedikitnya tiga sumbu komposisi berubah pada carousel 5 sampai 7 slide;
- sedikitnya tiga anchor menjaga kohesi post;
- text-safe area dan beban copy cocok;
- gambar melakukan pekerjaan komunikasi yang dapat dijelaskan.

MUST_NOT:

- menganggap pergantian objek sebagai variasi jika background, crop, posisi, headline scale, dan text zone tetap sama;
- mengulang background putih, portrait kanan-bawah, dan headline raksasa pada seluruh slide tanpa alasan;
- memakai pose stok atau simbol uang klise sebagai shortcut visual;
- menyalin subjek, properti, identitas, atau layout referensi secara literal;
- mencampur lebih dari dua keluarga visual hanya untuk terlihat beragam.
