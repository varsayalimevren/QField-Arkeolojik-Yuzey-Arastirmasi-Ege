# QField Arkeolojik Yüzey Araştırması Şablonu – Ege Bölgesi ve İstanbul Uyarlaması

QGIS ve QField ile arkeolojik yüzey araştırması (pedestrian reconnaissance) verisi toplamak için hazırlanmış, ücretsiz ve açık kaynaklı proje şablonunun **Ege Bölgesi ve İstanbul çevresi** için uyarlanmış halidir.

> ## Atıf
> Bu çalışma, **Devin B. Pettigrew**'un
> [QField-Archaeological-Field-Mapping](https://github.com/dpettig/QField-Archaeological-Field-Mapping)
> projesine dayanmaktadır ve onun MIT Lisansı kapsamında uyarlanmıştır.
> Şablonun tüm özgün tasarımı ve emeği Pettigrew'a aittir. Lütfen bu şablonu kullanırken veya uyarlarken ona atıf yapın.
> Çalışma, deneme amaçlı bir demo olarak yapılmış olup, kullanıma hazır olup olmadığı kontrol edilmelidir. Garanti verilmez. 

> ## ⚠️ Güncellik Notu
> Bu depodaki dosyalar **güncel olmayabilir**. Orijinal şablon geliştirilmeye devam etmekte olup yeni QGIS/QField sürümleriyle uyum sorunları ortaya çıkabilir.
> **Güncellenmiş bir sürüme ihtiyaç duyarsanız** aşağıdaki [İletişim](#iletişim) bölümünden bize ulaşabilirsiniz.
> Her zaman en güncel orijinal şablon için [Pettigrew'un deposuna](https://github.com/dpettig/QField-Archaeological-Field-Mapping) da bakmanızı öneririz.

---

## Bu uyarlamada neler değişti?

- Proje, **Ege Bölgesi ve İstanbul çevresini** kapsayacak şekilde yapılandırıldı.
- Proje koordinat sistemi yerel kullanıma uygun olarak ayarlandı (test projesinde EPSG:32635 kullanıldı; kendi çalışma alanınıza göre değiştirmeniz gerekebilir).
- Altlık harita olarak OpenTopoMap kullanıldı.
- Kullanım adımları Türkçeye çevrildi.



## Şablonun Özellikleri

- Nokta, çizgi ve poligon katmanları; artefakt, datum, özellik gibi sınıflar için benzersiz semboller
- Her cihaz ve kayıt sınıfı için **otomatik saha numarası (fn)**
- Bir `site_boundary` poligonunun içinde kalan veya onunla kesişen kayıtlara otomatik **site kodu (site_fn)**
- Uygulama içinden çekilen fotoğrafların her kayda bağlı alt kayıt olarak saklanması
- Artefakt sayımları, bileşen ve ortam açıklamaları içeren site formları
- QR kod okuyucu ile örnek etiketlerinin hızlı kaydı
- İsteğe bağlı Bluetooth GPS alıcısı ile daha yüksek konum doğruluğu
- Uzun notlar için sesten yazıya çeviri uygulamalarıyla (ör. FUTO Voice) dikte imkânı

## Gereksinimler

- [QGIS](https://qgis.org) — orijinal şablon **QGIS 3.44.9** için paketlenmiştir. Hata almamak için aynı sürümü kullanmanız önerilir.
- [QField](https://qfield.org) (Android/iOS)
- (İsteğe bağlı) [QFieldCloud](https://qfield.cloud) hesabı
- (İsteğe bağlı) Bluetooth GPS alıcısı

## Kurulum ve Kullanım

> Aşağıdaki adımlar QFieldCloud kullanımına göredir. Kablo ile aktarım için QField belgelerine bakın; bu durumda 5. ve 6. adımlar değişir ve çevrimdışı harita dosyalarını her projeye eklemeniz gerekir.

**Cihazın ilk kurulumu (bir kez):**
QField'da *Ayarlar → Değişkenler* bölümüne gidin ve yeni bir değişken ekleyin. Adı tam olarak `device_id` olsun, değer olarak cihazınıza bir kimlik verin. Otomatik saha numarası bu kimliğin **ilk karakteriyle** başlar. Bu yüzden projede kullanılan her cihazın kimliği farklı bir karakterle başlamalıdır (ör. `D` ile başlayan cihazda ilk artefakt `D_ART001` olur).

**Proje oluşturma:**
1. `ProjectTemplate` klasörünü bilgisayarınıza indirin (içinde bir `.gpkg` dosyası ve boş bir `DCIM` klasörü bulunur). Klasörü kopyalayıp her yeni proje için yeniden adlandırın.
2. QGIS'te Tarayıcı panelinde *GeoPackage* altından yeni proje klasöründeki `ArchFieldMapping.gpkg` dosyasına bağlanın ve `ProjectTemplate`'i geopackage içinden açın.
3. *Proje Özellikleri*'nde projeye bir ad verin.
4. Proje CRS'sini çalışma alanınıza uygun yerel bir CRS ile değiştirin. Ardından nokta, çizgi ve poligon katmanlarının CRS'sini de proje CRS'sine eşitleyin.
5. Arazide internet olmayacaksa QGIS'te *Generate XYZ Tiles (MBTiles)* ile bir harita oluşturup QGIS katmanlarına ekleyin ve cihazınızda `/Android/data/ch.opengis.qfield/files/QField/basemaps` klasörüne kopyalayın. Ayrıntılar için [bu tartışmaya](https://github.com/opengisch/QField/discussions/5942#discussioncomment-11834073) bakın.
6. QFieldCloud eklentisiyle bulut projesini oluşturun. Bundan sonra `ProjectTemplate` değil, oluşturulan bulut `.qgz` dosyası üzerinde çalışırsınız.

Artık projeyi mobil cihazınızda açıp haritalamaya başlayabilirsiniz. Yeni bir proje için 2–6. adımları tekrarlayın.

**Saha sonrası:**
Veriler QGIS'e senkronize edildikten sonra katmanların öznitelik tablolarından kopyalanabilir. Artefakt türü gibi sınıflandırmaları değiştirmek için şablonda ilgili tip alanlarına (`art_type`, `dat_type` vb.) yeni `.csv` dosyaları yükleyebilirsiniz. Mevcut `.csv` dosyaları `Class Types.zip` içindedir.

## Veri Gizliliği Uyarısı

Bu depoda **gerçek arkeolojik alan koordinatı yer almaz**; yalnızca boş şablon ve örnek test kaydı bulunur. Koruma altındaki alanların konumlarını herkese açık biçimde paylaşmak yağma riski taşır ve bazı ülkelerde yasal sorun doğurabilir. Kendi projelerinizin verilerini bu depoya yüklemeyin.

## İletişim

Güncellenmiş sürüm, soru, geri bildirim veya uyarlama talepleri için:

- **E-posta:** [evren200435@gmail.com]


Şablonun özgün geliştiricisi için: [github.com/dpettig](https://github.com/dpettig)

## Lisans

Bu proje **MIT Lisansı** ile dağıtılmaktadır. Lisans metni için [LICENSE](LICENSE) dosyasına bakın.
Özgün çalışmanın telif hakkı Devin B. Pettigrew'a aittir; lisans dosyasındaki telif satırı değiştirilmeden korunmalıdır.

## Sorumluluk Reddi

Bu şablon "olduğu gibi" sunulmaktadır ve herhangi bir garanti verilmez. Saha çalışmalarında veri kaybına karşı düzenli yedek almanızı öneririz.
