# Pipeline — Carousel Brief Engine

Dokumen ini mendefinisikan **alur kerja konseptual** `carousel-brief-engine`.

Jika:

- `README.md` menjelaskan gambaran sistem;
- `scope.md` menjelaskan batas tanggung jawab;
- `principles.md` menjelaskan prinsip pengambilan keputusan;

maka `pipeline.md` menjawab:

> **Bagaimana input bergerak melalui sistem sampai menjadi production brief atau BLOCKED output?**

Dokumen ini mendefinisikan **logical pipeline**, bukan implementation architecture.

Artinya:

- satu stage tidak harus berarti satu AI call;
- satu stage tidak harus berarti satu agent;
- beberapa stage dapat dijalankan dalam satu model execution;
- pipeline dapat dijalankan manual pada V0;
- orchestration implementation dapat berubah tanpa mengubah logical behavior.

---

# 1. Pipeline Overview

Core transformation:

```text
INPUT PACKAGE
      │
      ▼
[1] INTAKE & VALIDATION
      │
      ▼
[2] MATERIAL INTERPRETATION
      │
      ▼
[3] EDITORIAL DISTILLATION
      │
      ▼
[4] ANGLE RESOLUTION
      │
      ▼
[5] NARRATIVE ARCHITECTURE
      │
      ▼
[6] SLIDE PLANNING
      │
      ▼
[7] COPY DEVELOPMENT
      │
      ▼
[8] VISUAL DIRECTION
      │
      ▼
[9] ASSET STRATEGY
      │
      ▼
[10] PRODUCTION COMPILATION
      │
      ▼
[11] QA & VALIDATION
      │
      ├───────────────┐
      ▼               ▼
NEEDS_REVIEW        BLOCKED
````

Successful engine run berakhir pada:

```text
NEEDS_REVIEW
```

bukan `APPROVED`.

Approval diberikan melalui human review setelah engine selesai.

---

# 2. Pipeline Philosophy

Pipeline dibangun berdasarkan prinsip:

```text
UNDERSTAND
before
SELECT

SELECT
before
STRUCTURE

STRUCTURE
before
WRITE

WRITE
before
VISUALIZE

VISUALIZE
before
PRODUCE
```

Engine tidak seharusnya langsung menulis slide hanya karena raw material tersedia.

Kesalahan di stage awal akan mengalir ke seluruh downstream output.

Contoh:

```text
wrong editorial selection
        ↓
wrong narrative
        ↓
wrong slide content
        ↓
wrong visual
        ↓
beautiful but incorrect carousel
```

Karena itu, pipeline harus menyelesaikan masalah upstream sebelum mempercantik downstream.

---

# 3. Stage 0 — Context Assembly

Sebelum content reasoning dimulai, engine mengumpulkan seluruh context yang tersedia.

Engine harus lebih dulu menyelesaikan `context_profile` sesuai aturan resolusi di `SYSTEM.md`. Jika input tidak menyebut profil, gunakan profil default repository dari `contexts/defaults.json`. File profil adalah base context. Context inline dapat mengganti kategori untuk pengujian `MOCK` atau menambahkan kebutuhan khusus run `PRODUCTION`.

Context dapat terdiri dari:

```text
CORE INPUT
├── topic
├── objective
├── raw material
└── sources

OPTIONAL EDITORIAL CONTEXT
├── initial angle
├── mandatory points
├── optional points
└── exclusions

OPTIONAL AUDIENCE CONTEXT
├── audience profile
├── knowledge level
└── communication context

OPTIONAL BRAND CONTEXT
├── tone
├── voice
├── terminology
└── visual rules

OPTIONAL PRODUCTION CONTEXT
├── canvas
├── production capability
├── asset constraints
└── tool conventions
```

Context dapat berada dalam:

```text
MOCK
```

atau:

```text
PRODUCTION
```

mode.

---

# 4. Stage 0 Output

Stage ini menghasilkan **assembled working context**.

Secara konseptual:

```text
WORKING CONTEXT
│
├── objective
├── source material
├── constraints
├── available contexts
├── missing optional contexts
└── context mode
```

Tidak ada editorial decision pada tahap ini.

Tujuannya hanya memastikan engine mengetahui apa yang tersedia dan apa yang tidak tersedia.

Working context harus memuat isi profil yang sudah di-resolve. Menyimpan ID profil tanpa membaca file context belum dianggap sebagai context assembly.

---

# 5. Stage 1 — Intake & Validation

Tahap pertama pipeline adalah memeriksa apakah input layak diproses.

Engine tidak langsung membuat carousel.

Pertanyaan awal:

```text
Apakah objective tersedia?
Apakah raw material tersedia?
Apakah material relevan dengan objective?
Apakah material cukup untuk mulai reasoning?
Apakah critical source information tersedia?
Apakah ada conflict yang langsung membuat objective tidak dapat dijawab?
```

---

# 6. Input Validation Categories

Temuan validation dibagi menjadi:

```text
VALID
WARNING
FATAL
```

## VALID

Input cukup untuk melanjutkan.

## WARNING

Input memiliki kelemahan tetapi masih memungkinkan reliable output.

Contoh:

```text
tidak ada contoh konkret
visual source terbatas
supporting detail tipis
```

Pipeline lanjut.

## FATAL

Input tidak memungkinkan reliable production brief.

Contoh:

```text
objective tidak didukung material
raw material terlalu sedikit
critical claim tanpa evidence
material bertentangan secara fundamental
mandatory information hilang
```

Pipeline berhenti.

---

# 7. Early Failure Exit

Jika validation menghasilkan fatal condition:

```text
STATUS:
BLOCKED
```

Engine tidak melanjutkan ke:

```text
narrative
copy
visual
production
```

Sebagai gantinya engine menghasilkan:

```text
BLOCKED OUTPUT
│
├── reason
├── missing information
├── impact
├── recommendation
├── upstream repair instruction
└── resume condition
```

Prinsip:

> Jangan menghasilkan downstream work berdasarkan foundation yang sudah diketahui invalid.

---

# 8. Stage 2 — Material Interpretation

Jika input valid, engine mulai memahami raw material.

Tahap ini **belum memilih apa yang masuk carousel**.

Tujuan pertama adalah memetakan isi material.

Engine mengidentifikasi:

```text
main concepts
facts
numbers
claims
definitions
relationships
examples
supporting evidence
uncertainties
source disagreements
possible implications
```

---

# 9. Fact Classification

Informasi yang ditemukan harus dibedakan menjadi:

```text
FACT
DERIVED
CREATIVE
```

Pada stage ini fokus utama adalah `FACT`.

Setiap important factual claim idealnya memiliki hubungan ke source.

Contoh konseptual:

```text
CLAIM A
└── source_01

CLAIM B
└── source_02

CLAIM C
├── source_01
└── source_03
```

---

# 10. Source Conflict Detection

Pada tahap interpretation, engine mendeteksi disagreement.

Contoh:

```text
SOURCE A:
3 months emergency fund

SOURCE B:
6 months emergency fund

SOURCE C:
depends on personal condition
```

Engine tidak langsung memilih salah satu.

Conflict ditandai untuk dipertimbangkan pada tahap editorial.

---

# 11. Stage 2 Output

Conceptual output:

```text
MATERIAL MAP
│
├── facts
├── claims
├── source mapping
├── definitions
├── relationships
├── examples
├── uncertainties
├── disagreements
└── potential gaps
```

Material map menjadi dasar editorial reasoning.

---

# 12. Stage 3 — Editorial Distillation

Tahap ini adalah salah satu core stage paling penting.

Pertanyaan utama:

> **Jika audience hanya mengingat satu hal dari carousel ini, apa yang harus mereka ingat?**

Engine menentukan:

```text
CENTRAL TAKEAWAY
```

Kemudian seluruh material dievaluasi terhadap takeaway dan objective.

---

# 13. Information Classification

Material dikategorikan menjadi:

```text
MUST INCLUDE

SUPPORTING

OPTIONAL

OMIT
```

## MUST INCLUDE

Tanpa informasi ini, objective tidak dapat dipenuhi dengan benar.

## SUPPORTING

Memperjelas atau memperkuat central argument.

## OPTIONAL

Berguna tetapi tidak diperlukan.

## OMIT

Tidak diperlukan untuk carousel ini.

---

# 14. Omission Reasoning

Material dapat di-omit karena:

```text
redundant
outside objective
too detailed
weak supporting value
requires excessive context
better suited for separate content
low relevance to central takeaway
```

Engine tidak harus memasukkan informasi hanya karena informasinya benar.

---

# 15. Editorial Compression Test

Setelah selection awal, engine mengecek:

```text
Apakah central takeaway tetap benar?

Apakah audience mendapat cukup context?

Apakah nuance penting masih ada?

Apakah ada detail yang dapat dibuang lagi?

Apakah material terlalu luas untuk satu carousel?
```

Jika scope tetap terlalu besar bahkan setelah compression:

```text
SCOPE_TOO_BROAD
→ BLOCKED
```

---

# 16. Stage 3 Output

Conceptual output:

```text
EDITORIAL DISTILLATION
│
├── central takeaway
├── must include
├── supporting
├── optional
├── omitted
├── omission rationale
├── unresolved issues
└── scope assessment
```

Belum ada slide pada tahap ini.

---

# 17. Stage 4 — Angle Resolution

Setelah mengetahui apa yang sebenarnya perlu dikatakan, engine menentukan:

> **Dari sudut mana informasi ini paling efektif disampaikan?**

Input dapat menyediakan initial angle.

Namun initial angle bukan selalu final.

---

# 18. Angle Evaluation

Angle dievaluasi berdasarkan:

```text
objective alignment
factual support
clarity
editorial focus
carousel suitability
narrative potential
visual potential
audience accessibility
```

Engine dapat:

```text
KEEP INITIAL ANGLE
```

atau:

```text
REFRAME INITIAL ANGLE
```

atau:

```text
SELECT NEW ANGLE
```

selama objective tidak berubah.

---

# 19. Angle Transparency

Jika angle berubah, perubahan harus terlihat.

Contoh:

```text
INITIAL ANGLE:
Cara mulai dana darurat dari nominal kecil.

SELECTED ANGLE:
Dana darurat bukan soal punya banyak uang,
tetapi soal memiliki buffer.

REASON:
Selected angle membuat central takeaway lebih jelas
dan lebih mudah dikembangkan sebagai carousel.
```

---

# 20. Angle Alternatives

Engine boleh mempertimbangkan beberapa angle secara internal.

Namun final brief tidak perlu membebani reviewer dengan option dump.

Ideal:

```text
SELECTED ANGLE
```

Bukan daftar panjang kemungkinan angle.

---

# 21. Stage 4 Output

```text
EDITORIAL DIRECTION
│
├── objective
├── central takeaway
├── selected angle
├── angle rationale
└── relevant constraints
```

Setelah tahap ini, sistem sudah tahu:

```text
WHAT
+
WHY
+
FROM WHAT ANGLE
```

Baru kemudian narrative dibuat.

---

# 22. Stage 5 — Narrative Architecture

Narrative architecture menentukan bagaimana audience bergerak dari:

```text
initial attention
```

menuju:

```text
understanding
```

kemudian:

```text
takeaway
```

---

# 23. Narrative Is Not a Fixed Template

Engine tidak harus selalu menghasilkan:

```text
HOOK
PROBLEM
EXPLANATION
EXAMPLE
CONCLUSION
```

Narrative dipilih berdasarkan content.

Contoh struktur:

```text
HOOK
↓
PROBLEM
↓
REFRAME
↓
EXPLANATION
↓
EXAMPLE
↓
TAKEAWAY
```

atau:

```text
MYTH
↓
REALITY
↓
MECHANISM
↓
IMPLICATION
```

atau:

```text
QUESTION
↓
ANSWER
↓
WHY
↓
EXAMPLE
↓
ACTION
```

---

# 24. Narrative Stage Questions

Engine mengevaluasi:

```text
Apa yang audience perlu tahu terlebih dahulu?

Informasi mana yang membutuhkan context?

Di mana curiosity dibangun?

Di mana claim utama dijelaskan?

Di mana example dibutuhkan?

Apa ending paling natural?

Apakah CTA diperlukan?
```

---

# 25. Narrative Coherence

Setiap bagian harus memiliki hubungan logis.

Engine harus dapat menjelaskan:

```text
WHY slide B follows slide A
```

Narrative tidak boleh hanya berupa sekumpulan fakta yang kebetulan berada dalam satu carousel.

---

# 26. Stage 5 Output

```text
NARRATIVE PLAN
│
├── narrative type
├── opening function
├── progression
├── climax / key explanation
├── ending function
└── preliminary slide roles
```

Belum perlu final copy.

---

# 27. Stage 6 — Slide Planning

Narrative kemudian dipecah menjadi unit slide.

Setiap slide memiliki:

```text
role
purpose
core message
relationship to surrounding slides
```

Contoh:

```text
SLIDE 1
role: hook

SLIDE 2
role: context

SLIDE 3
role: explanation

SLIDE 4
role: example

SLIDE 5
role: takeaway
```

---

# 28. Slide Count Resolution

Default:

```text
5–7 slides
```

Hard maximum:

```text
10 slides
```

Jumlah slide ditentukan setelah narrative diketahui.

Bukan sebelum narrative dibangun.

---

# 29. One Core Message Test

Setiap slide menjalani test:

> Dapatkah isi slide diringkas menjadi satu core message?

Jika tidak:

```text
simplify
split
or restructure
```

Supporting copy boleh menambah explanation tetapi tidak boleh membawa argument baru.

---

# 30. Density Resolution

Jika slide terlalu padat, urutan respons:

```text
1. remove unnecessary detail
2. simplify language
3. split content
4. restructure surrounding slides
```

Jika seluruh narrative melampaui hard maximum setelah optimisasi:

```text
BLOCKED
```

---

# 31. Stage 6 Output

```text
SLIDE ARCHITECTURE
│
├── total slide count
│
└── slides
    ├── index
    ├── role
    ├── purpose
    ├── core message
    └── narrative dependency
```

Pada tahap ini carousel secara editorial sudah terbentuk, tetapi belum production-ready.

---

# 32. Stage 7 — Copy Development

Setelah message setiap slide resolved, engine menulis final-ish copy.

Urutan ini penting:

```text
message first
copy second
```

Bukan sebaliknya.

---

# 33. Copy Components

Copy per slide disusun sebagai satu atau lebih display-copy block. Setiap block dapat berfungsi sebagai:

```text
context
focal statement
explanation
label
list
transition
CTA
```

Daftar tersebut bukan template wajib. Jangan memaksa setiap slide menjadi headline besar yang selalu diikuti supporting line kecil.

Setiap block harus menetapkan:

```text
reading order
attention priority
typographic scale
weight
alignment
color
placement
optional relation to visual
```

Reading order dan attention priority dapat berbeda. Focal statement disarankan ketika berguna, tetapi tidak wajib dan tidak selalu memuat seluruh pesan slide.

---

# 34. Copy Goals

Copy harus:

```text
clear
concise
accurate
readable
aligned with the slide message
compatible with visual layout
written for scanning on a slide
```

Jika brand context tersedia, copy juga harus:

```text
on-brand
```

---

# 35. Copy Compression

Jika copy terlalu panjang:

```text
remove
simplify
split
```

Engine tidak menyelesaikan masalah dengan membuat layout penuh teks.

Sentence fragment diperbolehkan jika lebih mudah dilihat, diingat, dan dipahami tanpa mengubah makna. Kepadatan dinilai dari keseluruhan komposisi, bukan batas kata yang kaku.

---

# 36. Cover Copy

Cover biasanya berfungsi sebagai hook.

Hook dapat menggunakan:

```text
question
contrast
provocative statement
unexpected framing
specific number
tension
```

selama tidak misleading.

Cover adalah hook slide. Ia dapat memakai beberapa block, misalnya context kecil yang dibaca lebih dulu dan focal question yang menarik perhatian lebih dulu.

---

# 37. Slide Message and Display Copy

`core_message` menjelaskan apa yang perlu dipahami audience. Display copy tidak harus menyalin kalimat tersebut secara utuh.

Setiap slide harus menyampaikan message atau menjalankan fungsi naratif yang diperlukan. Definition-only slide sebaiknya menambahkan relevance atau implication, atau digabung ke slide lain. Transition slide boleh membawa sedikit informasi baru jika membangun tension atau pacing yang diperlukan.

Jika display copy berubah menjadi ringkasan artikel atau membutuhkan beberapa paragraf, ada masalah pada:

```text
selection
message
or slide architecture
```

---

# 38. Caption Development

Setelah carousel copy cukup matang, engine menghasilkan satu short caption.

Caption dapat berupa:

```text
commentary
question
CTA
additional hook
short contextual note
```

Caption tidak boleh menyimpan informasi penting yang hilang dari carousel.

---

# 39. Stage 7 Output

```text
COPY PLAN
│
├── slides
│   ├── core message
│   └── display-copy blocks
│       ├── semantic role
│       ├── text
│       ├── reading order
│       ├── attention priority
│       ├── typography
│       └── placement
│
└── caption
```

---

# 40. Stage 8 — Visual Direction

Setelah message dan copy diketahui, engine menentukan bagaimana setiap slide harus divisualisasikan.

Pertanyaan utama:

> **Apa visual paling efektif untuk membantu audience memahami atau merasakan message ini?**

---

# 41. Visual Function Resolution

Untuk setiap slide, tentukan fungsi visual:

```text
EXPLAIN
COMPARE
DEMONSTRATE
SYMBOLIZE
CONTEXTUALIZE
ATTRACT_ATTENTION
DECORATIVE
```

`DECORATIVE` valid tetapi bukan default.

---

# 42. Visual Concept Generation

Engine dapat mengeksplor beberapa visual internally.

Namun output sebaiknya memiliki:

```text
PRIMARY VISUAL CONCEPT
```

Primary harus menjadi resolved execution path.

---

# 43. Visual Concept Test

Primary visual dievaluasi berdasarkan:

```text
message relevance
clarity
production feasibility
visual interest
brand compatibility
composition potential
risk of misleading interpretation
```

Visual yang menarik tetapi tidak berhubungan dengan message tidak otomatis dianggap baik.

---

# 44. Literal vs Metaphorical Visual

Engine dapat memilih:

```text
literal
metaphorical
environmental
decorative
```

berdasarkan message.

Contoh:

```text
MESSAGE:
pengeluaran kecil terus-menerus mengurangi cashflow

VISUAL:
dompet dengan beberapa kebocoran kecil
```

Metaphor valid jika mudah dipahami.

---

# 45. Minimal Visual Cases

Jika slide seperti conclusion sulit divisualisasikan:

```text
minimal environmental photo
photographed texture
simple photographic object
architectural image
```

dapat digunakan.

Engine tidak perlu memaksakan metaphor kompleks.

---

# 46. Composition Planning

Visual direction harus mempertimbangkan layout sejak awal.

Contoh properties:

```text
hero position
text zone
negative space
foreground/background
subject scale
visual balance
crop
framing
```

Tujuannya agar generated/source asset dapat langsung digunakan dalam design.

---

# 47. Stage 8 Output

```text
VISUAL PLAN
│
└── each slide
    ├── visual function
    ├── primary concept
    ├── subject
    ├── scene
    ├── composition
    ├── text zone
    ├── negative space
    ├── background
    ├── framing
    ├── visual hierarchy
    └── editing treatment
```

---

# 48. Stage 9 — Asset Strategy

Setelah visual concept resolved, engine menentukan **bagaimana visual tersebut sebaiknya diproduksi**.

Supported V0 strategies:

```text
AI_SYNTHETIC
REAL_ASSET
HYBRID_COMPOSITE
```

---

# 49. Asset Strategy Decision

Decision mempertimbangkan:

```text
real-world specificity
documentary requirement
visual complexity
production effort
generation feasibility
editing feasibility
accuracy risk
```

---

# 50. Real Entity Rule

Jika visual merepresentasikan:

```text
real person
real company
real event
documentary occurrence
```

maka:

```text
REAL_ASSET preferred
```

AI synthetic tidak boleh digunakan sedemikian rupa sehingga terlihat seperti documentary evidence palsu.

---

# 51. AI Synthetic Rule

`AI_SYNTHETIC` paling sesuai untuk:

```text
generic scenes
photorealistic conceptual scene
symbolic objects
visual metaphors
fictional examples
```

---

# 52. Hybrid Composite Rule

Pilih `HYBRID_COMPOSITE` jika visual terbaik membutuhkan kombinasi.

Contoh:

```text
real subject
+
AI-generated photorealistic background
+
light image compositing
```

atau:

```text
real product
+
generated environment
+
manual typography
```

---

# 53. Image Asset Planning Rule

Carousel menggunakan image + text. Visual utama harus image-led; AI-generated image default-nya realistic/photorealistic, terlihat seperti foto nyata. Untuk konsep atau scene generic, prioritaskan AI-generated photorealistic image. Style lain hanya jika input memintanya secara eksplisit; topik edukasi bukan alasan otomatis untuk cartoon, vector/flat illustration, atau illustrated infographic.

Untuk real person, real company, real event, atau documentary evidence, prioritaskan REAL_ASSET. HYBRID_COMPOSITE digunakan jika perlu kombinasi image asset atau compositing ringan; menambahkan text ke image saja tidak membuat strategy menjadi hybrid.

Registry hanya berisi image asset AI_GENERATED atau REAL_ASSET. Text, angka, dan label tetap berada di slide copy/design instructions, bukan asset registry. Visual yang dipilih harus mengikuti batas ini.

---

# 54. Real Asset Requirement

Jika `REAL_ASSET` dipilih, engine mendefinisikan requirement.

Contoh:

```text
ASSET REQUIRED:
real photo of subject

PREFERRED:
waist-up
clear silhouette
high resolution
neutral lighting
easy background separation

INTENDED USE:
right-bottom hero element
```

Engine tidak mencari file tersebut pada V0.

---

# 55. Stage 9 Output

```text
ASSET PLAN
│
└── each slide
    ├── asset strategy
    ├── required assets
    ├── asset specification
    ├── source/generate designation
    └── production complexity
```

---

# 56. Stage 10 — Production Compilation

Stage ini mengubah editorial + visual plan menjadi **actionable production brief**.

Di sinilah engine berpindah dari:

```text
creative planning
```

menjadi:

```text
execution planning
```

---

# 57. Image Prompt Compilation

Untuk asset dengan strategy:

```text
AI_SYNTHETIC
```

atau AI-generated component dalam:

```text
HYBRID_COMPOSITE
```

engine menghasilkan image prompt.

Prompt berasal dari visual specification, bukan dibuat terpisah.

---

# 58. Image Prompt Requirements

Prompt dapat mencakup:

```text
subject
action
scene
composition
position
framing
camera
background
lighting
negative space
text-safe area
visual treatment
undesired elements
```

Prompt harus memperhitungkan final layout.

---

# 59. Typography Rule for Generated Assets

Default:

```text
DO NOT GENERATE MAIN TYPOGRAPHY
```

Image generator membuat asset.

Design tool menambahkan informational text.

Pengecualian hanya jika text merupakan bagian alami dari photographed object dan memang dibutuhkan.

---

# 60. Global Production Direction

Engine menghasilkan instruction yang berlaku untuk seluruh carousel.

Contoh:

```text
- gunakan canvas 4:5
- jaga visual hierarchy
- hindari generated typography
- pastikan text readability
- pertahankan treatment cohesive
- jangan memenuhi seluruh frame dengan asset
```

Global rule tidak perlu diulang pada setiap slide.

---

# 61. Per-Slide Production Instruction

Setiap slide kemudian memiliki actionable sequence.

Contoh:

```text
SLIDE 03

1. Buka platform yang biasa digunakan untuk generate gambar.
2. Copy dan paste image prompt.
3. Generate beberapa output.
4. Pilih hasil dengan subject berada di kanan bawah.
5. Simpan asset.
6. Buka Canva.
7. Import asset.
8. Position asset sesuai visual specification.
9. Tambahkan display-copy blocks sesuai reading order dan attention priority.
10. Terapkan typography, placement, dan relation to visual yang ditetapkan.
11. Pastikan text zone tetap bersih.
12. Lakukan crop ringan jika diperlukan.
```

Instruksi:

```text
tool-agnostic
but
operationally specific
```

---

# 62. Hybrid Production Instruction

Untuk `HYBRID_COMPOSITE`, sequence dapat berupa:

```text
1. Ambil real asset yang telah disediakan.
2. Remove background.
3. Generate background menggunakan prompt.
4. Import kedua asset ke Canva.
5. Layer real subject di foreground.
6. Sesuaikan scale.
7. Atur opacity atau gradient ringan hanya jika dibutuhkan untuk readability.
8. Tambahkan copy.
9. Review visual hierarchy.
```

---

# 63. Design Tool Boundary

Canva/design tool digunakan untuk display-copy blocks, typography, crop, resize/reposition image, remove background bila perlu, gradient ringan untuk readability, opacity, dan layering sederhana image + text.

Engine tidak merencanakan custom graphic components, icon system, Canva shapes sebagai visual utama, diagram manual, decorative graphic composition, atau illustrated infographic components. Larangan ini juga berlaku di asset requirements, prompts, dan production instructions; jangan menyamarkan komponen grafis sebagai AI_GENERATED atau REAL_ASSET. Manusia boleh mengimprovisasi graphic embellishment saat desain, tetapi itu di luar tanggung jawab dan output engine.

---

# 64. Production Feasibility Check

Sebelum final brief selesai, engine bertanya:

```text
Apakah instruction dapat dilakukan dengan available resources?

Apakah visual terlalu kompleks?

Apakah image-generation requirement realistis?

Apakah manual editing terlalu berat?

Apakah ada simpler execution yang hampir sama efektif?
```

Jika konsep sangat sulit diproduksi, simplify sebelum compilation.

---

# 65. Stage 10 Output

```text
PRODUCTION PLAN
│
├── global production direction
│
└── slides
    ├── final copy
    ├── visual specification
    ├── asset strategy
    ├── asset requirement
    ├── image prompt
    └── production steps
```

---

# 66. Stage 11 — QA & Validation

Sebelum brief keluar dari engine, keseluruhan output diperiksa ulang.

QA bukan hanya grammar check.

QA memastikan setiap upstream decision tetap konsisten setelah seluruh downstream work selesai.

---

# 67. QA Dimensions

Minimal evaluasi mencakup:

```text
OBJECTIVE
FACT
EDITORIAL
NARRATIVE
DENSITY
COPY
VISUAL
ASSET
PRODUCTION
SOURCE
BRAND
```

---

# 68. Objective QA

Pertanyaan:

```text
Apakah carousel benar-benar memenuhi objective?

Apakah angle tetap sesuai objective?

Apakah narrative menyimpang?
```

---

# 69. Factual QA

Pertanyaan:

```text
Apakah ada fakta yang tidak berasal dari input?

Apakah derived claim valid?

Apakah uncertainty dipertahankan?

Apakah source conflict disajikan dengan benar?

Apakah headline melebih-lebihkan evidence?
```

---

# 70. Editorial QA

Pertanyaan:

```text
Apakah central takeaway jelas?

Apakah masih ada information overload?

Apakah ada detail yang seharusnya di-omit?

Apakah carousel mencoba membahas terlalu banyak hal?
```

---

# 71. Narrative QA

Pertanyaan:

```text
Apakah slide memiliki urutan logis?

Apakah setiap slide diperlukan?

Apakah transition masuk akal?

Apakah ending menyelesaikan promise cover?
```

---

# 72. Density QA

Pertanyaan:

```text
Apakah satu slide membawa terlalu banyak konsep?

Apakah copy terlalu padat?

Apakah layout berpotensi menjadi paragraph-heavy?
```

Jika ya:

```text
revise
before output
```

---

# 73. Visual QA

Periksa primary visual: visual utama image-led, default AI photorealistic kecuali input meminta style lain, dan tidak ada graphic component yang disamarkan sebagai image.

Pertanyaan:

```text
Apakah visual memperkuat message?

Apakah metaphor mudah dipahami?

Apakah visual misleading?

Apakah terlalu banyak decorative visual?

Apakah visual variety masih cohesive?
```

---

# 74. Production QA

Periksa bahwa registry hanya AI_GENERATED/REAL_ASSET, strategy hanya AI_SYNTHETIC/REAL_ASSET/HYBRID_COMPOSITE, text berada di copy, dan instruksi Canva sebatas editing image + text. Graphic embellishment manusia tidak boleh menjadi rencana atau dependency output engine.

Pertanyaan:

```text
Apakah production instruction cukup jelas?

Apakah asset strategy realistis?

Apakah prompt sesuai composition?

Apakah operator masih harus mengambil fundamental creative decision?
```

Jika jawabannya ya untuk pertanyaan terakhir, brief belum selesai.

---

# 75. Source QA

Important factual claims harus memiliki traceability yang cukup.

Jika required source mapping hilang pada critical claim:

```text
repair
```

atau jika tidak mungkin:

```text
BLOCKED
```

---

# 76. Brand QA

Jika production brand context tersedia:

```text
Apakah tone sesuai?
Apakah vocabulary sesuai?
Apakah visual constraints dipatuhi?
```

Brand tidak boleh override factual integrity.

---

# 77. Warning Compilation

Non-fatal problems yang masih ada dikompilasi menjadi warning.

Contoh:

```text
WARNING:
Slide 5 menggunakan decorative visual karena
tidak ditemukan visual metaphor sederhana yang
meningkatkan komunikasi.
```

atau:

```text
WARNING:
Material tidak menyediakan concrete example.
```

Warnings harus berguna bagi reviewer.

---

# 78. Final Failure Check

Setelah QA, engine menentukan:

```text
Can this production brief be responsibly reviewed and produced?
```

Jika:

```text
YES
```

→ `NEEDS_REVIEW`

Jika:

```text
NO
```

→ `BLOCKED`

---

# 79. Successful Exit

Successful output:

```text
STATUS:
NEEDS_REVIEW
```

Artinya:

```text
engine work complete
human judgment required
production not yet authorized
```

---

# 80. Production Brief Handoff

Production brief kemudian diserahkan ke:

```text
CONTENT REVIEWER
```

Reviewer mengevaluasi:

```text
factual presentation
editorial direction
narrative
copy
visual direction
production feasibility
```

---

# 81. Review Outcomes

Human review dapat menghasilkan:

```text
APPROVED
```

atau:

```text
REVISION_REQUIRED
```

---

# 82. APPROVED Flow

Jika approved:

```text
NEEDS_REVIEW
      ↓
APPROVED
      ↓
PRODUCTION
```

Production berada di luar core engine.

---

# 83. REVISION_REQUIRED Flow

Jika reviewer meminta perubahan:

```text
NEEDS_REVIEW
      ↓
REVISION_REQUIRED
      ↓
REVISION INPUT
      ↓
ENGINE
```

Revision dapat bersifat global atau lokal.

---

# 84. Local Revision

Contoh:

```text
“Visual slide 4 terlalu generik.
Cari visual concept lain.”
```

Engine dapat hanya merevisi slide terkait.

Namun harus memeriksa:

```text
slide 3 → slide 4 transition
slide 4 → slide 5 transition
overall narrative coherence
```

---

# 85. Global Revision

Contoh:

```text
“Angle terlalu akademik.”
```

Perubahan seperti ini dapat memengaruhi seluruh downstream pipeline.

Engine harus kembali ke stage yang relevan.

Contoh:

```text
ANGLE REVISION
      ↓
Narrative Architecture
      ↓
Slide Planning
      ↓
Copy
      ↓
Visual
      ↓
Production
      ↓
QA
```

---

# 86. Revision Should Restart at the Correct Stage

Tidak semua revision harus menjalankan seluruh pipeline dari awal.

Prinsip:

```text
restart from
the earliest affected stage
```

Contoh:

```text
typo fix
→ copy stage

visual concept change
→ visual stage

asset strategy change
→ asset stage

angle change
→ angle stage

objective change
→ new run / upstream change
```

---

# 87. Dependency Logic

Pipeline memiliki dependency tree.

Secara sederhana:

```text
OBJECTIVE
    ↓
MATERIAL
    ↓
EDITORIAL SELECTION
    ↓
ANGLE
    ↓
NARRATIVE
    ↓
SLIDE MESSAGE
    ↓
COPY
    ↓
VISUAL
    ↓
ASSET
    ↓
PRODUCTION
```

Jika upstream decision berubah, downstream decision harus dianggap potentially stale.

---

# 88. Do Not Repair Downstream Symptoms Upstream Problems Create

Contoh:

```text
copy terlalu panjang
```

jangan langsung diasumsikan sebagai copywriting problem.

Bisa jadi:

```text
slide message terlalu luas
```

atau:

```text
editorial selection terlalu banyak
```

Pipeline harus mencari **earliest cause**.

---

# 89. Stage Ownership

Logical ownership:

```text
STAGE 0
Context Assembly

STAGE 1
Input Validity

STAGE 2
Material Understanding

STAGE 3
Editorial Selection

STAGE 4
Angle

STAGE 5
Story

STAGE 6
Slide Structure

STAGE 7
Language

STAGE 8
Visual Communication

STAGE 9
Asset Method

STAGE 10
Execution

STAGE 11
Quality Assurance
```

---

# 90. Pipeline State Model

Conceptual states:

```text
RECEIVED
    ↓
VALIDATING
    ↓
PROCESSING
    ↓
NEEDS_REVIEW
```

Possible terminal deviation:

```text
BLOCKED
```

Human-controlled states:

```text
APPROVED
REVISION_REQUIRED
```

V0 implementation tidak wajib menyimpan semua intermediate state.

State model hanya mendefinisikan lifecycle semantics.

---

# 91. V0 Execution Model

Logical pipeline **tidak berarti** V0 harus mempunyai 12 separate prompt calls.

V0 dapat dijalankan sebagai:

```text
one interactive AI session
```

atau:

```text
one structured compile command
```

selama logical stages tetap dihormati.

---

# 92. Example V0 Execution

Misalnya melalui Claude Code/Codex:

```text
/compile-brief fixtures/dana-darurat.json
```

AI membaca:

```text
system rules
scope
principles
input
```

kemudian menjalankan logical pipeline dan menghasilkan:

```text
output/brief.md
output/brief.json
```

Ini hanya contoh implementation direction, bukan contract V0 yang sudah final.

---

# 93. Pipeline vs Prompt Architecture

Jangan menyamakan:

```text
logical stage
```

dengan:

```text
prompt file
```

Contoh:

```text
Editorial Distillation
Angle Resolution
Narrative Architecture
```

dapat berada dalam satu prompt selama behavior stabil.

Jika nanti evaluation menunjukkan hasil lebih baik jika dipisah, implementation dapat berubah.

---

# 94. Pipeline vs Agent Architecture

Jangan menyamakan:

```text
Visual Director
```

sebagai logical responsibility dengan:

```text
Visual Director Agent
```

V0 tidak membutuhkan agent identity.

Gunakan stage sebagai:

```text
responsibility boundary
```

bukan architecture requirement.

---

# 95. Automation Boundary

Pipeline harus dapat berjalan tanpa n8n.

Future orchestration mungkin:

```text
new input
↓
n8n
↓
run engine
↓
validate structured output
↓
save files
↓
notify reviewer
```

Tetapi automation hanya membungkus pipeline.

Automation tidak mendefinisikan reasoning pipeline.

---

# 96. Pipeline Invariants

Terlepas dari implementation, urutan dependency berikut harus dipertahankan:

```text
validate before creating

understand before selecting

select before structuring

structure before writing

know the message before choosing visual

know the visual before choosing asset strategy

know the asset strategy before writing production instructions

validate before handoff
```

---

# 97. Pipeline Anti-Patterns

Engine harus menghindari:

```text
RAW MATERIAL
↓
immediately write carousel
```

---

```text
RAW MATERIAL
↓
generate image prompts
↓
figure out message later
```

---

```text
write long copy
↓
try to squeeze it into slides
```

---

```text
generate many creative options
↓
ask human to choose everything
```

---

```text
input invalid
↓
continue anyway
```

---

# 98. Pipeline Success Criteria

Pipeline dianggap berfungsi dengan baik jika:

```text
raw material
```

berubah menjadi:

```text
clear editorial decision
+
coherent narrative
+
low-density slide structure
+
production-ready copy
+
meaningful visual direction
+
appropriate asset strategy
+
executable production instructions
```

tanpa:

```text
invented facts
unnecessary complexity
information dumping
decision dumping
```

---

# 99. Pipeline Failure Criteria

Pipeline dianggap gagal jika hasil membutuhkan production operator untuk kembali melakukan pekerjaan seperti:

```text
menentukan angle dari nol
memilih informasi utama
menentukan urutan cerita
menulis ulang semua copy
menentukan visual dari nol
menentukan asset production strategy
membuat prompt sendiri dari nol
```

Jika hal-hal tersebut masih diperlukan, compilation belum selesai.

---

# 100. V0 Pipeline Summary

```text
┌───────────────────────────────┐
│          INPUT PACKAGE        │
└───────────────┬───────────────┘
                ▼
       Context Assembly
                ▼
       Intake Validation
                │
        fatal? ─┴──────► BLOCKED
                │
                ▼
      Material Interpretation
                ▼
      Editorial Distillation
                │
     too broad? ┴──────► BLOCKED
                │
                ▼
        Angle Resolution
                ▼
    Narrative Architecture
                ▼
        Slide Planning
                ▼
       Copy Development
                ▼
       Visual Direction
                ▼
        Asset Strategy
                ▼
    Production Compilation
                ▼
          Final QA
                │
        fatal? ─┴──────► BLOCKED
                │
                ▼
         NEEDS_REVIEW
                ▼
          Human Review
          ┌─────┴─────┐
          ▼           ▼
      APPROVED    REVISION_REQUIRED
          │           │
          ▼           └────► earliest affected stage
      PRODUCTION
```

---

# 101. Final Pipeline Rule

Pipeline dapat diringkas dengan satu prinsip:

> **Do not make a downstream decision before the upstream decision it depends on is sufficiently resolved.**

`carousel-brief-engine` bukan sekadar sequence untuk menghasilkan file.

Pipeline adalah mekanisme untuk memastikan bahwa setiap keputusan produksi memiliki foundation editorial yang jelas:

```text
evidence
↓
meaning
↓
selection
↓
story
↓
slide
↓
copy
↓
visual
↓
asset
↓
execution
```

Itulah urutan reasoning yang harus dipertahankan bahkan jika implementation V0 nantinya hanya menggunakan satu model, satu command, dan satu execution session.

