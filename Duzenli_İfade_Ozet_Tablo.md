# Düzenli İfadeler Özet Tablosu (Regular Expressions Cheat Sheet)

## Sabitleyiciler / Sınırlayıcılar

| Simge | Desen Açıklaması                                                                  | Örnek Desen | Eşleşen Örnek                                                                         | Açıklama                                                                                                                                                                                                                      |
| ----- | --------------------------------------------------------------------------------- | ----------- | ------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `^`   | Çok satırlı desende ya da bir karakter dizisinin **başlangıç verisini** belirtir. | `^rec`      | **rec**ep                                                                             | Sadece kendinden sonra gelen BİR karaktere BAKMIYOR. Desenin tümüne bakıyor. Farklı Paragraflarda arama yapar.                                                                                                                |
| `\A`  | Sadece karakter dizisinin **(Dizenin) başlangıcını** belirtir.                    | `\Ar`       | **r**amazan                                                                           | Sadece Kelime dizisinde  arama yapar, paragrafa bakmaz.                                                                                                                                                                       |
| `$`   | Çok satırlı desenin ya da dizelerin nasıl **biteceğini** belirtir.                | `zan$`      | rama**zan**                                                                           | Sadece kendinden önceki BİR karaktere BAKMIYOR, tüm desene bakıyor.                                                                                                                                                           |
| `\Z`  | Karakter dizisinin nasıl **biteceğini** belirtir.                                 | `an\Z`      | ramaz**an**                                                                           | Kelime, kendinden önceki desen (**an**) ile bitmeli.                                                                                                                                                                          |
| `\b`  | Kelime **başlangıcını** belirtir                                                  | `\bman`     | **man**zara                                                                           | Kelimenin **man** ile **başlaması** gerektiğini belirtiyor.                                                                                                                                                                   |
| `\b`  | Kelime **bitimini** belirtir                                                      | `man\b`     | za**man**                                                                             | Kelimenin **man** ile **bitmesi** gerektiğini belirtiyor.                                                                                                                                                                     |
| `\b`  | Kelime **kesin sınırını** belirtir                                                | `\bHalil\b` | **"Halil."**, **"(Halil)"** ve  "adım **Halil** demiştim."                            | Karakter dizini içinde tam kelime eşleşmesi arar. **Halili** kelimesi desen ile eşleşmez çünkü kelime içinde başka harf te bulunuyor. Noktalama işaretleri, parantez,...vb karakterler harf olmadığı için sorun oluşturmuyor. |
| `\B`  | `\b` nin tam tersidir.                                                            | 'py\B'      | **"python, py3, py2"**                                                                | `py` ile BİTMEYENLERİ göster demiş olduk. **"py," , "py."** ve **"py!"** ile eşleşmez                                                                                                                                         |
| `\B`  | `\b` nin tam tersidir. `\B...\B` şeklinde kullanımına dair örnek                  | '\Ber\B'    | **"Sertaç"** `er` ibaresi kelimenin içinde olacak ancak başında ve sonunda OLMAYACAK. | **"erkek,"**, **seher**,  ve **"şeker"** kelimeleri eşleşmez, çünkü bu kelimeler **er** ibaresi kelimelerin başında ya da sonunda bulunuyor. Sadece içinde **er** ibaresi olan kelimeler eşleşir.                             |

## Karakter Türleri

| Simge            | Desen Açıklaması                                                                        | Örnek Desen | Eşleşen Örnek | Açıklama                           |
| ---------------- | --------------------------------------------------------------------------------------- | ----------- | ------------- | ---------------------------------- |
| `.`              | herhangi bir tek karakterle eşleşir                                                     |             |               |                                    |
| `\d`             | herhangi bir rakamla (digit) eşleşir                                                    |             |               |                                    |
| `\D`             | rakam olmayan herhangi bir karakterle eşleşir                                           |             |               |                                    |
| `\w`             | herhangi bir kelime karakteriyle (word) eşleşir (alfanümerik karakterler ve alt çizgi). |             |               | `[a-zA-Z0-9_]` ifadesine eşittir.  |
| `\W`             | alfanümerik karakterler ve alt çizgi dışındaki karakterlerle eşleşir                    |             |               | `\w` 'nin tersidir.                |
| `\s`             | herhangi bir (space) boşluk karakteriyle (boşluk, sekme, yeni satır vb.) eşleşir.       |             |               |                                    |
| `\S`             | boşluk karakteri (boşluk, sekme, yeni satır vb.) dışında karakterle eşleşir.            |             |               | `\s` 'nin tersidir.                |
| `\metacharacter` | Metakarakterle eşleşecek bir karakterle eşleşir.                                        |             |               | `\.` ifadesi nokta karakteri arar. |

## Karakter Sınıfları

| Simge    | Desen Açıklaması                                                                 | Örnek Desen | Eşleşen Örnek     | Açıklama                                                                |
| -------- | -------------------------------------------------------------------------------- | ----------- | ----------------- | ----------------------------------------------------------------------- |
| `[xy]`   | Köşeli parantez içindeki her bir karakteri eşleştirir.                           | `h[au]y`    | **hay, huy**      |                                                                         |
| `[x-y]`  | `-` ile belirtilen karakter aralığındaki her bir karakteri eşleştirir.           | `se[h-r]+`  | **seher, sertaç** | **se** 'den sonra **h** ile **r** arasındaki tüm harfler gelebilir.     |
| `[^xy]`  | `^` simgesi köşeli parantez içinde kullanıldığında **HARİÇ TUT** anlamına gelir. | `se[^h-m]+` | **sertaç**        | **se** 'den sonra **h** ile **m** arasındaki hiçbir harfler **GELEMEZ** |
| `[\^\.]` | karakter sınıfı içindeki metakarakterleri eşleştir.                              | `.+\.`      | 2.345             | İçinde **.** (nokta) olan ifadeyle eşleşir.                             |

## Tekrar / Yineleme / Kopya

| Simge    | Desen Açıklaması                                                                       | Örnek Desen | Eşleşen Örnek                    | Açıklama                                                                   |
| -------- | -------------------------------------------------------------------------------------- | ----------- | -------------------------------- | -------------------------------------------------------------------------- |
| `*`      | Kendinden önce gelen karakteri SIFIR veya daha fazla sayıda eşleştirir.                | `sa*t`      | st, s**a**t, s**aa**t, s**aaa**t | `a` karakteri **hiç** olmasada, **birden fazla** kez olsa da olur.         |
| `+`      | Kendisinden önce gelen karakteri BİR veya DAHA FAZLA sayıda eşleştirir.                | `.+met`     | ah**met**, meh**met**            | `met` karakter dizisinden önce **BİR veya DAHA FAZLA** karakter bulunsun.  |
| `?`      | Kendisinden önce gelen karakterin SIFIR veya BİR defa eşleştirir.                      | `sa?t`      | st, s**a**t                      | `a` karakteri ya **HİÇ** olmasın ya da **BİR** tane olsun.                 |
| `{}`     | Bir eşleşmeden kaç adet istediğimizi belirtebiliyoruz.                                 | `sa{3}t`    | s**aaa**t                        | `a` karakteri **3 kez** tekrar etsin                                       |
| `{x,}`   | Bir karakterin **en az** kaç kez tekrar etmesini istediğimizi belirtebiliriz           | `sa{2,}t`   | s**aa**t, s**aaa**t              | `a` karakteri 2 ve daha fazla tekrar etsin.                                |
| `{x,y}`  | Bir karakterin **en az ve en çok** kaç kez tekrar etmesini istediğimizi belirtebiliriz | `sa{1,2}t`  | s**a**t, s**aa**t                | `a` karakteri **en az BİR, en fazla İKİ** kez bulunsun.                    |
| `(x\|y)` | Düzenli ifade kalıplarını gruplar.                                                     | `a(b\|l)i`  | a**l**i, a**b**i                 | **a**'dan sonra **b** ya da **l** gelsin, desen **i** ile bisin            |
| `(x-y)`  | Düzenli ifade kalıplarını gruplar.                                                     | `(a-g)l`    | **a**l, **e**l                   | desen **a** ile **g** arasındaki tüm harflerle başlasın, **l** ile bitsin. |

## Kaynak:

* https://www.datacamp.com/cheat-sheet/regular-expresso
* https://docs.python.org/tr/3/library/re.html#module-re
* https://www.youtube.com/watch?v=V3Jr2sAHNno&list=WL&index=36&t=10
