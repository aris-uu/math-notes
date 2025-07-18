---
tags:
---
# Modul 1 Logika Proposisional

## Tujuan Pembelajaran

1. Memahami dasar-dasar pembuktian menggunakan Lean.
2. Memahami logika proposisional, meliputi konjungsi, disjungsi, negasi, implikasi, dan biimplikasi.

## Pendahuluan

Lean merupakan *interactive theorem prover* atau *proof assistant* yang dikembangkan oleh Leonardo de Moura dari sejak 2013[^1]. Mengapa Lean? Dalam beberapa tahun terakhir, Lean sudah mulai terkenal pada kalangan matematikawan untuk memformalisasikan hasil riset yang telah mereka kerjakan. Salah satu matematikawan ternama yang telah menggunakan Lean adalah Terence Tao yang memiliki beberapa proyek menggunakan Lean, di antaranya adalah [PFR](https://teorth.github.io/pfr/). Beberapa alasan terkenalnya Lean pada kalangan matematikawan adalah *syntax*-nya yang cukup *user-friendly* karena adanya *tactics* yang memungkinkan kita menuliskan bukti secara interaktif dan jika dibaca mirip seperti bukti pada kertas, adanya beberapa *tools* untuk menyederhanakan bentuk atau hitungan sederhana, komunitas yang cukup luas, dan adanya pustaka teorema matematika yang cukup besar, yaitu [mathlib](https://leanprover-community.github.io/mathlib-overview.html).

Dalam praktikum MA2111 Dasar-Dasar Matematika ini, Lean digunakan untuk membantu teman-teman sekalian dalam menuliskan bukti dengan benar. Dengan menggunakan Lean, kita terpaksa untuk menuliskan bukti yang benar karena jika tidak, Lean akan memberikan error yang menandakan bahwa ada sesuatu yang salah dalam bukti kita. Sebaliknya, jika Lean tidak memberikan error, maka dapat dipastikan bahwa bukti yang kita tuliskan sudah benar. Dalam praktisnya, verifikasi formal seperti ini dapat membantu matematikawan untuk membuktikan hal yang kompleks dengan keyakinan penuh bahwa buktinya sudah benar dan tidak ada kesalahan kecil yang terlewat. 

Lean dapat di-*install* secara offline dan digunakan melalui VSCode, tetapi pada praktikum ini, kita akan menggunakan Lean Web Server yang tersedia pada laman https://live.lean-lang.org/.

## Syntax Dasar

Pada praktikum ini, praktikan akan diberikan *file* yang berisikan pernyataan dari teorema-teorema yang belum ada atau hanya ada sebagian buktinya. Tugas dari praktikan adalah untuk mengisi lubang-lubang yang berada pada bukti tersebut. Meskipun tidak akan diujikan pada praktikum, penting untuk mengetahui bagaimana cara menuliskan pernyataan suatu teorema pada Lean.

Secara umum, *syntax* untuk menuliskan pernyataan teorema adalah sebagai berikut.

```lean
theorem {nama_teorema} {hipotesis} : {pernyataan} := {bukti}
```

Contoh 1
```haskell
theorem contoh_1 (P Q : Prop) : P ∧ Q → P := sorry
```

Pada contoh di atas, `sorry` digunakan sebagai *placeholder* untuk bukti dari teorema tersebut. Praktikan harus mengganti setiap `sorry`  dengan bukti yang valid. 

Catatan: untuk mengetik simbol-simbol matematika dapat menggunakan *backslash* dan diikuti dengan namanya, misal `\and` untuk mengetik `∧`.  Referensi lengkapnya dapat dilihat di *file cheatsheet*.

Jika tidak ingin memberi nama, maka bisa menggunakan *keyword* `example` seperti pada contoh berikut.

Contoh 2
```haskell
example (P Q : Prop) : P ∧ Q → P := sorry
```

Perbedaannya adalah ketika kita memberi nama pada suatu teorema, maka teorema tersebut dapat kita gunakan pada bukti-bukti setelahnya.

## Pembuktian Dasar

Seperti yang telah dijelaskan pada pendahuluan, Lean memiliki mode *tactic* yang membantu kita untuk menuliskan bukti secara interaktif dan membuat bukti yang kita tulis mirip seperti yang biasa ditulis di kertas. Oleh karena itu, pada praktikum ini, kita hanya akan menggunakan mode *tactic*, meskipun praktikan boleh tidak menggunakannya jika ingin bereksplorasi. Dalam modul ini, praktikan akan dikenalkan dengan beberapa taktik secara satu-persatu sesuai dengan konteks penggunaannya.

Untuk masuk ke mode *tactic*, gunakan keyword `by` setelah `:=`. 

```haskell
example (P : Prop) (h : P) : P := by
  -- mode tactic
```

Setelah masuk mode *tactic*, letakkan *cursor* pada baris di bawahnya, dan akan terdapat *tactic state* pada jendela di sebelah kanan.

> Tactic state
> **1 goal**
**P** : Prop
**h** : P
**⊢** P

Baris terakhir memberi tahu tentang *goal*, yaitu pernyataan yang harus kita buktikan, sedangkan baris di atasnya adalah hipotesis yang kita miliki. Dalam kasus ini, kita memiliki dua hipotesis, `P : Prop` yang menyatakan bahwa `P` adalah suatu pernyataan dan `h : P` yang menyatakan bahwa `h` adalah bukti bahwa `P` benar. Kemudian, *goal* kita adalah `P`, yang berarti kita harus membuktikan bahwa `P` benar. Namun, kita sudah punya bukti tersebut, yaitu `h`. Maka, dalam kasus ini, dapat digunakan taktik `exact` untuk memberikan buktinya secara langsung.

```lean
example (P : Prop) (h : P) : P := by
  exact h
```

Perhatikan bahwa *tactic state* pada saat ini adalah "No goals" sehingga buktinya telah selesai (hore!).

## Konjungsi

Konjungsi `P ∧ Q` benar jika dan hanya jika `P` dan `Q` benar keduanya. Untuk membuktikan *goal* dengan bentuk `P ∧ Q`, dapat dilakukan dengan cara membuktikan `P` dan `Q` masing-masing secara terpisah. Hal ini dapat dilakukan menggunakan taktik `constructor`.

```lean
example (P Q : Prop) (hp : P) (hq : Q) : P ∧ Q := by
  constructor
```

Saat ini, *tactic state*-nya adalah
> **2 goals**
**P Q** : Prop
**hp** : P
**hq** : Q
**⊢** P
> 
> **P Q** : Prop
**hp** : P
**hq** : Q
**⊢** Q

Kita dapat fokus satu per satu untuk setiap goal dengan menggunakan *syntax* `.` dan selesaikan *goal*-nya menggunakan taktik `exact` seperti di atas. Maka hasil akhirnya adalah sebagai berikut.

```lean
example (P Q : Prop) (hp : P) (hq : Q) : P ∧ Q := by
  constructor
  . exact hp
  . exact hq
```

Selain itu, bisa juga langsung memberikan bentuk eksak dari awal dengan menggunakan kurung siku (dapat diketik dengan `\<` dan `\>`) sebagai berikut.

```lean
example (P Q : Prop) (hp : P) (hq : Q) : P ∧ Q := by
  exact ⟨hp, hq⟩
```

Untuk menggunakan hipotesis berbentuk `h : P ∧ Q`, dapat menggunakan *syntax* `h.left` dan `h.right` untuk mengambil masing masing `P` dan `Q`. Bisa juga menggunakan `rcases h with ⟨hp, hq⟩` untuk langsung mengubah hipotesisnya menjadi dua hipotesis `hp : P` dan `hq : Q`.

```haskell
example (P Q : Prop) (h : P ∧ Q) : P := by
  exact h.left

example (P Q : Prop) (h : P ∧ Q) : P := by
  rcases h with ⟨hp, hq⟩
  exact hp
```
## Disjungsi

Disjungsi `P ∨ Q` benar jika dan hanya jika setidaknya salah satu dari `P` atau `Q` benar. Untuk membuktikan goal dengan bentuk `P ∨ Q` (ketik dengan `\or`) , kita dapat menggunakan taktik `left` atau `right` untuk mengubah goal menjadi `P` atau `Q` berturut-turut. 

```haskell
example (P Q : Prop) (hp : P) : P ∨ Q := by
  left
  exact hp
```

Kita juga bisa langsung memberikan bentuk eksaknya dengan menggunakan `Or.inl` atau `Or.inr` sebagai berikut.

```haskell
example (P Q : Prop) (hp : P) : P ∨ Q := by
  exact Or.inl hp
```

Untuk menggunakan hipotesis berbentuk `h : P ∨ Q`, kita dapat melakukan bagi kasus menggunakan `rcases h with hp | hq`. Setelah melakukan bagi kasus, maka *goal* akan terpisah menjadi dua, yang satu dengan hipotesis `hp : P` dan satu lagi dengan hipotesis `hq : Q`.

```haskell
example (P Q : Prop) (h : P ∨ Q) : Q ∨ P := by
  rcases h with hp | hq
  . exact Or.inr hp
  . exact Or.inl hq
```

Catatan: Perhatikan bahwa `rcases` dapat digunakan untuk konjungsi maupun disjungsi. Untuk sekarang, kita dapat menganggap taktik tersebut sebagai taktik "dekonstruksi". Pada konjungsi, `rcases` berfungsi untuk memecah pernyataan ke bagiannya, dan pada disjungsi berfungsi untuk membagi kasus.
## Implikasi

Implikasi `P → Q` benar jika dan hanya jika `Q` selalu benar jika kita asumsikan `P` benar. Untuk membuktikan *goal* berbentuk `P → Q` (tulis dengan `\r`), kita harus mengasumsikan `P` dan membuktikan `Q`, yang dapat dilakukan dengan taktik `intro h`. Taktik tersebut akan membuat hipotesis baru yaitu `h : P` dan mengubah *goal*-nya menjadi `Q`. Taktik ini ekivalen dengan mengatakan "Misalkan P benar" pada pembuktian biasa.

```haskell
example (P Q : Prop) : P → P ∨ Q := by
  intro h
  exact Or.inl h
```

Terdapat beberapa cara untuk menggunakan hipotesis berbentuk `h : P → Q`. Sebelum itu, harus kita ketahui bahwa kita dapat memperlakukan hipotesis `h` sebagai fungsi yang menerima masukan sesuatu dengan tipe `P` dan memberikan keluaran dengan tipe `Q`. Jika kita memiliki hipotesis `hp : P`, ekspresi `h hp` akan memiliki tipe `Q`. Ekspresi tersebut dapat kita interpretasikan sebagai `h(hp)`, yaitu mengaplikasikan fungsi `h` dengan masukan `hp`, hanya saja pengaplikasian fungsi di Lean tidak wajib menggunakan tanda kurung.

```haskell
example (P Q : Prop) (h : P → Q) (hp : P) : Q := by
  exact h hp
```

Selain itu, kita juga dapat menggunakan taktik `apply`. Jika kita memiliki *goal* berbentuk `Q` dan hipotesis `h : P → Q`, taktik `apply h` akan mengubah *goal*-nya menjadi `P`. Hal ini dapat kita interpretasikan sebagai kalimat berikut, "Karena `P → Q` benar dan kita ingin membuktikan `Q`, maka cukup untuk membuktikan bahwa `P` benar." 

```haskell
example (P Q : Prop) (h : P → Q) (hp : P) : Q := by
  apply h
  exact hp
```
## Negasi

Dalam Lean, pernyataan negasi `¬P` (tulis dengan `\not`) hanyalah notasi untuk `P → False`. Maka, untuk menggunakan hipotesis dengan negasi dan membuktikan negasi, sama dengan menggunakan dan membuktikan implikasi seperti telah dijelaskan di atas.

```haskell
example (P Q : Prop) (h : ¬(P ∨ Q)) : ¬P ∧ ¬Q := by
  constructor
  . intro hp
    exact h (Or.inl hp)
  . intro hq
    exact h (Or.inr hq)
```
## Biimplikasi

Biimplikasi `P ↔ Q` benar jika dan hanya jika `P→ Q` dan `Q → P` keduanya benar. Mirip seperti konjungsi, untuk membuktikan *goal* berbentuk `P ↔ Q` (tulis dengan `\lr`), dapat digunakan taktik `constructor` yang akan membuat dua *goal* terpisah, yaitu `P → Q` dan `Q → P`.

```haskell
example (P Q : Prop) : P ∧ Q ↔ Q ∧ P := by
  constructor
  . intro h
    rcases h with ⟨hp, hq⟩
    constructor
    . exact hq
    . exact hp
  . intro h
    rcases h with ⟨hq, hp⟩
    constructor
    . exact hp
    . exact hq
```

Sedangkan, untuk menggunakan hipotesis berbentuk `h : P ↔ Q`, dapat diambil masing-masing implikasinya dengan `h.mp : P → Q` dan `h.mpr : Q → P`. Selain itu, dapat digunakan juga taktik `rw [h]` yang akan mensubstitusikan `P` dengan `Q` pada *goal*.  Jika ingin melakukan substitusi sebaliknya, gunakan *syntax* `rw [←h]`. Jika ingin melakukan substitusi pada hipotesis, gunakan *syntax* `at`. 

```haskell
example (P Q : Prop) (h : P ↔ Q) (hp : P) : Q := by
  exact h.mp hp

example (P Q : Prop) (h : P ↔ Q) (hp : P) : Q := by
  rw [←h]
  exact hp

example (P Q : Prop) (h : P ↔ Q) (hp : P) : Q := by
  rw [h] at hp
  exact hp
```
## Beberapa Taktik Khusus

Untuk membuktikan *goal* berbentuk `True`, dapat digunakan taktik `trivial`.

```haskell
example (P : Prop) : P ∨ True := by
  right
  trivial
```

Jika kita dapat membuktikan `False`, maka pernyataan apa pun benar. Hal ini disebut dengan Principle of Explosion. Taktik `exfalso` dapat mengubah goal apa pun menjadi `False`. 

```haskell
example (P Q : Prop) (hp : P) (hnp : ¬P) : Q := by
  exfalso
  exact hnp hp
```

Sering kali *goal* yang kita miliki terlalu kompleks untuk diselesaikan secara langsung. Oleh karena itu, kita bisa menggunakan taktik `have` untuk menambahkan hipotesis baru yang akan membantu kita untuk menyelesaikan *goal* utama. Jika kita memiliki `h : P → Q` dan `hp : P`, maka `have hq := h hp` akan menambahkan hipotesis `hq : Q`. Selain itu, kita juga bisa menggunakan `have` untuk menambahkan *goal* sementara dengan *syntax* berikut `have h : (goal sementara) := by`. Baris tersebut akan mengubah *goal*-nya ke yang kita berikan dan kita harus membuktikannya. Setelah terbukti, maka hipotesis `h` akan ditambahkan yang dapat membantu kita untuk menyelesaikan *goal* utama.
## Logika Klasik

Sejauh ini, logika yang kita gunakan adalah logika konstruktif, karena kita sama sekali tidak menggunakan Law of Excluded Middle (LEM), yaitu `P ∨ ¬P` benar untuk setiap proposisi `P`. Di dalam logika klasik, kita dapat menggunakan LEM, biasanya digunakan untuk membagi kasus apakah `P` benar atau salah. Kita dapat menggunakan taktik `by_cases hp : P` untuk membagi kasus tersebut.

```haskell
example (P Q : Prop) : ¬(P ∧ Q) → ¬P ∨ ¬Q := by
  intro h
  by_cases hp : P
  . right
    intro hq
    exact h ⟨hp, hq⟩
  . exact Or.inl hp
```

Selain itu, kita juga bisa melakukan pembuktian dengan kontradiksi menggunakan taktik `by_contra h` untuk mengubah *goal* `P` menjadi `False` dan menambahkan hipotesis `h : ¬ P`. Namun, taktik ini memerlukan mathlib, sehingga kita harus mengimpornya terlebih dahulu menggunakan `import Mathlib.Tactic`. Alternatif yang tidak menggunakan mathlib adalah dengan menggunakan teorema `Classical.by_contradiction`.

Terakhir, di mathlib terdapat juga taktik `push_neg` yang akan "mendorong" negasi masuk ke dalam menggunakan hukum de morgan dan sejenisnya. Misalnya, `¬ (P ∨ Q)` akan diubah menjadi `¬P ∧ ¬Q`. Terdapat juga taktik yang menggabungkan kedua taktik di atas, yaitu `by_contra!` yang akan melakukan `push_neg` pada hipotesis yang baru.

# Latihan Soal

Buktikan sifat-sifat dari operator logika berikut.

```haskell
variable (p q r : Prop)

-- commutativity of ∧ and ∨
example : p ∧ q ↔ q ∧ p := sorry
example : p ∨ q ↔ q ∨ p := sorry

-- associativity of ∧ and ∨
example : (p ∧ q) ∧ r ↔ p ∧ (q ∧ r) := sorry
example : (p ∨ q) ∨ r ↔ p ∨ (q ∨ r) := sorry

-- distributivity
example : p ∧ (q ∨ r) ↔ (p ∧ q) ∨ (p ∧ r) := sorry
example : p ∨ (q ∧ r) ↔ (p ∨ q) ∧ (p ∨ r) := sorry

-- other properties
example : (p → (q → r)) ↔ (p ∧ q → r) := sorry
example : ((p ∨ q) → r) ↔ (p → r) ∧ (q → r) := sorry
example : ¬(p ∨ q) ↔ ¬p ∧ ¬q := sorry
example : ¬p ∨ ¬q → ¬(p ∧ q) := sorry
example : ¬(p ∧ ¬p) := sorry
example : p ∧ ¬q → ¬(p → q) := sorry
example : ¬p → (p → q) := sorry
example : (¬p ∨ q) → (p → q) := sorry
example : p ∨ False ↔ p := sorry
example : p ∧ False ↔ False := sorry -- jelasin exfalso
example : (p → q) → (¬q → ¬p) := sorry

-- classical
example : (p → q ∨ r) → ((p → q) ∨ (p → r)) := sorry
example : ¬(p ∧ q) → ¬p ∨ ¬q := sorry
example : ¬(p → q) → p ∧ ¬q := sorry
example : (p → q) → (¬p ∨ q) := sorry
example : (¬q → ¬p) → (p → q) := sorry
example : p ∨ ¬p := sorry
example : (((p → q) → p) → p) := sorry

```

Sumber: https://leanprover.github.io/theorem_proving_in_lean4/propositions_and_proofs.html

[^1]: https://lean-lang.org/about/