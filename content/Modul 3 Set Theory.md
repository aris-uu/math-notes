
# Modul 3 Teori Himpunan

## Tujuan Pembelajaran

1. Memahami konsep himpunan dalam Lean.
2. Memahami operator himpunan bagian, komplemen, irisan, dan gabungan dalam Lean.
3. Memahami pembuktian yang berkaitan tentang himpunan dan operatornya dalam Lean.
## Himpunan

Pada modul ini, kita akan bekerja dalam suatu tipe semesta yang kita sebut sebagai `U`. Himpunan dalam Lean bersifat homogen, yaitu elemen dalam himpunannya harus memiliki tipe yang sama. Untuk bekerja dengan himpunan, kita memerlukan mathlib dan menambahkan baris `import Mathlib.Data.Set.Basic`. Jika `A` adalah himpunan dengan elemen dari `U`, kita bisa tulis sebagai `A : Set U`.  Dalam Lean, himpunan didefinisikan sebagai suatu predikat yang benar jika elemen tersebut ada di himpunannya. Jadi, sebenarnya `A` adalah suatu predikat yang bertipe `U → Prop`, dan `x ∈ A` (tulis dengan `\mem`) akan bernilai benar jika predikat `A x` bernilai benar.
## Himpunan Bagian

Jika `A` dan `B` merupakan sebuah himpunan, maka `A` disebut sebagai himpunan bagian dari `B` jika setiap anggota dari `A` juga merupakan anggota dari `B`. Kita bisa tulis ini sebagai `A ⊆ B` (tulis dengan `\sub`). Perhatikan bahwa `A ⊆ B` hanyalah notasi untuk `∀ x : U, x ∈ A → x ∈ B` sehingga kita bisa gunakan taktik `intro` seperti dijelaskan pada modul sebelumnya.

```haskell
import Mathlib.Data.Set.Basic

variable (U : Type) (A B C : Set U)

example (h1 : A ⊆ B) (h2 : x ∈ A) : x ∈ B := by
  exact h1 h2

example (h1 : A ⊆ B) (h2 : B ⊆ C) : A ⊆ C := by
  intro x h
  exact h2 (h1 h)
```
## Komplemen

Jika `A` merupakan sebuah himpunan, maka komplemennya dapat ditulis dengan `Aᶜ` (tulis dengan `\^c`). Pernyataan `x ∈ Aᶜ` didefinisikan sebagai `x ∉ A` (tulis dengan `\notin`). Fakta tersebut dapat diakses melalui teorema `Set.mem_compl_iff`.

```haskell
example (h : x ∉ A) : x ∈ Aᶜ := by
  exact h
```
### Komplemen Relatif

Jika `A` dan `B` merupakan himpunan, maka kita bisa menuliskan komplemen relatifnya dengan `A \ B`. Pernyataan `x ∈ A \ B` didefinisikan sebagai `x ∈ A ∧ ¬x ∈ B`. Fakta ini dapat diakses melalui teorema `Set.mem_diff`.

```haskell
example (h1 : x ∈ A) (h2 : x ∉ B) : x ∈ A \ B := by
  exact ⟨h1, h2⟩
```
## Irisan

Jika `A` dan `B` merupakan himpunan, maka irisannya dapat ditulis dengan `A ∩ B` (tulis dengan `\inter`). Pernyataan `x ∈ A ∩ B` didefinisikan sebagai `x ∈ A ∧ x ∈ B`. Fakta ini dapat diakses melalui teorema `Set.mem_inter_iff`.

```haskell
example (h1 : x ∈ A) (h2 : x ∈ B) : x ∈ A ∩ B := by
  exact ⟨h1, h2⟩
```
## Gabungan

Jika `A` dan `B` merupakan himpunan, maka irisannya dapat ditulis dengan `A ∪ B` (tulis dengan `\union`).  Pernyataan `x ∈ A ∪ B` didefinisikan sebagai `x ∈ A ∨ x ∈ B`. Fakta ini dapat diakses melalui teorema `Set.mem_union`.

```haskell
example (h : x ∈ A) : x ∈ A ∪ B := by
  exact Or.inl h
```
## Beberapa Himpunan Khusus

Selain operasi di atas, terdapat juga beberapa himpunan khusus, di antaranya himpunan semesta dan himpunan kosong, yang masing-masing dapat ditulis dengan `Set.univ` dan `∅` (tulis dengan `\empty`). Keduanya didefinisikan melalui predikat konstan yang berturut-turut selalu menghasilkan `True` dan `False`. Maka, pernyataan `x ∈ Set.univ` akan selalu benar dan `x ∈ ∅` akan selalu salah.

```haskell
example : (∅ : Set U) ⊆ Set.univ := by
  intro x h
  contradiction

example : (∅ : Set U) ⊆ Set.univ := by
  intro x h
  trivial
```

Perhatikan bahwa kedua bukti di atas merupakan bukti yang valid. Bukti yang pertama benar karena kita memiliki hipotesis `x ∈ ∅` yang merupakan kontradiksi. Bukti yang kedua benar karena kita memiliki *goal* `x ∈ Set.univ` yang selalu benar.
## Kesamaan Himpunan

Jika `A` dan `B` merupakan himpunan, kesamaan `A = B` didefinisikan sebagai `∀ x, x ∈ A ↔ x ∈ B`. Fakta ini dikenal sebagai "*extensionality*", yang menyatakan bahwa kedua benda itu sama jika tersusun oleh objek yang sama. Pada kasus ini, dua himpunan dianggap sama jika semua elemennya sama. Kita dapat menggunakan taktik `ext` untuk menerapkan fakta di atas. Misalnya, jika kita memiliki *goal* `A = B`, maka taktik `ext x` akan menambahkan hipotesis `x : U` dan mengubah *goal* menjadi `x ∈ A ↔ x ∈ B`. 

```haskell
example : Aᶜᶜ = A := by
  ext x
  rw [Set.mem_compl_iff, Set.mem_compl_iff]
  rw [Classical.not_not]
```
## Soal Latihan

```haskell
import Mathlib.Data.Set.Basic

variable (U : Type) (A B C : Set U)

example : A ∪ B = B ∪ A := by sorry
example : A ∩ B = B ∩ A := by sorry
example : A ∩ (B ∪ C) = (A ∩ B) ∪ (A ∩ C) := by sorry
example : A ⊆ A ∪ B := by sorry
example : A \ B ⊆ A := by sorry
example : A ∩ Bᶜ = A \ B := by sorry
```
