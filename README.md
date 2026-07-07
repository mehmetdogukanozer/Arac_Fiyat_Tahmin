# 🚗 Sentetik Araç Veri Seti ile Uçtan Uca Veri Ön İşleme ve Regresyon Modeli

Bu proje, staj öncesi pratik kazanmak, veri ön işleme (data preprocessing) kaslarını geliştirmek ve ham bir veri setini temizleyerek makine öğrenmesi modeline hazır hale getirmek amacıyla geliştirilmiş bir **baseline (taban) model** çalışmasıdır.

## 📊 Proje İş Akışı (Pipeline)
Proje süresince bir veri bilimcinin izlediği standart adımlar sırasıyla uygulanmıştır:
1. **Veri Keşfi (EDA):** Veri setinin yapısal özellikleri (`info()`, `describe()`) incelenmiş, yapısal problemler tespit edilmiştir.
2. **Millileştirme ve Dönüşüm:** Sütun isimleri Türkçeleştirilmiş; mil cinsinden verilen araç mesafeleri, vektörize işlemler (broadcasting) kullanılarak kilometereye çevrilmiş ve yuvarlanmıştır.
3. **Veri Temizliği:** Veri setinde yer alan ve tamamen boş (NaN) bırakılan 250 satır `dropna()` ile kalıcı olarak temizlenmiştir.
4. **Korelasyon Analizi:** Sayısal özniteliklerin birbirleriyle olan ilişkileri Seaborn kütüphanesi kullanılarak bir Isı Haritası (Heatmap) ile görselleştirilmiştir.
5. **Kategorik Veri Dönüştürme:** Metinsel veriler (`Marka`, `Vites` vb.), Kukla Değişken Tuzağından (Dummy Variable Trap) kaçınmak adına `drop_first=True` parametresi kullanılarak **One-Hot Encoding** yöntemiyle sayısallaştırılmıştır.
6. **Model Eğitimi:** Veri %80 eğitim, %20 test olarak bölünmüş ve `Scikit-learn` kütüphanesi ile **Linear Regression** algoritması eğitilmiştir.

## 🚨 ÖNEMLİ NOT: Model Performansı ve Veri Analizi
Modelin test verileri üzerindeki başarı metrikleri şu şekildedir:
* **R2 Skoru:** 0.0018
* **MAE (Ortalama Mutlak Hata):** 23400.89

### 🧠 Mühendislik Değerlendirmesi (Neden R2 Düşük?)
Kod mimarisi, veri temizliği ve modelleme adımları tamamen doğru olmasına rağmen R2 skorunun sıfıra çok yakın çıkması **veri setinin karakteristiğinden** kaynaklanmaktadır. 
Kullanılan Kaggle veri seti gerçek hayattan toplanmamış, **bilgisayar tarafından rastgele (sentetik) üretilmiştir.** Öznitelikler (Yıl, Kilometre, Yakıt vb.) ile hedef değişken (Fiyat) arasında doğrusal hiçbir matematiksel bağ bulunmamaktadır (Yazılım dilinde **Pure Noise / Saf Gürültü** durumu). 

Bu proje, model başarısını maksimize etmekten ziyade, **gerçek bir veri ön işleme ve modelleme hattı (pipeline) inşa etmek** amacıyla tamamlanmıştır.