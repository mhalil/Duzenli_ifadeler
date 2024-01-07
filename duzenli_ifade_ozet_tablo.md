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
| `\B`  | `\b` nin tam tersidir.                                                            | 'py\B'      | **"python, py3, py2"**                                                                | `py` içeren ancak `py` ile BİTMEYENLERİ göster demiş olduk. **"py," , "py."** ve **"py!"** ile eşleşmez                                                                                                                       |
| `\B`  | `\b` nin tam tersidir. `\B...\B` şeklinde kullanımına dair örnek                  | '\Ber\B'    | **"Sertaç"** `er` ibaresi kelimenin içinde olacak ancak başında ve sonunda OLMAYACAK. | **"erkek,"**, **seher**,  ve **"şeker"** kelimeleri eşleşmez, çünkü bu kelimeler **er** ibaresi kelimelerin başında ya da sonunda bulunuyor. Sadece içinde **er** ibaresi olan kelimeler eşleşir.                             |

## Karakter Türleri

| Simge            | Desen Açıklaması                                                                        | Örnek Desen  | Eşleşen Örnek                   | Açıklama                                                                                                                                          |
| ---------------- | --------------------------------------------------------------------------------------- | ------------ | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `.`              | herhangi bir tek karakterle eşleşir                                                     | `"öz.an"`    | öz**c**an, öz**k**an, öz**h**an | **öz** ile başla ardından herhangi BİR karakter gelsin **an** ile bitsin.                                                                         |
| `\d`             | herhangi bir rakamla (digit) eşleşir                                                    | `"\d{2}"`    | **41**, **60**, **65**          | 2 tane rakam yanyana gelsin.                                                                                                                      |
| `\D`             | rakam olmayan herhangi bir karakterle eşleşir                                           | `"-\D"`      | **-A**, **-$**                  | Tire (-) olsun ardından rakam olmayan bir karakter gelsin.                                                                                        |
| `\w`             | herhangi bir kelime karakteriyle (word) eşleşir (alfanümerik karakterler ve alt çizgi). | `"\w{3}"`    | **TR_** , **015** , **Vn4**     | `[a-zA-Z0-9_]` ifadesine eşittir.                                                                                                                 |
| `\W`             | alfanümerik karakterler ve alt çizgi dışındaki karakterlerle eşleşir                    | `"\d\W"`     | **9&**, **1+**, **3]**          | `\w` 'nin tersidir. `[^a-zA-Z0-9_]` ifadesine eşittir.                                                                                            |
| `\s`             | herhangi bir (space) boşluk karakteriyle (boşluk, sekme, yeni satır vb.) eşleşir.       | `"\d\s\w"`   | **5 W**, **7 a**                | Bir rakam, ardından bir boşluk ve son olarak alfanümerik karakter ile eşleş.                                                                      |
| `\S`             | boşluk karakteri (boşluk, sekme, yeni satır vb.) dışında karakterle eşleşir.            | `"\d+\S\w+"` | **2Nisan**, **1-Ocak**          | `\s` 'nin tersidir. Başta Rakam olsun, sonrasında Boşluk dışında bir karakter gelsin ve onu bir veya daha fazla alfanumerik karakter takip etsin. |
| `\metacharacter` | Metakarakterle eşleşecek bir karakterle eşleşir.                                        | `"\d\.\w+"`  | **3.14**, **6.Mart**            | `\.` ifadesi nokta karakteri arar. `\\` ifadesi `\` karakterini arar.                                                                             |

## Karakter Sınıfları

| Simge   | Desen Açıklaması                                                                 | Örnek Desen | Eşleşen Örnek               | Açıklama                                                                                                                                                                                              |
| ------- | -------------------------------------------------------------------------------- | ----------- | --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `[xy]`  | Köşeli parantez içindeki her bir karakteri eşleştirir.                           | `h[au]y`    | **hay, huy**                |                                                                                                                                                                                                       |
| `[x-y]` | `-` ile belirtilen karakter aralığındaki her bir karakteri eşleştirir.           | `se[h-r]+`  | **seher, sertaç**           | **se** 'den sonra **h** ile **r** arasındaki tüm harfler gelebilir.                                                                                                                                   |
| `[^xy]` | `^` simgesi köşeli parantez içinde kullanıldığında **HARİÇ TUT** anlamına gelir. | `se[^h-m]+` | **sertaç**                  | **se** 'den sonra **h** ile **m** arasındaki hiçbir harfler **GELEMEZ**                                                                                                                               |
| `[^.]`  | Karakter sınıfı içindeki metakarakterleri eşleştir.                              | `.+[.^]`    | **2.345**, **3^2**, **py.** | İçinde **.** (nokta) ya da **^** (şapka) işareti olan ifadeyle eşleşir. Köşeli parantez dışında meta karakterleri eşleştirirken kaçış dizisi olan ters taksim `\` sembolü kullanılmalı. Örneğin `\. ` |

## Tekrar / Yineleme / Kopya

| Simge   | Desen Açıklaması                                                                       | Örnek Desen | Eşleşen Örnek                    | Açıklama                                                                  |
| ------- | -------------------------------------------------------------------------------------- | ----------- | -------------------------------- | ------------------------------------------------------------------------- |
| `*`     | Kendinden önce gelen karakteri SIFIR veya DAHA FAZLA sayıda eşleştirir.                | `sa*t`      | st, s**a**t, s**aa**t, s**aaa**t | `a` karakteri **hiç** olmasada, **birden fazla** kez olsa da olur.        |
| `+`     | Kendisinden önce gelen karakteri BİR veya DAHA FAZLA sayıda eşleştirir.                | `.+met`     | ah**met**, meh**met**            | `met` karakter dizisinden önce **BİR veya DAHA FAZLA** karakter bulunsun. |
| `?`     | Kendisinden önce gelen karakterin SIFIR veya BİR defa eşleştirir.                      | `sa?t`      | st, s**a**t                      | `a` karakteri ya **HİÇ** olmasın ya da **BİR** tane olsun.                |
| `{}`    | Bir eşleşmeden kaç adet istediğimizi belirtebiliyoruz.                                 | `sa{3}t`    | s**aaa**t                        | `a` karakteri **3 kez** tekrar etsin                                      |
| `{x,}`  | Bir karakterin **en az** kaç kez tekrar etmesini istediğimizi belirtebiliriz           | `sa{2,}t`   | s**aa**t, s**aaa**t              | `a` karakteri 2 ve daha fazla tekrar etsin.                               |
| `{x,y}` | Bir karakterin **en az ve en çok** kaç kez tekrar etmesini istediğimizi belirtebiliriz | `sa{1,2}t`  | s**a**t, s**aa**t                | `a` karakteri **en az BİR, en fazla İKİ** kez bulunsun.                   |

## Gruplama, Yakalama, değiştirme ve geri referanslar

| Simge         | Desen Açıklaması                                        | Örnek Desen                           | Eşleşen Örnek                                  | Açıklama                                                                                                                                                                                     |
| ------------- | ------------------------------------------------------- | ------------------------------------- | ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `(x)`         | Bir deseni gruplamak için kullanılır                    | `\w+(li)+\w+`                         | a**li**, ha**li**l, ha**lili**                 | `(li)+` ile birden fazla karakteri grup olarak ayarlayıp, **li** ifadesinden birden fazla var mı? ya da `(li){3}` deseni ile **li** ifadesinden peşpeşe 3 tane  var mı? diye aratabiliyoruz. |
| `(?:x)`       | Yakalamadan grup oluşturur.                             | `(?:us)(ta)`                          | M**usta**fa                                    | `us` ifadesini `group()` metodunu kullanarak yakalayamayız. `group() = group(0)` yani tüm eşleşmeyi yazdırır. `group(1)` ifadesi **ta** yı işaret eder, yani ilk eşleşmeyi.                  |
| `(?P<isim>x)` | Adlandırılmış bir yakalama grubu oluştur                | (?P\<birinci>\d{2})(?P\<ikinci>\d{2}) | Eşleşen: **1325**, "birinci": 13, "ikinci": 25 | `..group(1)` yerine, `...group("birinci")` yazarak eşleşme bölümlerine ulaşılabilir. Dikkat edin adlar, `group()` metodu içerisine **çift tırnak içinde** yazılmalı.                         |
| `(x\|y)`      | Düzenli ifade kalıplarını gruplar.                      | `a(b\|l)i`                            | a**l**i, a**b**i                               | **a**'dan sonra **b** ya da **l** gelsin, desen **i** ile bisin                                                                                                                              |
| `(x-y)`       | Düzenli ifade kalıplarını bir aralık dahilinde gruplar. | `(a-g)lim`                            | **a**lim, **e**lim                             | desen **a** ile **g** arasındaki tüm harflerle başlasın, **lim** ifadesi ile bitsin.                                                                                                         |

## Kaynak:

* [DataCamp.com](https://www.datacamp.com/cheat-sheet/regular-expresso)
* [Python.org](https://docs.python.org/tr/3/library/re.html#module-re)
* [Evieplus Academy](https://www.youtube.com/watch?v=V3Jr2sAHNno&list=WL&index=36&t=10)