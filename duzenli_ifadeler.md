# Düzenli İfadeler (Regular Expressions)

Python’daki düzenli ifadelere ilişkin her şey, bir modül içinde tutulur. Bu modülün adı **re**'dir. 
Düzenli ifadeleri kullanabilmemiz için öncelikle bu **re** modülünü içe aktarmamız gerekir:

```python
import re
```

## match() Metodu

Bir karakter dizisi içinde belirli bir kelimenin ya da kelime grubunun geçip geçmediğini öğrenmek istiyorsak bu işlemi `match()` metodunu kullanarak yapabiliriz:

```python
cumle = "python güçlü bir programlama dilidir."
re.match("python", cumle)
```

    <re.Match object; span=(0, 6), match='python'>

**match()** metodunun ilk argümanı karşılaştırılacak (aranacak) değer, ikinci argümanı ise , karşılaşırmanın (aramanın) yapılacağı karakter dizisi olmalıdır.
Bu çıktıdaki **span** parametresi, aradığımız **python** karakter dizisinin, **cumle** değişkeninin 0. ile 6. karakterleri arasında yer aldığını söylüyor bize.

```python
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

### group() Metodu

`x = re.match("python", cumle)` ifadesi ile eşleştirme komutunu bir değişkene (**x**'e) atadık. Hatırlarsanız, bu fonksiyonu komut satırına yazdığımızda bir eşleşme nesnesi elde ediyorduk. İşte burada değişkene atadığımız şey aslında bu eşleşme nesnesinin kendisi oluyor. Bu durumu şu şekilde teyit edebilirsiniz:

```python
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
print(re.match("Java", cumle))
```

    None

Python, **match()** metodu yardımıyla aradığımız şeyi eşleştirdiği (bulduğu) zaman bir eşleşme nesnesi (match object) döndürüyor. Eğer eşleşme yoksa, o zaman da **None** değerini döndürüyor.

```python
print(re.match("güçlü", cumle))
```

    None

**cumle** değişkeninde **güçlü** ifadesi geçtiği halde `match()` metodu bize bir eşleşme nesnesi döndürmedi. Peki ama neden?

Aslında bu gayet normal. Çünkü `match()` metodu bir karakter dizisinin sadece en başına bakar. 
Yani **python güçlü bir programlama dilidir.** ifadesini tutan **cumle** değişkenine `re.match(“güçlü”, cumle)` gibi bir fonksiyon uyguladığımızda, `match()` metodu **cumle** değişkeninin yalnızca en başına bakacağı ve **cumle** değişkeninin en başında **güçlü** yerine **python** ifadesi olduğu için, `match()` metodu bize olumsuz yanıt verecektir.

Aslında `match()` metodunun yaptığı bu işi, karakter dizilerinin `split()` metodu yardımıyla da yapabiliriz:

```python
cumle.split()[0] == "python"
```

    True

```python
cumle.split()[0] == "güçlü"
```

    False

aynı işi sadece `startswith()` metodunu kullanarak dahi yapabiliriz:

```python
cumle.startswith("python")
```

    True

Eğer düzenli ifadelerden tek beklentiniz bir karakter dizisinin en başındaki veriyle eşleştirme işlemi yapmaksa, `split()` veya `startswith()` metotlarını kullanmak daha mantıklıdır. Çünkü `split()` ve `startswith()` metotları `match()` metodundan çok daha hızlı çalışacaktır.

## search() Metodu

`search()` metodu ile `match()` metodu arasında çok önemli bir fark vardır. `match()` metodu bir karakter dizisinin en başına bakıp bir **eşleştirme** işlemi yaparken, `search()` metodu karakter dizisinin genelinde bir **arama** işlemi yapar. Yani biri eşleştirir, öbürü arar.

**güçlü** ifadesini `search()` metodu yardımı ile, **cumle** değişkeni içerisinde **arayalım**.

```python
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
for i in liste:
    nesne = re.search("kebap", i)
    if nesne:
        print(nesne.group())
```

    kebap

## findall() Metodu

```python
metin = """Guido Van Rossum Python'ı geliştirmeye 1990 yılında başlamış... Yani aslında Python için nispeten yeni
bir dil denebilir. Ancak Python'un çok uzun bir geçmişi olmasa da, bu dil öteki dillere kıyasla kolay olması, hızlı
olması, ayrı bir derleyici programa ihtiyaç duymaması ve bunun gibi pek çok nedenden ötürü çoğu kimsenin gözdesi
haline gelmiştir. Ayrıca Google'ın da Python'a özel bir önem ve değer verdiğini, çok iyi derecede Python bilenlere
iş olanağı sunduğunu da hemen söyleyelim. Mesela bundan kısa bir süre önce Python'ın yaratıcısı Guido Van Rossum 
Google'de işe başladı..."""
```

Bu metin içinde geçen bütün “Python” kelimelerini bulmak istiyoruz:

```python
print(re.findall("Python", metin))
```

    ['Python', 'Python', 'Python', 'Python', 'Python', 'Python']

Gördüğünüz gibi, metinde geçen bütün “Python” kelimelerini bir çırpıda liste olarak aldık.
