# Flutter Mini Katalog Projesi — Yol Haritası ve Teslim Şablonu

Bu belge, [proje yönergesindeki PDF](<Proje_Yönergesi/Mobil Uygulama Geliştirme; Android _ iOS Proje Yönergesi.pdf>) esas alınarak hazırlanmıştır.

> **Kısaca istenen:** Flutter ile çalışan, ürünleri listeleyen küçük bir katalog uygulaması yap; ürün detayına sayfalar arası veri taşıyarak git; `GridView` ile kartlı görünüm oluştur; sepette basit bir durum güncellemesi göster. Projeyi herkese açık GitHub deposunda, çalışan hali ve istenen README bilgileriyle teslim et.

## 1. Yönergedeki zorunluluklar

- [ ] Proje Flutter ve Dart ile geliştirilmeli; geliştirme ortamında Flutter SDK, Dart SDK, VS Code ve Android Studio/emülatör kullanılmalı.
- [ ] Proje Android emülatöründe veya fiziksel Android cihazda çalıştırılmalı.
- [ ] Temel Flutter/Material bileşenleri kullanılmalı; yönerge kapsamı dışında **ek paket eklenmemeli**.
- [ ] Çalışan bir **Mini Katalog Uygulaması** hazırlanmalı.
- [ ] Ana sayfa, ürün listesi ve ürün detay ekranı bulunmalı.
- [ ] Ekranlar arası geçiş yapılmalı ve ürün bilgisi `Route Arguments` ile detay ekranına aktarılmalı.
- [ ] Ürünler `GridView` ve kart tabanlı bir tasarımla gösterilmeli.
- [ ] Sepet butonuyla basit bir state güncellemesi yapılmalı; gerçek ödeme/sepet altyapısı beklenmiyor.
- [ ] Proje klasör yapısı ve asset yönetimi doğru kullanılmalı; görseller ve JSON dosyaları düzenli tutulmalı.
- [ ] GitHub deposu **public** olmalı ve proje çalışır durumda bulunmalı.
- [ ] Depoda bir `README.md` olmalı. README şu bilgileri içermeli:
  - Proje adı
  - Kısa açıklama
  - Kullanılan Flutter sürümü
  - Çalıştırma adımları
- [ ] Uygulamaya ait ekran görüntüleri GitHub deposuna eklenmeli.

> **Teslim uyarısı:** Yönergeye göre GitHub deposunun URL’si olmayan veya ekran görüntüleri eksik olan projeler teslim edilmiş sayılmayacak.

## 2. Yönergede anlatılanlar ve ek özelliklerin farkı

### Eğitimde gösterilen, projede kullanılması beklenen temel konular

- Widget ağacı ve `BuildContext`
- `StatelessWidget` / `StatefulWidget`
- Dart değişkenleri, fonksiyonlar, koleksiyonlar ve null safety
- `Row`, `Column`, `Container`, `Padding`, `Expanded`, `Card`, `ListTile`, butonlar
- `Navigator`, `MaterialPageRoute` ve sayfalar arasında argüman taşıma
- JSON modeli, `fromJson` / `toJson` mantığı ve `ListView.builder`
- Asset görsel kullanımı
- Basit arama/filtreleme mantığı

### Zorunlu olmayanlar

- Gerçek ödeme, kullanıcı hesabı, backend veya veritabanı
- Canlı API’den veri çekme
- Arama/filtreleme (eğitim içeriğinde anlatılıyor; teslim çıktıları arasında açık zorunluluk olarak sayılmıyor)
- iOS cihazında çalıştırma veya App Store’a yayınlama
- Animasyon, gelişmiş state management ya da üçüncü taraf paketler

PDF’de WantAPI banner ve ürün adresleri eğitim/demo kaynağı olarak verilmiş; Fake Store API ve DummyJSON ise **opsiyonel test API’leri** olarak belirtilmiş. Bu adresler gerçek e-ticaret altyapısı olarak sunulmuyor. Paket kısıtını ve uygulamanın çevrimdışı çalışmasını korumak için başlangıçta yerel JSON ve asset kullan; canlı API’yi ancak eğitmenin beklentisi netleşirse ve ek paket kuralı ihlal edilmeyecekse düşün.

## 3. Adım adım uygulama planı

### Aşama 0 — Projeyi çalıştır ve kapsamı sabitle

- [x] Projeyi VS Code’da aç.
- [x] Terminalde `flutter doctor` çalıştır; Flutter SDK ve Android emülatör/cihaz durumunu kontrol et.
- [x] `flutter pub get` ile bağımlılıkları al.
- [x] `flutter run` ile başlangıç uygulamasını çalıştır.
- [x] İlk çalışan sürümün ekran görüntüsünü al veya not et.
- [x] Ek paket kullanmama kuralını koru; gerekiyorsa ihtiyaç duyulan özelliği Flutter’ın yerleşik araçlarıyla çöz.

**Bu projedeki mevcut başlangıç noktası:** `lib/main.dart` içinde “Hello World” gösteren Flutter iskeleti var. Bu dosyayı uygulamanın giriş ekranına dönüştür.

### Aşama 1 — Uygulama iskeleti ve klasörler

- [ ] Uygulama adını ve katalog temasını belirle: **[Proje adı / tema]**
- [ ] `MaterialApp`, tema ve başlangıç rotasını oluştur.
- [ ] Ekranlar, modeller, veri ve tekrar kullanılan widget’lar için aşağıdaki gibi anlaşılır bir yapı kur.
- [ ] Ana sayfada başlık/banner alanı ve ürün kataloğuna giden içerik oluştur.

Örnek klasör yapısı:

```text
lib/
  main.dart
  models/
    product.dart
  data/
    product_data.dart
  screens/
    home_screen.dart
    product_detail_screen.dart
    cart_screen.dart
  widgets/
    product_card.dart
assets/
  images/
  data/
    products.json
screenshots/
```

Klasör isimlerini projene göre değiştirebilirsin; önemli olan kodu, veriyi ve asset’leri tek dosyada yığmamaktır.

### Aşama 2 — Ürün modeli ve liste ekranı

- [ ] Ürün modeli oluştur. En azından `id`, `name`, `description`, `price` ve `image` alanlarını düşün.
- [ ] Birkaç örnek ürün verisi hazırla.
- [ ] Veriyi yönergedeki JSON/model yaklaşımına uygun düzenle. Yerel JSON asset’i kullanıyorsan `pubspec.yaml` içinde asset’i tanımla.
- [ ] Ürünleri ana katalog ekranında `GridView` ile kartlar halinde göster.
- [ ] Kartlarda görsel, ürün adı ve fiyat gibi temel bilgileri göster.
- [ ] Görsel yüklenemediğinde boş/hatalı bir alan yerine anlaşılır bir yer tutucu göster.

### Aşama 3 — Ürün detay ekranı ve gezinme

- [ ] Ürün kartına dokunulduğunda detay ekranına geçiş yap.
- [ ] Seçilen ürünü `Navigator` / `MaterialPageRoute` üzerinden `Route Arguments` olarak aktar.
- [ ] Detay ekranında ürün görseli, adı, açıklaması ve fiyatı göster.
- [ ] Geri dönüşün çalıştığını kontrol et.

### Aşama 4 — Sepet simülasyonu ve etkileşim

- [ ] Ürün detayında veya kartında “Sepete ekle” butonu oluştur.
- [ ] Butona basılınca `StatefulWidget` ve `setState` gibi temel bir yöntemle sepet durumunu güncelle.
- [ ] Sepet ekranında eklenen ürünleri veya en azından sepet sayısını göster.
- [ ] Aynı ürünü tekrar ekleme davranışını belirle: **[Adet artsın / tekrar satır eklensin]**
- [ ] İşlemin gerçek sipariş/ödeme olmadığını arayüzde açık tut.

### Aşama 5 — Görsel düzen, doğrulama ve teslim

- [ ] Renkleri, boşlukları ve yazı stillerini tutarlı hale getir.
- [ ] Ana sayfa → ürün detayı → sepete ekle → sepet akışını baştan sona dene.
- [ ] Uygulamayı emülatörde veya fiziksel Android cihazda tekrar çalıştır.
- [ ] `flutter analyze` çalıştır ve projeden kaynaklanan sorunları düzelt.
- [ ] README’yi aşağıdaki şablona göre tamamla.
- [ ] Ana sayfa, ürün detayı ve sepet ekranlarının ekran görüntülerini `screenshots/` içine koy.
- [ ] GitHub deposunu public yap; README, kod ve ekran görüntülerinin depoda olduğuna bak.
- [ ] GitHub URL’sini ve teslim bilgilerini aşağıya yaz.

## 4. Tamamlanma kontrol listesi

### Uygulama

- [ ] Uygulama açılıyor ve kapanmadan temel akış tamamlanıyor.
- [ ] Ürün listesi `GridView` ile gösteriliyor.
- [ ] Ürün kartından detay ekranına geçiliyor.
- [ ] Doğru ürün bilgisi route argument ile detay ekranına ulaşıyor.
- [ ] Sepet etkileşimi ekranda gözle görülür bir state değişikliği yapıyor.
- [ ] Görsel/JSON asset’leri doğru klasörde ve uygulama içinde kullanılabilir durumda.
- [ ] Yönerge kapsamı dışında uygulama paketi eklenmedi.

### GitHub teslimi

- [ ] Depo public: **[Evet / Hayır]**
- [ ] Depoda güncel ve çalışan kaynak kod var.
- [ ] README proje adı, kısa açıklama, Flutter sürümü ve çalıştırma adımlarını içeriyor.
- [ ] Ekran görüntüleri depoya eklendi.
- [ ] Depo URL’si: **[GitHub URL’sini buraya yapıştır]**

## 5. README şablonu

Proje kökündeki `README.md` dosyasına uyarlayabilirsin:

```markdown
# [Proje adı]

[Uygulamanın ne yaptığını 1-2 cümleyle açıkla.]

## Özellikler

- Ürün kataloğu ve kartlı ürün listesi
- Ürün detay ekranı ve sayfalar arası ürün aktarımı
- Basit sepet simülasyonu

## Kullanılan teknoloji

- Flutter: [flutter --version çıktısındaki sürüm]
- Dart: [dart --version çıktısındaki sürüm]
- Uygulama bağımlılıkları: [Flutter SDK; kullanılan ek paket varsa burada belirt]

## Çalıştırma

1. Depoyu klonla.
2. Proje klasöründe `flutter pub get` çalıştır.
3. Android emülatörünü veya cihazı aç.
4. `flutter run` çalıştır.

## Ekran görüntüleri

### Ana sayfa
![Ana sayfa](screenshots/home.png)

### Ürün detayı
![Ürün detayı](screenshots/product_detail.png)

### Sepet
![Sepet](screenshots/cart.png)
```

## 6. Proje bilgileri — doldur

- **Proje adı:** [ ]
- **Katalog teması / ürün türü:** [ ]
- **Ürün verisinin kaynağı:** [Yerel JSON / başka: ]
- **Test edilen cihaz veya emülatör:** [ ]
- **Flutter sürümü:** [ ]
- **GitHub deposu (public):** [ ]
- **Ekran görüntülerinin konumu:** [ ]
- **Son kontrol tarihi:** [ ]
