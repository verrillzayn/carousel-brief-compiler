### Ringkasan utama

Video ini membahas bagaimana mengatur AI coding agent melalui beberapa lapisan konteks:

**System prompt → `AGENTS.md` / `CLAUDE.md` → Skills → Documentation → Codebase → Prompt pengguna.**

Ketika kita memberi prompt, AI tidak hanya menerima prompt tersebut. Agent juga bisa menerima instruksi sistem, isi `AGENTS.md`, metadata skill, dokumentasi yang dibuka, serta bagian codebase yang dianggap relevan. Karena itu, semakin banyak konteks yang diberikan bukan berarti hasilnya otomatis semakin bagus.

Menurut pembicara, kesalahan paling umum adalah **memasukkan terlalu banyak hal ke dalam `AGENTS.md`.**

---

## 1. Fungsi masing-masing file

**System prompt** adalah instruksi paling dasar tentang bagaimana agent bekerja. Biasanya pengguna tidak mengontrol bagian ini, sehingga tidak perlu terlalu dipikirkan.

**`AGENTS.md`** adalah aturan proyek yang secara relatif sering ikut masuk ke konteks agent. Pada tool tertentu namanya bisa berbeda, misalnya `CLAUDE.md`, tetapi secara konsep fungsinya mirip: memberi agent informasi tentang proyek dan bagaimana ia harus bekerja.

Karena file ini sangat sering dibaca, isinya seharusnya hanya berupa informasi yang **benar-benar relevan secara luas**.

**Documentation** berisi aturan yang lebih detail, misalnya:

```text
docs/
├── css-conventions.md
├── react-conventions.md
├── typescript-conventions.md
├── testing.md
├── api-conventions.md
└── submitting-pr.md
```

`AGENTS.md` cukup menunjuk ke dokumentasi tersebut.

**Skills** digunakan untuk pengetahuan atau workflow yang lebih spesifik dan hanya diperlukan pada kondisi tertentu.

---

# 2. Masalah terbesar: `AGENTS.md` terlalu besar

Pembicara memberi contoh repository besar yang mempunyai `AGENTS.md` berisi ratusan baris.

Misalnya satu file mencampur:

* aturan TypeScript,
* React,
* CSS,
* API,
* testing,
* snapshot testing,
* code review,
* styling,
* aturan PR,
* repository structure,
* dan banyak aturan lainnya.

Masalahnya, ketika kamu sedang meminta AI memperbaiki API misalnya, agent tetap mendapat instruksi tentang CSS, React, snapshot testing, dan lain-lain.

Menurut video, ini menghasilkan dua masalah.

Pertama adalah **waste of context/tokens**.

Kedua, yang lebih penting, terlalu banyak instruksi dapat membuat agent lebih sulit menentukan aturan mana yang relevan.

Kyle menyebut fenomena ini sebagai semacam **context poisoning**: konteks yang sebenarnya tidak dibutuhkan malah mengganggu reasoning agent.

Contoh yang ia tunjukkan adalah `AGENTS.md` Apache Airflow sekitar **537 baris dan ±8.600 token**.

Walaupun model modern memiliki context window besar, argumennya adalah:

> Context window besar bukan berarti kita sebaiknya mengisinya sebanyak mungkin.

Semakin sedikit informasi yang relevan, semakin mudah agent fokus.

---

# 3. Prinsip utama videonya: Progressive Disclosure

Walaupun istilah tersebut tidak terlalu ditekankan secara eksplisit, seluruh pendekatannya pada dasarnya mengikuti prinsip:

> **Berikan AI sedikit informasi terlebih dahulu. Biarkan AI membuka detail ketika dibutuhkan.**

Jadi jangan membuat:

```text
AGENTS.md
  500 baris semua aturan proyek
```

Tetapi buat struktur seperti:

```text
AGENTS.md
   ↓
references
   ↓
docs/
├── react.md
├── typescript.md
├── css.md
├── testing.md
└── api.md
```

Agent mulai dari informasi umum.

Jika mengerjakan React → baca `react.md`.

Jika mengerjakan API → baca `api.md`.

Jika melakukan testing → baca `testing.md`.

Dengan demikian konteks yang dimasukkan menjadi **task-specific**.

---

# 4. Seperti apa `AGENTS.md` yang bagus?

Menurut video, isinya seharusnya sangat kecil.

Kurang lebih:

```md
# Project

Full-stack application for ...

Package manager: pnpm.

## Repository

- apps/web — frontend
- apps/api — backend

## Conventions

For web conventions:
see docs/web.md

For API conventions:
see docs/api.md

For testing:
see docs/testing.md

When submitting a PR:
see docs/submitting-pr.md
```

Jadi `AGENTS.md` bertindak seperti **index / routing layer**, bukan encyclopedia.

Ini mungkin insight paling penting dari seluruh video.

---

# 5. Jangan memasukkan “Getting Started” yang panjang

Banyak `AGENTS.md` berisi:

* install dependencies,
* setup project,
* environment configuration,
* cara menjalankan project dari nol,
* dan sebagainya.

Kyle berpendapat informasi ini biasanya tidak perlu berada di sana.

Agent umumnya bekerja di repository yang sudah di-setup.

Informasi seperti:

```bash
npm install
npm run dev
...
```

lebih cocok ditempatkan di `README.md` atau dokumentasi onboarding.

Yang perlu berada di `AGENTS.md` hanyalah hal yang tidak obvious, misalnya:

> Package manager proyek ini adalah `pnpm`, bukan `npm`.

Atau script khusus yang sangat sering diperlukan.

---

# 6. Jangan mendokumentasikan struktur folder terlalu detail

Misalnya jangan membuat:

```text
src/
  components/
    Button/
      Button.tsx
      Button.test.tsx
      Button.module.css
...
```

Karena struktur repository mudah berubah.

Akibatnya dokumentasi tersebut bisa menjadi stale.

Agent kemudian mendapat dua sumber kebenaran:

**actual repository**

vs.

**AGENTS.md yang sudah kedaluwarsa**

Itu justru bisa membuat hasil AI lebih buruk.

Karena itu, kalau ingin mendokumentasikan struktur repository, gunakan level tinggi:

```text
apps/web → frontend
apps/api → backend
packages/ui → shared UI
packages/db → database layer
```

---

# 7. Jangan meminta AI “scan repo lalu buat AGENTS.md”

Ini salah satu rekomendasi yang cukup menarik.

Kyle tidak menyarankan prompt seperti:

> Read this entire repository and create an AGENTS.md.

Karena AI kemungkinan akan menghasilkan dokumen yang sangat verbose dan mencoba memasukkan semua hal yang ditemukan.

Sebaliknya:

Mulailah dari **AGENTS.md sangat kecil**.

Kemudian biarkan aturan berkembang berdasarkan masalah nyata.

Contoh:

AI beberapa kali menulis TypeScript seperti:

```ts
as any
```

padahal tim tidak menginginkan itu.

Barulah tambahkan aturan ke:

```text
docs/typescript-conventions.md
```

Misalnya:

```md
Avoid `any` unless absolutely necessary.
Prefer explicit interfaces or inferred types.
```

Dengan kata lain:

> **Jangan mencoba memprediksi semua kesalahan AI. Dokumentasikan kesalahan setelah kesalahan itu benar-benar muncul.**

---

# 8. Gunakan error-driven configuration

Ini salah satu filosofi paling berguna dari videonya.

Workflow-nya:

```text
AI melakukan pekerjaan
        ↓
AI membuat kesalahan
        ↓
identifikasi pola kesalahan
        ↓
buat aturan
        ↓
letakkan aturan di lokasi yang tepat
        ↓
AI punya guidance untuk pekerjaan berikutnya
```

Jadi konfigurasi agent berkembang secara empiris.

Bukan:

```text
Bayangkan 500 kemungkinan AI bisa salah
↓
buat 500 aturan
```

Tetapi:

```text
AI salah
↓
catat kesalahannya
↓
tambahkan rule
```

Ini membuat aturan tetap relevan.

---

# 9. `CLAUDE.md`, `AGENTS.md`, `GEMINI.md`

Masalah lain muncul ketika developer memakai beberapa coding agent.

Misalnya:

```text
AGENTS.md
CLAUDE.md
GEMINI.md
```

Jika kita menyalin isi yang sama ke tiga file, lama-lama isinya bisa tidak sinkron.

Contohnya:

```text
AGENTS.md
Rule A
Rule B
Rule C
```

sementara:

```text
CLAUDE.md
Rule A
Rule B
Rule C
Rule D
```

Sekarang behavior agent berbeda tergantung tool.

Solusi yang direkomendasikan adalah menggunakan **symbolic link**.

Misalnya:

```text
CLAUDE.md → AGENTS.md
```

Sehingga hanya ada satu source of truth.

Untuk Unix/macOS ia memberi contoh kira-kira:

```bash
ln -s AGENTS.md CLAUDE.md
```

Untuk Windows ia menggunakan `mklink`.

Konsep pentingnya bukan command-nya, tetapi:

> Jangan maintain beberapa file instruksi yang isinya seharusnya identik.

---

# 10. Nested `AGENTS.md` untuk monorepo

Untuk project besar atau monorepo, satu `AGENTS.md` juga belum tentu ideal.

Contoh:

```text
root/
├── AGENTS.md
│
├── apps/
│   ├── web/
│   │   └── AGENTS.md
│   │
│   └── api/
│       └── AGENTS.md
```

Root `AGENTS.md`:

```text
informasi umum seluruh repository
```

Web `AGENTS.md`:

```text
React
TypeScript
frontend conventions
```

API `AGENTS.md`:

```text
backend conventions
API conventions
database rules
```

Ketika agent bekerja di bagian web, ia mendapat:

```text
root instructions
+
web instructions
```

bukan seluruh aturan backend.

Ini membuat instruction hierarchy mengikuti struktur repository.

---

# 11. Perbedaan Documentation vs Skills

Ini bagian kedua yang paling penting setelah `AGENTS.md`.

Menurut Kyle:

### Documentation

Digunakan untuk aturan yang relatif umum dan berkaitan dengan bagaimana codebase bekerja.

Misalnya:

```text
TypeScript conventions
React conventions
testing conventions
repository architecture
API style
CSS conventions
```

Agent diarahkan ke dokumen tersebut melalui `AGENTS.md`.

### Skills

Digunakan untuk tugas **spesifik atau relatif jarang dilakukan**.

Contohnya ia menyebut authentication.

Misalnya aplikasi menggunakan custom authentication yang kompleks.

Daripada memasukkan semuanya ke `AGENTS.md`:

```text
500 baris cara authentication bekerja
```

buat skill:

```text
skills/authentication/
    SKILL.md
```

Ketika agent mendapat tugas:

> Add Google login.

Barulah skill authentication dimuat.

---

# 12. Tetapi terlalu banyak Skill juga buruk

Ada nuance yang cukup penting.

Skill memang tidak selalu memuat seluruh isi `SKILL.md`.

Tetapi agent biasanya perlu mengetahui minimal:

```text
skill name
skill description
```

agar bisa menentukan skill mana yang harus digunakan.

Kalau kamu install:

```text
100 skills
```

maka metadata 100 skill tersebut tetap bisa menghabiskan context.

Jadi prinsip yang sama berlaku:

> Jangan menginstall skill hanya karena tersedia.

Install hanya skill yang benar-benar digunakan oleh project.

---

# 13. Skill sebaiknya spesifik

Skill ideal menangani satu kemampuan yang jelas.

Misalnya:

```text
authentication
database migration
API generation
UI screenshot testing
deployment
```

Bukan skill super besar:

```text
How to build everything in our application
```

Skill juga dapat dipanggil:

* otomatis oleh agent berdasarkan description,
* atau secara manual.

Jadi skill mirip **procedure / playbook on demand**.

---

# Arsitektur ideal menurut video

Kalau seluruh video disederhanakan menjadi sebuah diagram:

```text
                     USER PROMPT
                          │
                          ▼
                      AGENTS.md
                    /     |      \
                   /      |       \
                  ▼       ▼        ▼
              docs/     docs/     docs/
             React      API      Testing
                  \
                   \
                    ▼
                  SKILLS
            ┌───────────────┐
            │ Authentication│
            │ Migration     │
            │ Deployment    │
            │ etc.          │
            └───────────────┘
```

`AGENTS.md` bukan tempat seluruh knowledge.

Ia lebih seperti:

**router menuju knowledge.**

---

# Mental model paling sederhana

Menurut saya, isi video ini paling mudah diingat dengan tiga lapisan:

| Layer         | Isi                     | Kapan dibaca        |
| ------------- | ----------------------- | ------------------- |
| **AGENTS.md** | aturan global + routing | hampir selalu       |
| **Docs**      | detail conventions      | ketika relevan      |
| **Skills**    | workflow/task khusus    | saat tugas spesifik |

Contohnya:

```text
AGENTS.md
"Project ini menggunakan TypeScript.
Untuk TS conventions lihat docs/typescript.md."

docs/typescript.md
"Gunakan strict typing, hindari any, ..."

skills/authentication/SKILL.md
"Jika membuat auth flow, lakukan A → B → C..."
```

---

# Prinsip inti seluruh video

Kalau saya compress video ±24 menit ini menjadi satu kalimat:

> **Jangan mencoba membuat AI pintar dengan memberinya sebanyak mungkin instruksi; buat AI efektif dengan memberinya sesedikit mungkin informasi yang tepat pada saat informasi itu dibutuhkan.**

Dan menjadi beberapa aturan praktis:

1. **Keep `AGENTS.md` small.**
2. **Gunakan `AGENTS.md` sebagai index/router.**
3. **Pindahkan conventions ke docs.**
4. **Gunakan skills untuk workflow spesifik.**
5. **Jangan install terlalu banyak skills.**
6. **Nested `AGENTS.md` untuk monorepo.**
7. **Hindari dokumentasi detail yang cepat stale.**
8. **Jangan generate seluruh `AGENTS.md` dari repo secara otomatis.**
9. **Tambahkan rule berdasarkan kesalahan nyata AI.**
10. **Minimize context, maximize relevance.**

---

## Hal yang menurut saya sangat relevan untuk AI agent yang sedang kamu bangun

Dari konteks kamu sebelumnya tentang membangun agent yang menghasilkan JSON, copy, dan prompt visual carousel, insight video ini justru sangat applicable.

Misalnya sekarang kamu mungkin tergoda membuat satu `AGENTS.md` besar yang berisi:

```text
brand identity
copywriting rules
carousel storytelling
visual rules
typography
image prompt rules
JSON schema
research guidelines
headline rules
CTA rules
examples
negative examples
...
```

Pendekatan video ini akan menyarankan memecahnya:

```text
AGENTS.md
│
├── docs/
│   ├── brand.md
│   ├── storytelling.md
│   ├── carousel-structure.md
│   ├── copywriting.md
│   ├── visual-language.md
│   └── json-schema.md
│
└── skills/
    ├── research/
    ├── carousel-outline/
    ├── visual-reference-analysis/
    ├── image-prompt-generation/
    └── final-carousel-generation/
```

Lalu `AGENTS.md` hanya menjelaskan **kapan harus membaca apa**.

Ini kemungkinan jauh lebih efektif daripada memasukkan seluruh “otak Mantri Uang” ke satu system prompt atau satu Markdown raksasa.

Kalau kamu mau, langkah berikutnya yang menurut saya paling menarik adalah **kita bedah arsitektur AI agent carousel yang sedang kamu buat menggunakan prinsip dari video ini**, lalu menentukan secara konkret: **mana yang masuk `AGENTS.md`, mana jadi docs, mana jadi skill, mana yang justru tidak perlu diberikan ke agent sama sekali.**
