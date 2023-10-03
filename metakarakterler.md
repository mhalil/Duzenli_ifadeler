## Metakarakterler (Özel Karakterler)

Metakarakterler; kabaca, programlama dilleri için özel anlam ifade eden sembollerdir. Örneğin `\n` bir bakıma bir metakarakterdir, çünkü `\n` sembolü Python programlama dili için özel bir anlam taşır. Python bu sembolü gördüğü yerde yeni bir satıra geçer. Metakarakterler, **Kendisiyle eşleşmeyen karakterler** olarak ifade edilebilir. Örneğin, **a** harfi yalnızca kendisiyle eşleşir. Tıpkı **istihza** kelimesinin yalnızca kendisiyle eşleşeceği gibi. Ancak mesela `\t` ifadesi kendisiyle eşleşmez. Python bu işareti gördüğü yerde sekme (tab) düğmesine basılmış gibi tepki verecektir. İşte düzenli ifadelerde de buna benzer metakarakterlerden yararlanacağız. Düzenli ifadeler içinde de, özel anlam ifade eden pek çok sembol, yani metakarakter vardır. Şimdi bu meta karakterleri ayrı ayrı başlıklar altında inceleyelim.

## [] Köşeli Parantez

İlk inceleyeceğimiz metakarakterlerden biri Köşeli Parantez `[ ]` sembolüdür. 
Python, **köşeli parantez içinde gördüğü bütün karakterleri tek tek liste öğelerine uygular.**

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

Bu metakarakter, **yeni satır karakteri hariç bütün karakterleri temsil etmek için kullanılır.**  `.` metakarakteri, **sadece tek bir karakterin yerini tutar**. Aşağıdaki örneği inceleyelim:

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

`+` metakarakteri **kendisinden önce gelen karakteri BİR veya DAHA FAZLA sayıda** tekrar eden karakterleri ayıklar.

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

{ } Küme Parantezi metakarakterimiz yardımıyla **bir eşleşmeden kaç adet istediğimizi** belirtebiliyoruz. Yine aynı örnek üzerinden gidelim:

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

`^` sembolünün iki işlevi var. Birinci işlevi, **Çok satırlı desende ya da bir karakter dizisinin en başındaki veriyi sorgulamaktır**. Yani aslında `match()` metodunun varsayılan olarak yerine getirdiği işlevi bu metakarakter yardımıyla `search()` metodunda da kullanabiliyoruz. **Sadece kendinden sonra gelen BİR karaktere BAKMIYOR**.

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

`$` metakarakteri, **Çok satırlı desenin ya da dizelerin nasıl biteceğini** belirliyor. Bu sembol arama/eşleştirme işleminin karakter dizisinin en sonuna bakmasını sağlıyor. **Sadece kendinden önceki BİR karaktere BAKMIYOR**. Hatırlarsınız `^` metakarakteri eşleştirme işleminin karakter dizisinin en başından başlamasını sağlıyordu.

```python
liste = ["at", "katkı", "fakat", "atkı", "rahat", "mat", "yat", "sat", "satılık", "katılım"]
```

Diyelim ki yukarıda tanımlı listeden, **at** hecesiyle biten kelimeleri ayıklamak istiyoruz:

```python
for i in liste:
    if re.search("at$",i):
        print(i)
```

    at
    fakat
    rahat
    mat
    yat
    sat

Burada `$` metakarakteri sayesinde aradığımız karakter dizisinin nasıl bitmesi gerektiğini belirleyebildik. Eğer biz **at** ile başlayan bütün öğeleri ayıklamak isteseydik ne yapmamız gerektiğini biliyorsunuz:

```python
for i in liste:
    if re.search("^at",i):
        print(i)
```

    at
    atkı

Gördüğünüz gibi, `^` işareti bir karakter dizisinin nasıl başlayacağını belirlerken, `$` işareti aynı karakter dizisinin nasıl biteceğini belirliyor. 

Dikkat edilmesi gereken bir husu ta şudur ki;

* `^` işareti bir karakter dizisinin başına yazılırken
* `$` işareti karakter dizisinin sonuna yazılırken

## \ Ters Bölü

Bu işaret bildiğimiz **kaçış dizisi**dir. Peki burada ne işi var? Şimdiye kadar öğrendiğimiz konulardan gördüğünüz gibi, Python’daki düzenli ifadeler açısından özel anlam taşıyan bir takım semboller/metakarakterler var. Bunlar kendileriyle eşleşmiyorlar. Yani bir karakter dizisi içinde bu sembolleri arıyorsak eğer, bunların taşıdıkları özel anlam yüzünden bu sembolleri ayıklamak hemencecik mümkün olmayacaktır. Yani mesela biz `$` sembolünü arıyor olsak, bunu Python’a nasıl anlatacağız? Çünkü bu sembolü yazdığımız zaman Python bunu farklı algılıyor. Lafı dolandırmadan hemen bir örnek verelim…

Diyelim ki elimizde şöyle bir liste var:

```python
liste = ["10$", "25€", "20$", "10TL", "25£"]
```

Amacımız bu listedeki **dolarlı** değerleri ayıklamaksa ne yapacağız? Şunu deneyelim önce:

```python
for i in liste:
    if re.match("[0-9]+$",i):
        print(i)
```

Python `$` işaretinin özel anlamından dolayı, bizim sayıyla biten bir karakter dizisi aradığımızı zannedecek, dolayısıyla da herhangi bir çıktı vermeyecektir. Çünkü listemizde sayıyla biten bir karakter dizisi yok.

Peki biz ne yapacağız? İşte bu noktada `\` metakarakteri devreye girecek. Hemen bakalım:

```python
for i in liste:
    if re.match("[0-9]+\$",i):
        print(i)
```

    10$
    20$

Gördüğünüz gibi, “\” sembolünü kullanarak “$” işaretinin özel anlamından kaçtık.

## | Dik Çizgi, Boru (Pipe) Sembolü

Bu metakarakter, birden fazla düzenli ifade kalıbını birlikte eşleştirmemizi sağlar. `|` sembolü, **VEYA** anlamına gelir diyebiliriz. Yani birkaç alternatif modelden **herhangi birini** eşleştirir. Eşleştirme için birden fazla kriter belirlermek için `|` sembölünü kullanabiliriz. Hemen örnek yapalım:

```python
liste = ["at", "katkı", "fakat", "atkı", "rahat", "mat", "yat", "sat", "satılık", "katılım"]

for i in liste:
    if re.search("^at|at$",i):
        print(i)
```

    at
    fakat
    atkı
    rahat
    mat
    yat
    sat

Gördüğünüz gibi `|` metakarakterini kullanarak **at** ile başlayan **ve** biten kelimeleri bulduk / ayıkladık. `|` sembolünü kullanmasaydık ve aşağıdaki ifadesiyi yazsaydık **atat** ile başlayan ve biten kelime aramış olurduk ve sonuç bulamazdık.

```python
for i in liste:
    if re.search("^atat$",i):
        print(i)
```

Aşağıdaki ifadesiyi yazmış olsaydık ise **at** ile başlayan ve biten kelime aramış olurduk ve sadece **at** sonucunu elde ederdik.

```python
for i in liste:
    if re.search("^at$",i):
        print(i)
```

    at

## ( ) Parantez

Bu metakarakter yardımıyla **düzenli ifade kalıplarını gruplayacağız**. Ayrıca gruplandırılmış ifadelerine denk gelen kalıpları saklar ve en fazla 9 kalıp saklayabilir. Bu metakarakter bizim bir karakter dizisinin istediğimiz kısımlarını ayıklamamızda çok büyük kolaylıklar sağlayacak.

```python
x = ["ali", "veli", "deli", "zeki", "abi"]

for i in x:
    if re.search("a(b|l)i", i):
        print(i)
```

    ali
    abi

```python
veri = ['650-654-7544', 'Mustafa Halil', '650524495', '65080976', '08069114', '656037422', '6504476824', '6508000010',
 '6501552207', '(650)605 09 96', '650-537-82-34', '6503320122', '650_919_64', '650-abc-7425', '6509318724', '6502184706',
 '650-xyz-1653', '6501921596']

for i in veri:
    if re.search(r"(\d{3})-([a-z]{3})-(\d{4})", i):
        print(i)
```

    650-abc-7425
    650-xyz-1653

`r"(\d{3})-([a-z]{3})-(\d{4})"` deseni ile 3 adet grup oluşturduk. Bu desenleri açıklayalım;

* `(\d{3})` = **3 adet rakam**, ardından  
* `-` = **Tire işareti** , ardından
* `([a-z]{3})` = **a'dan z'ye kadar 3 adet küçük harf** , ardından
* `-` = **Tire işareti** ve son olarak
* `(\d{4})` = **4 adet rakam**

dan oluşan bir değer arıyorum.

Şimdi grupları açıklamaya çalışayım.

```python
veri = "08069114 6501552207 650-abc-7425 (650)605 09 96 650-537-82-34 650_919_64 6509318724 650-xyz-1653"

desen = r"(\d{3})-([a-z]{3})-(\d{4})"
eslesen = re.finditer(desen, veri)

for es in eslesen:
    print(es.group())
```

    650-abc-7425
    650-xyz-1653

Görüldüğü üzere aranan desene uygun 2 adet sonuç elde ettik; **650-abc-7425** ve **650-xyz-1653**. 

Parantez içine aldığımız desenlerin her biri **bir grubu ifade ediyor**.  Bu değerleri ekrana yazdırmak için `group()` metodunu kullandık. `group()` metodu ile `group(0)` metodu aynıdır. Desenimizde (parantez içinde) 3 grup olduğu için `group(1), group(2)` ve `group(3)` yöntemiyle, eşleşen 3 gruba ayrı ayrı erişebiliriz. Aşağıdaki kodları inceleyin;

```python
desen = r"(\d{3})-([a-z]{3})-(\d{4})"
eslesen = re.finditer(desen, veri)

print("1. Grup Değerleri:")
for es in eslesen:
    print(es.group(1))
```

    1. Grup Değerleri:
    650
    650

```python
desen = r"(\d{3})-([a-z]{3})-(\d{4})"
eslesen = re.finditer(desen, veri)

print("2. Grup Değerleri:")
for es in eslesen:
    print(es.group(2))
```

    2. Grup Değerleri:
    abc
    xyz

```python
desen = r"(\d{3})-([a-z]{3})-(\d{4})"
eslesen = re.finditer(desen, veri)

print("3. Grup Değerleri:")
for es in eslesen:
    print(es.group(3))
```

    3. Grup Değerleri:
    7425
    1653

# Eşleşme Nesnelerinin Metotları

## group() metodu

Bu bölümde doğrudan düzenli ifadelerin değil, ama düzenli ifadeler kullanılarak üretilen eşleşme nesnelerinin bir metodu olan `group()` metodundan bahsedeceğiz. Esasında biz bu metodu önceki bölümlerde de kullanmıştık. Ama burada bu metoda biraz daha ayrıntılı olarak bakacağız.

Daha önceki bölümlerden hatırlayacağınız gibi, bu metot düzenli ifadeleri kullanarak eşleştirdiğimiz karakter dizilerini görme imkanı sağlıyordu. Bu bölümde bu metodu `( )` metakarakteri yardımıyla daha verimli bir şekilde kullanacağız. İsterseniz ilk olarak şöyle basit bir örnek verelim:

```python
kardiz = "python bir programlama dilidir"
nesne = re.search("(python) (bir) (programlama) (dilidir)", kardiz)

print(nesne.group())
```

    python bir programlama dilidir

Burada düzenli ifade kalıbımızı nasıl grupladığımıza dikkat edin. `print(nesne.group())` komutunu verdiğimizde eşleşen karakter dizileri ekrana döküldü. Şimdi bu grupladığımız bölümlere tek tek erişelim:

```python
nesne.group(0)
```

    'python bir programlama dilidir'

Gördüğünüz gibi, “0” indeksi eşleşen karakter dizisinin tamamını veriyor. Gerisinin nasıl olacağını tahmin edebilirsiniz:

```python
print(nesne.group(1))
print(nesne.group(2))
print(nesne.group(3))
print(nesne.group(4))
```

    python
    bir
    programlama
    dilidir

`group()` metoduna ait benzer bir örnek yukarıdaki **( ) Parantez** başlığı altında detaylı anlatıldı.

## groups() metodu

Bu metot, bize kullanabileceğimiz bütün grupları bir *demet* halinde sunar:

```python
nesne.groups()
```

    ('python', 'bir', 'programlama', 'dilidir')

# Özel Diziler

## \s   Boşluk Karakterinin Yerini Tutan Özel Dizi.

Bu sembol (`\s`), bir karakter dizisi içinde geçen **boşlukları (boşluk, tab ve enter karakterlerini) yakalamak** için kullanılır.

```python
a = ["5 Ocak", "27Mart", "4 Ekim", "Nisan 3"]

for i in a:
    nesne = re.search("[0-9]\s[A-Za-z]+",i)
    if nesne:
        print(nesne.group())
```

    5 Ocak
    4 Ekim

Yukarıdaki örnekte, bir sayı ile başlayan, ardından bir adet boşluk karakteri içeren, sonra da bir büyük veya küçük harfle devam eden karakter dizilerini ayıkladık. Burada boşluk karakterini `\s` simgesi ile gösterdiğimize dikkat edin.

## \S   Boşluk Karakterinin Dışındaki Karakterlerin Tutan Özel Dizi.

`\S` özel dizisi, **boşluk olmayan karakterleri** avlar.

```python
for i in a:
    nesne = re.search("\d+\S\w+",i)
    if nesne:
        print(nesne.group())
```

    27Mart

## \d   Sayıların Yerini Tutan Özel Dizi.

Bu sembol, bir karakter dizisi içinde geçen **rakamları (ondalık sayıları) eşleştirmek için** kullanılır. Yani `[0-9]` ifadesi ile eşdeğerdir.

Buraya kadar olan örneklerde bu işlevi yerine getirmek için `[0-9]` ifadesinden yararlanıyorduk. Şimdi artık aynı işlevi daha kısa yoldan, `\d` dizisi ile yerine getirebiliriz. İsterseniz yine yukarıdaki örnekten gidelim:

```python
a = ["5 Ocak", "27Mart", "4 Ekim", "Nisan 3"]

for i in a:
    nesne = re.search("\d\s[A-Za-z]+",i)
    if nesne:
        print(nesne.group())
```

    5 Ocak
    4 Ekim

Burada, `[0-9]` yerine `\d` yerleştirerek daha kısa yoldan sonuca vardık.

## \D   Sayı Olmayan Karakterlerin Yerini Tutan Özel Dizi.

`\D` özel dizisi **rakam (ondalık sayı) olmayan karakterleri** avlar. Yani `[^0-9]` ile eşdeğerdir.

```python
for i in a:
    nesne = re.search("\D+",i)
    if nesne:
        print(nesne.group())
```

     Ocak
    Mart
     Ekim
    Nisan 

```python
for i in a:
    nesne = re.search("\s\D+",i)
    if nesne:
        print(nesne.group())
```

     Ocak
     Ekim

## \w   Alfanümerik Karakterlerin Yerini Tutan Özel Dizi.

Bu sembol, bir karakter dizisi içinde geçen **alfanümerik karakterleri (harf, rakam) ve buna ek olarak alt çizgi karakterini** `_` bulmak için kullanılır. 

Bu özel dizi şu ifadeyle aynı anlama gelir: `[a-zA-Z0-9_]`. Bu ifadeyi yazmaktansa `\w` yazmanın ne kadar kolay olduğu ortada.

```python
a = "abc123_$%+"
print(re.search("\w*", a).group())
```

    abc123_

## \W   Alfanümerik Karakterlerin Dışındaki Karakterlerin Yerini Tutan Özel Dizi.

Bu sembol **Harf, rakam ve alt çizgi karakteri dışında** herhangi bir şeyle eşleşir. 

Bu özel dizi şu ifadeyle aynı anlama gelir: `[^a-zA-Z0-9_]` ile eşdeğerdir

```python
b = ["abc", "123", "$%+"]

for i in b:
    print(re.search("\W*", i).group())
```

    $%+

Şimdi bu özel diziler için genel bir örnek verip konuyu kapatalım.

```python
veriler = ["esra : istinye 05331233445", "esma : levent 05322134344", "sevgi : dudullu 05354445434", 
           "kemal : sanayi 05425455555", "osman : tahtakale 02124334444","metin : taksim 02124344332"]
```

Amacımız bu listede yer alan isim ve telefon numaralarını `isim > telefon numarası` şeklinde almak:

```python
for i in veriler:
    nesne = re.search("(\w+)\s+:\s(\w+)\s+(\d+)",i)
    if nesne:
        print("{} > {}".format(nesne.group(1), nesne.group(3)))
```

    esra > 05331233445
    esma > 05322134344
    sevgi > 05354445434
    kemal > 05425455555
    osman > 02124334444
    metin > 02124344332

Burada formülümüz şu şekilde: `Bir veya daha fazla karakter` + `bir veya daha fazla boşluk` + `’:’ işareti` + `“bir adet boşluk` + `bir veya daha fazla sayı`

## \b Kelime Sınırını Belirten Özel Dizi

`\b` sembolü ile Kelimenin nasıl **başlaması**, nasıl **bitmesi** ya da tam olarak **sınırlarının ne olması** gerektiğini belirtebiliriz.

```python
veri = "Doğum günüm 01.02.1980. Ağabeyim Doğum günü ise 03.04.1975'te doğdu. Bilgisayarın ip adresi 04.05.18741'dir."
desen = r"\b[A-Z]\w+"
b_harf = re.findall(desen, veri)

print(b_harf)
```

    ['Doğum', 'Ağabeyim', 'Doğum', 'Bilgisayarın']

Büyük harf ile başlayan kelimeleri görmek istediğimizde yukarıdaki deseni kullanabiliriz.

Cümle sonlarını bulmak için ise aşağıdaki desen işimize yarayabilir.

```python
desen = r"\w+\.\s\b"
cumle_sonu = re.findall(desen, veri)

print(cumle_sonu)
```

    ['1980. ', 'doğdu. ']

```python
veri = "Doğum günüm 01.02.1980. ağabeyim ise 03.04.1975'te doğdu. bilgisayarımın ip adresi 04.05.18741'dir."

desen = r"\d{2}\.\d{2}\.\d{4}"
d_gunleri = re.findall(desen, veri)

print(d_gunleri)
```

    ['01.02.1980', '03.04.1975', '04.05.1874']

Görüldüğü gibi desene uygun sonuçlar aldık ancak çıktıdaki son değer, doğum günü olmamasına rağmen desenle eşleşti. Bu sorunu çözmek için, deseni başlangıç ve bitiş sınırlarını belirterek tanımlamalıyız. Yani desenin başına ve sonuna `\b` sembolünü eklemeliyiz.

```python
desen = r"\b\d{2}\.\d{2}\.\d{4}\b"
d_gunleri = re.findall(desen, veri)

print(d_gunleri)
```

    ['01.02.1980', '03.04.1975']

Desenin başına ve sonuna `\b` sembolünü ekleyerek, kelimenin tüm sınırlarını tanımlamış olduk. Bu desen ile; Kelime başında 2 adet rakam, ardından 1 nokta (.) sonrasında tekrar 2 adet rakam ve ardından nokta (.) gelsin son olarak ta 4 adet rakam olsun demiş olduk. BU desen sayesinde **04.05.18741** değerini safdışı bırakış olduk.

Eğer verimizde tarih yazım biçimi farklı (örneğin nokta (.) ve taksim, bölü (/) işareti) olan birden fazla değerler olsaydı nasıl bir yol izlemeliydik? Buna da bir örnek verelim.

```python
veri = "Doğum günüm 01.02.1980. ağabeyim ise 03/04/1975'te doğdu. bilgisayarımın ip adresi 04.05.18741'dir."

desen = r"\b\d{2}[./]\d{2}[./]\d{4}\b"
d_gunleri = re.findall(desen, veri)

print(d_gunleri)
```

    ['01.02.1980', '03/04/1975']

Gördüğünüz gibi nokta (.) ve taksim, bölü (/) işaretini, köşeli parantez içerisine yazarak alternatif seçenekler oluşturmuş olduk.

**NOT:** **Nokta işaretini** desen içinde doğrudan yazarken kaçış dizisi olan ters taksim işaretini yazmamız gerekiyor. Oysa köşeli parantez içerisinde yazdığımızda kaçış dizini olan ters bölü işaretini kullanmıyoruz. Bu, Köşeli parantezin bir özelliğidir. Diğer sembolleri de nokta gibi yazabiliyoruz.

## \B Özel Dizisi

`\b` özel dizisinin tam tersidir.

Örneğin `py\b` deseni, **py** ile biten dizilerle eşleşirken `py\B` deseni,    **py** ifadesini içeren ancak **py** ile **BİTMEYENLERLE** eşleşir. 

```python
metin = "Recep Ramazan Seher (Halil) Sertaç Halili zaman erkek Halil. şeker 2.345 python, py3, py2 py py. py!"
desen = r"\w+er\b" # başında alfanümerik karakterler olan sonu "er" ile biten kelimeleri bul.

print(re.findall(desen, metin))
```

    ['Seher', 'şeker']

`"\w+er\b"` deseni ile, başında alfanümerik karakterler olan sonu **er** ile biten kelimeleri bulmaya çalıştık.

```python
liste = ['Recep', 'Ramazan', 'Seher', '(Halil)', 'manzara', 'Sertaç', 'Halili', 'zaman', 'erkek', 'Halil.', 
         'şeker', '2.345', 'python,', 'py3,', 'py2','py', 'py.', 'py!']

desen = r"er\B" 

for oge in liste:
    if re.search(desen, oge):
        print(oge)
```

    Sertaç
    erkek

`"er\B"` deseni ile, içinde **er** ifadesi olan ancak sonu **er** ile **bitmeyen** kelimeleri bulmaya çalıştık.

```python
desen = r"\Ber\B" 

for oge in liste:
    if re.search(desen, oge):
        print(oge)
```

    Sertaç

`"\Ber\B"` deseni ile, içinde **er** ifadesi olan ancak başında ve sonunda **er** ifadesi **bulunmayan** kelimeleri bulmaya çalıştık.

# Düzenli İfadelerin Derlenmesi

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

## compile() ile Derleme Seçenekleri

Bir önceki bölümde `compile()` metodunun ne olduğunu, ne işe yaradığını ve nasıl kullanıldığını görmüştük. Bu bölümde ise **compile (derleme)** işlemi sırasında kullanılabilecek seçenekleri anlatacağız.

## re.IGNORECASE veya re.I

Bildiğiniz gibi, Python’da büyük-küçük harfler önemlidir. Yani eğer **python** kelimesini arıyorsanız, alacağınız çıktılar arasında **Python** olmayacaktır. Çünkü **python** ve **Python** birbirlerinden farklı iki karakter dizisidir. İşte `re.IGNORECASE` veya kısaca `re.I` adlı derleme seçenekleri bize **büyük-küçük harfe dikkat etmeden arama yapma** imkanı sağlar. Hemen bir örnek verelim:

```python
metin = """Programlama dili, programcının bir bilgisayara ne yapmasını
istediğini anlatmasının standartlaştırılmış bir yoludur. Programlama
dilleri, programcının bilgisayara hangi veri üzerinde işlem yapacağını,
verinin nasıl depolanıp iletileceğini, hangi koşullarda hangi işlemlerin
yapılacağını tam olarak anlatmasını sağlar. Şu ana kadar 2500’den fazla
programlama dili yapılmıştır. Bunlardan bazıları: Pascal, Basic, C, C#,
C++, Java, Cobol, Perl, Python, Ada, Fortran, Delphi programlama
dilleridir."""

derli = re.compile("programlama", re.IGNORECASE)
print(derli.findall(metin))
```

    ['Programlama', 'Programlama', 'programlama', 'programlama']

Gördüğünüz gibi, metinde geçen hem **programlama** kelimesini hem de **Programlama** kelimesini ayıklayabildik. Bunu yapmamızı sağlayan şey de `re.IGNORECASE` adlı derleme seçeneği oldu. 

Eğer bu seçeneği kullanmasaydık, çıktıda yalnızca **programlama** kelimesini görürdük. Çünkü aradığımız şey aslında **programlama** kelimesi idi. Biz istersek `re.IGNORECASE` yerine kısaca `re.I` ifadesini de kullanabiliriz. Aynı anlama gelecektir.

## re.DOTALL veya re.S

Bildiğiniz gibi, metakarakterler arasında yer alan `.` sembolü herhangi bir karakterin yerini tutuyordu. Bu metakarakter bütün karakterlerin yerini tutmak üzere kullanılabilir. Hatırlarsanız, `.` metakarakterini anlatırken, bu metakarakterin, **yeni satır karakterinin yerini tutmayacağını** söylemiştik. Bunu bir örnek yardımıyla görelim. Diyelim ki elimizde şöyle bir karakter dizisi var:

```python
a = "Ben Python,\nMonty Python"
print(a)
```

    Ben Python,
    Monty Python

Bu karakter dizisi içinde **Python** kelimesini temel alarak bir arama yapmak istiyorsak eğer, kullanacağımız şu kod istediğimiz şeyi yeterince yerine getiremeyecektir:

```python
print(re.search("Python.*", a).group())
```

    Python,

Bunun sebebi, `.` metakarakterinin `\n` (yeni satır) kaçış dizisini dikkate almamasıdır. Bu yüzden **bu kaçış dizisinin ötesine geçip orada arama yapmıyor**. Ama şimdi biz ona bu yeteneği de kazandıracağız:

```python
derle = re.compile("Python.*", re.DOTALL)
nesne = derle.search(a)

if nesne:
    print(nesne.group())
```

    Python,
    Monty Python

`re.DOTALL` seçeneğini sadece `re.S` şeklinde de kısaltabilirsiniz.

# Düzenli İfadelerle Metin/Karakter Dizisi Değiştirme İşlemleri

## sub() metodu

Şimdiye kadar hep düzenli ifadeler yoluyla bir karakter dizisini nasıl eşleştireceğimizi inceledik. Ama tabii ki düzenli ifadeler yalnızca bir karakter dizisi **bulmak**la ilgili değildir. Bu araç aynı zamanda bir karakter dizisini **değiştirmeyi** de kapsar. Bu iş için temel olarak iki metot kullanılır. Bunlardan ilki `sub()` metodudur. Bu bölümde sub() metodunu inceleyeceğiz.

En basit şekliyle `sub()` metodunu şu şekilde kullanabiliriz:

```python
a = "Kırmızı başlıklı kız, kırmızı elma dolu sepetiyle anneannesinin evine gidiyormuş!"

derle = re.compile("kırmızı", re.IGNORECASE)
print(derle.sub("yeşil", a))
```

    yeşil başlıklı kız, yeşil elma dolu sepetiyle anneannesinin evine gidiyormuş!

Burada karakter dizimiz içinde geçen bütün **kırmızı** kelimelerini **yeşil** kelimesiyle değiştirdik. Bunu yaparken de `re.IGNORECASE` adlı derleme seçeneğinden yararlandık.

Elbette `sub()` metoduyla daha karmaşık işlemler yapılabilir. Bu noktada şöyle bir hatırlatma yapalım. Bu `sub()` metodu karakter dizilerinin `replace()` metoduna çok benzer. Ama tabii ki `sub()` metodu hem kendi başına `replace()` metodundan çok daha güçlüdür, hem de beraber kullanılabilecek derleme seçenekleri sayesinde `replace()` metodundan çok daha esnektir. Ama tabii ki, eğer yapmak istediğiniz iş `replace()` metoduyla halledilebiliyorsa en doğru yol, `replace()` metodunu kullanmaktır.

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

`b = nesne.group().split()`

Burada, fonksiyonumuzun argümanı olarak vazife gören eşleşme nesnesine ait metotlardan biri olan `group()` metodunu kullanıyoruz. Böylece `derle = re.compile("çile[kğ]", re.IGNORECASE)` satırı yardımıyla metin içinde bulduğumuz bütün **“çilek”** ve çeşitlerini alıyoruz. Karakter dizilerinin `split()` metodunu kullanmamızın nedeni ise `group()` metodunun verdiği çıktıyı liste haline getirip daha kolay manipüle etmek. Burada `for i in b: print(i)` komutunu verirseniz `group()` metodu yardımıyla ne bulduğumuzu görebilirsiniz:

<code>
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
</code>

Bu çıktıyı gördükten sonra, kodlarda yapmaya çalıştığımız şey daha anlamlı görünmeye başlamış olmalı. Şimdi sonraki satıra geçiyoruz:

<code>for i in b:
    return a[i]
</code>

Burada, `group()` metodu yardımıyla bulduğumuz eşleşmeler üzerinde bir `for` döngüsü oluşturduk. 
    Ardından da `return a[i]` komutunu vererek “a” adlı sözlük içinde yer alan öğeleri yazdırıyoruz. Bu arada, buradaki **“i”**nin yukarıda verdiğimiz `group()` çıktılarını temsil ettiğine dikkat edin. `a[i]` gibi bir komut verdiğimizde aslında sırasıyla şu komutları vermiş oluyoruz:  

<code>
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
</code>

Bu komutların çıktıları sırasıyla **“erik”, “eriğ”, “erik”, “Eriğ”, “erik”, “erik”, “erik”, “Eriğ”, “erik”, “erik”** olacaktır. İşte bu return satırı bir sonraki kod olan `print(derle.sub(degistir,metin))` ifadesinde etkinlik kazanacak. Bu son satırımız sözlük öğelerini tek tek metne uygulayacak ve mesela `a["çilek"]` komutu sayesinde metin içinde **“çilek”** gördüğü yerde **“erik”** kelimesini yapıştıracak ve böylece bize istediğimiz şekilde değiştirilmiş bir metin verecektir…

Bu kodların biraz karışık gibi göründüğünü biliyorum, ama aslında çok basit bir mantığı var: `group()` metodu ile metin içinde aradığımız kelimeleri ayıklıyor. Ardından da **“a”** sözlüğü içinde bunları anahtar olarak kullanarak **“çilek”** ve çeşitleri yerine **“erik”** ve çeşitlerini koyuyor.

Yukarıda verdiğimiz düzenli ifadeyi böyle ufak bir metinde kullanmak çok anlamlı olmayabilir. Ama çok büyük metinler üzerinde çok çeşitli ve karmaşık değişiklikler yapmak istediğinizde bu kodların işinize yarayabileceğini göreceksiniz.

## subn() metodu

Bu metodu çok kısa bir şekilde anlatıp geçeceğiz. Çünkü bu metot `sub()` metoduyla neredeyse tamamen aynıdır. Tek farkı, `subn()` metodunun bir metin içinde yapılan değişiklik sayısını da göstermesidir. Yani bu metodu kullanarak, kullanıcılarınıza **“toplam şu kadar sayıda değişiklik yapılmıştır”** şeklinde bir bilgi verebilirsiniz. Bu metot çıktı olarak iki öğeli bir demet verir. 

Birinci öğe değiştirilen metin, ikinci öğe ise yapılan değişiklik sayısıdır. Yani kullanıcıya değişiklik sayısını göstermek için yapmanız gereken şey, bu demetin ikinci öğesini almaktır. Mesela `sub()` metodunu anlatırken verdiğimiz kodların son satırını şöyle değiştirebilirsiniz:

```python
ab = derle.subn(degistir, metin)
print("Toplam {} değişiklik yapılmıştır.".format(ab[1]))
```

    Toplam 12 değişiklik yapılmıştır.

# Sonuç

Böylelikle düzenli ifadeler konusunu bitirmiş olduk. Buradaki amacımız, size düzenli ifadeler konusunda genel bir bakış sunabilmekti. Bu yazıları okuduktan sonra kafanızda düzenli ifadelerle ilgili kabataslak da olsa bir resim oluştuysa bu yazılar amacına ulaşmış demektir. Elbette düzenli ifadeler burada anlattıklarımızdan ibaret değildir. Bu konunun üzerine eğildiğinizde aslında düzenli ifadelerin dipsiz bir kuyu gibi olduğunu göreceksiniz. 

Esasında en başta da dediğimiz gibi, düzenli ifadeler apayrı bir dil gibidir. Doğrusu şu ki, düzenli ifadeler başlı başına bağımsız bir sistemdir. Hemen hemen bütün programlama dilleri öyle ya da böyle düzenli ifadeleri destekler. Python’da düzenli ifadeleri bünyesine adapte etmiş dillerden biridir. Bizim düzenli ifadeler konusundaki yaklaşımımız, her zaman bunları **“gerektiğinde”** kullanmak olmalıdır. Dediğimiz gibi, eğer yapmak istediğiniz bir işlemi karakter dizilerinin metotları yardımıyla yapabiliyorsanız düzenli ifadelere girişmemek en iyisidir. Çünkü karakter dizisi metotları hem daha hızlıdır hem de anlaması daha kolaydır.

Kaynak: https://python-istihza.yazbel.com/standart_moduller/regex.html
