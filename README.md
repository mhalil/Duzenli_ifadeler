# Düzenli İfadeler (Regular Expressions - Regex )

Düzenli İfadeler (Regular Expressions) konusunu farklı kaynaklardan okuyup inceleyerek öğrenmeye çalışıyor ve öğrendiklerimi repoma ekleyerek paylaşıyorum.

Aşağıda detaylı olarak anlatılan Düzenli İfade konusunun **Özet Tablosuna (Cheat Sheet)** [BURADAN](duzenli_ifade_ozet_tablo.md) erişebilirsiniz.

![regex](img/regex.png)

### Düzenli İfadeler (Regular Expressions) Nedir ?

> Düzenli ifadeler (Regular Expressions, kısaca "Regex" ya da "Regexp"), Python programlama dilinin en çetrefilli konularından biridir. Ama bütün zorluklarına rağmen programlama deneyimimizin bir noktasında mutlaka karşımıza çıkacak olan bu yapıyı öğrenmemizde büyük fayda var. Düzenli ifadeleri öğrendikten sonra, elle yapılması saatler sürecek bir işlemi saliseler içinde yapabildiğinizi gördüğünüzde eminim düzenli ifadelerin ne büyük bir nimet olduğunu siz de anlayacaksınız.

> Peki, düzenli ifadeleri kullanarak neler yapabiliriz? Çok genel bir ifadeyle, bu yapıyı kullanarak metinleri veya karakter dizilerini parmağımızda oynatabiliriz. Örneğin bir web sitesinde dağınık halde duran verileri bir çırpıda ayıklayabiliriz. Bu veriler, mesela, toplu halde görmek istediğimiz web adreslerinin bir listesi olabilir. Bunun dışında, örneğin, çok sayıda belge üzerinde tek adımda istediğimiz değişiklikleri yapabiliriz.

> Ancak genel bir kural olarak, düzenli ifadelerden kaçabildiğimiz müddetçe kaçmamız gerekir. Eğer Python’daki karakter dizisi metotları, o anda yapmak istediğimiz şey için yeterli geliyorsa mutlaka o metotları kullanmalıyız. Çünkü karakter dizisi metotları, düzenli ifadelere kıyasla hem daha basit, hem de çok daha hızlıdır. Ama bir noktadan sonra karakter dizilerini kullanarak yazdığınız kodlar iyice karmaşıklaşmaya başlamışsa, kodların her tarafı if deyimleriyle dolmuşsa, hatta basit bir işlemi gerçekleştirmek için yazdığınız kod sayfa sınırlarını zorlamaya başlamışsa, işte o noktada artık düzenli ifadelerin dünyasına adım atmanız gerekiyor olabilir.
> 
> Kaynak: [Düzenli İfadeler - Yazbel Python Belgeleri](https://python-istihza.yazbel.com/standart_moduller/regex.html)

# Konu Başlıkları

[Düzenli İfade Metotları (Fonksiyonları)](duzenli_ifade_tanim_ve_metotlari.md)

... **match()** Metodu

...... *span() Metodu*

...... *string Özelliği*

...... *group() Metodu*

... **split()** Metodu

... **search()** Metodu

...... *start() Metodu*

...... *end() Metodu*

... **findall()** Metodu

... **finditer()** Metodu

... **sub()** Metodu

**... subn()** Metodu

**... escape()** Metodu

**... compile()** Metodu

**... purge()** Metodu

[MetaKarakterler, Özel Dizinler ve Bayraklar](metakarakterler.md)

... **Meta Karakterler**

...... **[ ]** Köşeli Parantez

...... **.** Nokta

...... ***** Yıldız

...... **+** Artı

...... **?** Soru İşareti

...... **{ }** Küme Parantezi

...... **^** Şapka

...... **$** Dolar

...... \ Ters Bölü

...... **|** Dik Çizgi, Boru (Pipe) Sembolü

...... **( )** Parantez

... **Özel Diziler**

...... \s

...... \S

...... \d

...... \D

...... \w

...... \W

...... \A

...... \Z

...... \b

...... \B

**... Bayraklar (Flags)**

...... *re.IGNORECASE* veya *re.I*

...... *re.MULTILINE veya re.M*

...... *re.DOTALL* veya *re.S*

...... *re.UNICODE veya re.U*

... **Sonuç**

[Eşleşme Nesnesi Metotları ve Gruplar](gruplar.md)

... group() metodu

... groups() metodu

... (?P<...> ile Etiketleme

... Lookahead (İleriye bak)

...... *(?= ...) Pozitif Lookahead*

...... *(?! ...) Negatif Lookahead*

... Look Behind (Geriye bak)

...... *(?<=...) Pozitif Lookbehind*

...... *(?<!...) Negatif Lookbehind*

[Düzenli Tablo Özet Tablosu (Cheat Sheet)](duzenli_ifade_ozet_tablo.md)
