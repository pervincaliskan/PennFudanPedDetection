# Penn-Fudan Pedestrian Detection Projesi

Bu depo, PyTorch ve TorchVision kütüphaneleri kullanılarak Penn-Fudan Pedestrian Detection veri seti üzerinde eğitilmiş bir nesne algılama (object detection) modelini içermektedir. Projenin temel amacı, görüntülerdeki yayaları (insanları) tespit etmek ve konumlarını belirlemektir.

## Projenin Kapsamı

Bu proje aşağıdaki adımları kapsamaktadır:

1.  **Ortam Kurulumu:** Gerekli Python kütüphanelerinin (torch, torchvision, matplotlib, scikit-learn) kurulumu.
2.  **Veri Seti İndirme ve Hazırlık:**
    *   Penn-Fudan Pedestrian Detection veri setinin indirilmesi ve çıkarılması.
    *   Özel bir PyTorch `Dataset` sınıfı (`PennFudanDataset`) oluşturularak, veri setindeki görüntüler ve ilgili maske/kutucuk (bounding box) bilgileri yüklenir ve işlenir.
    *   Veri seti, eğitim, doğrulama (validation) ve test setlerine rastgele olarak bölünür.
    *   DataLoader'lar kullanılarak veri setleri toplu (batch) işleme için hazırlanır.
3.  **Model Tanımlama:**
    *   TorchVision kütüphanesindeki önceden eğitilmiş (pretrained) Faster R-CNN modelinin (fasterrcnn\_resnet50\_fpn) kullanılması.
    *   Modelin son katmanı, veri setindeki sınıf sayısına (insan ve arka plan olmak üzere 2 sınıf) uygun şekilde yeniden yapılandırılır.
4.  **Model Eğitimi:**
    *   Model, belirlenen cihazda (GPU veya CPU) eğitime hazır hale getirilir.
    *   SGD optimizasyon algoritması ve adım tabanlı öğrenme oranı çizelgeleyici (StepLR) kullanılır.
    *   Özel bir `train_one_epoch` fonksiyonu ile modelin tek bir epok (epoch) boyunca eğitimi gerçekleştirilir.
    *   Belirlenen sayıda epok boyunca eğitim döngüsü çalıştırılır ve her epok sonunda eğitim kaybı (loss) izlenir.
5.  **Eğitim Kaybı Görselleştirmesi:** Eğitim süresince hesaplanan kayıp değerleri bir grafik üzerinde gösterilir.
6.  **Test ve Görselleştirme:**
    *   Eğitim sonrası modelin performansı rastgele seçilen test görüntüleri üzerinde test edilir.
    *   Modelin tahmin ettiği sınırlayıcı kutucuklar (bounding boxes) ve güven skorları (confidence scores) görüntüler üzerinde görselleştirilir. Özellikle belirli bir güven skorunun üzerindeki "person" (insan) tahminleri gösterilir.

## Nasıl Çalıştırılır

Bu projenin kodunu çalıştırmak için Google Colab gibi bir ortamı kullanmanız tavsiye edilir.

1.  Bu depoyu bilgisayarınıza klonlayın veya dosyaları indirin.
2.  Ana Python notebook dosyasını (genellikle `.ipynb` uzantılı) Google Colab'a yükleyin.
3.  Notebook'taki hücreleri sırasıyla çalıştırın. İlk hücreler gerekli kütüphaneleri kuracak ve veri setini indirecektir.
4.  Model eğitim hücresini çalıştırarak modeli eğitin. Bu işlem kullanılan donanıma göre biraz zaman alabilir.
5.  Son hücreyi çalıştırarak test örnekleri üzerindeki tahminleri görselleştirin.

## Gereksinimler

*   Python 3.x
*   PyTorch
*   TorchVision
*   Matplotlib
*   Scikit-learn
*   PIL (Pillow)
*   NumPy

Bu kütüphaneler genellikle Colab ortamında mevcuttur veya notebook'un başındaki `!pip install` komutları ile kurulabilir.

## Veri Seti

Kullanılan veri seti Penn-Fudan Pedestrian Detection veri setidir. Bu veri seti hakkında daha fazla bilgi için [veri setinin orijinal web sitesi](https://www.cis.upenn.edu/~jshi/ped_html/) ziyaret edilebilir. (Not: Bağlantı, projenin indirme komutunda kullanılmıştır.)

