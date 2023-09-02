## Metakarakterler

Metakarakterler; kabaca, programlama dilleri için özel anlam ifade eden sembollerdir. Örneğin `\n` bir bakıma bir metakarakterdir, çünkü `\n` sembolü Python programlama dili için özel bir anlam taşır. Python bu sembolü gördüğü yerde yeni bir satıra geçer. Yukarıda **kendisiyle eşleşmeyen karakterler** ifadesiyle kastettiğimiz şey de işte bu metakarakterlerdir. Örneğin, **a** harfi yalnızca kendisiyle eşleşir. Tıpkı **istihza** kelimesinin yalnızca kendisiyle eşleşeceği gibi. Ancak mesela `\t` ifadesi kendisiyle eşleşmez. Python bu işareti gördüğü yerde sekme (tab) düğmesine basılmış gibi tepki verecektir. İşte düzenli ifadelerde de buna benzer metakarakterlerden yararlanacağız. Düzenli ifadeler içinde de, özel anlam ifade eden pek çok sembol, yani metakarakter vardır. Şimdi bu meta karakterleri ayrı ayrı başlıklar altında inceleyelim.

## [] Köşeli Parantez

İlk inceleyeceğimiz metakarakterlerden biri Köşeli Parantez `[ ]` sembolüdür. 
Python, köşeli parantez içinde gördüğü bütün karakterleri tek tek liste öğelerine uygular.

Şimdi aşağıdaki listeden **özcan**, **özhan** ve **özkan** öğelerini bu sembolden yararlanarak nasıl ayıklayacağımızı görelim:

```python
import re

liste = ["özcan", "mehmet", "süleyman", "selim", "kemal", "özkan", "esra", "dündar", "esin", "esma", "özhan", 
         "özlem"]

for i in liste:
    nesne = re.search("öz[chk]an", i)
    if nesne:
        print(nesne.group())
```

    özcan
    özkan
    özhan

Yukarıdaki örnekte, bir liste içinde geçen **özcan**, **özhan** ve **özkan** öğelerini ayıklıyoruz. Burada bu üç öğedeki farklı karakterleri (**c**, **h** ve **k**) köşeli parantez içinde nasıl belirttiğimize dikkat edin. 

Python, köşeli parantez içinde gördüğü bütün karakterleri tek tek liste öğelerine uyguluyor. Önce **öz** ile başlayan bütün öğeleri alıyor, ardından **öz** hecesinden sonra **c** harfiyle devam eden ve **an** hecesi ile biten öğeyi buluyor. Böylece **özcan** öğesini bulmuş oldu. 

Aynı işlemi, **öz** hecesinden sonra **h** harfini barındıran ve **an** hecesiyle biten öğeye uyguluyor. Bu şekilde ise **özhan** öğesini bulmuş oldu. 

En son hedef ise **öz** ile başlayıp **k** harfi ile devam eden ve **an** ile biten öğe. Yani listedeki **özkan** öğesi… En nihayetinde de elimizde **özcan**, **özhan** ve **özkan** öğeleri kalmış oluyor.

Yeni bir örnek ile devam edelim.

```python
a = ["23BH56","TY76Z","4Y7UZ","TYUDZ","34534"]
```

Mesela biz bu listedeki öğeler içinde, sayıyla başlayanları ayıklayalım:

```python
for i in a:
    if re.match("[0-9]",i):
        print(i)
```

    23BH56
    4Y7UZ
    34534

Burada parantez içinde kullandığımız ifadeye dikkat edin. **0** ile **9** arasındaki bütün öğeleri içeren bir karakter dizisi tanımladık. Yani kısaca, içinde herhangi bir sayı barındıran öğeleri kapsama alanımıza aldık. Burada ayrıca `search()` yerine `match()` metodunu kullandığımıza da dikkat edin. `match()` metodunu kullanmamızın nedeni, bu metodun bir karakter dizisinin sadece en başına bakması. Amacımız sayı ile başlayan bütün öğeleri ayıklamak olduğuna göre, yukarıda yazdığımız kod, liste öğeleri içinde yer alan ve sayı ile başlayan bütün öğeleri ayıklayacaktır.

Şimdi de isterseniz listedeki **TY76Z** öğesini nasıl alabileceğimize bakalım:

```python
for i in a:
    if re.match("[A-Z][A-Z][0-9]",i):
        print(i)
```

    TY76Z

Burada dikkat ederseniz düzenli ifademizin başında **A-Z** diye bir şey yazdık. Bu ifade “A” ile “Z” harfleri arasındaki bütün karakterleri temsil ediyor. Biz burada yalnızca büyük harfleri sorguladık. Eğer küçük harfleri sorgulamak isteseydik **A-Z** yerine **a-z** diyecektik. 

Düzenli ifademiz içinde geçen birinci “A-Z” ifadesi aradığımız karakter dizisi olan “TY76Z” içindeki “T” harfini, ikinci “A-Z” ifadesi “Y” harfini, “0-9” ifadesi ise “7” sayısını temsil ediyor. Karakter dizisi içindeki geri kalan harfler ve sayılar otomatik olarak eşleştirilecektir. O yüzden onlar için ayrı bir şey yazmaya gerek yok. Yalnız bu söylediğimiz son şey sizi aldatmasın. Bu “otomatik eşleştirme” işlemi bizim şu anda karşı karşıya olduğumuz karakter dizisi için geçerlidir. Farklı nitelikteki karakter dizilerinin söz konusu olduğu başka durumlarda işler böyle yürümeyebilir. Düzenli ifadeleri başarılı bir şekilde kullanabilmenin ilk şartı, üzerinde işlem yapılacak karakter dizisini tanımaktır. Bizim örneğimizde yukarıdaki gibi bir düzenli ifade kalıbı oluşturmak işimizi görüyor. Ama başka durumlarda, duruma uygun başka kalıplar yazmak gerekebilir/gerekecektir. Dolayısıyla, tek bir düzenli ifade kalıbıyla hayatın geçmeyeceğini unutmamalıyız.

Bu arada, düzenli ifadelerle ilgili daha fazla şey öğrendiğimizde yukarıdaki kodu çok daha sade bir biçimde yazabileceğiz.

## . Nokta

Bu metakarakter, yeni satır karakteri hariç bütün karakterleri temsil etmek için kullanılır.  `.` metakarakteri, **sadece tek bir karakterin yerini tutar**. Aşağıdaki örneği inceleyelim:

```python
for i in liste:
    nesne = re.match("öz.an",i)
    if nesne:
        print(nesne.group())
```

    özcan
    özkan
    özhan

Gördüğünüz gibi, daha önce `[]` metakarakterini kullanarak yazdığımız bir düzenli ifadeyi bu kez farklı şekilde yazıyoruz. Unutmayın, bir düzenli ifade birkaç farklı şekilde yazılabilir. Biz bunlar içinde en basit ve en anlaşılır olanını seçmeliyiz. Ayrıca yukarıdaki kodu birkaç farklı şekilde de yazabilirsiniz. Mesela şu yazım da bizim durumumuzda geçerli bir seçenek olacaktır:

```python
for i in liste:
    if re.match("öz.an",i):
        print(i)
```

    özcan
    özkan
    özhan

Yalnız, unutmamamız gereken şey, bu `.` adlı metakarakterin sadece tek bir karakterin yerini tutuyor olmasıdır. Yani şöyle bir kullanım bize istediğimiz sonucu vermez:

```python
liste = ["ahmet","kemal", "kamil", "mehmet"]

for i in liste:
    if re.match(".met",i):
        print(i)
```

Burada `.` sembolü “ah” ve “meh” hecelerinin yerini tutamaz. `.` sembolünün görevi sadece tek bir karakterin yerini tutmaktır (yeni satır karakteri hariç). Ama biraz sonra öğreneceğimiz metakarakter yardımıyla “ah” ve “meh” hecelerinin yerini de tutabileceğiz.

`.` sembolünü kullanarak bir örnek daha yapalım.

```python
a = ['23BH56', 'TY76Z', '4Y7UZ', 'TYUDZ', '34534', "1agAY54"]

for i in a:
    if re.match(".[0-9a-z]", i):
        print(i)
```

    23BH56
    34534
    1agAY54

Burada yaptığımız şey çok basit. Şu özelliklere sahip bir karakter dizisi arıyoruz:

1. Herhangi bir karakter ile başlayacak. Bu karakter sayı, harf veya başka bir karakter olabilir.
2. Ardından bir sayı veya alfabedeki küçük harflerden herhangi birisi gelecek.
3. Bu ölçütleri karşıladıktan sonra, aradığımız karakter dizisi herhangi bir karakter ile devam edebilir.

Yukarıdaki ölçütlere uyan karakter dizilerimiz: “23BH56”, “34534”, “1agAY54”

## * Yıldız

Bu metakarakter, **kendinden önce gelen karakteri SIFIR veya daha fazla** sayıda eşleştirir. Tanımı biraz karışık olsa da örnek yardımıyla bunu da anlayacağız:

```python
yeniliste = ["st", "sat", "saat", "saaat", "falanca"]

for i in yeniliste:
    if re.match("sa*t",i):
        print(i)
```

    st
    sat
    saat
    saaat

Burada `*` sembolü kendinden önce gelen `a` karakterini sıfır veya daha fazla sayıda eşleştiriyor. Yani mesela `st` içinde sıfır adet `a` karakteri var. Dolayısıyla bu karakter yazdığımız düzenli ifadeyle eşleşiyor. `sat` içinde bir adet `a` karakteri var. Dolayısıyla bu da eşleşiyor. `saat` ve `saaat` karakter dizilerinde sırasıyla iki ve üç adet `a` karakteri var. Tabii ki bunlar da yazdığımız düzenli ifadeyle eşleşiyor. Listemizin en son öğesi olan `falanca`da da ilk hecede bir adet `a` karakteri var. Ama bu öğedeki sorun, bunun `s` harfiyle başlamaması. Çünkü biz yazdığımız düzenli ifadede, aradığımız şeyin `s` harfi ile başlamasını, sıfır veya daha fazla sayıda `a` karakteri ile devam etmesini ve ardından da `t` harfinin gelmesini istemiştik. `falanca` öğesi bu koşulları karşılamadığı için süzgecimizin dışında kaldı.

`s` harfinin de sıfır veya daha fazla sayıda eşleşmesini istersek düzenli ifademizi `s*a*t` veya `[sa]*t` biçiminde yazmamız gerekir. Bu iki seçenek içinde `[sa]*t` şeklindeki yazımı tercih etmenizi tavsiye ederim. 

Bir başka örnek inceleyelim:

```python
liste = ["ahmet", "kemal", "kamil", "mehmet"]

for i in liste:
    if re.match(".*met", i):
        print(i)
```

    ahmet
    mehmet

Gördüğünüz gibi `ahmet` ve `mehmet` öğelerini başarıyla ayıkladık. Bunu yapmamızı sağlayan şey de `*` adlı metakarakter oldu. Burada Python’a şu emri verdik: *Bana kelime başında herhangi bir karakteri (`.` sembolü herhangi bir karakterin yerini tutuyor) sıfır veya daha fazla sayıda içeren ve sonu da `met` ile biten bütün öğeleri ver!*

Kısaca ifade etmek gerekirse, bu komut sayesinde, sonu `met` ile biten her şey (`met` ifadesinin kendisi de dâhil olmak üzere) kapsama alanımıza girecektir.

## + Artı

`+` metakarakteri **kendisinden önce gelen karakteri BİR veya daha fazla sayıda** tekrar eden karakterleri ayıklar.

```python
liste = ["ahmet", "mehmet", "met", "kezban"]

for i in liste:
    if re.match(".+met",i):
        print(i)
```

    ahmet
    mehmet

```python
yeniliste = ["st", "sat", "saat", "saaat", "falanca"]

for i in yeniliste:
    if re.match("sa+t", i):
        print(i)
```

    sat
    saat
    saaat

```python
a = ["23BH56", "TY76Z", "4Y7UZ", "TYUDZ", "34534"]

for i in a:
    if re.match("[A-Z]+[0-9]",i):
        print(i)
```

    TY76Z

## ? Soru İşareti

`?` metakarakteri, **kendisinden önce gelen karakterin SIFIR veya BİR defa** eşleştiği durumları kapsar. Örneğe bakalım:

```python
yeniliste = ["st", "sat", "saat", "saaat", "falanca"]

for i in yeniliste:
    if re.match("sa?t",i):
        print(i)
```

    st
    sat

Şimdi bu metakarakteri kullanarak gerçek hayatta karşımıza çıkabilecek bir örnek verelim. Bu metakarakterin tanımına tekrar bakarsak, **olsa da olur olmasa da olur** diyebileceğimiz durumlar için bu metakarakterin rahatlıkla kullanılabileceğini görürüz. 

Şöyle bir örnek verelim: Diyelim ki bir metin üzerinde arama yapacaksınız. Aradığınız kelime `uluslararası`:

```python
metin = """Uluslararası hukuk, uluslar arası ilişkiler altında bir disiplindir. Uluslararası ilişkilerin hukuksal 
boyutunu bilimsel bir disiplin içinde inceler. Devletlerarası hukuk da denir. Ancak uluslar arası ilişkilere yeni
aktörlerin girişi bu dalı sadece devletlerarası olmaktan çıkarmıştır."""
```

Şimdi yapmak istediğimiz şey `uluslararası` kelimesini bulmak. Ama dikkat ederseniz metin içinde `uluslararası` kelimesi aynı zamanda `uluslar arası` şeklinde de geçiyor. Bizim bu iki kullanımı da kapsayacak bir düzenli ifade yazmamız gerekecek.

```python
nesne = re.findall("[Uu]luslar ?arası", metin)

for i in nesne:
    print(i)
```

    Uluslararası
    uluslar arası
    Uluslararası
    uluslar arası

Verdiğimiz düzenli ifade kalıbını dikkatlice inceleyin. Bildiğiniz gibi, `?` metakarakteri, kendinden önce gelen karakterin **sıfır veya bir kez** geçtiği durumları arıyor. Burada `?` sembolünü ` ` karakterinden, yani `boşluk` karakterinden sonra kullandık. Dolayısıyla, *boşluk karakterinin sıfır veya bir kez geçtiği durumları* hedefledik. Bu şekilde hem `uluslar arası` hem de `uluslararası` kelimesini ayıklamış olduk. Düzenli ifademizde ayrıca `[Uu]` yazdık, çünkü metnimiz içinde `uluslararası` kelimesinin büyük harfle başladığı yerler de var. Bildiğiniz gibi, `uluslar` ve `Uluslar` kelimeleri asla aynı değildir. Dolayısıyla hem `u` harfini hem de `U` harfini bulmak için, daha önce öğrendiğimiz `[]` metakarakterini kullanıyoruz.

## {} Küme Parantezi

{ } Küme Parantezi metakarakterimiz yardımıyla bir eşleşmeden kaç adet istediğimizi belirtebiliyoruz. Yine aynı örnek üzerinden gidelim:

```python
for i in yeniliste:
    if re.match("sa{3}t",i):
        print(i)
```

    saaat

Burada `a` karakterinin **3 kez** tekrar etmesini istediğimizi belirttik. Python da bu emrimizi hemen yerine getirdi.

Bu metakarakterin ilginç bir özelliği daha vardır. Küme içinde iki farklı sayı yazarak, **bir karakterin en az ve en çok** kaç kez tekrar etmesini istediğimizi belirtebiliriz. Örneğin:

```python
for i in yeniliste:
    if re.match("sa{0,3}t",i):
        print(i)
```

    st
    sat
    saat
    saaat

`sa{0,3}t` ifadesiyle, `a` harfinin en az sıfır kez, en çok da üç kez tekrar etmesini istediğimiz söyledik. Dolayısıyla, “a” harfinin sıfır, bir, iki ve üç kez tekrar ettiği durumlar ayıklanmış oldu. 

## ^ Şapka

`^` sembolünün iki işlevi var. Birinci işlevi, **bir karakter dizisinin en başındaki veriyi sorgulamaktır**. Yani aslında `match()` metodunun varsayılan olarak yerine getirdiği işlevi bu metakarakter yardımıyla `search()` metodunda da kullanabiliyoruz.

```python
a = ['23BH56', 'TY76Z', '4Y7UZ', 'TYUDZ', '34534', '1agAY54']

for i in a:
    nesne = re.search("^[A-Z]+[0-9]",i)
    if nesne:
        print(nesne.group())
```

    TY7

Gördüğünüz gibi, `^` (şapka) metakarakteri `search()` metodunun, karakter dizilerinin sadece en başına bakmasını sağladı. O yüzden de bize sadece, `TY7` çıktısını verdi. 

Aynı kodu, şapkasız olarak, şu şekilde kullanırsak:

```python
for i in a:
    nesne = re.search("[A-Z]+[0-9]",i)
    if nesne:
        print(nesne.group())
```

    BH5
    TY7
    Y7
    AY5

Gördüğünüz gibi, `^` şapka sembolü olmadığında `search()` metodu karakter dizisinin tamamını tarıyor. Biz yukarıdaki koda bir `^` sembolü ekleyerek, metodumuzun sadece karakter dizisinin en başına bakmasını istedik. 

Burada dikkatimizi çekmesi gereken başka bir nokta da, `search()` metodundaki çıktının **kırpılmış** olması. Dikkat ettiyseniz, `search()` metodu bize öğenin tamamını vermedi. Öğelerin yalnızca `[A-Z]+[0-9]` kalıbına uyan kısımlarını verdi. Çünkü biz ona tersini söylemedik. Eğer öğelerin tamamını istiyorsak bunu açık açık belirtmemiz gerekir:

```python
for i in a:
    nesne = re.search("[A-Z]+[0-9].*",i)
    if nesne:
        print(nesne.group())
```

    BH56
    TY76Z
    Y7UZ
    AY54

Veya metodumuzun karakter dizisinin sadece en başına bakmasını istersek:

```python
for i in a:
    nesne = re.search("^[A-Z]+[0-9].*",i)
    if nesne:
        print(nesne.group())
```

    TY76Z

Bu kodlarda düzenli ifade kalıbının sonuna `.*` sembolünü eklediğimize dikkat edin. Böylelikle metodumuzun sonu herhangi bir şekilde biten öğeleri bize vermesini sağladık.

`^` metakarakterinin, karakter dizilerinin en başına demir atmak dışında başka bir görevi daha vardır: **Hariç** anlamına gelmektedir.

Bu görevini sadece `[]` metakarakterinin içinde kullanıldığı zaman yerine getirir. Bunu bir örnekle görelim. Yukarıdaki listemiz üzerinde öyle bir süzgeç uygulayalım ki, **1agAY54** öğesi çıktılarımız arasında görünmesin. 

Bu öğeyi avlayabilmek için kullanmamız gereken düzenli ifade şöyle olacaktır: `[0-9A-Z][^a-z]+`

```python
for i in a:
    nesne = re.match("[0-9A-Z][^a-z]+",i)
    if nesne:
        print(nesne.group())
```

    23BH56
    TY76Z
    4Y7UZ
    TYUDZ
    34534

Burada şu ölçütlere sahip bir öğe arıyoruz:

1. Aradığımız öğe bir sayı veya büyük harf ile başlamalı
2. En baştaki sayı veya büyük harften sonra küçük harf **GELMEMELİ** (Bu ölçütü “^” işareti sağlıyor)
3. Üstelik bu **“küçük harf gelmeme durumu”** bir veya daha fazla sayıda tekrar etmeli. Yani baştaki sayı veya büyük harften sonra kaç tane olursa olsun asla küçük harf gelmemeli (Bu ölçütü de “+” işareti sağlıyor”)

Bu ölçütlere uymayan tek öğe “1agAY54” olacaktır. Dolayısıyla bu öğe çıktıda görünmez.

Burada, `^` işaretinin nasıl kullanıldığına ve küçük harfleri nasıl dışarıda bıraktığına dikkat edin. Unutmayalım, bu `^` işaretinin **hariç** anlamı sadece `[]` metakarakterinin içinde kullanıldığı zaman geçerlidir.

## $ Dolar

```python

```





Kaynak: [Düzenli İfadeler - Yazbel Python Belgeleri](https://python-istihza.yazbel.com/standart_moduller/regex.html)
