[README.md](https://github.com/user-attachments/files/33903564/README.md)
# Peşindeyiz — İlk 11 mobil uygulaması

Android ve iOS için Capacitor 8 projesi. Kaynak: https://pesindeyiz.com/gs11/
Paket adı: com.pesindeyiz.ilk11 · Sürüm: 1.1.0

Bu ZIP kaynak projedir; telefona yüklenebilir APK veya IPA değildir.

## Hazır özellikler

- Yerel kadro ekranı, 22 formasyon, serbest oyuncu yerleşimi.
- 24 Ekim 2026 tarihinde canlı sayfadan alınmış 38 oyunculuk başlangıç kadrosu.
- Paket içinde 32 fotoğraf, aslan simgesi, Peşindeyiz alt bandı ve açılış ekranları.
- WordPress yönetim panelindeki güncel oyuncuları ve görselleri Yenile ile okuma.
- Yeni verileri Uygula ile açma; mevcut taslak oyuncu kimlikleri üzerinden korunur.
- İnternet yokken paket/son kaydedilen kadro ve görsellerle çalışma.
- Cihazda taslak, özel oyuncu, fotoğraf, renk sıfırlama, baştan başlama ve geri alma.
- Native PNG kaydetme/paylaşım ekranı; kadro başlığı, formasyon ve site bağlantısı.
- X, Instagram ve WhatsApp butonları sistem paylaşım menüsünü açar. Hedef uygulama
  kullanıcı tarafından seçilir; hedefin yazı ve görsel kabulü kendi desteğine bağlıdır.
- Android geri tuşu, çentik/güvenli alan boşlukları, uygulama hakkında ekranı.

Kullanıcı giriş sistemi, bildirim veya reklam takibi eklenmedi. Uygulama bir uzak
sayfayı WebView içinde doğrudan çalıştırmaz; paketlenmiş kadro kodunu kullanır.
WordPress sayfasından yalnızca JSON verisi okunur; uzak JavaScript çalıştırılmaz.

## Bilgisayarda çalıştırma

Node 22+ kurulu olmalı:

    npm ci
    npm test
    npm run dev

Tarayıcı önizlemesinde yerel oyuncular ve kadro özellikleri çalışır. Native dosya
paylaşımı gerçek Android/iOS derlemesinde kullanılabilir. Tarayıcının CORS kuralı
canlı veriyi engellerse önizleme başlangıç kadrosuna döner.

## Android

Android Studio 2025.2.1+ ve SDK Platform 36 / uygun JDK gerekir:

    npm ci
    npm run sync
    npm run android

Android Studio'da SDK konumunu tanımlayıp bağlı telefon veya emülatörde Run kullanın.
Debug APK: Build APK(s) veya npm run android:debug.
Beklenen çıktı: android/app/build/outputs/apk/debug/app-debug.apk.
Mağaza sürümü için kendi uygulama imzalama anahtarınızla release AAB oluşturun.
Bu pakette imzalama anahtarı veya mağaza erişim bilgisi yoktur.

## iPhone

Mac ve Xcode 26+ gerekir. iOS projesi Swift Package Manager kullanır:

    npm ci
    npm run sync
    npm run ios

Xcode'da Signing & Capabilities altında kendi Team hesabınızı seçin.
Simülatörde Run; gerçek cihaz/TestFlight için uygun imzalama ve dağıtım ayarlarını yapın.
Uygulama simgeleri, fotoğraf kullanım açıklamaları ve Filesystem privacy manifesti
projeye eklendi. Mağaza gizlilik yanıtlarını gerçek kullanımınıza göre tamamlayın.

## Dosyalar

- src/main.js: başlangıç, WordPress güncellemesi, offline önbellek, mobil kabuk.
- src/config.js: JSON veri doğrulama ve görsel kaynak kontrolü.
- src/native.js: Capacitor paylaşım, dosya ve dış bağlantı işlemleri.
- public/assets/app.js: mevcut İlk 11 motorunun native paylaşım uyarlaması.
- android/: Android Studio projesi.
- ios/App/App.xcodeproj: Xcode projesi.

Native projeleri değiştirdikten sonra npm run sync ile web paketini eşitleyin.
webDir yerel dist dizinidir; canlı sunucu URL'si kullanılmaz. iOS Public dosyaları
sync sırasında oluşturulur. Cache dosyası uygulamanın özel Data dizinindedir.
Görsel paylaşımları yalnızca Cache dizininden yapılır; son beş PNG dönüşümlü tutulur.
Özel taslaklar web sitesi ve farklı cihazlarla eşitlenmez.

## Veri ve haklar

Oyuncu isimleri/numaraları sitenizdeki güncel panelden alınmıştır; spor verileri için
bağımsız doğrulama yapılmamıştır. Oyuncu fotoğrafları önceki eklentiyle birlikte verilen
Quicklineup referansından gelir; kaynak eşlemesi PHOTO-SOURCES.json içindedir.
Marka görselleri kullanıcı tarafından sağlandı. Kod GPL-2.0-or-later; fotoğraf ve marka
görsellerinin hakları sahiplerinde kalır.

## Doğrulama ve sınırlar

Web üretim derlemesi, yerel kadro motoru etkileşimleri, formasyonlar, PNG native köprüsü,
WordPress veri doğrulaması ve native proje eşitlemesi kontrol edildi.
Android derleme girişimi Gradle indirmesinde ağ kısıtıyla durdu; burada Android SDK yok.
Bu Linux ortamında Xcode olmadığından iOS derlenmedi. APK/IPA ve fiziksel cihaz testi
henüz tamamlanmadı; mağazaya yükleme veya yayın yapılmadı.

Resmî kurulum kaynakları:
https://capacitorjs.com/docs/getting-started/environment-setup
https://capacitorjs.com/docs/apis/share
https://capacitorjs.com/docs/apis/filesystem

## 1.0.1: WordPress yönetimi
WordPress eklentisinin 1.6 sürümünü yükleyin. İlk 11 Kur! panelindeki bilgiler
GET /wp-json/pesindeyiz-ilk11/v1/config üzerinden otomatik alınır. Eski eklentide
HTML verisini okuma alternatifi korunur. Açılış, öne gelme, bağlantının geri gelmesi
ve Yenile sırasında güncellenir. Uygula adımı kaldırıldı. Aktif kadro yerleşimi ve
geri alma geçmişi korunur. Yönetici ayarları, kullanıcının özel tercihini değiştirmez;
varsayılanı takip eden başlık ve renkler yeni varsayılana geçer.
Android APK 1.0.1 bu ortamda derlendi; imzası doğrulandı. Fiziksel cihaz testi yapılmadı.
iOS projesi güncel; iOS derlemesi yapılmadı. Kaynaktan APK kurulumunda Android
kaynak izni isteyebilir; bu izin Play Protect ayarından ayrıdır.

## 1.1.0
Android ve iOS hücum yönü yukarı sabitlendi; eski aşağı yönlü taslaklar yansıtılarak
oyuncuları korunur. Yön seçimi kaldırıldı. Galeriye kaydet paylaşım menüsünü açmaz.
Android: MediaStore ile Pictures/Pesindeyiz; eski Android 7–9 sürümlerinde yazma izni
ve medya tarayıcı kullanılır. iOS: Fotoğraflar’a ekleme izni ve Media savePhoto kullanılır.
Yenileme mesajları Güncelleniyor/Güncellendi olarak sadeleştirildi. Alt bölümde
Instagram @pesindeyizcom ve Twitter/X @PesindeyizApp takip bağlantıları eklendi.
iOS adımları IOS-KURULUM.md içinde; simülatör derleme betiği scripts klasöründedir.
Android 1.1.0 APK derlendi ve imzası doğrulandı. iOS derlemesi ve fiziksel cihazda
galeriye kaydetme testi bu ortamda yapılmadı.
