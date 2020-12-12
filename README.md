# Ev Fiyat Tahmini

İnternette bulunan bir emlak danışmanlık sitesinden topladığımız veriler ışığında gerçekleştirdiğimiz ev fiyat tahmin modelimizi sizlere sunuyorum.

Modelimiz belirli özelliklere göre evin fiyatını yaklaşık olarak bulmaya çalışmaktadır. İlk veri setimizin özelliklerini sıralayacak olursak:

​	

* fiyat
* ilan no
* ilan oluşturulmak tarihi
* ilan güncellenme tarihi
* tür
* kategori
* yapı tipi
* net metrekare
* brüt metrekare
* salon metrekare
* oda sayısı
* bina yaşı
* bulunduğu kat
* bina kat sayısı
* ısıtma tipi
* aidat
* kira getisi
* banyo sayısı
* WC sayısı
* site içi bilgisi
* eşya durumu
* kullanım durumu
* fiyat durumu
* yapı durumu
* krediye uygunluk durumu
* yatırıma uygunluk durumu
* takas durumu



Topladığımız verilerin özelliklerine bakacak olursak '27' adet öznitelik ve 510 satır veri içermektedir. Teoride fazla öznitelik sayısı iyi bir durum gibi gözükse de aslında tam tersidir. Çok fazla öznitelik olması veri modelimizin performansını düşürmektedir. Bu nedenle bazı özniteliklerin veri setinden çıkarılması gerekmektedir. Çıkarılması gereken öznitelikleri aşağıdaki tabloda nedenleri ile birlikte gösterelim.



| Öznitelik Adı     |                          Durum                          |
| ----------------- | :-----------------------------------------------------: |
| ilan_no           |              Fiyat tahmini için anlamsız.               |
| olusturma_tarihi  |              Fiyat tahmini için anlamsız.               |
| guncelleme_tarihi |              Fiyat tahmini için anlamsız.               |
| tur               |     Özniteliğe ait tüm verilerin aynı olması(Konut)     |
| kategori          |    Özniteliğe ait tüm verilerin aynı olması(Satılık)    |
| yapi_tip          |    Bulunan verilerin büyük kısmının boş değer olması    |
| salon_m2          |    Bulunan verilerin büyük kısmının boş değer olması    |
| aidat             |    Bulunan verilerin büyük kısmının boş değer olması    |
| kira-getiri       |    Bulunan verilerin büyük kısmının boş değer olması    |
| WC_sayi           |    Bulunan verilerin büyük kısmının boş değer olması    |
| esya_durumu       |    Bulunan verilerin büyük kısmının boş değer olması    |
| kullanım_durum    |    Bulunan verilerin büyük kısmının boş değer olması    |
| fiyat_durum       |  Özniteliğe ait tüm verilerin aynı olması(Genel Fiyat)  |
| yapi_durum        |    Bulunan verilerin büyük kısmının boş değer olması    |
| krediye_uygunluk  | Özniteliğe ait tüm verilerin aynı olması(Krediye Uygun) |
| yatirima_uygunluk |    Bulunan verilerin büyük kısmının boş değer olması    |
| takas             |              Fiyat tahmini için anlamsız.               |



Bu öznitelikleri tablodan çıkardığımızda artık veri  önişleme işlemine başlanır.

> Normalde öznitelik seçim işlemi feature selection işlemi ile belirlenmektedir. sklearn kütüphanesinde bulunan feature_selection sınıfı ile
>
> özniteliklerin skoruna göre makine öğrenmesi modeline en uygun öznitelikler belirlenirken uygun olmayan öznitelikler çıkarılır.



#### Kullanılan Kütüphaneler



- [Pandas][https://pandas.pydata.org]
- [Numpy][https://numpy.org]
- [Matplotlib][https://matplotlib.org]
- [Sklearn][https://scikit-learn.org/stable/]
- [Seaborn][https://seaborn.pydata.org]
- [XGBOOST][https://xgboost.readthedocs.io/en/latest/]



Bu kütüphaneleri kullanarak veri seti oluşturulup xgboost kütüphanesi ile bir Makine Öğrenmesi modeli oluşturuldu.

Modele ait tahmin ve gerçek verilerin karşılaştırılmasını görüyoruz. Genel olarak bakıldığında tutarlı gözüksede yüksek değere sahip outlier değerler göze hemen çarpıyor. Bunlar için outlier-detected işleminin gerçekleştirilmesi gerekiyor. Bu işlem gerçekleştiğinde modelin tahmin katsayısı kesin olarak artacaktır.

![alt](https://i.hizliresim.com/2Pgp9F.png)

