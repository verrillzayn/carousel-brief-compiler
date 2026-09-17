# Principles — Carousel Brief Engine

Dokumen ini mendefinisikan **prinsip kerja inti** `carousel-brief-engine`.

Jika `scope.md` menjawab:

> “Apa yang termasuk dan tidak termasuk tanggung jawab sistem?”

maka `principles.md` menjawab:

> “Bagaimana sistem harus mengambil keputusan ketika menjalankan tanggung jawab tersebut?”

Prinsip di dokumen ini bukan template output dan bukan detail implementasi.

Prinsip adalah **behavioral rules** yang harus tetap berlaku meskipun:

- model AI berubah;
- prompt berubah;
- workflow berubah;
- brand berubah;
- tool produksi berubah;
- struktur repository berkembang.

---

# 1. Core Principle

> **Transform material into a production-ready decision system, not merely into shorter text.**

Tugas engine bukan hanya meringkas.

Engine harus mengubah material menjadi serangkaian keputusan yang dapat dieksekusi:

```text
what matters
↓
what does not matter
↓
what should be said
↓
in what order
↓
how it should be written
↓
how it should be visualized
↓
how it should be produced
````

Output yang hanya “merapikan informasi” belum dianggap cukup.

---

# 2. Quality Over Completeness

Carousel tidak harus memuat seluruh informasi yang tersedia.

Sistem harus memprioritaskan:

```text
understanding
over
information volume
```

Prinsip:

> **Lebih baik menyampaikan sedikit informasi dengan benar dan jelas daripada memasukkan banyak informasi yang membuat pesan utama hilang.**

Completeness bukan objective utama.

---

# 3. Factual Integrity Comes First

Factual integrity memiliki prioritas tertinggi.

Engine tidak boleh:

* menciptakan fakta baru;
* mengubah angka;
* memperkuat klaim melebihi source;
* menyembunyikan uncertainty;
* memilih satu fakta dari conflicting sources tanpa alasan;
* mengubah fakta demi hook;
* mengubah fakta demi brand voice;
* mengubah fakta demi visual yang lebih menarik.

Urutan prioritas:

```text
1. factual integrity
2. clarity
3. editorial focus
4. visual communicability
5. engagement
6. completeness
```

Jika engagement bertentangan dengan factual integrity:

```text
factual integrity wins
```

---

# 4. Evidence Transformation, Not Evidence Invention

Engine bekerja berdasarkan material yang diberikan.

Prinsip:

> **The system may transform evidence, but it may not invent evidence.**

Informasi dibedakan menjadi:

```text
FACT
DERIVED
CREATIVE
```

## FACT

Harus didukung material/source.

## DERIVED

Boleh dihasilkan jika merupakan konsekuensi langsung dari fakta yang tersedia.

## CREATIVE

Boleh dibuat untuk membantu komunikasi, selama tidak disajikan sebagai fakta.

---

# 5. Creativity Must Not Masquerade as Fact

Creative output seperti:

* analogy;
* hypothetical example;
* visual metaphor;
* illustrative scenario;
* provocative headline;

diperbolehkan.

Namun audience tidak boleh dibuat mengira bahwa elemen kreatif tersebut adalah kejadian nyata.

Contoh:

```text
“Bayangkan kamu punya Rp1 juta...”
```

dapat digunakan sebagai hypothetical example.

Tetapi:

```text
“Mahasiswa rata-rata kehilangan Rp1 juta karena...”
```

tidak boleh dibuat tanpa evidence.

---

# 6. Objective Is a Contract

Content objective dari upstream diperlakukan sebagai contract.

Engine boleh mengubah:

```text
angle
framing
story
sequence
copy
visual interpretation
```

tetapi tidak boleh diam-diam mengubah objective.

Jika objective tidak dapat dipenuhi menggunakan material yang tersedia:

```text
BLOCK
```

bukan:

```text
invent a new objective
```

---

# 7. Angle Is Flexible

Berbeda dari objective, angle merupakan editorial decision.

Engine boleh memperbaiki atau mengganti angle jika:

* angle baru lebih jelas;
* angle baru lebih cocok untuk format carousel;
* angle baru lebih mudah divisualisasikan;
* angle baru memungkinkan compression yang lebih baik;
* objective tetap sama;
* factual basis tetap sama.

Perubahan angle harus transparan.

---

# 8. Editorial Selection Is a Core Capability

Engine harus berani memilih.

Engine tidak boleh memperlakukan setiap bagian raw material sebagai sesuatu yang wajib masuk.

Prinsip:

> **Not every true fact is relevant to this carousel.**

Informasi dapat dikategorikan menjadi:

```text
MUST INCLUDE
SUPPORTING
OPTIONAL
OMIT
```

`OMIT` adalah valid editorial outcome.

---

# 9. Omission Requires Reasoning

Informasi tidak dibuang secara acak.

Jika engine menghilangkan informasi yang terlihat relevan, keputusan idealnya dapat dijelaskan.

Contoh alasan:

```text
redundant
too detailed
outside objective
requires too much context
weak supporting value
better suited for separate content
```

Tujuannya bukan membuat semua keputusan verbose, tetapi memastikan omission merupakan keputusan editorial yang disengaja.

---

# 10. One Carousel, One Central Takeaway

Setiap carousel harus memiliki satu central takeaway yang jelas.

Setelah melihat keseluruhan carousel, audience idealnya dapat menjawab:

> “Hal utama apa yang baru saja dijelaskan?”

Jika terdapat beberapa takeaway yang sama kuat dan tidak dapat disatukan, scope kemungkinan terlalu luas.

---

# 11. One Slide, One Core Message

Setiap slide **SHOULD** memiliki satu core message.

Core message harus dapat diringkas menjadi satu kalimat.

Display copy tidak harus menyalin core message sebagai satu kalimat utuh. Ia dapat memakai beberapa block dengan fungsi berbeda, termasuk context, focal statement, explanation, label, list, transition, atau CTA.

Setiap block harus tetap berhubungan dengan core message atau fungsi naratif slide. Definition-only slide sebaiknya menambahkan relevance atau implication, atau digabung ke slide lain. Transition slide boleh membawa sedikit informasi baru jika membangun pacing atau tension yang diperlukan.

Prinsip:

```text
one slide
≈
one unit of understanding
```

bukan:

```text
one slide
=
one sentence only
```

---

# 12. Split Before You Compress Too Hard

Jika satu slide terlalu padat, urutan solusi yang disukai adalah:

```text
1. remove unnecessary information
2. simplify
3. split into multiple slides
4. restructure narrative
```

Bukan:

```text
shrink font
add paragraph
reduce whitespace
```

Readability tidak boleh dikorbankan hanya untuk mempertahankan slide count.

Copy carousel ditulis untuk dilihat dalam komposisi. Sentence fragment diperbolehkan jika meningkatkan scanability tanpa mengubah makna. Reading order dan attention priority harus ditentukan secara terpisah karena block yang dibaca pertama tidak selalu menjadi block yang paling menarik perhatian.

Hierarki tipografi bukan template tetap. Focal statement disarankan ketika berguna, tetapi tidak wajib dan tidak selalu berisi seluruh pesan slide. Compiler menentukan scale, weight, alignment, color, placement, dan hubungan copy dengan visual. Operator boleh merevisi keputusan tersebut. Jika approved prior posts tersedia, engine harus menjaga identitas brand tanpa menyalin cover formula, scene, atau komposisi terlalu dekat.

---

# 13. Slide Count Serves the Narrative

Default:

```text
5–7 slides
```

Hard maximum:

```text
10 slides
```

Namun jumlah slide bukan target yang harus dipenuhi secara mekanis.

Prinsip:

> **Use as many slides as needed to explain the argument clearly, but no more than necessary.**

Jika content masih tidak muat dalam 10 slide setelah compression yang wajar:

```text
BLOCK
```

dan rekomendasikan scope yang lebih sempit.

---

# 14. Density Is Conceptual Before Numerical

Word count bukan satu-satunya ukuran density.

Prioritas evaluasi:

```text
1. conceptual density
2. visual/text-area density
3. word count
```

18 kata dengan tiga konsep berbeda dapat lebih berat daripada 30 kata yang menjelaskan satu ide sederhana.

Word count digunakan sebagai guardrail, bukan definisi kualitas.

---

# 15. The Carousel Must Stand on Its Own

Carousel harus self-contained.

Audience harus dapat memahami central argument tanpa:

* membaca caption;
* membuka komentar;
* membuka source;
* membuka website;
* membaca postingan lain.

Caption tidak boleh digunakan untuk menambal reasoning yang hilang dari carousel.

---

# 16. Caption Is Supporting Content

Caption bukan artikel kedua.

Caption bersifat supplementary.

Fungsi yang valid:

```text
short commentary
question
CTA
small contextual note
additional hook
```

Caption harus singkat kecuali suatu hari terdapat perubahan explicit pada content strategy.

---

# 17. CTA Is Optional

CTA bukan mandatory component.

Engine tidak perlu selalu menghasilkan:

```text
“save postingan ini”
“share ke temanmu”
“komen di bawah”
```

CTA hanya digunakan jika:

* natural;
* sesuai narrative;
* memiliki fungsi jelas.

CTA dapat ditempatkan di:

```text
carousel
caption
none
```

---

# 18. Hook May Be Strong, But Never Misleading

Cover dapat provocative.

Contoh:

```text
GAJI NAIK,
KOK MALAH MAKIN MISKIN?
```

diperbolehkan jika carousel benar-benar menjelaskan claim tersebut.

Prinsip:

> **Increase curiosity, not factual exaggeration.**

Hook tidak boleh:

* menjanjikan sesuatu yang tidak dibahas;
* mengubah probabilistic claim menjadi certainty;
* membuat hubungan sebab-akibat yang tidak didukung;
* menggunakan angka yang tidak tersedia;
* menyembunyikan nuance yang penting.

---

# 19. Clarity Beats Cleverness

Copy yang terlihat pintar tetapi sulit dipahami bukan output yang baik.

Prioritas:

```text
clear
before
clever
```

Analogi, wordplay, humor, atau provocative framing hanya digunakan jika meningkatkan komunikasi.

Jika justru menambah cognitive load, gunakan expression yang lebih sederhana.

---

# 20. Simplify Language, Not Meaning

Engine harus mampu menyederhanakan bahasa keuangan.

Namun simplification tidak boleh menghapus nuance penting.

Prinsip:

> **Simplify the explanation without simplifying away the truth.**

Istilah teknis dapat:

* dijelaskan;
* diganti dengan bahasa sederhana;
* diberi contoh;

tetapi tidak boleh dipelintir menjadi konsep berbeda.

---

# 21. Visual Is Part of Communication

Visual bukan decoration layer yang ditambahkan setelah copy selesai.

Visual merupakan bagian dari cara message disampaikan.

Default principle:

> **Every visual should have a communication function.**

Fungsi dapat berupa:

```text
EXPLAIN
COMPARE
DEMONSTRATE
SYMBOLIZE
CONTEXTUALIZE
ATTRACT_ATTENTION
```

---

# 22. Visual Does Not Need to Be Literal

Visual yang baik tidak harus menjadi representasi literal kalimat.

Contoh message:

```text
“Pengeluaran kecil bisa menggerus cashflow.”
```

Visual tidak harus berupa:

```text
orang sedang membayar tagihan
```

Bisa menggunakan:

```text
dompet bocor
```

selama metaphor mudah dipahami dan tidak menyesatkan.

---

# 23. Decorative Visual Is an Exception, Not a Failure

Beberapa message sulit atau tidak perlu divisualisasikan secara langsung.

Contoh:

* conclusion;
* transition;
* abstract takeaway.

Dalam kondisi ini decorative/environmental visual diperbolehkan.

Contoh:

```text
minimal building photo
photographed texture
subtle environmental image
```

Prinsipnya:

> Jangan memaksakan visual metaphor buruk hanya agar slide terlihat “pintar”.

---

# 24. Every Slide Still Needs Visual Treatment

Meskipun visual tidak selalu explanatory, setiap slide idealnya memiliki visual treatment.

Visual treatment dapat berupa:

```text
hero image
background photo
photographed texture
minimal photographic object
```

Text-only slide bukan default.

---

# 25. Choose the Simplest Visual That Works

Jika satu concept dapat disampaikan dengan:

```text
simple object
```

jangan otomatis memilih:

```text
complex cinematic scene
```

Prinsip:

> **Visual complexity should be justified by communication value.**

Sederhana sering lebih efektif untuk carousel.

---

# 26. Visual Variety Without Visual Chaos

Carousel tidak harus menggunakan layout identik di setiap slide.

Variasi diperbolehkan dalam:

* composition;
* object position;
* background;
* scale;
* metaphor;
* visual format.

Namun variation harus tetap terasa cohesive melalui:

* brand constraints;
* typography system;
* hierarchy;
* recurring visual language;
* production treatment.

Tujuannya bukan membuat template kaku.

Tujuannya membangun:

> **visual grammar**

bukan:

> **visual repetition**

---

# 27. Visual Direction Must Be Production-Aware

Visual idea yang menarik tetapi sangat sulit diproduksi dengan resource tersedia merupakan visual direction yang buruk.

Engine harus mempertimbangkan:

* available tools;
* manual editing capability;
* AI generation limitations;
* asset availability;
* time;
* complexity.

Prinsip:

> **Creative direction must survive contact with production.**

---

# 28. High-Resolution Instructions

Visual direction tidak boleh berhenti di level:

```text
“orang sedang budgeting”
```

Brief harus cukup detail untuk dieksekusi.

Minimal dapat mencakup:

```text
subject
visual function
scene
composition
framing
position
negative space
text zone
background
lighting
hierarchy
editing treatment
```

Semakin downstream keputusan tersebut dibutuhkan, semakin jelas brief harus menjelaskannya.

---

# 29. Resolve Decisions Before Handoff

Engine bertujuan mengurangi blank-page work dan decision fatigue.

Karena itu, output tidak boleh hanya berisi:

```text
“mungkin gunakan A/B/C/D”
```

Default:

```text
PRIMARY DECISION
```

Primary adalah resolved path.

---

# 30. Avoid Option Dumping

Memberikan terlalu banyak alternatif bukan selalu membantu.

Jika engine memberikan:

```text
10 headlines
8 visual concepts
7 compositions
```

maka keputusan hanya dipindahkan kembali ke manusia.

Prinsip:

> **The engine should make decisions, not outsource decisions back to the reviewer.**

---

# 31. Real Events Prefer Real Evidence

Untuk:

* tokoh nyata;
* perusahaan nyata;
* kejadian nyata;
* dokumentasi sejarah;
* news event;

real asset lebih diutamakan.

AI-generated imagery tidak boleh menghasilkan synthetic documentation yang mudah disalahartikan sebagai foto kejadian nyata.

---

# 32. Synthetic Visuals Are Best for Concepts

AI-generated visual sangat sesuai untuk:

```text
conceptual metaphor
generic scenario
symbolic object
fictional photographic scene
abstract financial idea
```

Bukan untuk memalsukan dokumentasi.

---

# 33. Asset Strategy Follows Communication Need

Carousel menggunakan image + text. Visual utama harus image-led; AI-generated image default-nya realistic/photorealistic, terlihat seperti foto nyata. Untuk konsep atau scene generic, prioritaskan AI-generated photorealistic image. Style lain hanya jika input memintanya secara eksplisit; topik edukasi bukan alasan otomatis untuk cartoon, vector/flat illustration, atau illustrated infographic.

Untuk real person, real company, real event, atau documentary evidence, prioritaskan REAL_ASSET. HYBRID_COMPOSITE digunakan jika perlu kombinasi image asset atau compositing ringan; menambahkan text ke image saja tidak membuat strategy menjadi hybrid.

Registry hanya berisi image asset AI_GENERATED atau REAL_ASSET. Text, angka, dan label tetap berada di slide copy/design instructions, bukan asset registry. Visual yang dipilih harus mengikuti batas ini.

Pilihan strategy per slide: AI_SYNTHETIC, REAL_ASSET, HYBRID_COMPOSITE. Pemilihan tetap mempertimbangkan message, kebutuhan documentary evidence, dan production feasibility.

---

# 34. Image Generation Is an Asset Step, Not Final Design

AI image generator digunakan untuk menghasilkan asset.

Bukan final carousel.

Typography utama, informational copy, dan final composition dikerjakan pada design stage.

Prinsip:

```text
AI
→ asset generation

Canva/design tool
→ image placement and typography
```

---

# 35. Generated Images Should Respect Layout Needs

Prompt tidak hanya menjelaskan subject.

Prompt juga harus mempertimbangkan bagaimana asset digunakan.

Contoh:

```text
leave negative space on left
place subject on lower-right
avoid text inside generated image
clean separation from background
```

Image generation harus direncanakan sebagai bagian dari layout.

---

# 36. Tool-Agnostic, Operationally Specific

Core engine tidak bergantung pada tool tertentu.

Instruksi tidak perlu berkata:

```text
Open Midjourney
```

tetapi juga tidak boleh terlalu abstrak:

```text
Generate an image.
```

Prinsip:

> **Abstract the tool, not the action.**

Contoh:

```text
Buka platform yang biasa digunakan untuk generate gambar.
Copy prompt berikut.
Generate beberapa hasil.
Pilih output yang paling sesuai dengan composition requirement.
```

---

# 37. Manual Work Is Not a System Failure

Canva/design tool digunakan untuk display-copy blocks, typography, crop, resize/reposition image, remove background bila perlu, gradient ringan untuk readability, opacity, dan layering sederhana image + text.

Engine tidak merencanakan custom graphic components, icon system, Canva shapes sebagai visual utama, diagram manual, decorative graphic composition, atau illustrated infographic components. Larangan ini juga berlaku di asset requirements, prompts, dan production instructions; jangan menyamarkan komponen grafis sebagai AI_GENERATED atau REAL_ASSET. Manusia boleh mengimprovisasi graphic embellishment saat desain, tetapi itu di luar tanggung jawab dan output engine.

Tujuan bukan mengotomatisasi semua langkah.

Manual editing diperbolehkan jika:

* lebih cepat;
* lebih reliable;
* lebih mudah dikontrol;
* tidak worth diotomatisasi.

Prinsip:

> **Optimize for total effort, not automation percentage.**

Workflow hybrid dapat menjadi solusi terbaik.

---

# 38. Human Review Is a Feature

Human review bukan fallback karena AI tidak cukup bagus.

Human review merupakan bagian intentional dari architecture.

Sistem harus menghasilkan:

```text
NEEDS_REVIEW
```

sebelum production.

Reviewer melakukan judgment terhadap:

* factual presentation;
* editorial direction;
* copy;
* narrative;
* visual;
* production feasibility.

---

# 39. Do Not Require Human Review at Every Internal Step

Meskipun human gate penting, engine tidak perlu meminta approval setelah setiap tahap internal.

Default lifecycle:

```text
INPUT
↓
ENGINE PROCESS
↓
PRODUCTION BRIEF
↓
HUMAN REVIEW
```

Tujuannya tetap mengurangi operational friction.

---

# 40. Local Revision Should Stay Local When Possible

Jika hanya satu slide bermasalah, jangan otomatis membuat ulang seluruh carousel.

Namun local revision harus mengecek consistency dengan:

```text
previous slide
next slide
overall narrative
```

Prinsip:

> **Minimize unnecessary regeneration without breaking narrative coherence.**

---

# 41. Failure Is Better Than Hallucinated Success

Engine tidak harus selalu menghasilkan carousel.

Jika input tidak cukup:

```text
BLOCK
```

lebih baik daripada menghasilkan output lemah yang terlihat meyakinkan.

Prinsip:

> **A useful refusal is better than an unreliable brief.**

---

# 42. Failure Must Be Actionable

`BLOCKED` bukan akhir tanpa arah.

Failure output harus menjawab:

```text
what is wrong?
why does it matter?
what is missing?
what should upstream do?
when can the engine resume?
```

Failure harus menghasilkan repair path.

---

# 43. Distinguish Fatal and Non-Fatal Problems

Tidak semua masalah membutuhkan STOP.

## Fatal

Contoh:

```text
objective unsupported
critical information missing
central claim unresolved
scope fundamentally too broad
```

→ `BLOCKED`

## Non-Fatal

Contoh:

```text
no concrete example
visual source unavailable
one secondary source weak
```

→ continue + warning

Prinsip:

> **Block only when continuing would make the brief unreliable or fundamentally incomplete.**

---

# 44. Preserve Uncertainty

Jika source mengatakan:

```text
may
can
often
in some cases
```

engine tidak boleh mengubahnya menjadi:

```text
always
will
definitely
```

Uncertainty adalah bagian dari factual meaning.

---

# 45. Preserve Relevant Disagreement

Jika credible material berbeda pendapat dan perbedaan tersebut penting bagi audience, engine harus mempertahankannya.

Engine tidak harus memaksakan satu jawaban hanya agar narrative terlihat bersih.

Clarity bukan berarti menghapus uncertainty.

---

# 46. Trace Important Claims

Important factual claims harus traceable.

Terutama:

```text
numbers
statistics
regulations
research findings
specific claims
specific historical facts
```

Traceability diperlukan untuk:

* review;
* QA;
* revision;
* citation decision.

---

# 47. Visible Citation Is Contextual

Internal source mapping dan visible citation adalah dua hal berbeda.

Tidak semua basic statement harus memenuhi layout dengan source label.

Namun statistik, regulasi, study, atau klaim spesifik dapat membutuhkan visible source.

Prinsip:

> **Trace everything important internally; display sources externally when useful or necessary.**

---

# 48. Brand Changes Expression, Not Truth

Brand context dapat mengubah:

```text
tone
vocabulary
humor
sentence structure
visual language
energy
personality
```

Brand context tidak dapat mengubah:

```text
facts
evidence
meaning
uncertainty
```

---

# 49. Brand Is Injected Context

Brand identity bukan bagian permanen dari editorial core.

Core harus tetap berfungsi saat brand context berubah.

Prinsip:

```text
core behavior
+
injected brand constraints
```

bukan:

```text
brand assumptions hard-coded into reasoning
```

---

# 50. Mock Must Be Explicitly Mock

Mock context digunakan untuk development.

Jika audience, brand, tone, atau raw material belum final:

```text
context_mode: MOCK
```

harus terlihat jelas.

Prinsip:

> **Never allow a temporary assumption to silently become system truth.**

---

# 51. Production Context Is Replaceable

Hal seperti:

```text
canvas ratio
preferred design tool
preferred image generator
export convention
```

adalah production context.

Bukan core editorial principle.

Jika tool berubah, engine core seharusnya tetap sama.

---

# 52. Standardize Quality, Not Creativity

Engine harus konsisten pada:

```text
factual grounding
editorial discipline
output structure
reviewability
brand constraints
```

Tetapi boleh variatif pada:

```text
story
headline
metaphor
composition
visual concept
creative expression
```

Prinsip:

> **Predictable quality, non-predictable creativity.**

---

# 53. Rules Have Different Severity

Tidak semua rule mempunyai kekuatan sama.

Gunakan tiga tingkat:

## MUST

Tidak boleh dilanggar.

Contoh:

```text
MUST NOT invent factual claims.
```

## SHOULD

Default yang diharapkan.

Dapat dilanggar jika terdapat alasan.

Contoh:

```text
A slide SHOULD have one core message.
```

## MAY

Creative discretion.

Contoh:

```text
A slide MAY use a visual metaphor.
```

---

# 54. Do Not Turn Guidelines Into Rigid Templates

Sistem tidak boleh menyimpulkan:

```text
“hook harus selalu slide 1”
“example harus selalu slide 4”
“conclusion harus selalu slide 6”
```

hanya karena pola tersebut sering digunakan.

Prinsip harus menghasilkan consistency tanpa membuat format monoton.

---

# 55. Story Structure Should Follow Material

Narrative dipilih berdasarkan material.

Possible structures antara lain:

```text
hook → problem → explanation → example → takeaway
```

atau:

```text
myth → reality → mechanism → implication
```

atau struktur lain.

Tidak ada satu universal narrative template.

---

# 56. Avoid Fake Storytelling

Tidak semua konten membutuhkan cerita dramatis.

Engine tidak perlu membuat karakter fiktif atau mini-story jika explanation sederhana lebih efektif.

Storytelling adalah tool.

Bukan kewajiban.

---

# 57. Production Feasibility Is Part of Quality

Output belum dianggap bagus jika:

```text
editorially strong
but
nearly impossible to produce
```

Brief harus mempertimbangkan kemampuan produksi aktual.

Production feasibility termasuk quality dimension.

---

# 58. Production Operator Should Not Start From Zero

Setelah brief approved, operator seharusnya tidak perlu bertanya lagi:

```text
“visualnya apa?”
“headline-nya apa?”
“foto apa yang perlu dicari?”
“prompt-nya bagaimana?”
“elemen ini ditaruh di mana?”
```

Micro-decisions tetap ada.

Fundamental creative decisions seharusnya sudah resolved.

---

# 59. Do Not Over-Specify Micro-Decisions

Meskipun brief harus detail, engine tidak perlu menentukan semua detail pixel-level.

Out of scope untuk reasoning utama:

```text
exact kerning
exact font size
1–2 pixel spacing
minor crop adjustment
tiny positional tuning
```

Prinsip:

> **Resolve creative intent, leave execution micro-adjustments to production.**

---

# 60. Keep Core Model-Agnostic

Prinsip sistem tidak boleh bergantung pada behavior unik satu model.

Prompt boleh berubah.

Model boleh berubah.

Evaluation harus tetap mengecek behavior yang sama.

---

# 61. Keep Core Tool-Agnostic

Engine bukan workflow Midjourney.

Bukan workflow Canva.

Bukan workflow Claude.

Bukan workflow Codex.

Tool hanyalah implementation layer.

---

# 62. Prefer Simple Architecture Until Complexity Is Earned

V0 tidak membutuhkan complexity hanya karena complexity memungkinkan.

Tidak otomatis menggunakan:

```text
multi-agent
MCP
vector database
memory system
multiple orchestration layers
autonomous loops
```

Prinsip:

> **Complexity must solve an observed problem.**

---

# 63. Manual First, Automate Second

Workflow baru sebaiknya diuji secara manual sebelum diotomatisasi.

Urutan:

```text
design
↓
run manually
↓
observe
↓
refine
↓
repeat
↓
identify stable repetition
↓
automate
```

Bukan:

```text
guess workflow
↓
automate
↓
discover workflow was wrong
```

---

# 64. Evaluation Before Optimization

Sebelum mengoptimalkan prompt atau workflow, sistem harus mempunyai cara menilai output.

Contoh dimension:

```text
factual integrity
editorial compression
clarity
narrative coherence
copy density
visual relevance
production feasibility
```

Prinsip:

> **Do not optimize behavior you cannot evaluate.**

---

# 65. Test Against Different Input Conditions

Engine tidak hanya diuji dengan input ideal.

Testing harus mencakup:

```text
simple material
dense material
numerical material
ambiguous material
conflicting material
insufficient material
```

Tujuannya bukan hanya melihat apakah engine dapat sukses.

Tujuannya juga melihat apakah engine:

```text
knows when not to succeed
```

---

# 66. Stable Contracts, Flexible Internals

Input/output contract idealnya lebih stabil daripada internal prompting.

Internal implementation dapat berevolusi.

Prinsip:

```text
stable interface
+
replaceable implementation
```

Hal ini memudahkan engine berkembang tanpa merusak downstream workflow.

---

# 67. Human-Readable and Machine-Readable

System artifacts harus sebisa mungkin dapat digunakan oleh:

```text
human
+
AI
+
automation
```

Dokumentasi harus dapat dibaca manusia.

Structured output harus dapat diproses mesin.

Keduanya tidak boleh saling mengorbankan.

---

# 68. Explain Important Decisions

Engine tidak perlu menjelaskan setiap token yang dibuat.

Namun keputusan fundamental sebaiknya memiliki rationale jika berguna untuk review.

Contoh:

```text
selected angle
omitted major material
asset strategy
blocked reason
warning
```

Tujuannya adalah reviewability, bukan chain-of-thought reproduction.

---

# 69. Minimize Reviewer Cognitive Load

Reviewer seharusnya mengevaluasi keputusan, bukan membongkar bagaimana sistem bekerja.

Brief harus memudahkan pertanyaan:

```text
Is this correct?
Is this clear?
Is this on-brand?
Can this be produced?
```

Bukan:

```text
What exactly is the AI trying to do here?
```

---

# 70. A Good Brief Is Executable

Production brief dinilai bukan hanya dari kualitas tulisan.

Tes akhirnya:

> **Bisakah seseorang menjalankan brief ini menjadi carousel tanpa harus mengulang proses berpikir dari awal?**

Jika jawabannya tidak, brief belum selesai.

---

# 71. V0 Principle Hierarchy

Jika beberapa prinsip bertabrakan, gunakan hierarchy berikut:

```text
1. Factual Integrity
2. Objective Integrity
3. Clarity
4. Editorial Focus
5. Production Feasibility
6. Visual Communicability
7. Brand Consistency
8. Engagement
9. Completeness
10. Creative Novelty
```

Catatan:

Brand consistency berada di bawah factual dan objective integrity bukan karena brand tidak penting, tetapi karena brand mengatur **expression**, bukan factual truth.

---

# 72. Final Principle

Semua prinsip di atas dapat diringkas menjadi:

> **Make fewer, better, grounded decisions before production begins.**

`carousel-brief-engine` berhasil ketika ia mampu mengubah material yang belum terstruktur menjadi brief yang:

```text
focused
grounded
clear
visual
executable
reviewable
```

tanpa mengubah proses menjadi sistem yang lebih kompleks daripada masalah yang sedang diselesaikan.

