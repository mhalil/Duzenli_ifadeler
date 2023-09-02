# Düzenli İfadeler (Regular Expressions - Regex )

Düzenli İfadeler (Regular Expressions) konusunu farklı kaynaklardan okuyup inceleyerek öğrenmeye çalışıyor ve öğrendiklerimi repoma ekleyerek paylaşıyorum. 

İlerleyen zamanlarda Düzenli İfadelere ait Türkçe içerikli Özet Tablo (Cheat Sheet) hazırlamayı ve belirlediğimiz özelliklere göre Düzenli ifade yapılarını oluşturan python kodu / programı yazıp paylaşmayı düşünüyorum.

### Düzenli İfadeler (Regular Expressions) Nedir ?

> Düzenli ifadeler (Regular Expressions, kısaca "Regex" ya da "Regexp"), Python programlama dilinin en çetrefilli konularından biridir. Ama bütün zorluklarına rağmen programlama deneyimimizin bir noktasında mutlaka karşımıza çıkacak olan bu yapıyı öğrenmemizde büyük fayda var. Düzenli ifadeleri öğrendikten sonra, elle yapılması saatler sürecek bir işlemi saliseler içinde yapabildiğinizi gördüğünüzde eminim düzenli ifadelerin ne büyük bir nimet olduğunu siz de anlayacaksınız. 

> Peki, düzenli ifadeleri kullanarak neler yapabiliriz? Çok genel bir ifadeyle, bu yapıyı kullanarak metinleri veya karakter dizilerini parmağımızda oynatabiliriz. Örneğin bir web sitesinde dağınık halde duran verileri bir çırpıda ayıklayabiliriz. Bu veriler, mesela, toplu halde görmek istediğimiz web adreslerinin bir listesi olabilir. Bunun dışında, örneğin, çok sayıda belge üzerinde tek adımda istediğimiz değişiklikleri yapabiliriz.

> Ancak genel bir kural olarak, düzenli ifadelerden kaçabildiğimiz müddetçe kaçmamız gerekir. Eğer Python’daki karakter dizisi metotları, o anda yapmak istediğimiz şey için yeterli geliyorsa mutlaka o metotları kullanmalıyız. Çünkü karakter dizisi metotları, düzenli ifadelere kıyasla hem daha basit, hem de çok daha hızlıdır. Ama bir noktadan sonra karakter dizilerini kullanarak yazdığınız kodlar iyice karmaşıklaşmaya başlamışsa, kodların her tarafı if deyimleriyle dolmuşsa, hatta basit bir işlemi gerçekleştirmek için yazdığınız kod sayfa sınırlarını zorlamaya başlamışsa, işte o noktada artık düzenli ifadelerin dünyasına adım atmanız gerekiyor olabilir. 
> 
> Kaynak: [Düzenli İfadeler - Yazbel Python Belgeleri](https://python-istihza.yazbel.com/standart_moduller/regex.html)

# Konu Başlıkları

1. [Düzenli İfadeler](duzenli_ifadeler.md)
   
   * [match() Metodu](duzenli_ifadeler.md#match() Metodu) 
   * [search() Metodu](duzenli_ifadeler.md##search() Metodu)
   * findall() Metodu

2. [MetaKarakterler](metakarakterler.md)
   
   * "[ ]" Köşeli Parantez
   
   * "." Nokta
   
   * "*" Yıldız
   
   * "+" Artı
   
   * "?" Soru İşareti
   
   * "{ }" Küme Parantezi
   
   * "^" Şapka
   
   ![regex](img/regex.png)