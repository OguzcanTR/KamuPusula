# KamuPusula

KamuPusula, Gemici Software tarafından geliştirilen kamu ilanı takip uygulamasıdır.

Sürüm 1.9. Android Studio'dan `release` derlemesi kişisel Gemici Software anahtarıyla imzalanır. Özel anahtar kaynak ZIP'ine veya GitHub deposuna konmaz; yerel Gradle kullanıcı özellikleri `GEMICI_STORE_FILE`, `GEMICI_STORE_PASSWORD`, `GEMICI_KEY_ALIAS` ve `GEMICI_KEY_PASSWORD` değerlerini sağlamalıdır. Debug derlemeleri Android debug anahtarıyla imzalanır.

Kariyer Kapısı'nın resmi RSS akışını okuyup kamu ilanlarını listeleyen, filtrene uyan yeni ilanlar için
bildirim gönderen ve tek dokunuşla resmi ilan/başvuru sayfasını açan kişisel Android uygulaması.

## Kurulum (Android Studio)

1. Android Studio'yu (güncel sürüm) aç → **Open** → bu klasörü seç.
2. Gradle senkronizasyonu bitene kadar bekle (ilk seferde internetten bağımlılık indirir).
   Studio "güncelle" önerirse (AGP / Gradle / Kotlin) kabul edebilirsin.
3. Telefonu USB ile bağla (Geliştirici seçenekleri → USB hata ayıklama açık) → **Run ▶**.
   Ya da **Build → Build APK(s)** ile APK üretip telefona kur.
4. İlk açılışta bildirim iznini ver.

## Nasıl çalışır

- Kaynak: `https://kariyerkapisi.gov.tr/RSS` (sitenin kendi RSS akışı, tüm aktif ilanlar).
- Uygulama açılınca ve arka planda seçtiğin sıklıkta (1/3/6/12 saat) akışı kontrol eder.
- İlk kontrolde mevcut ilanlar "bilinen" sayılır, bildirim yağmuru olmaz. Sonrasında yeni gelen ilanlar
  filtrene uyuyorsa bildirim gelir; bildirime dokununca ilanın resmi sayfası açılır.
- **Başvur:** Başvuru e-Devlet girişiyle Kariyer Kapısı'nda yapılır. Uygulama sadece ilanı/başvuru sayfasını
  açar; şifre ya da giriş bilgisi tutmaz.

## Ekranlar

- **İlanlar:** son başvuru tarihi yaklaşan ilanlar en üstte, en yakın tarih ilk sırada görünür. İlan türlerini kalıcı olarak gizleyebilir (örn. yurt dışı eğitim ilanları), ayrıca tür, metin ve profil uygunluğuna göre listeyi daraltabilirsin.
  Süresi geçmiş ilanlar ve tarihi alınamayanlar yaklaşan ilanların altında sıralanır. Kartlarda ilan başına
  pozisyon bazlı uygunluk, tanınan eğitim/bölüm/KPSS koşulları ve sonuçları gösterilir; tüm pozisyonlar
  ve bölüm şartlarının tamamı kartta açılır, pozisyon sayısına üst sınır uygulanmaz.
- **Favoriler:** yıldızladığın ilanlar (akıştan düşse bile kalır).
- **Başvurular:** "Başvurdum" dediğin ilanlar, işaretlediğin tarihe göre (akıştan düşse bile kalır).
  Başvurusu işaretlenen ilan için "son başvuru" hatırlatması gönderilmez. Yanlış işaretlersen "Geri al".
- **Gizlenenler:** İlan kartındaki "Gizle" düğmesi ilanı ana listeden kaldırıp bu sekmede saklar. "Gizliden çıkar" ile geri alabilirsin; gizlenen ilanlar RSS akışından düşse bile listede kalır.
- **Ayarlar:** profilim (mezuniyet düzeyi + bölüm/program + KPSS puanları), bildirim filtresi, kontrol sıklığı,
  RSS kaynakları, sistem/açık/koyu görünüm ve GitHub üzerinden uygulama güncelleme kontrolü.

## GitHub güncellemeleri

Uygulama herkese açık `OguzcanTR/KamuPusula` GitHub deposunun en son yayımlanan sürümünü denetler. Yeni sürümdeki APK uygulama içinden indirilebilir; indirme tamamlandığında Android kurulum ekranında kullanıcı güncellemeyi onaylar. GitHub Releases'e yüklenen APK dosyasının uzantısı `.apk` olmalı ve uygulamanın mevcut imza anahtarıyla imzalanmalıdır. Kaynak kodu, APK ya da anahtarı yüklemek tek başına yeni sürüm yayımlamaz; yeni sürüm için artan `versionCode` ile imzalı APK üretip GitHub Release'e eklemek gerekir. Özel anahtar ve parolalar GitHub'a yüklenmemelidir.

## Geri sayım

Karttaki alarm simgesine dokunup son başvuru gününü seç; kartın altında "Son başvuru: ... · 3 gün 4 saat kaldı"
görünür (son 3 günde kırmızı). Elle girilen gün, o günün 23:59'una kadar sayılır; ilan daha erken saatte
kapanıyorsa ilandaki saati esas al. İlan detay verisi bağlandığında (aşağıya bak) tarih otomatik gelir.

## Uygunluk (profil + şartlar)

Ayarlar → Profilim'de mezuniyet düzeylerini, bölüm/program adını (birden fazlaysa virgülle ayır), KPSS
puan türünü listeden seçip puanını ve iş deneyimi/yetkinliklerini gir. Bilgiler yalnızca telefonda saklanır. Kariyer Kapısı alt ilan servisi
pozisyon başlıklarını, öğrenim dalı listesini, KPSS puan türlerini ve taban puanı verdiğinde her pozisyon
profilinle ayrı karşılaştırılır:

- Kart, hangi pozisyonun profille eşleştiğini; gerekli öğrenim/bölüm/KPSS puanını ve senin profilinin
  karşılaştırma sonucunu ayrı ayrı yazar.
- Profilden eklenen yetkinlikler ilan başlığı ve ayrıntı metninde aranır; bu metin eşleşmesi resmi şart
  uygunluğu değildir.
- "Şartlarımı karşılamayanları gizle" filtresi çıkar.
- Yeni ilan bildiriminde "Sana uygun · ..." yazar; birden çok ilanda başlık "Sana uygun N yeni ilan var" olur.
- Uygulama açıkken yapılan yenileme de yeni ilanları bildirir; ayarlardaki test düğmesi gönderim durumunu açıklar.
- İstersen Ayarlar'dan açıkça uygun olmayan ilanlar için bildirim kapatılabilir. Şartı bilinmeyen ilanlar
  hiçbir zaman "uygun değil" sayılıp gizlenmez/bildirimden elenmez.

> **Durum:** Detaylar herkese açık Kariyer Kapısı servisinden gelir. Uygunluk; servisin açık alan olarak
> verdiği pozisyon, bölüm listesi, eğitim düzeyi, KPSS puan türleri ve taban puanla sınırlıdır. PDF ekinde
> veya serbest metinde kalan bölüm/denklik, yaş, deneyim, yabancı dil ve diğer koşullar otomatik
> doğrulanamayabilir. "Sana uygun" profil eşleşmesi başvuruya kesin uygunluk garantisi değildir; resmi ilanı
> ve eklerini kontrol et. Verisi eksik ya da belirsiz kalan pozisyonlar "bilgi eksik" gösterilir.

## Bilmen gerekenler

- RSS akışında **son başvuru tarihi, il ve KPSS bilgisi yok**; yalnızca ilan türü, başlık, yayın tarihi,
  link ve kurum logosu var. Son başvuru tarihi Kariyer Kapısı detay servisinden otomatik alınır; servis
  yanıt vermezse karttaki alarm simgesinden tarihi elle seçebilirsin.
- **İle göre filtre:** `kariyerkapisi.gov.tr/RSS/RssLinkiAl` sayfasında il/kurum/tür seçip "RSS Linkini
  oluştur" de, çıkan linki Ayarlar → RSS kaynakları'na ekle. İstersen varsayılan kaynağı silip yalnızca
  filtreli linki bırakabilirsin.
- Bildirim gecikirse: telefon ayarlarında uygulama için pil kısıtlamasını kaldır (özellikle Xiaomi, Huawei,
  Samsung'da).
- Uygulama her kontrolde kayıtlı RSS kaynaklarını okur; yeni ilanların ve önbellekteki eksik/eski ayrıntıların
  tamamını sırayla Kariyer Kapısı servisine sorar. İlan sayısına göre ilk yenileme uzun sürebilir. Eşzamanlı
  yenilemeler tek sıraya alınır. Eksik tarihler ve yeni pozisyon şeması sonraki kontrollerde tekrar denenir.
## Dosya yapısı

```
app/src/main/java/app/kamuradar/
  Model.kt          ilan modeli, tür listesi, bildirim eşleştirme
  Detail.kt         şart/son başvuru modeli, uygunluk hesabı, Kariyer Kapısı detay bağlantısı
  RssParser.kt      RSS ayrıştırıcı
  Store.kt          kalıcı veri (SharedPreferences)
  Repository.kt     indir → karşılaştır → bildir
  Notifier.kt       bildirimler
  Workers.kt        arka plan kontrolü + hatırlatmalar (WorkManager)
  MainViewModel.kt  ekran durumu
  Ui.kt, Theme.kt   Jetpack Compose arayüzü
```




