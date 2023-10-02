# Düzenli İfadeler (Regular Expressions)

Düzenli ifadeler (RegEx ya da Regular Expression), bir karakter serisi içinde belli bir düzene uyan eşleşmeleri bulmanıza ve yönetmenize yardımcı olacak desenler oluşturmanıza izin veren bir metin dizisidir. Bir metinde geçen karakterleri RegEx desenleri (pattern) kullanarak arayabiliriz.

Düzenli ifadeler bir arama işleminde eşleştirilecek bir deseni temsil eden özel dizelerdir. Java ve Perl gibi programlama dillerinden grep, sed ve metin düzenleyici vim gibi metin işleme araçlarına kadar çok çeşitli bilgi işlem uygulamalarında önemli bir araçtır. 

**Düzenli ifadeler sayesinde ne yapabiliriz bir bakalım :**

* **Yer değiştirme:** Belirli parçaları değiştirir. Örnek olarak metin içerisindeki tüm büyük harfleri küçük harf ya da tüm küçük harfleri büyük harfe dönüştürebilirsiniz.

* **Doğrulama :** Yazdığınız bir program olsun, bu programda büyük veya küçük harf, nokta veya rakam gibi kriterleri karşılayıp karşılamadığını kontrol edebilirsiniz.

* **Arama :** Bir metin imzası içerisindeki tüm ögeleri aratabilirsiniz. Örneğin telefon numaraları ya da e-posta adresleri gibi.

* **Koordinat ile hareket etme :** Örneğin, bir dizindeki belirli paketleri, dosyaları işlemek isteyebilirsiniz ancak yalnızca belirli koşulları karşılıyorlarsa, komut satırında çalıştırabiliyorsunuz.

* **Metni Yeniden Biçimlendirme :** Örneğin, Bir programdaki verileri metin dosyası olarak dışa aktarabilir, ardından düzenini değiştirerek metin düzenleyicisi kullanarak başka bir programa aktarabilirsiniz.

Python’daki düzenli ifadelere ilişkin her şey, bir modül içinde tutulur. Bu modülün adı **re**'dir. 
Düzenli ifadeleri kullanabilmemiz için öncelikle bu **re** modülünü içe aktarmamız gerekir:


```python
import re
```

## RegEx Fonksiyonları

**re** modülü bir veride geçen karakterleri bulmamıza ve değiştirmemize olanak sağlayan bazı fonksiyonlara sahiptir. Bunlar;

| Fonksiyon | Açıklama                                           |
| --------- | -------------------------------------------------- |
| match     | Karakter dizisinin başında eşleşme olup olmadığını göster |
| search    | Eşleşme olup olmadığını göster                     |
| findall   | Tüm eşleşmeleri göster (liste halinde)             |
| finditer  | Belirtilen desenlerin karakter dizileri içerisindeki konumunu bulmak için kullanabiliriz.|
| split     | Eşleşme noktalarından böl ve liste oluştur         |
| sub       | Eşleşmeleri verilen ifade ile değiştir             |

## match() Metodu

Bir karakter dizisi başında belirli bir kelimenin ya da kelime grubunun geçip geçmediğini öğrenmek istiyorsak bu işlemi `match()` metodunu kullanarak yapabiliriz.

**match()** metodunun;
* ilk argümanı eşleştirilecek (aranacak) değer, 
* ikinci argümanı ise , eşleştirilecek (aramanın) yapılacağı karakter dizisi olmalıdır.


```python
cumle = "python güçlü bir programlama dilidir."

re.match(r"python", cumle)
```




    <re.Match object; span=(0, 6), match='python'>



Düzenli ifadeler için bir desen tanımlarken, `r` ifadesini yazmamız istenir. Yazılmadığı zaman da sorun çıkarmıyor ancak tanımlanan ifadenin bir değişken mi? yoksa bir düzenli ifade deseni mi? olduğunu belirtmek için bu şekilde kullanım faydalı olacaktır.

Bu nesnenin dönen değeri ile ilgili bazı işlemler yapılabilir. Bunun için nesnenin yöntemleri kullanılır. Bunlar;

* `span()` tuple olarak başlangıç ve bitiş pozisyonlarını verir.
* `string` dönen string değeri yazdırır
* `group()` eşleşmelerinin yerlerini içerir

Bu çıktıdaki **span** parametresi, aradığımız **python** karakter dizisinin, **cumle** değişkeninin 0. ile 6. karakterleri arasında yer aldığını söylüyor bize.

### span() metodu

Eşleşmenin başladığı ve sona erdiği karakterlerin sırasını verir (0=1. karakter):


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

    Bu sabah yağmur var İstanbul'da...


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




    <re.Match object; span=(7, 12), match='güçlü'>



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

Belirtilen desenlerin karakter dizileri içerisindeki konumunu bulmak için `finditer()` metodunu kullanabiliriz.

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


## split() Metodu

`split()` metodu veriyi eşleşmelerin olduğu noktalardan böler ve liste haline getirir. Örneğin aşağıdaki kod çalıştırılırsa cümle boşluk (`\s`) karakterlerinden bölünür (yani kelimelere ayrılır):


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

## sub() Metodu

`sub()` metodu, eşleşmeleri verilen ifadelerle değiştirir. Pek çok uygulamadan bildiğimiz **Bul ve Değiştir** fonksiyonudur aslında.Bu Metod, diğer bölümde detaylı olarak anlatılıyor.

`sub()` metodunun;
* ilk argümanı değiştirilecek değeri, 
* ikinci argümanı yerine konulacak değeri, 
* üçüncü argümanı hangi yapı içinde değişimin yapılacağını,
* dördüncü argümanı kaç eşleşmede değişiklik yapılacağını,

tanımlar.

Aşağıdaki örnekte **kavun** kelimesini bulacak, ardından **karpuz** olarak değiştirecektir:


```python
txt = "Bugün kavun yedim."
x = re.sub("kavun", "karpuz", txt)
print(x)
```

    Bugün karpuz yedim.


yukarıdaki açıklamada `sub()` metodu ile kaç eşleşmede değişiklik yapılacağı, metodun 4. parametresinde (count) belirtilebileceğinden bahsetmiştik. Basit bir örnek yapalım;


```python
txt = "Yaz Yaz Yaz Bir Kenara Yaz"
x = re.sub("Yaz", "Çiz", txt, 2)
print(x)
```

    Çiz Çiz Yaz Bir Kenara Yaz


Kaynaklar:
* https://python-istihza.yazbel.com/standart_moduller/regex.html
* https://python.sitesi.web.tr/python-regex.html
* https://medium.com/@zeynepengin/regular-expressions-d%C3%BCzenli-i%CC%87fadeler-2e75f44d4f6f
* https://www.youtube.com/watch?v=bKWzIvYZmfA


```python

```
