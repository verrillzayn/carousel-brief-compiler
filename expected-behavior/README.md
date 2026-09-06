# Expected Behavior â€” Carousel Brief Engine

Folder ini mendefinisikan behavior yang diharapkan dari engine ketika menjalankan fixtures.

Expected behavior bukan golden output.

File di folder ini tidak menentukan:

- headline exact;
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

Assertion visual/asset/production pada empat fixture NEEDS_REVIEW adalah MUST/MUST_NOT, bukan golden wording. Semua pilihan `flexible` tetap tunduk pada contract ini. Validasi output memakai schema 0.2.0; input fixtures tetap 0.1.0. Kasus BLOCKED tetap diuji atas evidence/scope dan tidak perlu menghasilkan visual atau asset.

Schema validator memeriksa enum dan struktur. Evaluator juga wajib membaca makna primary/fallback, requirements, prompts, dan instruksi Canva: label AI_GENERATED tidak membuat rencana infographic menjadi valid. Manusia boleh menambahkan graphic embellishment di tahap desain atas inisiatif sendiri, tetapi engine tidak merencanakannya, bahkan sebagai opsi.

Untuk pemeriksaan regresi, gunakan variasi terkontrol dari fixture simple tanpa mengubah material/objective:

- Tanpa `context.visual`: default AI-generated visual tetap photorealistic.
- Dengan `context.visual.data.direction` secara eksplisit meminta watercolor illustration: style tersebut boleh pada image AI_GENERATED; engine tetap image + text dan tidak merencanakan komponen Canva. Pengecualian style tidak boleh digeneralisasi ke fixture tanpa permintaan itu.
- Dengan visual context meminta foto dokumenter laptop nyata yang dijelaskan mat_03: prioritaskan REAL_ASSET dengan sourcing requirements; jangan menghasilkan foto AI seolah dokumentasi laptop tersebut.
- Dengan visual context meminta kombinasi foto laptop nyata dan AI-generated background: HYBRID_COMPOSITE boleh, registry memuat image real dan AI dengan prompt, dan editing terbatas pada compositing ringan.

Pemeriksaan negatif schema: strategy GRAPHIC_ONLY, asset type GRAPHIC_COMPONENT/OTHER, dan output schema_version 0.1.0 harus ditolak; ketiga strategy serta kedua image asset type baru harus diterima pada struktur yang valid. Pemeriksaan semantik harus menolak rencana icon/shape/diagram yang disamarkan sebagai image, termasuk pada fallback. Tidak perlu menjalankan atau mengubah arsip manual runs lama untuk melakukan pemeriksaan contract ini.
