# Fixtures — Carousel Brief Engine

Folder ini berisi mock input yang digunakan untuk menguji behavior `carousel-brief-engine`.

Fixtures bukan contoh output ideal dan bukan production content.

Tujuan fixture adalah menyediakan kondisi input yang terkontrol sehingga behavior engine dapat diuji secara konsisten.

---

## Core Rule

Semua fixture harus:

1. valid terhadap `schemas/input.schema.json`;
2. menggunakan `schema_version` yang sesuai;
3. menggunakan stable IDs;
4. tidak sengaja dibuat rusak secara JSON;
5. memiliki tujuan testing yang jelas;
6. tidak dianggap sebagai production knowledge.

Masalah pada fixture harus bersifat **semantic**, bukan syntactic.

Contoh:

```text
GOOD TEST

JSON valid
+
raw material tidak cukup
→ menguji apakah engine menghasilkan BLOCKED
````

Bukan:

```text
BAD TEST

field wajib hilang
+
JSON tidak sesuai schema
→ hanya menguji schema validator
```

Schema-validation testing dapat dibuat terpisah jika dibutuhkan.

---

# Fixture Matrix

## 1. Simple

Path:

```text
simple/emergency-fund.json
```

Tujuan:

Menguji apakah engine dapat menangani material sederhana tanpa membuat output terlalu kompleks.

Karakteristik:

```text
small material
clear objective
little ambiguity
clear central takeaway
```

Expected outcome secara umum:

```text
NEEDS_REVIEW
```

---

## 2. Dense

Path:

```text
dense/budgeting.json
```

Tujuan:

Menguji kemampuan editorial distillation, selection, omission, dan compression.

Karakteristik:

```text
many true/relevant points
more information than one carousel should contain
multiple possible supporting directions
```

Engine seharusnya tidak mencoba memasukkan semua material.

Expected outcome secara umum:

```text
NEEDS_REVIEW
```

dengan substantial omission.

---

## 3. Numerical

Path:

```text
numerical/discount-trap.json
```

Tujuan:

Menguji perbedaan antara:

```text
FACT
```

dan:

```text
DERIVED
```

serta kemampuan engine menggunakan angka tanpa menciptakan data baru.

Expected outcome secara umum:

```text
NEEDS_REVIEW
```

---

## 4. Conflicting

Path:

```text
conflicting/emergency-fund-target.json
```

Tujuan:

Menguji behavior ketika beberapa source memberikan rekomendasi berbeda.

Engine tidak boleh:

```text
silently choose one source
```

Jika disagreement dapat dipertahankan secara benar, engine seharusnya tetap dapat menghasilkan carousel.

Expected outcome secara umum:

```text
NEEDS_REVIEW
```

dengan preserved nuance.

---

## 5. Insufficient

Path:

```text
insufficient/paylater-risk.json
```

Tujuan:

Menguji apakah engine mengetahui kapan evidence tidak cukup untuk memenuhi objective.

Fixture secara structural valid tetapi material tidak cukup mendukung central claim yang diminta.

Expected outcome secara umum:

```text
BLOCKED
```

Engine harus memberikan actionable upstream repair instructions.

---

## 6. Scope Too Broad

Path:

```text
scope-too-broad/personal-finance-basics.json
```

Tujuan:

Menguji apakah engine berani menolak satu objective yang mencoba memasukkan terlalu banyak domain ke dalam satu carousel.

Expected outcome secara umum:

```text
BLOCKED
```

dengan:

```text
reason_code = SCOPE_TOO_BROAD
```

atau equivalent reason code yang sesuai output contract.

---

# Mock Context

Audience, brand, dan visual context dalam fixture dapat menggunakan:

```text
mode = MOCK
```

Informasi tersebut hanya testing assumption.

Ia bukan permanent brand truth.

---

# Mock Sources

Sebagian fixture menggunakan mock/internal sources.

Source tersebut hanya dibuat agar provenance dan source-traceability behavior dapat diuji.

Mock sources:

* bukan referensi production;
* bukan rekomendasi finansial;
* tidak boleh dipindahkan ke production knowledge base;
* tidak dimaksudkan untuk merepresentasikan sumber eksternal nyata.

---

# Integration fixture

`integration/mantri-uang-brand-context.json` menguji resolusi profil brand repository. Fixture ini sengaja tidak memiliki `context` inline. Engine harus memuat `mantri-uang` dari `context_profile`, lalu menerapkan audience, voice, visual rules, dan risk policy sebagai production context.

Fixture integrasi tetap memakai material internal untuk pengujian. Jangan memperlakukannya sebagai sumber finansial production.

---

# Fixture Stability

Setelah fixture mulai digunakan sebagai test case, hindari mengubahnya hanya untuk membuat engine terlihat lebih baik.

Jika behavior engine buruk terhadap suatu fixture, prioritaskan:

```text
fix engine behavior
```

daripada:

```text
make fixture easier
```

Fixture boleh berubah jika:

* contract berubah;
* ditemukan kesalahan desain fixture;
* tujuan fixture memang direvisi.

Jika perubahan signifikan dilakukan, catat alasannya.

Visual context pada dense, numerical, conflicting, dan insufficient direvisi mengikuti production model image + text. Material, objective, dan tujuan editorial masing-masing tetap sama. Fixture sengaja tidak meminta style khusus agar default photorealistic dapat diuji. Input schema_version tetap 0.1.0; output contract kini 0.3.0. Semua fixture aktif memakai master canvas 4:5, 1080 × 1350 px.

