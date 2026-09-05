# Expected Behavior — Carousel Brief Engine

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
