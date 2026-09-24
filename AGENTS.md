# Carousel Brief Engine

Repository ini adalah source of truth untuk kontrak dan perilaku `carousel-brief-engine`. Repository dipakai untuk dua jenis pekerjaan: mengembangkan sistem dan menjalankan sistem untuk mengompilasi brief carousel.

## Tentukan mode kerja lebih dahulu

Klasifikasikan permintaan dari deliverable yang diminta sebelum bertindak. Penyebutan kata "carousel" saja tidak menentukan mode.

- **Pengembangan repository** berlaku ketika pengguna meminta perubahan, diagnosis, review, atau perancangan terhadap sistem, dokumentasi, schema, context, fixture, expected behavior, atau evaluasi. Dalam mode ini, perlakukan `SYSTEM.md` sebagai artefak spesifikasi yang sedang dianalisis atau diedit. Aturan seperti identitas engine, `JSON only`, dan status output di dalamnya bukan format respons coding agent.
- **Kompilasi carousel** berlaku ketika pengguna meminta input content dikompilasi menjadi production brief. Baca `SYSTEM.md` dan seluruh authoritative files yang diwajibkannya sebelum menjalankan pipeline. Hasil harus mengikuti kontrak output engine.
- **Pekerjaan campuran** dijalankan per tahap. Terapkan aturan pengembangan saat mengubah sistem, lalu aturan kompilasi saat menguji sistem dengan sebuah input.

Jika permintaan tetap ambigu dan pilihan mode akan menghasilkan deliverable yang berbeda, tanyakan satu pertanyaan singkat sebelum membuat perubahan atau mengompilasi output.

## Router pengembangan

Baca hanya dokumen yang relevan dengan perubahan:

- Arsitektur produk, boundary umum, dan keputusan desain: bagian terkait di `README.md`.
- Kontrak runtime dan aturan yang selalu berlaku pada kompilasi: `SYSTEM.md`.
- Scope atau boundary engine: `docs/scope.md`.
- Aturan editorial dan standar kualitas: `docs/principles.md`.
- Struktur copy, panjang relatif antar-block, line break, text zone, dan spacing: `docs/copy-composition.md`.
- Urutan proses dan dependency antartahap: `docs/pipeline.md`.
- Sistem visual dan pemilihan visual family: `docs/visual-language.md`. Buka `references/visuals/` hanya saat tugas menyentuh sumber referensi visual atau derivasi playbook.
- Struktur input, output, atau profil context: schema terkait di `schemas/`.
- Perubahan fixture atau pengujian perilaku: `fixtures/README.md`, `expected-behavior/README.md`, lalu hanya kasus yang relevan.
- Resolusi brand context: `contexts/defaults.json`, `schemas/context-profile.schema.json`, dan pasangan profil yang relevan di `contexts/brands/`.

`runs/` dan `evaluation-result/` berisi hasil historis. Jangan jadikan keduanya sumber kontrak aktif atau memperbaruinya secara massal saat kontrak berubah, kecuali pengguna memang meminta migrasi atau regenerasi arsip.

## Aturan perubahan

- Temukan source of truth untuk perilaku yang diubah sebelum mengedit.
- Pertahankan satu sumber aturan. Gunakan pointer ke dokumen detail, bukan menyalin isinya ke file lain.
- Untuk perubahan perilaku atau kontrak, periksa dampaknya pada `SYSTEM.md`, dokumen terkait, schema, fixture aktif, dan expected behavior. Ubah hanya bagian yang maknanya ikut berubah.
- Nilai expected behavior berdasarkan perilaku, bukan wording exact. Jangan melonggarkan fixture atau expectation hanya untuk menyembunyikan kegagalan model.
- Perlakukan file JSON sebagai kontrak mesin. Jaga referential integrity dan validasi file yang berubah terhadap schema yang relevan.
- Pertahankan perubahan pengguna yang tidak terkait dan batasi edit pada scope permintaan.

## Pemeliharaan instruksi agent

Jaga file ini sebagai router kecil. Tambahkan aturan global hanya setelah ada kebutuhan nyata yang berulang. Taruh convention rinci di dokumentasi dan workflow khusus yang jarang dipakai di skill. Hindari menyalin instruksi yang sudah dapat ditemukan langsung dari codebase atau konfigurasi.
