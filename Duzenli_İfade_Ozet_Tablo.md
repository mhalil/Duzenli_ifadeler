# Düzenli İfadeler Özet Tablosu (Regular Expressions Cheat Sheet)

## Karakterler Sınıfları

|Simge| Desen Açıklaması | Örnek Desen | Eşleşen Örnek | Açıklama |
|---|---|---|---|---|
| ^ | Çok satırlı desende ya da bir karakter dizisinin **başlangıç verisini** belirtir. |`^r` |**r**ecep |Sadece kendinden sonra gelen BİR karaktere BAKMIYOR. Farklı Paragraflarda arama yapar.|
|\A | Sadece karakter dizisinin **(Dizenin) başlangıcını** belirtir. |`\Ar` |**r**amazan | Sadece Kelime dizisinde  arama yapar, paragrafa bakmaz.|
|$ |  Çok satırlı desenin ya da dizelerin nasıl **biteceğini** belirtir. |`zan$` |ramaza**n** |Sadece kendinden önceki BİR karaktere BAKMIYOR |
|\Z | Karakter dizisinin nasıl **biteceğini** belirtir. |`\Zan`    |ramaz**an** | |
|\b | Kelime **başlangıcını** belirtir                  |`\bman`    |**man**zara | |
|\b | Kelime **bitimini** belirtir                      |`man\b`    | za**man**| | | 
|\b | Kelime **kesin sınırını** belirtir                |`\bhalil\b`| **"halil."**, **"(halil)"** ve  "adım **halil** demiştim."| karakter dizini iiçinde tam kelime eşleşmesi arar |
|\B | `\b` nin tam tersidir.                            |'py\B'     |**"python, py3, py2"** |**"py, py."** ve **"py!"** ile eşleşmez |
|\B | `\b` nin tam tersidir. `\B...\B` şeklinde kullanımına dair örnek         |'\Ber\B'     |**"seher, Sertaç"** |**"erkek,"** ve **"şeker"** ile eşleşmez, çünkü bu kelimeler **er** ile başlıyor ya da bitiyor. |
