Akbank Makine Öğrenmesi Bootcamp: Kalp Hastalığı Risk Tahmini Projesi
1. Proje Hakkında
Bu proje, Akbank Makine Öğrenmesi Bootcamp kapsamında gerçekleştirilen, gözetimli öğrenme teknikleriyle bir sınıflandırma problemi çözmeyi amaçlayan bir çalışmadır. Temel amaç, bireylerin çeşitli tıbbi ve demografik özelliklerine dayanarak kardiyovasküler (kalp) hastalığı riskini tahmin eden bir makine öğrenimi modeli geliştirmektir. Bu proje, veri analizi, model geliştirme ve değerlendirme konularında pratik deneyim kazanmayı hedeflemektedir.


2. Kullanılan Veri Seti
Projede, Kaggle platformundan elde edilen "Cardiovascular Disease dataset" kullanılmıştır.

Veri Seti Linki: Cardiovascular Disease dataset
Veri Boyutu: Yaklaşık 70.000 veri noktası içermektedir. Bu, projenin belirlenen minimum 10.000 veri noktası kriterini fazlasıyla karşılamaktadır.
Özellikler: Veri seti; yaş, cinsiyet, boy, kilo, kan basıncı (sistolik ve diyastolik), kolesterol seviyesi, glikoz seviyesi, sigara kullanımı, alkol kullanımı, fiziksel aktivite ve hedef değişken olan kalp hastalığı varlığı (cardio) gibi özellikleri barındırmaktadır.
3. Geliştirme Ortamı ve Araçlar
Proje geliştirme sürecinde Kaggle Notebook ortamı kullanılmıştır.

IDE/Platform: Kaggle Notebook (Python tabanlı).
Kütüphaneler: pandas (veri manipülasyonu için), numpy (sayısal işlemler için), matplotlib ve seaborn (veri görselleştirme için), scikit-learn (makine öğrenimi algoritmaları ve ön işleme için).
4. Proje Adımları ve Metodoloji
Proje, aşağıdaki adımları takip ederek uçtan uca bir makine öğrenimi yaşam döngüsünü içermektedir:

4.1. Keşifsel Veri Analizi (EDA) 
Veri setinin yapısını anlamak, eksik değerleri, aykırı değerleri ve özellikler arası ilişkileri tespit etmek amacıyla kapsamlı EDA yapılmıştır.

Ana Bulgular:
ap_hi (sistolik) ve ap_lo (diyastolik) kan basıncı sütunlarında fizyolojik olarak imkansız (negatif, aşırı yüksek) aykırı değerler tespit edilmiştir.
Boy ve kilo sütunlarında da bazı uç aykırı değerler gözlemlenmiştir.
Kolesterol ve glikoz seviyelerinin kalp hastalığı riskiyle pozitif ilişkisi olduğu, yaşın da kalp hastalığı riskini artırdığı gözlemlenmiştir.
Cinsiyet, sigara, alkol ve fiziksel aktivite gibi diğer özelliklerin kalp hastalığı ile doğrudan ilişkisi bu aşamada daha zayıf görünmüştür.
Hedef değişken (cardio) sınıflarının (0: Hastalık yok, 1: Hastalık var) yaklaşık olarak dengeli dağıldığı görülmüştür.
4.2. Veri Ön İşleme 
Ham verinin model eğitimine uygun hale getirilmesi için çeşitli ön işleme adımları uygulanmıştır.

Aykırı Değer Temizliği: Yaş, boy, kilo, sistolik ve diyastolik kan basıncı (ap_hi, ap_lo) sütunlarındaki mantıksız ve aşırı uç değerler, IQR (Interquartile Range) yöntemi ve fizyolojik kurallar (ap_hi > ap_lo gibi) kullanılarak temizlenmiştir. Bu temizlik sonrası veri seti boyutu 70.000'den 62.499'a düşmüştür.
Kategorik Değişken Dönüşümü: gender (cinsiyet) sütunu nominal bir değişken olduğu için One-Hot Encoding yöntemiyle dönüştürülmüştür. cholesterol ve gluc gibi sıralı (ordinal) kategorik değişkenler zaten sayısal değerler içerdiği için doğrudan kullanılmıştır.
Özellik Ölçeklendirme: Farklı ölçeklerdeki sayısal özellikler (age, height, weight, ap_hi, ap_lo), StandardScaler kullanılarak standartlaştırılmıştır (ortalama 0, standart sapma 1). Bu, modelin mesafe tabanlı hesaplamalarda baskın özelliklerden etkilenmesini önlemiştir.
Eğitim ve Test Kümelerine Bölme: Hazırlanan veri seti, modelin genelleme yeteneğini değerlendirmek amacıyla %80 eğitim ve %20 test kümelerine ayrılmıştır. stratify=y parametresi ile hedef değişken dağılımının her iki kümede de korunması sağlanmıştır.
4.3. Algoritma Seçimi ve Hiperparametre Optimizasyonu 
Kalp hastalığı tahmini için sınıflandırma algoritmaları değerlendirilmiş ve en iyi modelin hiperparametreleri optimize edilmiştir.

Deneme Yapılan Algoritmalar: Lojistik Regresyon, Karar Ağaçları, K-En Yakın Komşu (KNN) ve Destek Vektör Makineleri (SVM) gibi popüler sınıflandırma algoritmaları temel ayarlarla denenmiştir.
Çapraz Doğrulama: Modellerin genellenebilir performansını değerlendirmek için 5 katlı çapraz doğrulama uygulanmıştır.
Model Seçimi: Çapraz doğrulama sonuçlarına göre Lojistik Regresyon modeli, %72.43'lük ortalama doğruluk skoru ile en iyi performansı gösteren model olarak seçilmiştir.
Hiperparametre Optimizasyonu: Seçilen Lojistik Regresyon modelinin performansı, GridSearchCV kullanılarak optimize edilmiştir. C (regularizasyon gücü), penalty (regularizasyon tipi) ve solver (optimizasyon algoritması) hiperparametreleri için en iyi kombinasyon aranmıştır. En iyi parametreler {'C': 100, 'penalty': 'l1', 'solver': 'liblinear'} olarak bulunmuştur.
5. Model Değerlendirme 
Optimize edilmiş Lojistik Regresyon modelinin final performansı, test seti üzerinde çeşitli metrikler kullanılarak değerlendirilmiştir.

Performans Metrikleri:

Doğruluk (Accuracy): %71.85
Kesinlik (Precision): %74.44
Duyarlılık (Recall): %65.48
F1 Skoru (F1 Score): %69.68
Karışıklık Matrisi (Confusion Matrix): 

Doğru Negatifler (TN): 4938 (Modelin sağlıklı olarak doğru tahmin ettikleri) 
Yanlış Pozitifler (FP): 1388 (Modelin hasta olarak yanlış tahmin ettikleri sağlıklı kişiler) 
Yanlış Negatifler (FN): 2131 (Modelin sağlıklı olarak yanlış tahmin ettikleri hasta kişiler) 
Doğru Pozitifler (TP): 4043 (Modelin hasta olarak doğru tahmin ettikleri hasta kişiler) 
Python

# Karışıklık Matrisi Görseli (Eğer görseli README'ye ekleyecekseniz)
# ![Confusion Matrix for Optimized Logistic Regression](path/to/your/confusion_matrix_image.png)
Görseli eklemek için, Kaggle'dan indirip GitHub reponuza yükledikten sonra yukarıdaki gibi yolunu belirtmelisiniz.

Değerlendirme Özeti: Model, yaklaşık %72'lik bir doğrulukla makul bir performans sergilemektedir. Özellikle yüksek kesinlik değeri, modelin yaptığı pozitif teşhislerin (kalp hastalığı var) güvenilir olduğunu gösterirken, duyarlılık değeri (gerçek hastaları bulma oranı) iyileştirme potansiyeli taşımaktadır. Tıbbi uygulamalarda yanlış negatiflerin maliyeti yüksek olduğundan, bu alanın gelecekteki geliştirmelerde ele alınması önemlidir.

6. Sonuç ve Gelecek Geliştirmeler 
Bu proje, kardiyovasküler hastalık riskini tahmin etme konusunda veri bilimi süreçlerinin uçtan uca uygulanmasına dair kapsamlı bir deneyim sunmuştur. Elde edilen Lojistik Regresyon modeli, klinik uygulamalar için başlangıç seviyesinde bir öngörü aracı olarak potansiyel taşımaktadır.

Projeyi daha da geliştirmek ve model performansını artırmak için aşağıdaki adımlar düşünülebilir:

Daha Gelişmiş Modeller: Random Forest, Gradient Boosting (XGBoost/LightGBM) veya temel bir Yapay Sinir Ağı gibi daha karmaşık ensemble modelleri denemek.
Özellik Mühendisliği: Mevcut özelliklerden (boy, kilo, tansiyon) yeni anlamlı özellikler türetmek (örneğin: BMI hesaplama, tansiyon kategorileri oluşturma).
Sınıf Dengesizliği Yönetimi: Duyarlılığı artırmak ve yanlış negatifleri azaltmak için SMOTE (Synthetic Minority Over-sampling Technique) gibi aşırı örnekleme tekniklerini uygulamak.
Hiperparametre Optimizasyonu Genişletme: Daha geniş hiperparametre aralıkları veya RandomizedSearchCV gibi daha hızlı arama yöntemleriyle optimizasyonu derinleştirmek.
Model Yorumlanabilirliği: SHAP veya LIME gibi araçlarla modelin tahminlerinin nedenlerini anlamak ve hangi özelliklerin en etkili olduğunu belirlemek.
Model Dağıtımı (Deployment): Geliştirilen modeli bir web arayüzü (örn. Streamlit, Flask) üzerinden erişilebilir hale getirerek gerçek dünya uygulamalarına yaklaştırmak.
7. Kaggle Notebook ve GitHub Repo Linkleri
Kaggle Notebook: https://www.kaggle.com/code/irfanburakege/ml25-irfanburakege 
GitHub Repository: [Your GitHub Repo Link Here (Lütfen kendi GitHub repo linkinizi buraya ekleyin)] 
