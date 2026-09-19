
# Carousel Brief Engine

`carousel-brief-engine` adalah sistem internal untuk mengubah **raw material hasil riset** menjadi **production brief carousel edukasi keuangan** yang cukup detail untuk langsung masuk ke tahap produksi.

Sistem ini tidak bertujuan membuat final design secara otomatis. Fokus utamanya adalah menyelesaikan keputusan editorial dan creative-production sebelum proses desain dimulai.

Secara sederhana:

```text
Raw Material
    ↓
Editorial Distillation
    ↓
Angle Selection
    ↓
Narrative Architecture
    ↓
Slide Planning
    ↓
Copy
    ↓
Visual Direction
    ↓
Asset Strategy
    ↓
Image Prompt
    ↓
Production Instructions
    ↓
Production Brief
    ↓
Human Review
    ↓
Production
```

---

## Why This Exists

Project ini lahir dari satu masalah utama dalam proses pembuatan carousel:

> Banyak informasi yang tersedia, tetapi ruang dalam carousel terbatas.

Masalahnya bukan sekadar bagaimana menulis lebih pendek.

Sistem harus mampu menentukan:

* apa yang benar-benar penting;
* apa yang perlu dibuang;
* bagaimana materi disusun menjadi narrative;
* apa pesan utama setiap slide;
* bagaimana pesan tersebut ditulis secara ringkas;
* bagaimana pesan tersebut divisualisasikan;
* jenis asset apa yang paling sesuai;
* bagaimana asset tersebut diproduksi;
* dan bagaimana keseluruhan carousel dapat dieksekusi tanpa membutuhkan banyak keputusan kreatif tambahan.

Karena itu, `carousel-brief-engine` bukan sekadar text summarizer atau image prompt generator.

Ia berfungsi sebagai **production brief compiler**.

---

# Core Responsibility

Satu eksekusi sistem menerima material untuk **satu topik/content unit** dan menghasilkan **satu carousel lengkap**.

Unit kerja sistem adalah:

```text
1 input package
    ↓
1 editorial direction
    ↓
1 carousel
    ↓
N slides
    ↓
1 production brief
```

Sistem bertanggung jawab untuk:

1. memahami raw material;
2. menemukan core takeaway;
3. memilih informasi yang benar-benar diperlukan;
4. membuang informasi sekunder;
5. menentukan editorial angle;
6. merancang narrative carousel;
7. menentukan fungsi setiap slide;
8. menulis copy setiap slide;
9. menentukan konsep visual;
10. menentukan asset strategy;
11. menghasilkan image prompt jika diperlukan;
12. memberikan production instructions;
13. menghasilkan caption singkat;
14. melakukan QA terhadap output;
15. memberikan warning atau memblokir proses jika material tidak memadai.

---

# What This System Is Not

`carousel-brief-engine` **bukan**:

* sistem untuk melakukan primary research;
* topic discovery engine;
* social media strategy engine;
* brand strategy engine;
* image generation platform;
* asset search engine;
* Canva automation;
* publishing system;
* social media scheduler;
* analytics engine;
* end-to-end autonomous content agent.

Komponen-komponen tersebut dapat berada sebelum atau setelah sistem ini di masa depan.

Untuk V0, boundary sistem sengaja dibuat sempit.

---

# System Boundary

## Upstream

Sistem mengasumsikan bahwa beberapa proses sudah terjadi sebelum engine dijalankan.

Contohnya:

```text
Topic Selection
      ↓
Research
      ↓
Raw Material Preparation
      ↓
Carousel Brief Engine
```

Input upstream dapat berisi:

* topik;
* objective;
* raw material;
* sources;
* mandatory points;
* optional points;
* audience context;
* tone context;
* brand context;
* visual context;
* production constraints.

Sebagian context dapat bersifat optional.

---

## Inside the Engine

```text
RAW MATERIAL
     │
     ▼
EDITORIAL DISTILLATION
     │
     ▼
ANGLE SELECTION
     │
     ▼
NARRATIVE ARCHITECTURE
     │
     ▼
SLIDE COMPILATION
     │
     ▼
COPY DEVELOPMENT
     │
     ▼
VISUAL DIRECTION
     │
     ▼
ASSET PLANNING
     │
     ▼
PROMPT COMPILATION
     │
     ▼
PRODUCTION INSTRUCTIONS
     │
     ▼
QA
     │
     ▼
PRODUCTION BRIEF
```

---

## Downstream

Setelah brief selesai:

```text
Production Brief
      ↓
Human Review
      ↓
Asset Production
      ↓
Design / Canva
      ↓
Final Review
      ↓
Publishing
```

Asset production dan final design berada di luar scope V0 engine.

---

# Editorial Authority

Engine bukan sekadar formatter.

Engine diperbolehkan melakukan:

```text
select
omit
compress
reorder
split
reframe
```

terhadap material yang diberikan.

Sistem boleh memilih angle berbeda dari angle input apabila angle tersebut lebih efektif untuk format carousel, selama:

* objective utama tetap dipenuhi;
* perubahan dilakukan secara transparan;
* factual meaning tidak berubah.

Contoh:

```text
INPUT ANGLE:
Mulai dana darurat dari nominal kecil.

SELECTED ANGLE:
Dana darurat bukan soal punya uang banyak,
tetapi soal memiliki buffer.

REASON:
Angle kedua lebih mudah dikembangkan menjadi
narrative carousel dan tetap memenuhi objective.
```

---

# Evidence Boundary

Engine tidak boleh menciptakan factual knowledge baru yang tidak tersedia di input.

Informasi dibedakan menjadi tiga kelas.

## FACT

Informasi faktual yang harus berasal dari raw material atau source.

```text
FACT
→ must be grounded
```

Contoh:

* statistik;
* nominal;
* definisi;
* regulasi;
* hasil penelitian;
* pernyataan institusi;
* fakta tentang perusahaan atau peristiwa.

---

## DERIVED

Informasi yang dapat diturunkan secara langsung dari fakta yang tersedia.

Contoh:

```text
Pendapatan: Rp3.000.000
Pengeluaran: Rp2.700.000

Derived:
Sisa cashflow = Rp300.000
```

Derived information diperbolehkan selama proses penurunannya jelas dan tidak membutuhkan asumsi baru.

---

## CREATIVE

Creative transformation diperbolehkan.

Contohnya:

* headline;
* analogy;
* metaphor;
* hypothetical example;
* narrative device;
* hook;
* visual metaphor;
* visual composition.

Creative output tidak boleh disajikan seolah-olah merupakan fakta nyata.

---

# Factual Integrity

Factual integrity memiliki prioritas tertinggi.

Important factual claims harus dapat ditelusuri kembali ke source yang mendukungnya.

Jika beberapa source berbeda pendapat:

```text
NON-FATAL DISAGREEMENT
→ preserve nuance
→ continue

CENTRAL CLAIM CANNOT BE ESTABLISHED
→ BLOCKED
```

Engine tidak boleh memilih salah satu klaim secara diam-diam hanya karena lebih cocok dengan narrative.

---

# Quality Priority

Ketika terjadi trade-off, sistem menggunakan urutan prioritas berikut:

```text
1. Factual Integrity
2. Clarity
3. Editorial Focus
4. Visual Communicability
5. Engagement / Hook Strength
6. Completeness
```

`Completeness` sengaja ditempatkan paling bawah.

Tujuan carousel bukan memasukkan seluruh hasil riset.

Tujuannya adalah menyampaikan **informasi minimum yang diperlukan untuk memahami satu core takeaway dengan benar**.

---

# Carousel Philosophy

## One Core Message Per Slide

Setiap slide sebaiknya memiliki satu **core message** yang dapat diringkas menjadi satu kalimat.

Supporting copy diperbolehkan selama hanya menjelaskan core message tersebut.

Supporting copy tidak boleh memperkenalkan argument baru yang seharusnya menjadi slide tersendiri.

---

## Adaptive Slide Count

Default jumlah slide:

```text
5–7 slides
```

Hard maximum:

```text
10 slides
```

Jumlah slide dipilih berdasarkan kebutuhan narrative, bukan berdasarkan template yang selalu sama.

Jika suatu ide terlalu padat, sistem dapat memecahnya menjadi beberapa slide.

Contoh:

```text
Slide 4
Claim

Slide 5
Example
```

Jika material tetap tidak dapat dijelaskan dengan baik dalam maksimum 10 slide setelah secondary information dibuang, sistem tidak boleh memaksa material masuk.

Status menjadi:

```text
SCOPE_TOO_BROAD
→ BLOCKED
```

Sistem kemudian memberikan rekomendasi untuk mempersempit objective atau scope riset.

---

# Information Density

Kepadatan slide tidak dinilai hanya berdasarkan jumlah kata.

Prioritas evaluasinya adalah:

```text
1. Conceptual Density
2. Visual / Text-area Density
3. Word Count
```

Word count digunakan sebagai **guardrail**, bukan hukum absolut.

Target utama adalah menghindari carousel yang berubah menjadi kumpulan paragraf.

Kegagalan density juga dapat terjadi ke arah sebaliknya. Slide terlalu tipis jika hanya menyisakan punchline, sementara alasan, implication, contoh, atau langkah yang membuatnya dapat dipahami sudah hilang. Ringkas berarti tidak boros kata, bukan selalu memakai kata sesedikit mungkin.

---

# Display Copy

Copy carousel ditulis untuk dilihat di dalam komposisi, bukan sebagai ringkasan artikel atau potongan caption.

Setiap slide memiliki `core_message` dan satu atau lebih display-copy blocks. Block dapat berfungsi sebagai context, focal statement, explanation, label, list, transition, atau CTA. Fungsi tersebut fleksibel dan tidak membentuk template wajib.

Setiap block menetapkan:

```text
reading order
attention priority
typographic scale and weight
alignment and color
placement
optional relation to visual
```

Reading order dapat berbeda dari attention priority. Sebuah context line dapat dibaca lebih dulu, sementara focal statement di bawahnya memakai ukuran lebih besar dan menarik perhatian lebih dulu.

Focal statement tidak wajib dan tidak selalu menjadi seluruh pesan slide. Sentence fragment diperbolehkan jika membuat copy lebih mudah dilihat dan diingat tanpa mengubah makna. Compiler menentukan hierarki awal; operator boleh merevisi seluruh keputusan saat review atau produksi.

Slide definisi sebaiknya menambahkan relevance atau implication. Jika tidak, gabungkan definisi ke slide lain. Slide transisi boleh membawa sedikit informasi baru jika dibutuhkan untuk pacing atau tension.

Slide informasional harus dapat dipahami dari display copy. Pembaca tidak boleh membutuhkan `core_message`, caption, atau catatan produksi untuk mengerti claim dan relevansinya. Hook dan transition boleh lebih tipis daripada explanation, comparison, example, atau action slide.

Hierarki dan komposisi harus bervariasi antar-slide agar carousel terasa segar. Variasi bukan formula pergantian background atau layout. Kohesi tetap mengikuti brand context dan art direction post tersebut. Jika approved prior posts tersedia, engine juga harus menghindari pengulangan cover formula, scene, atau komposisi yang membuat post baru terasa seperti salinan.

---

# Cover

Cover biasanya berfungsi sebagai hook.

Namun cover tidak diwajibkan selalu menjadi pure curiosity slide.

Pemilihan fungsi cover bergantung pada material dan narrative.

Provocative framing diperbolehkan selama klaim tersebut masih dapat dipertanggungjawabkan.

Contoh yang diperbolehkan:

```text
GAJI NAIK,
KOK MALAH MAKIN MISKIN?
```

selama carousel benar-benar menjelaskan fenomena yang dijanjikan headline.

Clickbait yang misleading tidak diperbolehkan.

---

# Self-Contained Carousel

Carousel harus dapat dipahami tanpa:

* membaca caption;
* membuka komentar;
* membuka link;
* mencari informasi tambahan.

Informasi penting tidak boleh disembunyikan di caption.

---

# Caption

Caption tetap menjadi bagian dari production brief, tetapi bukan lokasi utama konten.

Caption sebaiknya singkat.

Fungsinya dapat berupa:

* short commentary;
* hook tambahan;
* pertanyaan;
* CTA;
* contextual note;
* pelengkap carousel.

CTA tidak wajib.

Jika CTA terasa lebih natural di caption, gunakan caption.

Jika narrative carousel memiliki titik CTA yang lebih natural di dalam slide, CTA boleh ditempatkan di carousel.

---

# Visual Philosophy

Default principle:

> Visual harus membantu menyampaikan atau memperkuat message slide.

Visual dapat memiliki fungsi seperti:

```text
explain
compare
demonstrate
symbolize
contextualize
attract_attention
```

Namun tidak semua slide harus memiliki visual metaphor yang kompleks.

Untuk rare cases seperti:

* conclusion;
* transition;
* abstract statement;
* simple takeaway;

image minimal atau environmental diperbolehkan.

Contoh:

* simple architectural background;
* photographed texture;
* environmental image;
* minimal object;
* simple photographic background.

Decorative visual adalah exception yang valid, bukan default.

Empat referensi di `references/visuals/` diringkas menjadi playbook pada `docs/visual-language.md`. Engine memilih keluarga typography-first poster, lifestyle editorial, conceptual object editorial, atau conceptual human cinematic berdasarkan fungsi slide. Referensi mengajarkan prinsip, bukan subjek yang harus disalin.

Satu post menetapkan satu primary visual family dan paling banyak satu secondary family bila diperlukan. Kohesi dijaga lewat palette, type system, alignment, continuity, dan image treatment. Variasi datang dari skala, framing, posisi subjek, rasio text-image, text zone, dan kepadatan copy.

Copy dan visual menjalani fit loop sebelum asset strategy dikunci. Komposisi harus memberi ruang untuk penjelasan yang dibutuhkan. Copy tidak dipangkas sampai maknanya hilang hanya untuk mempertahankan layout pertama.

---

# Contract Version

Input contract tetap `0.1.0`; output contract menjadi `0.4.0` untuk NEEDS_REVIEW maupun BLOCKED. Versi ini menghapus `production.global_instructions` beserta wrapper `production`, lalu menghapus `assets[].generation.prompt_spec`. Consumer memakai `slides[].production_instructions` untuk langkah eksekusi dan `assets[].generation.prompt` untuk prompt final. Detail visual terstruktur tetap tersedia pada slide, jadi tidak perlu disalin ke prompt spec.

Seluruh hasil dan evaluasi yang sudah ada di `runs/` dan `evaluation-result/` adalah arsip contract lama. File tersebut tidak diedit atau dijalankan ulang saat contract berubah.

---

# Asset Strategies

Setiap slide dapat menggunakan salah satu asset strategy berikut.

## AI_SYNTHETIC

Visual utama dibuat menggunakan generative AI.

Contoh:

```text
sebuah dompet dengan beberapa lubang kecil
yang menyebabkan uang keluar sedikit demi sedikit
```

Digunakan terutama untuk konsep atau scene generic dalam bentuk AI-generated photorealistic image.

---

## REAL_ASSET

Menggunakan aset dokumenter atau foto nyata.

Contoh:

* tokoh publik;
* perusahaan;
* gedung;
* produk;
* peristiwa;
* objek nyata tertentu.

---

## HYBRID_COMPOSITE

Menggabungkan beberapa sumber asset.

Contoh:

```text
real person cutout
+
AI-generated photorealistic background
+
light image compositing
```

---

## Image Asset Registry

Carousel menggunakan image + text. Visual utama harus image-led; AI-generated image default-nya realistic/photorealistic, terlihat seperti foto nyata. Untuk konsep atau scene generic, prioritaskan AI-generated photorealistic image. Style lain hanya jika input memintanya secara eksplisit; topik edukasi bukan alasan otomatis untuk cartoon, vector/flat illustration, atau illustrated infographic.

Untuk real person, real company, real event, atau documentary evidence, prioritaskan REAL_ASSET. HYBRID_COMPOSITE digunakan jika perlu kombinasi image asset atau compositing ringan; menambahkan text ke image saja tidak membuat strategy menjadi hybrid.

Registry hanya berisi image asset AI_GENERATED atau REAL_ASSET. Text, angka, dan label tetap berada di slide copy/design instructions, bukan asset registry. Visual yang dipilih harus mengikuti batas ini.

---

# Real People and Real Events

Untuk orang, perusahaan, dan peristiwa nyata:

```text
REAL ASSET PREFERRED
```

AI-generated visual tidak boleh membuat kejadian sintetis yang berpotensi dianggap sebagai dokumentasi kejadian nyata.

Untuk conceptual explanation, synthetic visual tetap diperbolehkan.

---

# Asset Discovery

Engine tidak bertanggung jawab mencari file atau foto asli pada V0.

Jika real asset diperlukan, engine cukup menghasilkan requirement.

Contoh:

```text
ASSET REQUIRED:
Real photo of [subject]

REQUIREMENTS:
- front-facing
- waist-up
- sufficient resolution
- clean separation from background preferred
```

Asset sourcing akan menjadi proses downstream.

---

# Visual Specification

Visual brief harus cukup detail untuk menjadi basis production.

Bukan hanya:

```text
Visual:
orang sedang budgeting
```

Tetapi mencakup elemen seperti:

```text
subject
scene
visual function
composition
camera / framing
object placement
background
negative space
text zone
lighting
visual hierarchy
asset strategy
editing treatment
```

Visual direction harus bersifat **high-resolution secara instruksional**.

---

# Visual Alternatives

Untuk creative decision yang memiliki beberapa kemungkinan, engine tidak memberikan terlalu banyak opsi.

Default:

```text
PRIMARY CONCEPT
```

Primary concept adalah resolved default path.

Fallback digunakan apabila primary concept sulit diproduksi atau hasil generation tidak memadai.

Tujuannya adalah mengurangi decision fatigue.

---

# Image Prompt

Jika slide membutuhkan AI-generated asset, production brief harus menyediakan prompt yang siap digunakan.

Image prompt berasal dari visual specification.

Output hanya menyimpan prompt final pada `assets[].generation.prompt`. Field visual terstruktur pada slide menjadi sumber penyusunan prompt dan tidak disalin lagi ke `prompt_spec`.

Prompt harus mempertimbangkan kebutuhan layout carousel, termasuk:

* subject position;
* framing;
* negative space;
* text zone;
* background;
* lighting;
* composition;
* asset isolation;
* visual hierarchy.

Generated image sebaiknya tidak memuat typography utama carousel.

Typography dan informational text ditambahkan pada tahap desain.

---

# Production Instructions

Canva/design tool digunakan untuk display-copy blocks, typography, crop, resize/reposition image, remove background bila perlu, gradient ringan untuk readability, opacity, dan layering sederhana image + text.

Engine tidak merencanakan custom graphic components, icon system, Canva shapes sebagai visual utama, diagram manual, decorative graphic composition, atau illustrated infographic components. Larangan ini juga berlaku di asset requirements, prompts, dan production instructions; jangan menyamarkan komponen grafis sebagai AI_GENERATED atau REAL_ASSET. Manusia boleh mengimprovisasi graphic embellishment saat desain, tetapi itu di luar tanggung jawab dan output engine.

Output sistem tidak berhenti pada image prompt.

Engine juga memberikan langkah produksi.

Instruksi harus:

```text
tool-agnostic
but
operationally specific
```

Contoh:

```text
1. Buka platform yang biasa digunakan untuk generate gambar.
2. Copy dan paste prompt yang tersedia.
3. Generate beberapa hasil.
4. Pilih hasil yang paling sesuai dengan composition requirement.
5. Simpan asset terpilih.
6. Buka Canva.
7. Masukkan asset ke canvas.
8. Tempatkan asset di area kanan bawah.
9. Tambahkan display-copy blocks sesuai hierarchy dan placement pada production brief.
10. Pastikan negative space tetap tersedia.
```

Engine tidak hard-code platform seperti Midjourney, ChatGPT, atau platform lainnya kecuali production context di masa depan secara eksplisit memerlukannya.

---

# Production Instruction Scope

Output hanya menyimpan per-slide production instructions. Aturan global berasal dari resolved context dan visual grammar internal, lalu diterapkan langsung pada visual, copy, prompt, dan instruksi slide tanpa ringkasan terpisah.

Instruksi spesifik untuk setiap slide.

Contoh:

```text
SLIDE 03

1. Generate hero asset menggunakan prompt yang tersedia.
2. Pilih asset dengan subject berada di kanan bawah.
3. Import ke Canva.
4. Crop apabila diperlukan.
5. Tambahkan setiap display-copy block sesuai reading order, attention priority, typography, dan placement.
6. Terapkan accent treatment dan relation to visual jika ditetapkan.
7. Pastikan visual tidak bertabrakan dengan text zone.
```

---

# Hybrid Production

Engine diperbolehkan memberikan workflow produksi yang menggabungkan AI dan manual editing.

Contoh operasi:

```text
GENERATE
SOURCE
REMOVE BACKGROUND
CROP
MASK
LAYER
COMPOSE
ADD TEXT
ADJUST
EXPORT
```

Tujuan sistem bukan memaksimalkan AI automation.

Tujuannya adalah menghasilkan proses produksi yang paling efisien dengan resource yang tersedia.

---

# Brand Context

Brand identity bukan bagian dari core logic engine.

Brand context di-inject sebagai constraint.

Contohnya:

* tone of voice;
* language style;
* color system;
* typography rules;
* visual treatment;
* audience;
* editorial personality.

Jika brand context tersedia, engine harus mematuhinya selama tidak bertentangan dengan factual integrity atau core editorial principles.

Brand dapat mengubah **cara sebuah fakta disampaikan**, tetapi tidak boleh mengubah fakta itu sendiri.

Repository ini memakai profil brand terstruktur. Profil default tercatat di `contexts/defaults.json`, sedangkan sumber production Mantri Uang berada di:

```text
contexts/brands/mantri-uang.md
contexts/brands/mantri-uang.context.json
```

File Markdown adalah brief yang dibaca manusia. File JSON adalah context yang dikonsumsi engine. Setiap run memuat profil default secara otomatis. Input dapat menyebut `context_profile` untuk memilih profil lain. Aturan merge dan perlindungan brand policy berada di `SYSTEM.md`.

---

# Context Modes

Sistem mengenal minimal dua context mode.

## MOCK

Digunakan selama development dan testing.

```text
context_mode: MOCK
```

Mock context dapat digunakan untuk:

* audience;
* tone;
* visual identity;
* brand assumptions;
* raw material;
* production constraints.

Mock context tidak boleh dianggap sebagai permanent brand truth.

---

## PRODUCTION

Digunakan ketika context aktual sudah tersedia.

```text
context_mode: PRODUCTION
```

Pada mode ini, production context dan brand constraints yang tersedia menjadi bagian dari aturan output.

---

# Consistency vs Creativity

Sistem harus konsisten pada:

```text
editorial discipline
factual grounding
brief structure
quality principles
brand constraints when available
```

Sistem boleh eksploratif pada:

```text
story structure
narrative expression
display copy
analogy
visual metaphor
visual concept
visual composition
```

Tujuannya adalah:

> standardize quality, not creativity.

---

# Rule Severity

Rules di dalam sistem dibedakan menjadi tiga level.

## MUST

Pelanggaran tidak diperbolehkan.

Contoh:

```text
MUST NOT invent factual claims.
```

---

## SHOULD

Default behavior.

Boleh dilanggar apabila terdapat alasan yang jelas.

Contoh:

```text
Each slide SHOULD contain one core message.
```

---

## MAY

Area creative discretion.

Contoh:

```text
A slide MAY use a visual metaphor.
```

---

# Failure Behavior

Engine tidak diwajibkan selalu menghasilkan carousel.

Jika input tidak cukup untuk membuat brief yang dapat dipertanggungjawabkan, sistem harus berhenti.

Status:

```text
BLOCKED
```

Failure output tetap dianggap sebagai valid deliverable.

Failure response harus menjelaskan:

```text
STATUS

REASON

MISSING

IMPACT

RECOMMENDATION

UPSTREAM REPAIR INSTRUCTION

RESUME WHEN
```

Contoh:

```text
STATUS:
BLOCKED

REASON:
Raw material belum cukup mendukung hubungan sebab-akibat
yang dibutuhkan objective.

MISSING:
Penjelasan mengenai alasan fenomena X terjadi.

RECOMMENDATION:
Lakukan riset tambahan yang berfokus pada mekanisme X → Y.

UPSTREAM REPAIR INSTRUCTION:
Cari sumber yang menjawab:
1. mengapa X terjadi;
2. faktor yang memengaruhi X;
3. bagaimana X berhubungan dengan Y.

RESUME WHEN:
Minimal satu sumber kredibel mendukung central claim.
```

---

# Non-Fatal Problems

Jika masalah tidak membuat output invalid, engine tetap melanjutkan proses dan memberikan warning.

Contoh:

```text
WARNING:
Material mendukung central argument,
tetapi tidak memiliki contoh konkret.
```

---

# Human Review Gate

Production brief tidak langsung masuk ke tahap produksi.

Lifecycle utama:

```text
ENGINE
    ↓
NEEDS_REVIEW
    ↓
CONTENT REVIEWER
    ↓
APPROVED
    ↓
PRODUCTION
```

Reviewer bertanggung jawab mengecek:

* editorial direction;
* factual presentation;
* narrative;
* copy;
* visual concept;
* production feasibility.

Role `CONTENT REVIEWER` tidak di-hard-code ke individu tertentu.

---

# Brief Status

V0 menggunakan status:

```text
NEEDS_REVIEW
APPROVED
REVISION_REQUIRED
BLOCKED
```

## NEEDS_REVIEW

Engine berhasil menghasilkan brief dan menunggu review manusia.

## APPROVED

Brief sudah disetujui untuk masuk production.

## REVISION_REQUIRED

Reviewer meminta perubahan.

## BLOCKED

Engine tidak dapat menghasilkan valid production brief karena masalah input atau constraint fundamental.

---

# Revision

Revision dapat dilakukan pada satu slide tanpa harus selalu regenerate seluruh carousel.

Namun local revision harus mengevaluasi dampaknya terhadap:

```text
previous slide
next slide
narrative transition
overall argument
```

Carousel tetap diperlakukan sebagai satu narrative unit.

---

# Master Content Format — V0

Format utama:

```text
Static Carousel
Image + Text (photorealistic by default)
```

Primary platform:

```text
Instagram
```

Carousel yang sama digunakan ulang untuk TikTok pada V0.

Tidak ada platform-specific adaptation layer pada versi awal.

---

# Master Canvas — V0

Default master canvas:

```text
Aspect Ratio:
4:5

Resolution:
1080 × 1350 px
```

Canvas specification merupakan production context, bukan bagian permanen dari editorial core.

---

# Definition of Done

Satu engine run dikategorikan `SUCCESS` apabila:

* objective terpenuhi;
* satu editorial angle telah dipilih;
* factual grounding terjaga;
* secondary information yang tidak diperlukan sudah dibuang;
* narrative carousel lengkap;
* setiap slide memiliki core message yang jelas;
* copy sudah cukup final untuk digunakan dalam desain;
* visual direction setiap slide sudah resolved;
* asset strategy sudah ditentukan;
* image prompt tersedia jika diperlukan;
* production instructions dapat dieksekusi;
* warning dan limitation telah diungkapkan;
* important factual claims dapat ditelusuri ke source;
* caption singkat tersedia;
* production operator tidak perlu mengambil fundamental creative decision sebelum memulai produksi.

Dengan kata lain:

> Output engine bukan ide tentang bagaimana carousel sebaiknya dibuat.

Output engine adalah **rencana eksekusi carousel yang telah menyelesaikan hampir seluruh keputusan editorial dan creative-production fundamental sebelum tahap desain dimulai.**

---

# V0 Design Principle

V0 sengaja dibangun sebagai sistem kecil.

Prioritas awal adalah:

```text
clear contract
clear editorial logic
predictable behavior
testable output
```

Bukan:

```text
maximum automation
multi-agent architecture
complex orchestration
production infrastructure
```

Sebelum workflow stabil melalui penggunaan nyata, proses dapat dijalankan secara manual menggunakan AI coding interface seperti Claude Code, Codex, atau tool serupa.

Automation seperti n8n akan diperkenalkan setelah workflow yang perlu diotomatisasi telah terbukti stabil dan repetitif.

---

# Current Development Stage

Saat ini project berada pada tahap awal system design.

Urutan pengembangan awal:

```text
Stage 0
System Definition

Stage 1
Input / Output Contracts

Stage 2
Mock Fixtures

Stage 3
Expected Behavior

Stage 4
Editorial Distillation Prototype

Stage 5
Narrative Prototype

Stage 6
Copy Prototype

Stage 7
Visual Direction Prototype

Stage 8
Prompt Compilation

Stage 9
Full Brief Compilation

Stage 10
Automation
```

Current focus:

```text
Stage 0 → Stage 1
```

---

# Repository Philosophy

Repository ini akan menjadi source of truth untuk behavior `carousel-brief-engine`.

Implementation detail dapat berubah.

AI model dapat berubah.

Production tools dapat berubah.

Workflow automation dapat berubah.

Namun core editorial contract, principles, and system behavior harus tetap eksplisit dan dapat diperiksa oleh manusia.

The system should remain:

```text
human-readable
machine-readable
model-agnostic
tool-agnostic
testable
```
