# dym

# Kullanıcı Etkileşimine Dayalı, Güvenlik Odaklı Otonom Domain Doğrulama Ve Yönlendirme

**[span_0](start_span)Proje Ana Alanı:** Yazılım[span_0](end_span)  
**[span_1](start_span)Proje Tematik Alanı:** Algoritma Tasarımı ve Uygulamaları[span_1](end_span)

---

## 1. Özet
[span_2](start_span)[span_3](start_span)İnternet kullanıcılarının web adreslerini (URL) hatalı yazması (Typosquatting), ciddi bir risk oluşturmaktadır[span_2](end_span)[span_3](end_span). [span_4](start_span)Mevcut sistemler statik listelerle sınırlı kalırken veya zararlı siteleri öğrenme riski taşırken, bu proje otonom öğrenme yeteneğine sahip bir çözüm sunar[span_4](end_span). [span_5](start_span)Sistem, Levenshtein Mesafesi temelli benzerlik algoritması kullanır ve yerel eşleşme yoksa Google API üzerinden öğrenme sürecini başlatır[span_5](end_span). [span_6](start_span)Özgünlüğü, domainin güvenlik katsayısını (TLD, Subdomain) değerlendiren Ağırlıklı Puanlama Algoritması kullanmasıdır[span_6](end_span).

## 2. Amaç
* **[span_7](start_span)Güvenlik Odaklı Karar Mekanizması:** Domainleri popülarite yerine TLD ve subdomain yapısı gibi kriterlere göre filtreleyerek phishing riskini minimize etmek[span_7](end_span).
* **[span_8](start_span)Otonom ve Adaptif Öğrenme:** Kullanıcı etkileşimleri sayesinde veritabanını (domains.json) sürekli güncelleyerek internet ortamına adapte olmak[span_8](end_span).
* **[span_9](start_span)Optimum Performans:** API kullanımını kısıtlayarak maliyeti düşürmek ve Flask tabanlı platform bağımsız bir servis sunmak[span_9](end_span).

## 3. Giriş
[span_10](start_span)Typosquatting saldırıları, kullanıcılar için en büyük siber tehditlerden biridir[span_10](end_span). [span_11](start_span)Literatürde metin benzerlik algoritmaları (Levenshtein) standart kabul edilse de[span_11](end_span)[span_12](start_span)[span_13](start_span), sadece kelime benzerliğine odaklanılması ve TLD güvenilirliğinin göz ardı edilmesi bir eksikliktir[span_12](end_span)[span_13](end_span). [span_14](start_span)Bu proje, otonom ve hafif bir mimari ile bu boşluğu doldurmayı hedefler[span_14](end_span).

## 4. Yöntem
[span_15](start_span)Projede Deneysel Yazılım Geliştirme Metodolojisi kullanılmıştır[span_15](end_span). 

* **[span_16](start_span)Teknik Altyapı:** Python ve Flask üzerine inşa edilen sistem, dinamik JSON yapılarını kullanır[span_16](end_span). 
* **[span_17](start_span)Veri Kaynağı:** Yerelde bulunmayan sorgular için Google Custom Search API ile gerçek zamanlı öğrenme sağlanır[span_17](end_span).
* **[span_18](start_span)Algoritmalar:** * **Levenshtein Mesafesi:** Fuzzywuzzy kütüphanesi ile Ana Liste için %50, Öğrenme Listesi için %40 eşik değeri belirlenmiştir[span_18](end_span).
    * **[span_19](start_span)Ağırlıklı Puanlama Algoritması:** TLD puanı (.edu, .gov +2; .com, .org +1), subdomain kontrolü (-1) ve kullanıcı teyidi (5 sorgu tetikleyicisi) kriterlerini içerir[span_19](end_span).

## 5. Proje İş-Zaman Çizelgesi
| İşin Adı | Nisan-Eylül | Ekim | Kasım | Aralık | Ocak |
| :--- | :---: | :---: | :---: | :---: | :---: |
| Literatür Taraması | | [span_20](start_span)X | X[span_20](end_span) | | |
| Arazi Çalışması | | [span_21](start_span)X | | | |
| Veri Analizi | X[span_21](end_span) | [span_22](start_span)X | X[span_22](end_span) | [span_23](start_span)X | |
| Proje Raporu Yazımı | | | | X[span_23](end_span) | |

## 6. Bulgular
### Benzerlik Eşiği Analizi
[span_24](start_span)200 adet yazım hatası senaryosu ile yapılan testlerde yüksek başarı oranları elde edilmiştir[span_24](end_span):
* **[span_25](start_span)YouTube:** %99.00 başarı[span_25](end_span).
* **[span_26](start_span)Facebook:** %98.00 başarı[span_26](end_span).

### Otonom Öğrenme
[span_27](start_span)[span_28](start_span)Sistem, bir domaini ilk kez Google API ile sorguladıktan sonra, 6. sorgu itibarıyla dış API bağımlılığını %0'a indirmiştir[span_27](end_span)[span_28](end_span). [span_29](start_span)[span_30](start_span)Bu, akıllı önbellekleme sayesinde kaynak verimliliği sağlamaktadır[span_29](end_span)[span_30](end_span).

## 7. Sonuç ve Tartışma
[span_31](start_span)Geliştirilen sistem, Levenshtein benzerlik eşiği testlerinde %98'in üzerinde başarı sergilemiştir[span_31](end_span). [span_32](start_span)TLD ve alt alan adı kontrollerinin sürece dahil edilmesi doğruluğu maksimize etmiştir[span_32](end_span). [span_33](start_span)Sistemin 6. sorguda dış bağlantıyı kesmesi, siber güvenlik araçlarındaki gecikme süresi (latency) sorununa hafif siklet bir çözüm sunmuştur[span_33](end_span).

## 8. Öneriler
* **[span_34](start_span)Eklenti Dönüşümü:** Sistemin bir Web Tarayıcı Eklentisi haline getirilerek phishing saldırılarının anlık engellenmesi[span_34](end_span).
* **[span_35](start_span)Derin Öğrenme:** Gelecek çalışmalarda LSTM veya BERT gibi modellerle anlamsal sahtecilik analizlerinin yapılması[span_35](end_span).

---
**[span_36](start_span)Kaynaklar:**[span_36](end_span)
**[span_37](start_span)Ekler:** https://gist.github.com/Berlinxr/00716c94a64a7ceeb5998080c832660d[span_37](end_span)
