# Düzenli İfadeler (Regular Expressions)

**Düzenli ifadeler (RegEx ya da Regular Expression)**, bir karakter dizisi içinde bulunan, belli bir düzene uyan eşleşmeleri bulmanıza ve yönetmenize yardımcı olacak **desenler** oluşturmanıza izin veren bir metin dizisidir (bir string ifadedir). Bir metinde geçen karakterleri **RegEx desenleri (pattern)** kullanarak arayabiliriz.

Düzenli ifadeler bir arama işleminde eşleştirilecek deseni temsil eden özel dizelerdir. **Java** ve **Perl** gibi programlama dillerinden **grep, sed** ve metin düzenleyici **vim** gibi metin işleme araçlarına kadar çok çeşitli bilgi işlem uygulamalarında kullanılan önemli bir araçtır. 

**Düzenli ifadeler sayesinde ne yapabiliriz bir bakalım :**

* **Yer değiştirme:** Belirli parçaları değiştirir. Örnek olarak metin içerisindeki tüm büyük harfleri küçük harf ya da tüm küçük harfleri büyük harfe dönüştürebilirsiniz.

* **Doğrulama :** Yazdığınız bir program olsun, bu programda büyük veya küçük harf, nokta veya rakam gibi kriterleri karşılayıp karşılamadığını kontrol edebilirsiniz.

* **Arama :** Bir metin içerisindeki tüm ögeleri aratabilirsiniz. Örneğin telefon numaraları ya da e-posta adresleri gibi.

* **Koordinat ile hareket etme :** Örneğin, bir dizindeki belirli paketleri, dosyaları işlemek isteyebilirsiniz ancak yalnızca belirli koşulları karşılıyorlarsa, komut satırında çalıştırabiliyorsunuz.

* **Metni Yeniden Biçimlendirme :** Örneğin, Bir programdaki verileri metin dosyası olarak dışa aktarabilir, ardından düzenini değiştirerek metin düzenleyicisi kullanarak başka bir programa aktarabilirsiniz.

Python’daki düzenli ifadelere ilişkin her şey, bir modül içinde tutulur. Bu modülün adı **re**'dir. **re** modülü Python'ın dahili (build-in) modeüllerindendir. Ayrıca yüklememize gerek yoktur. Bilgisayarınızda Python yüklü ise, **re modülü** de yüklenmiş ve kullanıma hazır olarak bekliyordur.

Düzenli ifadeleri kullanabilmemiz için öncelikle bu **re** modülünü içe aktarmamız gerekir:

```python
import re
```

## RegEx Fonksiyonları / Metotları

**re** modülü bir veride geçen karakterleri bulmamıza ve değiştirmemize olanak sağlayan bazı fonksiyonlara sahiptir. Bunlar;

| **Fonksiyon / Metot** | **Açıklama**                                                                             |
| --------------------- | ---------------------------------------------------------------------------------------- |
| **match()**           | Karakter dizisinin başında eşleşme olup olmadığını göster                                |
| **search()**          | Eşleşme olup olmadığını göster                                                           |
| **findall()**         | Tüm eşleşmeleri göster (liste halinde)                                                   |
| **finditer()**        | Belirtilen desenlerin karakter dizileri içerisindeki konumunu bulmak için kullanabiliriz |
| **split()**           | Eşleşme noktalarından böl ve liste oluştur                                               |
| **sub()**             | Eşleşmeleri verilen ifade ile değiştir                                                   |
| **subn()**            | Eşleşmeleri verilen ifade ile değiştir, kaç adet değişiklik yapıldığını gösterir         |
| **escape()**          | Bir metni, düzenli ifade içinde kullanılmaya uygun hale getirmek için kullanılır         |
| **compile()**         | Düzenli İfadeleri Derlemek için kullanılır                                               |
| **purge()**           | Düzenli ifade önbelleğini temizlemek için kullanılır                                     |

## match() Metodu

Bir **karakter dizisi başında** belirli bir kelimenin ya da kelime grubunun geçip geçmediğini öğrenmek istiyorsak bu işlemi `match()` metodunu kullanarak yapabiliriz.

**match()** metodunun;

* ilk argümanı eşleştirilecek (aranacak) değer, yani desen
* ikinci argümanı ise, aramanın yapılacağı karakter dizisi olmalıdır.

```python
cumle = "python güçlü bir programlama dilidir."

re.match(r"python", cumle)
```

    <re.Match object; span=(0, 6), match='python'>

Yukarıdaki `r"python"` deseni, yani aranan değer, zaten bulunan değeri ile aynı olduğu için, bu arama/eşleşme yönteminin kullanımı size anlamsız/saçma gelmiş olabilir. 

İlerleyen bölümlerde **Metakarakterler** konusunu anlatılırken çok farklı desenler oluştururarak farklı sonuçlar bulacağız. O bölümde düzenli ifadelerin ne için kullanılabileceğini ve bizlere ne kadar kolaylık sağladığını anlayacaksınız. 

Düzenli ifadeler için bir desen tanımlarken, `r` ifadesini yazmamız istenir. İlerleyen bölümlerde göreceğimiz üzere, **özel metakarakterleri** desen içerisinde yazmamız gerektiğinde `r` ifadesini kullanmadığımızda sorun ile karşılaşırız. Özel metakarakterleri desen içerisinde yazmadığımız zaman da `r` ifadesini kullanmak sorun çıkarmıyor. Üstelik `r` ile tanımlanan ifade, bir değişken mi? yoksa bir düzenli ifade deseni mi? olduğu kodu inceleyenlere yardımcı oluyor.

`match` nesnesinin dönen değeri ile bazı işlemler yapılabilir. Bunun için nesnenin yöntemleri kullanılır. Bunlar;

* `span()` Başlangıç ve bitiş konumlarını **tuple** olarak verir.
* `string` Dönen metinsel dizgi ifadesini (string) yazdırır
* `group()` Eşleşen grupları yazdırır. (`group(1)`, `group(2)`, ...vb. `group(0) = group()` eşittir, tüm eşleşmeleri yazdırır.)

Bu çıktıdaki **span** parametresi bize, aradığımız **python** karakter dizisinin (yani desenin), **cumle** değişkeninin 0. ile 6. karakterleri arasında yer aldığını söylüyor.

### span() metodu

Eşleşmenin başladığı ve sona erdiği karakterlerin sırasını verir (0 değeri 1. karakteri temsil eder):

```python
cumle = "python güçlü bir programlama dilidir."
x = re.match("python", cumle)
x.span()
```

    (0, 6)

`match()` metodunun `span()` metodunu kullanarak değerleri doğrudan elde edebiliriz.

```python
cumle[0:6]
```

    'python'

farklı tarzda yazmak istersek, şu ifadeyi de kullanabiliriz;

```python
cumle[x.span()[0]:x.span()[1]]
```

    'python'

```python
txt = "Bu sabah yağmur var İstanbul'da..."
a = re.search(r"\by\w+", txt)
print(a.span())
```

    (9, 15)

### string Özelliği

Eşleşme bulunan metni gösterir.

```python
txt = "Bu sabah yağmur var İstanbul'da..."
a = re.search(r"\by\w+", txt)
print(a.string)
```

```python
Bu sabah yağmur var İstanbul'da...
```

### group() Metodu

 Belirtilen desen ile eşleşen değeri döndürür.

```python
txt = "Bu sabah yağmur var İstanbul'da..."
a = re.search(r"\by\w+", txt)
print(a.group())
```

    yağmur

`x = re.match("python", cumle)` ifadesi ile eşleştirme komutunu bir değişkene (**x**'e) atadık. Hatırlarsanız, bu fonksiyonu komut satırına yazdığımızda bir eşleşme nesnesi elde ediyorduk. İşte burada değişkene atadığımız şey aslında bu eşleşme nesnesinin kendisi oluyor. Bu durumu şu şekilde teyit edebilirsiniz:

```python
cumle = "python güçlü bir programlama dilidir."
x = re.match("python", cumle)
type(x)
```

    re.Match

Gördüğünüz gibi **x** bir eşleştirme (match) nesnesidir.
`group()` metodu, düzenli ifadelerin değil, eşleşme nesnelerinin bir metodudur.

Bu metodu kullandığımızda direkt aranan değer ekrana yazdırılacaktır. Bu aşamada, metodun gereksiz ya da saçma olduğunu düşünüyor olabilirsiniz. **Eşleşme Nesnelerinin Metotları** başlığı altında  `group()` metodunun ne işe yaradığını daha detaylı inceleyeceğiz.

```python
x.group()
```

    'python'

`match()` metodu ile, **cumle** değişkeni içerisinde **Java** kelimesini arayıp, sonucu inceleyelim.

```python
cumle = "python güçlü bir programlama dilidir."
print(re.match("Java", cumle))
```

    None

Python, **match()** metodu yardımıyla aradığımız şeyi eşleştirdiği (bulduğu) zaman bir eşleşme nesnesi (match object) döndürüyor. Eğer eşleşme yoksa, o zaman da **None** değerini döndürüyor.

```python
cumle = "python güçlü bir programlama dilidir."
print(re.match("güçlü", cumle))
```

    None

**cumle** değişkeninde **güçlü** ifadesi geçtiği halde `match()` metodu bize bir eşleşme nesnesi döndürmedi. Peki ama neden?

Aslında bu gayet normal. Çünkü `match()` metodu bir karakter dizisinin sadece en başına bakar. 
Yani "**python güçlü bir programlama dilidir.**" ifadesini tutan **cumle** değişkenine `re.match(“güçlü”, cumle)` gibi bir fonksiyon uyguladığımızda, `match()` metodu **cumle** değişkeninin yalnızca en başına bakacak ve **cumle** değişkeninin en başında **güçlü** yerine **python** ifadesini gördüğü için, bize olumsuz yanıt verecektir.

Aslında `match()` metodunun yaptığı bu işi, karakter dizilerinin `split()` metodu yardımıyla da yapabiliriz:

## search() Metodu

`search()` metodu ile `match()` metodu arasında çok önemli bir fark vardır. `match()` metodu bir karakter dizisinin en başına bakıp bir **eşleştirme** işlemi yaparken, `search()` metodu karakter dizisinin genelinde bir **arama** işlemi yapar. Yani biri eşleştirir, öbürü arar.

`search()` metodu, eşleşmenin gerçekleştiği ilk değeri döndürür. Aranan değer ya da desen, karakter dizisi içerisinde birden fazla geçse bile, ilk eşleşmede işlem sonlanır.

**güçlü** ifadesini `search()` metodu yardımı ile, **cumle** değişkeni içerisinde **arayalım**.

```python
cumle = "python güçlü bir programlama dilidir."
re.search("güçlü", cumle)
```

```python
<re.Match object; span=(7, 12), match='güçlü'>
```

Gördüğünüz gibi, `search()` metodu **güçlü** kelimesini buldu. Çünkü `search()` metodu, `match()` metodunun aksine, bir karakter dizisinin sadece baş tarafına bakmakla yetinmiyor, karakter dizisinin geneli üzerinde bir arama işlemi gerçekleştiriyor.

Tıpkı `match()` metodunda olduğu gibi, `search()` metodunda da `span()` ve `group()` metotlarından faydalanarak bulunan şeyin hangi aralıkta olduğunu ve bu şeyin ne olduğunu görüntüleyebiliriz:

```python
kardiz = "Python güçlü bir dildir"
nesne = re.search("güçlü", kardiz)
nesne.span()
```

    (7, 12)

```python
nesne.group()
```

    'güçlü'

### Start() Medodu

Arama deseni ile eşleşen ifadenin, karakter dizisinin kaçıncı karakterinde **başladığını** görmek için `start()` metodunu kullanabiliriz ;

```python
nesne.start()
```

    7

### End() Medodu

Arama deseni ile eşleşen ifadenin, karakter dizisinin kaçıncı karakterinde **bittiğini** görmek için `end()` metodunu kullanabiliriz ;

```python
nesne.end()
```

    12

Şimdiye kadar hep karakter dizileri üzerinde çalıştık. İsterseniz biraz da listeler üzerinde örnekler verelim.

Şöyle bir listemiz olsun:

```python
liste = ["elma", "armut", "kebap"]
re.search("kebap", liste)
```

```python
---------------------------------------------------------------------------

TypeError                                 Traceback (most recent call last)

/tmp/ipykernel_3704/1944706800.py in <module>
      1 liste = ["elma", "armut", "kebap"]
----> 2 re.search("kebap", liste)


/usr/lib/python3.10/re.py in search(pattern, string, flags)
    198     """Scan through string looking for a match to the pattern, returning
    199     a Match object, or None if no match was found."""
--> 200     return _compile(pattern, flags).search(string)
    201 
    202 def sub(pattern, repl, string, count=0, flags=0):


TypeError: expected string or bytes-like object
```

Ne oldu? Hata aldınız, değil mi? Bu normal. Çünkü düzenli ifadeler karakter dizileri üzerinde işler. 
Bunlar doğrudan listeler üzerinde işlem yapamaz. O yüzden bizim Python’a biraz yardımcı olmamız gerekiyor:

```python
liste = ["elma", "armut", "kebap"]
for i in liste:
    nesne = re.search("kebap", i)
    if nesne:
        print(nesne.group())
```

    kebap

## findall() Metodu

Bir metin içinde geçen belirli kelimelerin tümünü bulmak istiyorsak `findall()` metodunu kullanmalıyız.

```python
metin = """Guido Van Rossum Python'ı geliştirmeye 1990 yılında başlamış... Yani aslında Python için nispeten yeni
bir dil denebilir. Ancak Python'un çok uzun bir geçmişi olmasa da, bu dil öteki dillere kıyasla kolay olması, hızlı
olması, ayrı bir derleyici programa ihtiyaç duymaması ve bunun gibi pek çok nedenden ötürü çoğu kimsenin gözdesi
haline gelmiştir. Ayrıca Google'ın da Python'a özel bir önem ve değer verdiğini, çok iyi derecede Python bilenlere
iş olanağı sunduğunu da hemen söyleyelim. Mesela bundan kısa bir süre önce Python'ın yaratıcısı Guido Van Rossum 
Google'de işe başladı..."""
```

Yukarıdaki **metin** değişkeni içinde geçen bütün **Python** kelimelerini bulmak istersek aşağıdaki kodu çalıştırmalıyız;

```python
print(re.findall("Python", metin))
```

    ['Python', 'Python', 'Python', 'Python', 'Python', 'Python']

Gördüğünüz gibi, metinde geçen bütün “Python” kelimelerini bir çırpıda liste olarak aldık.

## finditer() Metodu

Belirtilen desenlerin karakter dizileri içerisindeki konumunu bulmak için `finditer()` metodunu kullanabiliriz. `finditer()` metodu liste döndürmez, iterable bir nesne döndürür.

Örneğin, yukarıda belirtilen **metin** değişkeni içerisinde **Python** ifadesinin (deseninin) hangi konumda olduğunu (aranan desenin başlangıç ve bitiş değerlerini) bulmaya çalışalım.

```python
for i in re.finditer("Python", metin):
    print(i.span())
```

    (17, 23)
    (77, 83)
    (128, 134)
    (370, 376)
    (430, 436)
    (522, 528)

```python
desen = r"\d{4}"
eslesenler = re.finditer(desen, metin)

for eslesen in eslesenler:
    print(eslesen.group())
```

    1990

## split() Metodu

`split()` metodu veriyi eşleşmelerin olduğu noktalardan böler ve liste haline getirir. Örneğin aşağıdaki kod çalıştırılırsa cümle boşluk (`\s`) karakterlerinden bölünür (yani kelimelere ayrılır):

```python
desen = r"Python"
bol = re.split(desen, metin)

print(bol)
```

```
['Guido Van Rossum ', "'ı geliştirmeye 1990 yılında başlamış... Yani aslında ", ' için nispeten yeni\nbir dil denebilir. Ancak ', "'un çok uzun bir geçmişi olmasa da, bu dil öteki dillere kıyasla kolay olması, hızlı\nolması, ayrı bir derleyici programa ihtiyaç duymaması ve bunun gibi pek çok nedenden ötürü çoğu kimsenin gözdesi\nhaline gelmiştir. Ayrıca Google'ın da ", "'a özel bir önem ve değer verdiğini, çok iyi derecede ", ' bilenlere\niş olanağı sunduğunu da hemen söyleyelim. Mesela bundan kısa bir süre önce ', "'ın yaratıcısı Guido Van Rossum \nGoogle'de işe başladı..."]
```

Gördüğünüz gibi, metin, **Python** ibaresi gördüğün yerden itibaren parçalara ayrılarak liste oluşturdu. **Python** ibaresi listeye dahil edilmedi.

```python
cumle = "python güçlü bir programlama dilidir."
x = re.split("\s", cumle)
print(x)
```

    ['python', 'güçlü', 'bir', 'programlama', 'dilidir.']

```python
cumle.split()[0] == "python"
```

    True

```python
cumle.startswith("python")
```

    True

```python
cumle.split()[0] == "güçlü"
```

    False

Bölünme sayısı `split()` fonksiyonunun 3. parametresinde **(maxsplit)** belirtilebilir. Aşağıdaki örnekte veri en çok 2 boşluk kadar (3 parça) bölünecektir:

```python
cumle = "python güçlü bir programlama dilidir."
x = re.split("\s", cumle, 2)
print(x)
```

    ['python', 'güçlü', 'bir programlama dilidir.']

Aynı işi sadece `startswith()` metodunu kullanarak dahi yapabiliriz:

Eğer düzenli ifadelerden tek beklentiniz bir karakter dizisinin en başındaki veriyle eşleştirme işlemi yapmaksa, `split()` veya `startswith()` metotlarını kullanmak daha mantıklıdır. Çünkü `split()` ve `startswith()` metotları `match()` metodundan çok daha hızlı çalışacaktır.

## Metin/Karakter Dizisi Değiştirme İşlemleri

## sub() metodu

Şimdiye kadar hep düzenli ifadeler yoluyla bir karakter dizisini nasıl eşleştireceğimizi inceledik. Ama tabii ki düzenli ifadeler yalnızca bir karakter dizisi **bulmak**la ilgili değildir. Bu araç aynı zamanda bir karakter dizisini **değiştirmeyi** de kapsar. Bu iş için temel olarak iki metot kullanılır. Bunlardan ilki `sub()` metodudur. **Substitute** kelimesi, yerine koy, değiştir anlamına gelir. Bu metot, pek çok uygulamadan bildiğimiz **Bul ve Değiştir** fonksiyonudur aslında. Bu bölümde `sub()` metodunu inceleyeceğiz.

`sub()` metodunun;

- ilk argümanı, değiştirilecek değeri,
- ikinci argümanı, yerine konulacak değeri,
- üçüncü argümanı, hangi yapı/ dizgi/ paragraf içinde değişimin yapılacağını,
- dördüncü argümanı, kaç eşleşmede değişiklik yapılacağını,

tanımlar.

Aşağıdaki örnekte **kavun** kelimesini bulacak, ardından **karpuz** olarak değiştirecektir:

```python
txt = "Bugün kavun yedim."
x = re.sub("kavun", "karpuz", txt)
print(x)
```

```
Bugün karpuz yedim.
```

yukarıdaki açıklamada `sub()` metodu ile kaç eşleşmede değişiklik yapılacağı, metodun 4. parametresinde (count) belirtilebileceğinden bahsetmiştik. Basit bir örnek yapalım;

```python
txt = "Yaz Yaz Yaz Bir Kenara Yaz"
x = re.sub("Yaz", "Çiz", txt, 2)
print(x)
```

    Çiz Çiz Yaz Bir Kenara Yaz

`sub()` metodunu,  `compile()` metodu ile şu şekilde kullanabiliriz:

```python
a = "Kırmızı başlıklı kız, kırmızı elma dolu sepetiyle anneannesinin evine gidiyormuş!"

derle = re.compile("kırmızı", re.IGNORECASE)
print(derle.sub("yeşil", a))
```

    yeşil başlıklı kız, yeşil elma dolu sepetiyle anneannesinin evine gidiyormuş!

Burada karakter dizimiz içinde geçen bütün **kırmızı** kelimelerini **yeşil** kelimesiyle değiştirdik. Bunu yaparken de `re.IGNORECASE` adlı derleme seçeneğinden yararlandık.

Elbette `sub()` metoduyla daha karmaşık işlemler yapılabilir. Bu noktada şöyle bir hatırlatma yapalım. Bu `sub()` metodu karakter dizilerinin `replace()` metoduna çok benzer. Ama `sub()` metodu hem kendi başına `replace()` metodundan çok daha güçlüdür, hem de beraber kullanılabilecek derleme seçenekleri sayesinde `replace()` metodundan çok daha esnektir. Eğer yapmak istediğiniz iş `replace()` metoduyla halledilebiliyorsa en doğru yol, `replace()` metodunu kullanmaktır.

Şimdi bu `sub()` metodunu kullanarak biraz daha karmaşık bir işlem yapacağız. Aşağıdaki metne bakalım:

```python
metin = """Karadeniz Ereğlisi denince akla ilk olarak kömür ve demir-çelik
gelir. Kokusu ve tadıyla dünyaya nam salmış meşhur Osmanlı çileği ise ismini
verdiği festival günleri dışında pek hatırlanmaz. Oysa Çin'den Arnavutköy'e
oradan da Ereğli'ye getirilen kralların meyvesi çilek, burada geçirdiği değişim
sonucu tadına doyulmaz bir hal alır. Ereğli'nin havasından mı suyundan mı
bilinmez, kokusu, tadı bambaşka bir hale dönüşür ve meşhur Osmanlı çileği
unvanını hak eder. Bu nazik ve aromalı çilekten yapılan reçel de likör de bir
başka olur. Bu yıl dokuzuncusu düzenlenen Uluslararası Osmanlı Çileği Kültür
Festivali'nde 36 üretici arasında yetiştirdiği çileklerle birinci olan Kocaali
Köyü'nden Güner Özdemir, yılda bir ton ürün alıyor. 60 yaşındaki Özdemir,
çileklerinin sırrını yoğun ilgiye ve içten duyduğu sevgiye bağlıyor: "Erkekler
bahçemize giremez. Koca ayaklarıyla ezerler çileklerimizi" Çileği toplamanın zor
olduğunu söyleyen Ayşe Özhan da çocukluğundan bu yana çilek bahçesinde
çalışıyor. Her sabah 04.00'te kalkan Özhan, çileklerini özenle suluyor. Kasım
başında ektiği çilek fideleri haziran başında meyve veriyor."""
```

Gelin bu metin içinde geçen **çilek** kelimelerini **erik** kelimesi ile değiştirelim. Ama bunu yaparken, metin içinde **çilek** kelimesinin **Çilek** şeklinde de geçtiğine dikkat edelim. Ayrıca Türkçe kuralları gereği bu **çilek** kelimesinin bazı yerlerde ünsüz yumuşamasına uğrayarak **çileğ-** şekline dönüştüğünü de unutmayalım.

Bu metin içinde geçen **çilek** kelimelerini **erik**'le değiştirmek için birkaç yol kullanabilirsiniz. 

Birinci yolda, her değişiklik için ayrı bir düzenli ifade oluşturulabilir. Ancak bu yolun dezavantajı, metnin de birkaç kez kopyalanmasını gerektirmesidir. Çünkü ilk düzenli ifade oluşturulup buna göre metinde bir değişiklik yapıldıktan sonra, ilk değişiklikleri içeren metnin, farklı bir metin olarak kopyalanması gerekir (metin2 gibi.).

Ardından ikinci değişiklik yapılacağı zaman, bu değişikliğin metin2 üzerinden yapılması gerekir. Aynı şekilde bu metin de, mesela, metin3 şeklinde tekrar kopyalanmalıdır. Bundan sonraki yeni bir değişiklik de bu metin3 üzerinden yapılacaktır. Bu durum bu şekilde uzar gider. Metni tekrar tekrar kopyalamak yerine, düzenli ifadeleri kullanarak şöyle bir çözüm de üretebiliriz:

```python
derle = re.compile("çile[kğ]", re.IGNORECASE)

def degistir(nesne):
    a = {"çileğ":"eriğ", "Çileğ":"Eriğ", "Çilek":"Erik", "çilek":"erik"}
    b = nesne.group().split()
    for i in b:
        return a[i]

print(derle.sub(degistir, metin))
```

    Karadeniz Ereğlisi denince akla ilk olarak kömür ve demir-çelik
    gelir. Kokusu ve tadıyla dünyaya nam salmış meşhur Osmanlı eriği ise ismini
    verdiği festival günleri dışında pek hatırlanmaz. Oysa Çin'den Arnavutköy'e
    oradan da Ereğli'ye getirilen kralların meyvesi erik, burada geçirdiği değişim
    sonucu tadına doyulmaz bir hal alır. Ereğli'nin havasından mı suyundan mı
    bilinmez, kokusu, tadı bambaşka bir hale dönüşür ve meşhur Osmanlı eriği
    unvanını hak eder. Bu nazik ve aromalı erikten yapılan reçel de likör de bir
    başka olur. Bu yıl dokuzuncusu düzenlenen Uluslararası Osmanlı Eriği Kültür
    Festivali'nde 36 üretici arasında yetiştirdiği eriklerle birinci olan Kocaali
    Köyü'nden Güner Özdemir, yılda bir ton ürün alıyor. 60 yaşındaki Özdemir,
    eriklerinin sırrını yoğun ilgiye ve içten duyduğu sevgiye bağlıyor: "Erkekler
    bahçemize giremez. Koca ayaklarıyla ezerler eriklerimizi" Eriği toplamanın zor
    olduğunu söyleyen Ayşe Özhan da çocukluğundan bu yana erik bahçesinde
    çalışıyor. Her sabah 04.00'te kalkan Özhan, eriklerini özenle suluyor. Kasım
    başında ektiği erik fideleri haziran başında meyve veriyor.

Gördüğünüz gibi, `sub()` metodu, argüman olarak bir **fonksiyon** da alabiliyor. Yukarıdaki kodlar biraz karışık görünmüş olabilir. Tek tek açıklayalım.

Öncelikle şu satıra bakalım:

```python
derle = re.compile("çile[kğ]", re.IGNORECASE)
```

Burada amacımız, metin içinde geçen **çilek** ve **çileğ** kelimelerini bulmak. Neden **çileğ**? Çünkü **çilek** kelimesi bir sesli harften önce geldiğinde sonundaki **k** harfi **ğ**'ye dönüşüyor. Bu seçenekli yapıyı, daha önceki bölümlerde gördüğümüz `[ ]` adlı metakarakter yardımıyla oluşturduk. Düzenli ifade kalıbımızın hem büyük harfleri hem de küçük harfleri aynı anda bulması için `re.IGNORECASE` seçeneğinden yararlandık.

Şimdi de şu satırlara bakalım:

```python
def degistir(nesne):
    a = {"çileğ":"eriğ", "Çileğ":"Eriğ", "Çilek":"Erik", "çilek":"erik"}
    b = nesne.group().split()
    for i in b:
        return a[i]
```

Burada, daha sonra `sub()` metodu içinde kullanacağımız fonksiyonu yazıyoruz. Fonksiyonu, `def degistir(nesne)` şeklinde tanımladık. Burada **“nesne”** adlı bir argüman kullanmamızın nedeni, fonksiyon içinde `group()` metodunu kullanacak olmamız. Bu metodu fonksiyon içinde **“nesne”** adlı argümana bağlayacağız. Bu fonksiyon, daha sonra yazacağımız `sub()` metodu tarafından çağrıldığında, yaptığımız arama işlemi sonucunda ortaya çıkan **“eşleşme nesnesi”** fonksiyona atanacaktır (eşleşme nesnesinin ne demek olduğunu ilk bölümlerden hatırlıyorsunuz). İşte **“nesne”** adlı bir argüman kullanmamızın nedeni de, eşleşme nesnelerinin bir metodu olan `group()` metodunu fonksiyon içinde kullanabilmek.

Bir sonraki satırda bir adet sözlük görüyoruz:

```python
a = {"çileğ":"eriğ", "Çileğ":"Eriğ", "Çilek":"Erik", "çilek":"erik"}
```

Bu sözlüğü oluşturmamızın nedeni, metin içinde geçen bütün **“çilek”** kelimelerini tek bir **“erik”** kelimesiyle değiştiremeyecek olmamız. Çünkü **“çilek”** kelimesi metin içinde pek çok farklı biçimde geçiyor. Başta da dediğimiz gibi, yukarıdaki yol yerine metni birkaç kez kopyalayarak ve her defasında bir değişiklik yaparak da sorunu çözebilirsiniz. (Mesela önce **“çilek”** kelimelerini bulup bunları **“erik”** ile değiştirirsiniz. Daha sonra **“çileğ”** kelimelerini arayıp bunları **“eriğ”** ile değiştirirsiniz, vb…) Ama metni tekrar tekrar oluşturmak pek performanslı bir yöntem olmayacaktır. Bizim şimdi kullandığımız yöntem metin kopyalama zorunluluğunu ortadan kaldırıyor. Bu sözlük içinde **“çilek”** kelimesinin alacağı şekilleri sözlük içinde birer anahtar olarak, **“erik”** kelimesinin alacağı şekilleri ise birer **“değer”** olarak belirliyoruz.

Sonraki satırda iki metot birden var:

```python
b = nesne.group().split()
```

Burada, fonksiyonumuzun argümanı olarak vazife gören eşleşme nesnesine ait metotlardan biri olan `group()` metodunu kullanıyoruz. Böylece `derle = re.compile("çile[kğ]", re.IGNORECASE)` satırı yardımıyla metin içinde bulduğumuz bütün **“çilek”** ve çeşitlerini alıyoruz. Karakter dizilerinin `split()` metodunu kullanmamızın nedeni ise `group()` metodunun verdiği çıktıyı liste haline getirip daha kolay manipüle etmek. Burada `for i in b: print(i)` komutunu verirseniz `group()` metodu yardımıyla ne bulduğumuzu görebilirsiniz:

```python
çileğ
çilek
çileğ
çilek
Çileğ
çilek
çilek
çilek
Çileğ
çilek
çilek
çilek
```

Bu çıktıyı gördükten sonra, kodlarda yapmaya çalıştığımız şey daha anlamlı görünmeye başlamış olmalı. Şimdi sonraki satıra geçiyoruz:

```python
for i in b:
    return a[i]
```

Burada, `group()` metodu yardımıyla bulduğumuz eşleşmeler üzerinde bir `for` döngüsü oluşturduk. 
    Ardından da `return a[i]` komutunu vererek “a” adlı sözlük içinde yer alan öğeleri yazdırıyoruz. Bu arada, buradaki **“i”**nin yukarıda verdiğimiz `group()` çıktılarını temsil ettiğine dikkat edin. `a[i]` gibi bir komut verdiğimizde aslında sırasıyla şu komutları vermiş oluyoruz:  

```python
a["çilek"]
a["çileğ"]
a["çilek"]
a["Çileğ"]
a["çilek"]
a["çilek"]
a["çilek"]
a["Çileğ"]
a["çilek"]
a["çilek"]
```

Bu komutların çıktıları sırasıyla **“erik”, “eriğ”, “erik”, “Eriğ”, “erik”, “erik”, “erik”, “Eriğ”, “erik”, “erik”** olacaktır. İşte bu return satırı bir sonraki kod olan `print(derle.sub(degistir,metin))` ifadesinde etkinlik kazanacak. Bu son satırımız sözlük öğelerini tek tek metne uygulayacak ve mesela `a["çilek"]` komutu sayesinde metin içinde **“çilek”** gördüğü yerde **“erik”** kelimesini yapıştıracak ve böylece bize istediğimiz şekilde değiştirilmiş bir metin verecektir.

Bu kodların biraz karışık gibi göründüğünü biliyorum, ama aslında çok basit bir mantığı var: `group()` metodu ile metin içinde aradığımız kelimeleri ayıklıyor. Ardından da **“a”** sözlüğü içinde bunları anahtar olarak kullanarak **“çilek”** ve çeşitleri yerine **“erik”** ve çeşitlerini koyuyor.

Bir tane tarih verisi ile ilgili kullanım örneği verelim. Verilerimizde farklı tarih formatları bulunuyor. Örneğin, "01/01/2023", "1.5.2021", "12-2-1980", "25/10/18". Bu tarih formatlarını belirli bir formata dönüştürmek için `re.sub()` kullanabiliriz. Aşağıda, bu tarih formatlarını "dd/mm/yyyy" formatına dönüştüren bir örnek var:

```python
import re

tarihler = """
01/01/2023
1.5.2021
12-2-1980
25/10/18
"""

def duzenle(match):
    gun, ay, yil = match.groups()
    return f"{gun.zfill(2)}/{ay.zfill(2)}/{yil.zfill(4)}"

pattern = re.compile(r"(\d{1,2})[\/\.\-](\d{1,2})[\/\.\-](\d{2,4})")
duzenlenmis_tarihler = re.sub(pattern, duzenle, tarihler)

print(duzenlenmis_tarihler)
```

Bu kod, `re.sub()` fonksiyonunu kullanarak tarih formatlarını belirli bir formata dönüştürür. `duzenle` fonksiyonu, her eşleşme için çağrılır ve tarihi "dd/mm/yyyy" formatına dönüştürür.

```python
01/01/2023
01/05/2021
12/02/1980
25/10/2018
```

Bu örnekte `zfill` kullanarak gün, ay ve yılın sırasıyla 2, 2 ve 4 karakterli olmasını sağladık. İhtiyacınıza göre bu düzenlemeleri değiştirebilirsiniz.

Son olarak ta farklı biçimlerdeki telefon numaralarını düzenlemek için de `re.sub()` fonksiyonunu kullanarak bir örnek yapalım:

```python
import re

numaralar = """
1234567890
533-456-7891
544 456 7892
(216) 456-7893
"""

def duzenle_telefon(match):
    operator, üçhane, dorthane = match.groups()
    return f"({operator}) {üçhane}-{dorthane}"

telefon_pattern = re.compile(r"\(?(?P<operator>\d{3})\)?[ \-]?(?P<üçhane>\d{3})[ \-]?(?P<dorthane>\d{4})")
duzenlenmis_numaralar = re.sub(telefon_pattern, duzenle_telefon, numaralar)

print(duzenlenmis_numaralar)
```

Bu kod, farklı biçimlerdeki telefon numaralarını aynı formata ("(123) 
456-7890") dönüştürür. `duzenle_telefon` fonksiyonu, her eşleşme için çağrılır ve telefon numarasını belirli bir formata dönüştürür.

```python
(123) 456-7890
(533) 456-7891
(544) 456-7892
(216) 456-7893
```

Yukarıda verdiğimiz düzenli ifadeyi böyle ufak bir metinde kullanmak çok anlamlı olmayabilir. Ama çok büyük metinler üzerinde çok çeşitli ve karmaşık değişiklikler yapmak istediğinizde bu kodların işinize yarayabileceğini göreceksiniz.

## subn() metodu

Bu metodu çok kısa bir şekilde anlatıp geçeceğiz. Çünkü bu metot `sub()` metoduyla neredeyse tamamen aynıdır. Tek farkı, `subn()` metodunun bir metin içinde yapılan değişiklik sayısını da göstermesidir. Yani bu metodu kullanarak, kullanıcılarınıza **“toplam şu kadar sayıda değişiklik yapılmıştır”** şeklinde bir bilgi verebilirsiniz. Bu metot çıktı olarak iki öğeli bir demet verir. 

Birinci öğe değiştirilen metin, ikinci öğe ise yapılan değişiklik sayısıdır. Yani kullanıcıya değişiklik sayısını göstermek için yapmanız gereken şey, bu demetin ikinci öğesini almaktır. Mesela `sub()` metodunu anlatırken verdiğimiz kodların son satırını şöyle değiştirebilirsiniz:

```python
ab = derle.subn(degistir, metin)
print("Toplam {} değişiklik yapılmıştır.".format(ab[1]))
```

    Toplam 12 değişiklik yapılmıştır.   

## escape() metodu

`escape()` metodu (fonksiyonu), **bir metni düzenli ifade (regular expression) içinde kullanılmaya uygun hale getirmek için kullanılır.** Bu fonksiyon, metindeki özel karakterleri kaçış karakterleri ile değiştirir, böylece bu karakterler düzenli ifade içinde özel anlam taşımazlar ve doğrudan metin olarak eşleştirilebilirler.

Örneğin, bir kullanıcının girdiği metni doğrudan bir düzenli ifade içinde kullanmak istediğinizi düşünün. Kullanıcının girdisi içinde özel karakterler bulunabilir ve bu karakterlerin düzenli ifade içinde kullanılması sorunlara neden olabilir. `escape()` fonksiyonu, bu tür durumlar için kullanışlıdır.

Örneğin, elimizde kullanıcı tarafından tanımlanmış bir değişken (`user_input`) olduğunu ve bu değişkenin, düzenli ifadelerde kullanılan özel karakterler içerdiğini düşünün. 
`user_input` değişkenini `escape()` metoduna parametre olarak verdiğimizde nasıl bir sonuç elde ettiğimizi görelim;

```python
user_input = "(.*$"
escaped_input = re.escape(user_input)
print(escaped_input)
```

Kullanıcı tarafından belirlenen `(.*$` ifadesi, `escape()` metodu sayesinde aşağıdaki hale dönüştürülerek, düzenli ifadelerle rahatça kullanılabilecek hale getirilmiş olur.

```
\(\.\*\$
```

İşte örneğe ait tüm kodlar:

```python
import re

user_input = "(.*$"

# Kullanıcı girdisini düzenli ifade içinde güvenli hale getirme
escaped_input = re.escape(user_input)

# Düzenli ifadeyi kullanma
pattern = re.compile(escaped_input)
result = pattern.match("(.*$")

print(result.group())  
```

```python
'(.*$'
```

Bu örnekte, `re.escape()` fonksiyonu, `user_input` içindeki özel karakterleri kaçış karakterleriyle değiştirir ve bu düzenli ifade içinde güvenli bir şekilde kullanılabilir hale getirir. Bu, kullanıcının girdisinin düzenli ifade içinde istenmeyen yan etkiler oluşturmasını önler.

Bu fonksiyon özellikle dinamik olarak oluşturulan düzenli ifadelerde veya kullanıcı tarafından sağlanan metinlerle çalışırken güvenlik sağlamak için önemlidir.

## Düzenli İfadelerin Derlenmesi

## compile() metodu

En başta da söylediğimiz gibi, düzenli ifadeler, karakter dizilerine göre biraz daha yavaş çalışırlar. Ancak düzenli ifadelerin işleyişini hızlandırmanın da bazı yolları vardır. Bu yollardan biri de `compile()` metodunu kullanmaktır.

**compile** kelimesi İngilizcede **derlemek** anlamına gelir. İşte biz de bu `compile()` metodu yardımıyla düzenli ifade kalıplarımızı kullanmadan önce derleyerek daha hızlı çalışmalarını sağlayacağız. 

Küçük boyutlu projelerde `compile()` metodu pek hissedilir bir fark yaratmasa da özellikle büyük çaplı programlarda bu metodu kullanmak oldukça faydalı olacaktır.

Basit bir örnekle başlayalım:

```python
liste = ["Python2.7", "Python3.2", "Python3.3", "Python3.4", "Java"]

derli = re.compile("[A-Za-z]+[0-9]\.[0-9]")

for i in liste:
    nesne = derli.search(i)
    if nesne:
        print(nesne.group())
```

    Python2.7
    Python3.2
    Python3.3
    Python3.4

Burada öncelikle düzenli ifade kalıbımızı derledik. Derleme işlemini nasıl yaptığımıza dikkat edin. 

Derlenecek düzenli ifade kalıbını `compile()` metodunda parantez içinde belirtiyoruz. 

Daha sonra `search()` metodunu kullanırken ise, `re.search()` demek yerine, `derli.search()` şeklinde bir ifade kullanıyoruz. Ayrıca dikkat ederseniz `derli.search()` kullanımında parantez içinde sadece eşleşecek karakter dizisini `(i)` kullandık. 

Eğer derleme işlemi yapmamış olsaydık, hem bu karakter dizisini, hem de düzenli ifade kalıbını yan yana kullanmamız gerekecektir `.search("[A-Za-z]+[0-9].[0-9], i)"`. Ama düzenli ifade kalıbımızı yukarıda derleme işlemi esnasında belirttiğimiz için, bu kalıbı ikinci kez yazmamıza gerek kalmadı. 

Ayrıca burada kullandığımız düzenli ifade kalıbına da dikkat edin. Nasıl bir şablon oturttuğumuzu anlamaya çalışın. Gördüğünüz gibi, liste öğelerinde bulunan `.` işaretini eşleştirmek için düzenli ifade kalıbı içinde `\.` ifadesini kullandık. Çünkü bildiğiniz gibi, tek başına `.` işaretinin Python açısından özel bir anlamı var. Dolayısıyla bu özel anlamdan kaçmak için `\` işaretini de kullanmamız gerekiyor.

### Detaylandıralım;

`re.compile()`fonksiyonu, düzenli ifade desenini derler ve bir`re.RegexObject` nesnesi döner. Bu nesne, derlenmiş düzenli ifadeyi temsil eder ve aynı deseni birden çok kez kullanmak için daha verimli bir yol sunar.

İşte `re.compile()` fonksiyonunun temel amacı ve avantajları:

**Performans Artışı:** 

Düzenli ifade desenleri büyük ve karmaşık olabilir. Bu desenleri her seferinde kullanmak yerine, `re.compile()` ile derlenmiş bir nesneyi oluşturabilir ve bu nesneyi kullanarak performans avantajı elde edebilirsiniz. Derleme işlemi, desenin daha hızlı eşleşmesine ve işlenmesine olanak tanır.

Örneğin:

```python
import re

pattern = re.compile(r'\b\w+\b')
result = pattern.findall("Python is powerful")
```

**Tekrar Kullanım Kolaylığı:** 

Derlenmiş bir düzenli ifade nesnesi oluşturduktan sonra, aynı deseni farklı metinler üzerinde birden çok kez kullanabilirsiniz. Bu, aynı deseni defalarca yazmak yerine daha temiz ve okunabilir kod sağlar.

        Örneğin:

```python
import re

pattern = re.compile(r'\b\w+\b')

result1 = pattern.findall("Python is powerful")
result2 = pattern.findall("Regular expressions are versatile")
```

**Bayrakları Ayarlama:** 

`re.compile()` fonksiyonu, düzenli ifadenin derlenmesi sırasında bayrakları (flags) ayarlamanıza olanak tanır. (*Bayraklar konusu **metakarakterler** sayfasında detaylı olarak anlatılmaktadır.*) Örneğin, `re.IGNORECASE` veya `re.UNICODE` bayraklarını belirleyerek deseni derleyebilirsiniz.

Örneğin:

```python
import re

pattern = re.compile(r'\b\w+\b', re.IGNORECASE)
result = pattern.findall("Python is case-insensitive")
```

Bu avantajlar, `re.compile()` fonksiyonunu kullanmanın genellikle tercih edilen bir yöntem haline getirir. Ancak, küçük uygulamalarda veya tek seferlik kullanımlarda `re.compile()` kullanmak zorunlu değildir; `re.findall()` veya diğer `re` fonksiyonları doğrudan düzenli ifade desenini alabilir.

## purge() metodu

`purge()` metodu, **düzenli ifade (regex) önbelleğini temizlemek için kullanılır**. `re` modülü, derlenmiş düzenli ifade desenlerini ve ilgili verileri bir önbellekte saklar. Bu önbellek, aynı desenleri tekrar tekrar derlememek ve performansı artırmak için kullanılır. Ancak, bazen bu önbelleği temizlemek isteyebilirsiniz, özellikle çok sayıda düzenli ifade deseni kullanılıyorsa veya bellek kullanımını kontrol etmek istiyorsanız.

İşte `purge()` fonksiyonunun kullanımı:

```python
import re

# Örnek düzenli ifade deseni
pattern1 = re.compile(r'\b\w+\b')
pattern2 = re.compile(r'\d+')

# re modülü önbelleği temizleme
re.purge()

# Yeniden derleme yapmadan önce temizlenmiş önbelleği kullanma
result1 = pattern1.findall("This is a sample text.")
result2 = pattern2.findall("123 456")

print(result1)  # ['This', 'is', 'a', 'sample', 'text']
print(result2)  # ['123', '456']
```

Bu örnekte, `re.purge()` fonksiyonu çağrılarak `re` modülünün önbelleği temizlenir. Daha sonra, temizlenmiş önbelleği kullanarak `pattern1` ve `pattern2` düzenli ifade desenlerini tekrar derleriz.

`re.purge()` fonksiyonu genellikle programın çalışma süresi boyunca biriken düzenli ifade desenlerini temizlemek için kullanılır. Ancak, bu işlemi yapmak, genel performansı olumsuz etkileyebilir, çünkü bir sonraki derleme işlemi için aynı desenin tekrar derlenmesi gerekecektir. Bu nedenle, önbelleği temizlemek konusunda dikkatli olunmalıdır ve ihtiyaç doğrultusunda kullanılmalıdır.

### Kaynaklar:

* [İstihza YazBel](https://python-istihza.yazbel.com/standart_moduller/regex.html)
* [python.sitesi.web.tr](https://python.sitesi.web.tr/python-regex.html)
* [Zeynep ENGİN](https://medium.com/@zeynepengin/regular-expressions-d%C3%BCzenli-i%CC%87fadeler-2e75f44d4f6f)
* [Yakın Kampüs](https://www.youtube.com/watch?v=bKWzIvYZmfA)
* [ChatGPT](https://chat.openai.com)
