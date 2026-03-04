# Explainable-Genomic-Variant-Classification
Bu proje, ClinVar veri setinden elde edilen genetik varyantların Makine Öğrenmesi yöntemleri kullanılarak Patogen (1) veya Benign (0) olarak sınıflandırılmasını amaçlamaktadır.
# Explainable ClinVar Varyant Sınıflandırma Projesi

## Proje Özeti

Bu proje, ClinVar veri setinden elde edilen genetik varyantların Makine Öğrenmesi yöntemleri kullanılarak Patogen (1) veya Benign (0) olarak sınıflandırılmasını amaçlamaktadır.

Çalışma kapsamında:

- Biyolojik olarak anlamlı feature engineering uygulanmıştır.
- XGBoost algoritması ile güçlü bir sınıflandırma modeli geliştirilmiştir.
- Model performansı çeşitli metriklerle değerlendirilmiştir.
- SHAP analizi ile modelin açıklanabilirliği sağlanmıştır.

Bu proje, genomik varyant sınıflandırmasında hem performans hem de yorumlanabilirlik odaklı bir yaklaşım sunmaktadır.

---

## Amaç

- ClinVar varyantlarını güvenilir biçimde sınıflandırmak
- Biyolojik bilgi içeren özellikler üretmek
- Gradient boosting tabanlı bir model geliştirmek
- Model kararlarını SHAP ile yorumlamak
- Akademik ve yarışma seviyesinde bir makine öğrenmesi pipeline’ı oluşturmak

---

## Veri Seti

Veri seti ClinVar kaynaklıdır ve yalnızca ikili etiket içeren varyantlar kullanılmıştır:

- 0 → Benign
- 1 → Patogen

Çelişkili yorum içeren varyantlar veri setinden çıkarılmıştır.

---

## Özellik Mühendisliği (Feature Engineering)

Model performansını artırmak amacıyla aşağıdaki özellikler oluşturulmuştur:

### Popülasyon Frekansı Özellikleri
- AF_ESP
- AF_EXAC
- AF_TGP
- maf_mean
- maf_log (−log10 dönüşümü uygulanmış minör allel frekansı)

### Fonksiyonel Etki Skorları
- CADD_PHRED
- SIFT_score
- PolyPhen_score
- BLOSUM62
- radical_change (aminoasit değişiminin negatif etkisini gösteren binary değişken)

### Kategorik Değişken Kodlama
- IMPACT_encoded (Label Encoding uygulanmıştır)

Eksik değerler median imputation yöntemi ile doldurulmuştur.

---

## Model

Kullanılan algoritma:

XGBoost Classifier

Model parametreleri:

- n_estimators = 300
- max_depth = 4
- learning_rate = 0.05
- subsample = 0.8
- colsample_bytree = 0.8
- random_state = 42

Veri seti stratified train-test split yöntemi ile %80 eğitim, %20 test olarak ayrılmıştır.

---

## Değerlendirme Metrikleri

Model performansı aşağıdaki metriklerle değerlendirilmiştir:

- Classification Report (Precision, Recall, F1-score)
- ROC-AUC Skoru
- F1 Skoru

Bu metrikler, özellikle dengesiz veri senaryolarında güvenilir performans ölçümü sağlamak amacıyla tercih edilmiştir.

---

## Model Açıklanabilirliği

SHAP (SHapley Additive exPlanations) yöntemi kullanılarak:

- Global feature importance analizi yapılmıştır
- Tekil tahminlerin hangi özelliklerden etkilendiği incelenmiştir
- Biyolojik anlamlılık değerlendirilmiştir

Bu sayede model yalnızca yüksek doğruluk değil, aynı zamanda yorumlanabilirlik de sunmaktadır.

---

