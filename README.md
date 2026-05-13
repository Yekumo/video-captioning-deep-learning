# 🎬 Akıllı Video Analiz ve Özetleme Sistemi (Video Captioning & Summarization)

Bu proje, görüntü işleme ve doğal dil işleme (NLP) teknolojilerini kullanarak videoları otomatik olarak analiz eden ve içeriklerini mantıklı bir metin özeti haline getiren uçtan uca bir sistemdir. Google Colab ortamında, donanım kısıtları (RAM/VRAM) optimize edilerek tasarlanmıştır.

## 🚀 Özellikler

* **Akıllı Sahne Tespiti (OpenCV):** Sabit aralıklarla değil, pikseller arası fark analizi (`cv2.absdiff`) yöntemiyle sadece sahnede ani değişim (hareket/kamera açısı) olduğunda kare yakalar.
* **Karanlık Ekran Filtresi:** Hatalı analizleri önlemek için parlaklık ortalaması çok düşük olan siyah/boş geçiş sahnelerini algılar ve yoksayar.
* **Görüntü Anlamlandırma (BLIP):** Yakalanan karelere netleştirme filtresi (sharpening) uygulanarak Salesforce'un `BLIP-base` modeline gönderilir ve her kare için İngilizce açıklamalar (caption) üretilir.
* **Akıllı Metin Filtreleme (NLP):** * `SequenceMatcher` ile birbirine %50'den fazla benzeyen tekrarlı sahneler elenir.
* **Frekans Bazlı Skorlama (Term Frequency):** Bağlaçlar atıldıktan sonra kelime popülerliklerine göre cümleler puanlanır ve videonun ana temasıyla alakasız (outlier) halüsinasyonlar çöpe atılır.
* **Bağlamsal Özetleme (BART):** Temizlenmiş ve skoru yüksek saf cümleler, `BART-large-cnn` modeline verilerek tek bir akıcı olay örgüsü haline getirilir ve Google Translator API ile Türkçeye çevrilir.

## 🛠️ Kullanılan Teknolojiler

* **Computer Vision:** OpenCV (cv2), Pillow (PIL)
* **Deep Learning Framework:** PyTorch
* **Transformers (Hugging Face):** * `Salesforce/blip-image-captioning-base` (Görüntü İşleme)
  * `facebook/bart-large-cnn` (Metin Özetleme)
* **Yardımcı Araçlar:** `yt-dlp` (Video indirme), `deep-translator`, `difflib`

## ⚙️ Kurulum ve Kullanım

1) Bu projeyi bir Google Colab ortamında açın (GPU T4 hızlandırıcısı önerilir).
2) 1. Hücreyi çalıştırarak gerekli kütüphaneleri (`transformers`, `opencv-python-headless`, vb.) ve modelleri yükleyin.(Biraz zaman alabilir.)
3) 2. Hücreden MSR-VTT veri setinden rastgele bir video çekin.(Hücre çalıştığında otomatik video çekecektir.)
4) 3. Hücre ile sistemden çektiğiniz videoyu izleyebilirsiniz.(Opsiyonel)
5) 4. Hücreyi çalıştırarak sahne analizi, skorlama ve özetleme işlemini başlatın.
6) 5. Hücre ile çıktıyı türkçe olarak görebilirsiniz.(Opsiyonel)

## 👨‍💻 Geliştirici
**İbrahim Taha Özcan**
