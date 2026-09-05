# Scope — Carousel Brief Engine

Dokumen ini mendefinisikan **batas tanggung jawab** `carousel-brief-engine`.

Tujuannya adalah memastikan sistem tetap fokus pada satu pekerjaan utama dan tidak berkembang menjadi workflow end-to-end sebelum ada kebutuhan nyata.

Prinsip utamanya:

> `carousel-brief-engine` dimulai setelah material konten tersedia dan berhenti ketika production brief sudah cukup lengkap untuk direview manusia dan dieksekusi pada tahap produksi.

---

# 1. Core Scope

`carousel-brief-engine` bertanggung jawab mengubah:

```text
RAW CONTENT MATERIAL
````

menjadi:

```text
EXECUTABLE CAROUSEL PRODUCTION BRIEF
```

untuk satu static carousel edukasi keuangan.

Secara konseptual:

```text
INPUT PACKAGE
      │
      ▼
┌──────────────────────────────┐
│    CAROUSEL BRIEF ENGINE     │
│                              │
│  editorial decisions         │
│  narrative decisions         │
│  slide decisions             │
│  copy decisions              │
│  visual decisions            │
│  asset decisions             │
│  production planning         │
└──────────────────────────────┘
      │
      ▼
PRODUCTION BRIEF
```

Engine harus menyelesaikan sebanyak mungkin keputusan fundamental sebelum content producer mulai melakukan pekerjaan desain.

---

# 2. Unit of Work

Satu run selalu bekerja pada:

> **satu content unit yang menghasilkan satu carousel lengkap.**

Bukan satu slide.

Bukan satu batch konten.

Bukan beberapa postingan sekaligus.

```text
1 RUN
  │
  ├── 1 topic / content unit
  ├── 1 objective
  ├── 1 selected editorial angle
  ├── 1 narrative
  ├── 1 carousel
  ├── N slides
  ├── 1 caption
  └── 1 production brief
```

Default jumlah slide:

```text
5–7
```

Hard maximum:

```text
10
```

Jumlah slide bersifat adaptive berdasarkan kebutuhan narrative.

---

# 3. Entry Boundary

Engine dimulai setelah upstream telah menyediakan material yang cukup untuk diproses.

Secara ideal:

```text
Topic Selection
      ↓
Research
      ↓
Material Preparation
      ↓
─────────────────────────
CAROUSEL BRIEF ENGINE
─────────────────────────
```

Engine tidak bertanggung jawab menentukan bagaimana material tersebut diperoleh.

---

# 4. Expected Upstream Inputs

Input dapat mencakup:

* topic;
* content objective;
* raw research material;
* factual claims;
* sources;
* mandatory information;
* optional information;
* initial angle;
* audience context;
* tone context;
* brand context;
* visual context;
* production context;
* constraints.

Tidak semua context wajib tersedia pada setiap tahap development.

Beberapa context dapat bersifat optional atau mock.

---

# 5. Raw Material Responsibility

Engine **mengonsumsi** raw material.

Engine tidak melakukan primary research untuk menggantikan raw material yang tidak tersedia.

Contoh material yang valid:

```text
research notes
article summaries
source extracts
structured research output
approved internal knowledge
factual bullet points
data
statistics
```

Engine bertanggung jawab menentukan:

```text
what to use
what to omit
what to emphasize
how to order it
how to communicate it
```

Engine tidak bertanggung jawab menentukan apakah seluruh dunia informasi tentang topik tersebut sudah berhasil ditemukan upstream.

---

# 6. Editorial Scope

Editorial decision-making termasuk dalam core scope.

Engine diperbolehkan:

* menentukan core takeaway;
* memilih informasi utama;
* menghapus detail sekunder;
* mengompresi materi;
* mengelompokkan informasi;
* mengubah urutan informasi;
* memecah informasi menjadi beberapa slide;
* menyatukan informasi yang redundant;
* memilih narrative structure;
* menentukan fungsi setiap slide;
* memperbaiki atau mengganti editorial angle.

Engine tidak hanya memformat input yang diberikan.

---

# 7. Objective Boundary

Objective dari upstream merupakan constraint utama.

Engine boleh mengubah:

```text
angle
framing
story structure
ordering
copy expression
visual interpretation
```

tetapi tidak boleh diam-diam mengubah:

```text
core content objective
```

Jika objective tidak dapat dipenuhi menggunakan material yang tersedia, engine harus menghasilkan:

```text
BLOCKED
```

bukan membuat objective baru.

---

# 8. Angle Authority

Input dapat memiliki initial angle.

Initial angle bukan hard constraint kecuali secara eksplisit dinyatakan sebagai mandatory.

Engine dapat memilih angle yang berbeda apabila:

* lebih sesuai untuk carousel;
* lebih mudah dipahami;
* memungkinkan editorial compression yang lebih baik;
* lebih kuat secara narrative;
* tetap mendukung objective;
* tetap grounded pada material.

Perubahan angle harus transparan.

---

# 9. Knowledge Boundary

Engine tidak boleh menggunakan latent model knowledge untuk menciptakan factual content baru.

Batas informasi:

```text
FACT
    ↓
harus berasal dari input/source

DERIVED
    ↓
boleh diturunkan secara langsung

CREATIVE
    ↓
boleh dibuat oleh engine
```

---

# 10. Allowed Derived Information

Engine boleh menghasilkan derived information apabila hasil tersebut merupakan konsekuensi langsung dari data yang tersedia.

Contoh:

```text
INPUT

Pendapatan:
Rp3.000.000

Pengeluaran:
Rp2.700.000
```

Engine boleh menghasilkan:

```text
DERIVED

Sisa cashflow:
Rp300.000
```

Derived information tidak boleh membutuhkan asumsi faktual tambahan yang tidak tersedia.

---

# 11. Allowed Creative Transformation

Creative transformation termasuk dalam scope.

Engine boleh membuat:

* headline;
* hooks;
* analogies;
* visual metaphors;
* hypothetical examples;
* narrative framing;
* simplified explanations;
* visual scenarios;
* composition ideas;
* asset concepts.

Namun creative transformation tidak boleh disajikan sebagai factual evidence.

Contoh hypothetical example harus tetap terbaca sebagai ilustrasi, bukan kejadian nyata.

---

# 12. Editorial Compression

Editorial compression merupakan salah satu core responsibility terpenting.

Engine harus berani membuang informasi.

Targetnya bukan:

> Memasukkan sebanyak mungkin hasil riset ke dalam carousel.

Targetnya adalah:

> Memilih informasi minimum yang diperlukan agar audience memahami core takeaway secara benar.

Engine dapat mengklasifikasikan informasi menjadi:

```text
MUST INCLUDE

SUPPORTING

OPTIONAL

OMIT
```

Omission bukan kegagalan.

Omission adalah bagian dari editorial decision-making.

---

# 13. Narrative Scope

Engine bertanggung jawab menentukan bagaimana informasi bergerak dari slide pertama sampai terakhir.

Narrative tidak harus menggunakan satu template tetap.

Kemungkinan struktur dapat mencakup:

```text
HOOK
↓
PROBLEM
↓
EXPLANATION
↓
EXAMPLE
↓
TAKEAWAY
```

atau:

```text
QUESTION
↓
ANSWER
↓
MECHANISM
↓
IMPLICATION
```

atau:

```text
MYTH
↓
REALITY
↓
WHY
↓
EXAMPLE
↓
CONCLUSION
```

Struktur dipilih berdasarkan material.

---

# 14. Slide-Level Scope

Untuk setiap slide, engine minimal harus menyelesaikan keputusan tentang:

```text
purpose
core message
copy
visual direction
asset strategy
production direction
```

Engine tidak boleh hanya menghasilkan:

```text
Slide 3:
Bahas pentingnya dana darurat.
```

Output harus cukup resolved untuk diproduksi.

---

# 15. Copy Scope

Engine bertanggung jawab menghasilkan copy yang cukup final untuk ditempatkan ke desain.

Ini termasuk:

* cover headline;
* slide headline;
* supporting copy;
* emphasis;
* short labels jika diperlukan;
* CTA jika relevan;
* caption singkat.

Content producer tidak seharusnya perlu menulis ulang keseluruhan copy dari nol.

Micro-editing tetap diperbolehkan pada tahap produksi atau review.

---

# 16. Copy Density Scope

Engine bertanggung jawab menjaga readability.

Kepadatan dinilai berdasarkan:

```text
1. conceptual density
2. visual/text-area density
3. word count
```

Engine tidak boleh menyelesaikan masalah kepadatan hanya dengan:

* mengecilkan teks;
* membuat paragraph panjang;
* memasukkan terlalu banyak sub-points.

Strategi yang lebih diutamakan:

```text
remove
simplify
split
restructure
```

---

# 17. Visual Direction Scope

Visual direction adalah bagian core dari engine.

Engine harus menentukan visual yang sesuai untuk pesan slide.

Visual direction dapat mencakup:

* visual function;
* visual concept;
* visual metaphor;
* hero subject;
* scene;
* framing;
* composition;
* object placement;
* negative space;
* text area;
* background;
* lighting;
* visual hierarchy;
* editing treatment.

Output visual harus cukup detail untuk diterjemahkan menjadi asset production.

---

# 18. Visual Function Scope

Default:

> Visual harus memiliki alasan keberadaan.

Kemungkinan fungsi:

```text
EXPLAIN
COMPARE
DEMONSTRATE
SYMBOLIZE
CONTEXTUALIZE
ATTRACT_ATTENTION
```

Namun decorative visual diperbolehkan untuk rare cases ketika pesan tidak memiliki representasi visual yang meaningful.

Contoh:

* conclusion;
* transition;
* abstract statement;
* final takeaway.

Dalam kondisi tersebut engine tetap harus menentukan minimal visual treatment.

---

# 19. Asset Strategy Scope

Engine bertanggung jawab memilih asset strategy.

Supported V0 asset strategies:

```text
AI_SYNTHETIC
REAL_ASSET
HYBRID_COMPOSITE
GRAPHIC_ONLY
```

Pemilihan strategy dilakukan per slide.

---

# 20. AI_SYNTHETIC Scope

Engine dapat menentukan synthetic asset dan menghasilkan prompt untuk pembuatannya.

Engine tidak bertanggung jawab menjalankan image-generation API.

Workflow V0 dapat tetap manual:

```text
engine creates prompt
        ↓
human opens image-generation platform
        ↓
human generates asset
```

---

# 21. REAL_ASSET Scope

Jika slide membutuhkan real asset, engine bertanggung jawab menjelaskan:

```text
what asset is required
what subject is required
what framing is preferred
what technical characteristics are preferred
how the asset will be used
```

Engine tidak bertanggung jawab mencari atau mengunduh asset tersebut pada V0.

---

# 22. HYBRID_COMPOSITE Scope

Engine dapat merancang workflow seperti:

```text
real image
+
background removal
+
AI-generated background
+
additional graphic element
+
manual composition
```

Hybrid production termasuk dalam scope production planning.

---

# 23. GRAPHIC_ONLY Scope

Engine dapat memilih graphic-only approach jika photographic asset tidak diperlukan.

Contohnya:

```text
diagram
timeline
comparison
number visualization
icon
shape
simple chart
typography-led layout
```

Engine tidak harus memaksakan AI-generated image ke setiap slide.

---

# 24. Image Prompt Scope

Jika AI-generated asset dibutuhkan, engine harus menghasilkan image prompt.

Prompt harus berasal dari visual specification.

Engine dapat menentukan:

* subject;
* action;
* environment;
* composition;
* position;
* negative space;
* perspective;
* lighting;
* background treatment;
* intended placement.

Prompt tidak diharapkan menghasilkan final typography.

Text dan informational copy tetap dipasang pada tahap design.

---

# 25. Prompt Execution Boundary

Engine menghasilkan prompt.

Engine **tidak** secara langsung menjalankan image generation pada V0.

Boundary:

```text
ENGINE
↓
IMAGE PROMPT
────────────────────────
END OF AUTOMATED GENERATION
────────────────────────
HUMAN / PRODUCTION TOOL
↓
GENERATED ASSET
```

Automation ini dapat berubah di versi mendatang tanpa mengubah core responsibility.

---

# 26. Production Instruction Scope

Production planning termasuk dalam scope.

Engine harus mampu memberikan instruksi yang actionable.

Contoh:

```text
1. Buka platform yang biasa digunakan untuk generate gambar.
2. Copy prompt yang disediakan.
3. Generate beberapa hasil.
4. Pilih hasil yang paling sesuai dengan composition requirement.
5. Simpan asset.
6. Buka Canva.
7. Tempatkan asset sesuai layout direction.
8. Tambahkan copy.
9. Lakukan adjustment.
```

Instruksi bersifat:

```text
TOOL-AGNOSTIC
+
OPERATIONALLY SPECIFIC
```

---

# 27. Global vs Local Production Scope

Engine dapat memberikan dua jenis production instruction.

## Global

Berlaku pada keseluruhan carousel.

Contoh:

* canvas;
* typography behavior;
* common visual treatment;
* image-generation rules;
* cohesion rules.

## Per Slide

Berlaku hanya untuk slide tertentu.

Contoh:

* asset yang harus dibuat;
* positioning;
* cropping;
* masking;
* layering;
* text placement;
* editing.

---

# 28. Final Design Boundary

Engine **tidak menghasilkan final design**.

Out of scope:

* pixel-perfect layout;
* final typography sizing;
* final spacing;
* exact kerning;
* final color correction;
* final crop adjustment;
* Canva file creation;
* final export.

Engine memberikan cukup arah agar micro-decisions tersebut tidak membutuhkan creative planning baru.

---

# 29. Production Tool Boundary

Engine tidak bergantung pada satu tool tertentu.

Contoh instruksi yang diperbolehkan:

> Buka platform yang biasa digunakan untuk generate gambar.

Contoh instruksi yang tidak dijadikan core assumption:

> Buka Midjourney.

Tool tertentu dapat dimasukkan melalui production context di masa depan.

---

# 30. Brand Scope

Engine bukan brand-definition system.

Out of scope:

* memilih nama brand;
* menentukan positioning brand;
* menentukan personality brand;
* memilih logo;
* memilih final color palette;
* menentukan final typography system.

Engine hanya **mengonsumsi** brand context apabila context tersebut sudah tersedia.

---

# 31. Audience Scope

Engine tidak bertanggung jawab melakukan audience research atau audience segmentation strategis.

Jika audience context tersedia, engine menggunakannya sebagai constraint.

Contoh:

```text
age range
knowledge level
financial context
language preference
communication style
```

Pada development, audience context dapat berupa mock.

---

# 32. Context Injection

Context seperti:

```text
brand
audience
tone
visual identity
production setup
```

harus diperlakukan sebagai input/injected context.

Bukan hard-coded ke editorial core.

Tujuannya agar core behavior tetap stabil saat context berubah.

---

# 33. Mock Scope

Development menggunakan mock untuk dependency yang belum tersedia.

Mock dapat digunakan untuk:

* raw material;
* audience;
* tone;
* brand;
* visual identity;
* production context.

Mock harus eksplisit.

```text
context_mode: MOCK
```

Mock tidak boleh diperlakukan sebagai factual production context.

---

# 34. Source Traceability Scope

Engine bertanggung jawab menjaga hubungan antara important factual claims dan source pendukungnya.

Traceability digunakan untuk:

* QA;
* human review;
* revision;
* factual verification.

Tidak berarti setiap kalimat pada carousel harus memiliki visible citation.

Visible citation ditentukan berdasarkan kebutuhan konten.

---

# 35. Source Conflict Scope

Jika sources memberikan informasi berbeda, engine harus mempertahankan disagreement yang relevan.

Jika disagreement masih memungkinkan objective dijelaskan:

```text
continue
+
preserve nuance
```

Jika disagreement membuat central claim tidak dapat ditentukan:

```text
BLOCKED
```

Resolusi research disagreement bukan tanggung jawab engine apabila input tidak menyediakan dasar untuk memilih.

---

# 36. Visible Citation Scope

Engine dapat merekomendasikan visible source attribution untuk:

* statistics;
* studies;
* regulations;
* specific factual claims;
* specific reports.

Visible citation tidak diwajibkan untuk seluruh penjelasan dasar.

Internal source traceability tetap lebih lengkap.

---

# 37. Caption Scope

Engine menghasilkan satu short caption.

Caption bukan perluasan dari carousel.

Caption dapat berfungsi untuk:

```text
COMMENT
HOOK
QUESTION
CTA
SHORT CONTEXT
```

Informasi yang diperlukan untuk memahami carousel tidak boleh hanya terdapat di caption.

---

# 38. CTA Scope

CTA bersifat optional.

Engine boleh memilih:

```text
CTA IN CAROUSEL
```

atau:

```text
CTA IN CAPTION
```

atau:

```text
NO CTA
```

berdasarkan natural fit.

Tidak ada kewajiban memasukkan CTA ke setiap carousel.

---

# 39. Platform Scope — V0

V0 menggunakan satu master carousel.

Primary platform:

```text
Instagram
```

Carousel yang sama digunakan kembali untuk:

```text
TikTok
```

Tidak ada platform-specific content adaptation pada V0.

---

# 40. Canvas Scope — V0

Default master canvas:

```text
3:4
1080 × 1440 px
```

Canvas adalah production context.

Bukan permanent editorial rule.

---

# 41. Human Review Scope

Engine berhenti sebelum production tanpa approval.

Lifecycle:

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

Engine tidak menggantikan reviewer manusia.

---

# 42. Reviewer Responsibility

Reviewer bertanggung jawab melakukan final judgment terhadap:

* editorial direction;
* factual presentation;
* narrative quality;
* copy;
* visual direction;
* production feasibility.

Reviewer dapat:

```text
APPROVE
```

atau:

```text
REQUEST REVISION
```

---

# 43. Revision Scope

Engine mendukung conceptual local revision.

Contoh:

```text
revise slide 4 visual
```

Tidak berarti seluruh carousel harus selalu dibuat ulang.

Namun perubahan lokal harus mempertimbangkan:

```text
previous transition
next transition
overall narrative
```

---

# 44. Status Scope

Supported V0 statuses:

```text
NEEDS_REVIEW
APPROVED
REVISION_REQUIRED
BLOCKED
```

Engine-generated successful brief pertama kali masuk sebagai:

```text
NEEDS_REVIEW
```

---

# 45. Failure Scope

Tidak semua run harus menghasilkan carousel.

Fatal condition menghasilkan:

```text
BLOCKED
```

Contoh fatal conditions:

* material tidak cukup;
* objective tidak didukung material;
* central factual claim tidak dapat diverifikasi dari input;
* scope terlalu luas;
* source conflict membuat core argument tidak dapat ditentukan;
* mandatory information tidak tersedia.

---

# 46. Failure Deliverable

`BLOCKED` bukan error kosong.

Engine tetap harus menghasilkan actionable upstream repair brief.

Minimal:

```text
STATUS

REASON

MISSING

IMPACT

RECOMMENDATION

UPSTREAM REPAIR INSTRUCTION

RESUME WHEN
```

Engine harus membantu upstream mengetahui bagaimana memperbaiki material sebelum run dicoba kembali.

---

# 47. Non-Fatal Warning Scope

Engine dapat tetap menghasilkan brief jika terdapat masalah yang tidak membuat output invalid.

Contoh:

```text
Material tidak memiliki contoh konkret.
```

atau:

```text
Tidak tersedia visual documentary asset.
```

Output:

```text
NEEDS_REVIEW
+
WARNING
```

bukan otomatis `BLOCKED`.

---

# 48. Research Scope — Out of Scope

V0 tidak melakukan:

* autonomous web research;
* source discovery;
* research summarization dari nol;
* source credibility ranking;
* fact acquisition;
* research augmentation otomatis.

Research adalah upstream concern.

Jika engine membutuhkan informasi yang tidak tersedia:

```text
BLOCKED
+
research recommendation
```

---

# 49. Topic Discovery — Out of Scope

Engine tidak menentukan:

* topik apa yang sedang trending;
* topik apa yang harus diposting besok;
* content calendar;
* content pillar allocation;
* competitor-driven topic selection.

Input topic datang dari upstream.

---

# 50. Social Media Strategy — Out of Scope

Engine tidak menentukan:

* posting frequency;
* account growth strategy;
* campaign planning;
* community strategy;
* algorithm strategy;
* paid media;
* follower acquisition;
* distribution strategy.

---

# 51. Analytics — Out of Scope

V0 tidak:

* membaca Instagram analytics;
* membaca TikTok analytics;
* mengukur carousel performance;
* melakukan A/B analysis;
* mengubah behavior berdasarkan historical metrics.

Analytics dapat menjadi downstream feedback system di masa depan.

---

# 52. Memory — Out of Scope for V0

V0 tidak membutuhkan autonomous long-term memory.

Engine tidak secara otomatis:

* mengingat semua carousel sebelumnya;
* mempelajari engagement history;
* memperbarui brand knowledge;
* menyimpan audience learning.

Hal tersebut dapat ditambahkan ketika operating system yang lebih besar mulai terbentuk.

---

# 53. n8n Automation — Out of Scope for Core

n8n bukan bagian core behavior engine.

Automation dapat mengorkestrasi engine setelah workflow stabil.

Contoh future workflow:

```text
input received
↓
n8n
↓
engine run
↓
validate output
↓
save brief
↓
create review task
```

Namun engine harus tetap dapat digunakan tanpa n8n.

---

# 54. AI Agent Architecture — Out of Scope

V0 tidak membutuhkan:

* autonomous agent;
* multi-agent system;
* agent-to-agent communication;
* MCP infrastructure;
* long-running autonomous loop;
* complex orchestration.

Logical processing stages tidak harus menjadi agents terpisah.

---

# 55. Model Scope

Core system harus model-agnostic.

Sistem dapat dijalankan menggunakan:

```text
Claude Code
Codex
atau AI interface serupa
```

tanpa menjadikan satu provider sebagai permanent dependency.

---

# 56. Repository Scope

Repository bertanggung jawab menyimpan definisi dan behavior engine.

Repository dapat menyimpan:

```text
system documentation
principles
contracts
schemas
mock fixtures
prompts
evaluation criteria
test runs
reference material
```

Repository bukan application backend pada V0.

---

# 57. Explicitly In Scope — V0

Ringkasan hal yang termasuk scope:

```text
✓ consume raw material

✓ editorial distillation

✓ information selection

✓ information omission

✓ angle selection

✓ narrative architecture

✓ adaptive slide planning

✓ slide core-message definition

✓ carousel copy

✓ visual direction

✓ visual metaphor

✓ asset strategy

✓ AI image prompt

✓ real-asset requirement specification

✓ hybrid-production planning

✓ graphic-only planning

✓ production instructions

✓ short caption

✓ optional CTA

✓ source traceability

✓ QA

✓ warnings

✓ blocked state

✓ upstream repair recommendation

✓ human-review handoff
```

---

# 58. Explicitly Out of Scope — V0

```text
✗ topic discovery

✗ primary research

✗ autonomous web research

✗ source acquisition

✗ real-asset discovery

✗ image generation via API

✗ final graphic design

✗ Canva automation

✗ publishing

✗ scheduling

✗ social media analytics

✗ content calendar

✗ brand creation

✗ audience research

✗ autonomous memory

✗ multi-agent architecture

✗ n8n orchestration as core dependency

✗ platform-specific adaptation

✗ autonomous production
```

---

# 59. Exit Boundary

Engine dianggap selesai ketika salah satu dari dua kondisi tercapai.

## Successful Exit

```text
STATUS:
NEEDS_REVIEW
```

dan production brief sudah cukup lengkap sehingga reviewer dapat mengevaluasi hasil sebelum production.

---

## Blocked Exit

```text
STATUS:
BLOCKED
```

dan engine telah memberikan cukup informasi agar upstream mengetahui apa yang harus diperbaiki.

---

# 60. Scope Expansion Rule

Fitur baru tidak otomatis ditambahkan ke core.

Sebelum memperluas scope, tanyakan:

> Apakah capability ini diperlukan untuk mengubah raw material menjadi production brief?

Jika:

```text
YES
```

capability dapat dipertimbangkan sebagai bagian core.

Jika:

```text
NO
```

capability lebih mungkin menjadi:

```text
UPSTREAM FEATURE
DOWNSTREAM FEATURE
INTEGRATION
AUTOMATION
atau
SEPARATE MODULE
```

---

# 61. V0 Scope Philosophy

V0 sengaja kecil.

Tujuan awal bukan membuat sistem yang mampu melakukan semuanya.

Tujuannya adalah membuat satu transformation pipeline yang:

```text
clear
predictable
testable
useful
```

Core transformation:

```text
RAW MATERIAL
        ↓
EDITORIAL + CREATIVE-PRODUCTION REASONING
        ↓
EXECUTABLE PRODUCTION BRIEF
```

Jika transformation tersebut sudah stabil, capability lain dapat dibangun mengelilinginya tanpa membuat core engine kehilangan batas tanggung jawabnya.


