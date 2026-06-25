# GTSRB - Trafik İşareti Sınıflandırma Sistemi 🚦 (CNN)

![Accuracy](https://img.shields.io/badge/Accuracy-99.96%25-success)
![F1-Score](https://img.shields.io/badge/F1_Score-99.96%25-success)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)

Bu proje, Alman Trafik İşaretleri (GTSRB) veri setini kullanarak 43 farklı trafik işaretini otomatik olarak tanımak ve sınıflandırmak için sıfırdan geliştirilmiş, yüksek performanslı bir Evrişimli Sinir Ağı (CNN) modelidir. 

Gerçekleştirilen derin öğrenme mimarisi tasarımı ve eğitim optimizasyonları sayesinde model, test verilerinde **%99.96** gibi olağanüstü bir doğruluk (accuracy) seviyesine ulaşmıştır.

## 🚀 Model Mimarisi ve Kullanılan Teknikler

Sistemin bu kadar yüksek bir başarı oranına ulaşması için aşağıdaki ileri düzey derin öğrenme teknikleri projeye entegre edilmiştir:

1. **Özel CNN Mimarisi:** Görüntülerden hiyerarşik özellikleri (kenarlar, şekiller, desenler) otomatik çıkarmak için 4 katmanlı (32, 64, 128, 256 filtre) evrişim ağı tasarlandı.
2. **Batch Normalization:** Ağırlıkların daha hızlı ve dengeli öğrenilmesi için (internal covariate shift problemini önlemek adına) her evrişim katmanından sonra uygulandı. Eğitimi ciddi oranda hızlandırdı.
3. **Data Augmentation (Veri Çoğaltma):** Modelin ezberlemesini (overfitting) önlemek ve genelleme yeteneğini artırmak için eğitim sırasında görüntülere rastgele döndürme (±15°), kaydırma ve yakınlaştırma (zoom) uygulandı.
4. **Erken Durdurma (Early Stopping):** Modelin performansı tepe noktasına ulaştıktan sonra ezberlemeye başlamasını engellemek için, doğrulama (validation) başarısı 10 epoch boyunca artmadığında eğitim otomatik olarak durdurulacak şekilde tasarlandı.
5. **Dinamik Öğrenme Hızı (Learning Rate Scheduling):** Eğitimin sonlarına doğru daha hassas ince ayar yapabilmek için, öğrenme tıkandığında öğrenme hızını yarıya düşüren `ReduceLROnPlateau` mekanizması kullanıldı.
6. **Güçlü Düzenlileştirme (Dropout):** Modele yüksek oranlı (%25 ve %50) Dropout katmanları eklenerek nöronların rastgele kapatılması sağlandı. Bu sayede modelin tek bir özelliğe bağımlılığı kırıldı ve çok daha sağlam (robust) bir yapı elde edildi.
7. **Normalizasyon:** Görüntü piksel değerleri (0-255) eğitim hızını maksimize etmek için 0-1 aralığına ölçeklendirildi.

## 📊 Performans Sonuçları

Model, kendisi için ayrılmış ve daha önce hiç görmediği %20'lik test veri setinde aşağıdaki sonuçları vermiştir:

| Metrik | Performans |
|--------|------------|
| **Doğruluk (Accuracy)** | **%99.96** |
| **F1-Score (Ağırlıklı)** | **%99.96** |

*Not: Accuracy ve F1-Score değerlerinin birebir aynı çıkması, modelin veri setindeki tüm 43 sınıfa karşı dengeli ve tarafsız bir şekilde, mükemmel performans gösterdiğini kanıtlamaktadır.*

## 📁 Proje Dosyaları
* `gelistirilmis_model.py`: Modelin mimarisini barındıran, eğitimi ve test işlemlerini yapan ana Python betiği.
* `gelistirilmis_model.ipynb`: Adım adım açıklamalı, hücre bazında çalıştırılabilir Jupyter Notebook versiyonu.

## 🛠️ Kurulum ve Çalıştırma

1. Gerekli kütüphaneleri yükleyin:
   ```bash
   pip install -r requirements.txt
   ```
2. Kaggle üzerinden [GTSRB Veri Setini](https://www.kaggle.com/datasets/meowmeowmeowmeowmeow/gtsrb-german-traffic-sign) indirin ve `Train/`, `Test/` klasörlerini projenin ana dizinine yerleştirin.
3. Modeli eğitin ve test edin:
   ```bash
   python gelistirilmis_model.py
   ```

*(Not: Veri seti boyutu büyük olduğu için görüntüler GitHub reposuna dahil edilmemiştir.)*
