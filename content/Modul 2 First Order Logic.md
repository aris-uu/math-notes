# Modul 2 Logika Kuantor

## Tujuan Pembelajaran

1. Memahami pembuktian yang menggunakan kuantor universal dan eksistensial.
2. Memahami pembuktian sederhana mengenai bilangan asli yang mengandung pernyataan berkuantor.

## Pendahuluan

Pada modul sebelumnya, kita telah mempelajari bagaimana cara membuktikan pernyataan dalam logika proposisional. Pada modul ini, kita akan mempelajari tentang logika kuantor, yang terdiri dari kuantor universal dan eksistensial. Untuk menggunakan kuantor tersebut, sebelumnya perlu didefinisikan suatu predikat atau pernyataan yang bergantung terhadap suatu variabel.

## Predikat

Predikat adalah suatu pernyataan logika yang nilai kebenarannya bergantung kepada suatu variabel. Misalnya, pernyataan x > 3 untuk x bilangan bulat adalah suatu predikat karena pernyataan tersebut bisa benar untuk (misal) x = 4 dan salah untuk x = 0. Dalam Lean, jika kita memiliki tipe `a`, maka suatu predikat uner (hanya bergantung pada satu variabel) dapat dinyatakan dengan `p : a → Prop`.  Artinya, jika kita memiliki variabel `x : a`, maka `p x` adalah suatu pernyataan yang menyatakan bahwa `p` berlaku di `x` . Dengan cara yang sama, suatu predikat biner (bergantung pada dua variabel) dapat dinyatakan dengan tipe `a → a → Prop`. 

## Kuantor Universal

Kuantor universal `∀ x : a, p x` (dapat ditulis menggunakan `\forall`) menyatakan bahwa untuk setiap `x : a`, `p x` berlaku. Sebenarnya, kuantor universal hanyalah notasi untuk `(x : a) → p x`, sehingga cara untuk membuktikan dan menggunakannya sama dengan pernyataan implikasi. Untuk membuktikan pernyataan yang mengandung kuantor universal, kita dapat menggunakan `intro x` untuk menambahkan hipotesis `x : a` kemudian kita harus membuktikan `p x`. Hal ini sama dengan mengatakan "Ambil x sebarang" pada pembuktian biasa.

```haskell
variable (a : Type)
variable (P : a → Prop)

example : ∀ x : a, x = x := by
  intro x
  rfl

example (x₀ : a) (h : ∀ x, P x) : P x₀ := by
  exact h x₀
```

## Kuantor Eksistensial

Kuantor existensial dapat ditulis dengan `exists x : a, p x` atau u x : a, p x` (dapat ditulis menggunakan `\exists`). Untuk membuktikan kuantor eksistensial, caranya mirip dengan operator dan, yaitu kita cukup memberikan term `x : a` dan juga bukti bahwa `p x` benar. Jika kita punya `x : a` dan `h : p x`, maka `⟨x, h⟩` adalah bukti untuk pernyataan `∃ x : a, p x`. Jika bukti dari `p x` cukup sulit, maka kita bisa hanya memilih `x`-nya saja terlebih dahulu menggunakan taktik `exists x`.

Sedangkan, untuk menggunakan pernyataan eksistensial dapat digunakan taktik `obtain` seperti berikut. Jika kita memiliki `h : ∃ x : a, p x`, maka `obtain ⟨x, h1⟩ := h` akan mengubah hipotesis `h` menjadi `x : a` dan `h1 : p x`.

```haskell
variable (a : Type)
variable (P Q : a → Prop)

example (x : a) (h : P x) : ∃ x, P x := by
  exists x

example (h1 : ∃ x, P x) (h2 : ∃ x, Q x) : ∃ x y, P x ∧ Q y := by
  obtain ⟨x, hp⟩ := h1
  obtain ⟨y, hq⟩ := h2
  exists x, y
```

## Bilangan Asli dan Kesamaan

Teorema-teorema yang dapat kita buktikan dengan hanya menggunakan logika proposisional dan kuantor tidak terlalu banyak. Untuk memperluas contoh yang mungkin, pada bagian ini akan dikenalkan konsep bilangan asli dan kesamaan dalam Lean. Dalam *standard library* Lean, sudah terdapat definisi bilangan asli yang dapat langsung kita gunakan, yaitu tipe `Nat`. Bilangan asli pada Lean mulai dari 0, dan terdapat fungsi suksesor, yaitu fungsi yang menghasilkan bilangan asli selanjutnya.

Kemudian, kesamaan pada lean dapat ditulis menggunakan `x = y`. Pernyataan tersebut dapat dibuktikan menggunakan taktik `rfl` jika ruas kiri dan ruas kanan sama secara definisi. Biasanya ruas kiri dan kanan belum tentu sama secara definisi dan harus dilakukan substitusi dulu agar sama. Kita bisa menggunakan taktik `rw` untuk melakukan substitusi sebagai berikut.

```haskell
example (h : y = 2 * x + 1) : 2 + y = 2 + (2 * x + 1) := by
	rw [h]
```

Perhatikan bahwa `rw` akan otomatis melakukan `rfl` jika memungkinkan sehingga kita tidak perlu menuliskannya lagi. Jika tidak ingin begitu, kita bisa gunakan taktik `rewrite`. Perlu diketahui juga bahwa kedua taktik tersebut juga dapat melakukan substitusi pada biimplikasi.
 
Sekarang, kita bisa mendefinisikan predikat pada bilangan bulat `is_even` yang menyatakan bahwa suatu bilangan asli itu genap sebagai berikut.

```haskell
def is_even (a : Nat) := ∃ b, a = 2 * b
```

Dari definisi ini, kita dapat membuktikan bahwa 4 adalah bilangan genap dengan memberikan bilangan 2 dan bukti bahwa 4 = 2 * 2 menggunakan taktik `exists` sebagai berikut.

```haskell
example : is_even 4 := by
  exists 2
```

Perhatikan bahwa buktinya langsung selesai begitu saja karena taktik `exists` langsung mengecek apakah 4 = 2 * 2 sudah terpenuhi atau belum, dan pada kasus ini sudah karena 2 * 2 adalah 4 dari definisi (tinggal dihitung).

Jika ingin lebih *step-by-step*, bisa dilakukan seperti ini.

```haskell
example : is_even 4 := by
  refine ⟨2, ?_⟩
  rfl
```

Taktik `refine` di atas mirip seperti `exact` tapi kita bisa memberikan lubang untuk ekspresi yang belum kita ketahui. Bisa juga langsung menggunakan `exact` seperti berikut. 

```haskell
example : is_even 4 := by
  exact ⟨2, rfl⟩
```

Pembuktian lebih lanjut menggunakan bilangan asli dan kesamaan akan dieksplorasi pada modul induksi matematika.

## Soal Latihan

Buktikan pernyataan-pernyataan berikut.

```haskell
variable (α : Type) (p q : α → Prop)

example : (∀ x, p x ∧ q x) ↔ (∀ x, p x) ∧ (∀ x, q x) := sorry
example : (∀ x, p x → q x) → (∀ x, p x) → (∀ x, q x) := sorry
example : (∀ x, p x) ∨ (∀ x, q x) → ∀ x, p x ∨ q x := sorry
```

```haskell
variable (α : Type) (p q : α → Prop)
variable (r : Prop)

example : α → ((∀ x : α, r) ↔ r) := sorry
example : (∀ x, p x ∨ r) ↔ (∀ x, p x) ∨ r := sorry
example : (∀ x, r → p x) ↔ (r → ∀ x, p x) := sorry
```

```haskell
variable (men : Type) (barber : men)
variable (shaves : men → men → Prop)

example (h : ∀ x : men, shaves barber x ↔ ¬ shaves x x) : False := sorry

```

```haskell
def is_even (a : Nat) := ∃ (b : Nat), a = 2 * b

example : ∀n : Nat, is_even (2 * n) := sorry
example : ∀n m : Nat, is_even m ∧ is_even n → is_even (m + n) := sorry
```
