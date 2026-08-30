# Değişiklik Notları — 30 Ağustos 2026

Denetim raporundaki 11 maddenin tamamı uygulandı. Temel çıkış noktası:
**görsel dil aynı kalsın**, kırık davranışlar düzelsin, dil önceliği İngilizce olsun,
konumlandırma geliştirici kimliğine kaysın.

## Yeni dosyalar

| Dosya | Ne işe yarıyor |
|---|---|
| `og.png` | 1200×630 paylaşım kartı — sitenin kendi tipografisiyle üretildi |
| `apple-touch-icon.png` | 180×180 iOS ana ekran ikonu |
| `LICENSE` | MIT (kod için; metin ve görseller © Sedat Onat) |
| `CHANGES.md` | Bu dosya |

## index.html

**Kritik düzeltmeler**

- `og:image`, `og:image:width/height`, `og:image:alt`, `twitter:image` eklendi →
  LinkedIn / X / WhatsApp önizlemesi artık çalışıyor.
- `.stage` yüksekliği `100svh` oldu (`100vh` fallback ile) → mobilde adres çubuğu zıplaması bitti.
- `--fg-3` `#777` → `#8a8a8a`, `--fg-4` `#444` → `#6e6e6e` → footer ve etiketler WCAG AA eşiğini geçiyor.
- `apple-touch-icon` linki eklendi.

**Dil — İngilizce öncelikli**

- `<html lang="en">`; `title`, `description` ve tüm OG/Twitter etiketleri İngilizce.
- Türkçe artık `data-tr` üzerinden uygulanıyor (önceden tersiydi).
- Header'a `TR` / `EN` düğmesi eklendi; tercih `localStorage`'da (`so-lang`) saklanıyor.
- `og:locale` = `en_US`, `og:locale:alternate` = `tr_TR`.

**SEO**

- Başlık: `Sedat Onat — Supply Chain Systems & iOS`.
- Açıklama somut kanıt içeriyor (226 makale, 167 terim, Swift, AI ile kurulan haber sitesi).
- `<link rel="canonical">` eklendi.
- JSON-LD `Person` + `sameAs` (8 mülkün tamamı) + `knowsAbout` eklendi.

**Konumlandırma — geliştirici kimliği**

- Başlığın altına kimlik satırı geri geldi (v4'teki kendi ifaden):
  `Procurement Manager · Writer · Builder` / `Satınalma Yöneticisi · Yazar · Yapıcı`.
- Proje listesi yeniden sıralandı — kod tarafı öne alındı:

  | Yeni | Proje | Eski |
  |---|---|---|
  | 01 | swift.sedatonat.dev | 05 |
  | 02 | TZP.news | 02 |
  | 03 | GitHub · @sedatonat | 09 |
  | 04 | TedarikZinciriPortali.com | 01 |
  | 05 | SupplyChainGlossary | 04 |
  | 06 | ErpNasılAlınır.com | 03 |
  | 07 | SedatOnat.com | 06 |
  | 08 | SedatOnat.photography | 07 |
  | 09 | LinkedIn | 08 |

  İlk iki satır `featured` (daha parlak). TZP.news etiketi İngilizcede
  `Built with Claude Cowork` oldu — `#01` kısaltması dışarıdan anlaşılmıyordu.

  *Bu tek maddeye katılmıyorsan geri alması kolay: `<li>` bloklarının sırasını
  değiştirip `.num` değerlerini düzeltmek yeterli.*

**Erişilebilirlik ve semantik**

- `<main>` artık hem hero'yu hem proje bölümünü kapsıyor.
- "Projects" bir `div` değil `<h2>`.
- Popover açılıp kapandıkça `aria-expanded` güncelleniyor; `aria-controls` eklendi.
- "Kopyala" gerçek bir `<button>` oldu.
- Dekoratif oklar (`↗`, `↓`) `aria-hidden="true"`.
- `Escape` ile kapatınca odak tetikleyici düğmeye dönüyor.
- Toast'a `role="status"` eklendi.
- `:focus-visible` için görünür bir odak halkası tanımlandı.
- `@media (prefers-reduced-motion: reduce)` bloğu eklendi.
- Marka linki `href="#"` → `href="/"`.
- Bölüm id'si `#projeler` → `#projects` (dil önceliğiyle tutarlı).

**Mobil**

- 900px altında `.meta` artık gizlenmiyor — proje adının altına ikinci satır
  olarak geliyor. "226 articles", "167 terms", "Built with Claude Cowork"
  mobilde de görünüyor.

**Performans ve temizlik**

- Inter `200;300;500;700;900` → `300;500;700` (200 ve 900 hiç kullanılmıyordu).
- Bruno Ace SC `&text=SEDATON` ile subset edildi — tüm font yerine 7 glif.
- Kullanılmayan `--warm` tokenı kaldırıldı.
- `theme-color` `#000000` → `#0a0a0c` (gerçek zemin rengi).
- Transition'lar `all` yerine adlandırılmış özelliklere bağlandı.
- JS tek bir IIFE'de toplandı, `'use strict'` eklendi, `localStorage` erişimi
  try/catch ile sarıldı.

## 404.html

- Ana sayfayla aynı token seti, aynı font yükleme stratejisi (render-blocking değil).
- Favicon, `apple-touch-icon`, `theme-color`, `description`, `robots: noindex` eklendi.
- `100svh`, `:focus-visible`, `prefers-reduced-motion`.
- Dil katmanı eklendi — ana sayfadaki tercihi (`so-lang`) okuyor.
- CTA butonu ana sayfadaki pill formuna eşitlendi.

## favicon.svg

- Dolgu artık tema duyarlı: açık temada `#0a0a0c`, koyu temada `#f0f0f0`.
  Koyu sekmede görünmeme sorunu bitti.

## sitemap.xml / README.md

- Sitemap'e `<lastmod>` eklendi.
- README yeniden yazıldı — site artık "development & data analytics reference
  page" değil, proje hub'ı. Dosya tablosu, dil davranışı ve local preview eklendi.

## Doğrulama

Headless Chromium ile kontrol edildi:

- Masaüstü (1440×900) ve mobil (390×844) render'ı — yatay taşma yok.
- `TR` düğmesi: başlık `Gelişimin Sürekliliği`, rol satırı
  `SATINALMA YÖNETİCİSİ · YAZAR · YAPICI` olarak dönüyor.
- Popover açılışında `aria-expanded="true"`.
- Konsolda JS hatası yok.

## Sırada ne var

- `og.png`'yi canlıya aldıktan sonra LinkedIn Post Inspector ve X Card Validator
  ile önbelleği tazele.
- Analitik hâlâ yok — dokuz mülke dağıtım yapan bir sayfada hangi linkin
  çalıştığını ölçmek isteyebilirsin.

## Revizyon — Projeler listesi (yazılım/site odaklı)

Liste, yalnızca yazılım ve web projelerini içerecek şekilde yeniden düzenlendi.

**Çıkarılanlar** (yazılım projesi olmadığı için):
- ErpNasılAlınır.com — kitap (Google Play)
- SedatOnat.com — profil sayfası
- SedatOnat.photography — fotoğraf portfolyosu
- LinkedIn — bülten

**Eklenenler:**
- TradeArtery.com — küresel ticaret haritası
- TZP.academy — öğrenme platformu
- SedatOnat.finance — piyasa çalışma alanı

**Yeni sıralama (dev kimliği önce):**
01 TZP.news · 02 TZP.academy · 03 TradeArtery.com · 04 swift.sedatonat.dev ·
05 TedarikZinciriPortali.com · 06 SupplyChainGlossary · 07 SedatOnat.finance · 08 GitHub

Not: SupplyChainGlossary hâlâ tedarikzinciriportali.com/sozluk adresine bağlı —
supplychainglossary.com.tr denendi, bağlantı kurulamadı (henüz yayında değil).

JSON-LD `sameAs` listesine tzp.academy, tradeartery.com ve sedatonat.finance eklendi;
kimlik bağlantısı olduğu için LinkedIn / sedatonat.com / photography orada bırakıldı.

## Revizyon — iOS uygulaması eklendi

- **Albumize** (App Store) listeye 01 sırasına, öne çıkan satır olarak eklendi.
  Bağlantı ülke bağımsız biçimde verildi: `apps.apple.com/app/albumize/id6762205813`
  (ziyaretçi kendi App Store mağazasına yönlenir).
- JSON-LD `sameAs` listesine aynı bağlantı eklendi.
- **TZP News (iOS)** 02 sırasına, öne çıkan satır olarak eklendi:
  `apps.apple.com/app/tzp-news/id6767178018`. Web sürümünden ayrışsın diye
  satır adı "TZP News · iOS", web satırı ise "TZP.news" olarak bırakıldı.
- Güncel sıra: 01 Albumize · 02 TZP News · iOS · 03 TZP.news · 04 TZP.academy ·
  05 TradeArtery.com · 06 swift.sedatonat.dev · 07 TedarikZinciriPortali.com ·
  08 SupplyChainGlossary · 09 SedatOnat.finance · 10 GitHub

## Revizyon — satır biçimi tekleştirildi

- Albumize satırının adı "Albumize · iOS" oldu; TZP News satırıyla aynı kalıba girdi.
- "featured" vurgusu kaldırıldı: ilk iki satırdaki daha parlak/kalın isim biçimi
  artık yok, on satırın tamamı aynı ağırlık ve renkte. Kullanılmayan
  `.projects .featured .name-l` CSS kuralı da silindi.

## Logo — nav kilidi (Alternatif A)

Altıgen marka, sol üstte "SEDAT ONAT" yazısının soluna amblem olarak eklendi.

- SVG doğrudan `index.html` içine gömüldü (ek ağ isteği yok, ~330 bayt).
- Boyut `em` cinsinden verildi (`0.72em`), yani marka yazısıyla birlikte ölçekleniyor:
  masaüstünde 23px, ≤900px'de 17px, ≤480px'de 14px. Ekstra medya sorgusu gerekmedi.
- `fill: currentColor` — logo, marka yazısının rengini miras alıyor; ileride
  renk değişirse tek yerden değişir.
- `aria-hidden="true"` — bağlantının metni zaten "SEDAT ONAT", ekran okuyucuya
  ikinci bir işaret okutmaya gerek yok.

## Logo — gerçek marka uygulandı

Geçici altıgen işaret kaldırıldı; yerine gerçek fırça darbeli "S" enso logosu geldi.

- Kaynak: `sedatonat.finance/logo.png` (1133×1157 raster). Vektör sürümü olmadığı için
  potrace ile izlendi ve SVGO ile sadeleştirildi → tek bir SVG, ~5.9 KB, iki path.
  İzleme 800px genişlikte yapıldı; fırça dokusu korunuyor, düğüm sayısı makul kalıyor.
- **Nav** — `index.html` içine gömülü SVG, `fill: currentColor`. Boyut 1.06em
  (masaüstünde ~34px). Altıgen dolu bir formdu, bu ise ince konturlu bir daire;
  aynı görsel ağırlığı vermesi için 0.72em'den 1.06em'e çıkarıldı, yazıyla arasındaki
  boşluk 0.34em'den 0.30em'e indirildi.
- **favicon.svg** — aynı path, kare viewBox (`-8.5 0 817 817`), açık/koyu tema dolgusu.
  16px'te zayıf ama okunur; 32px ve üstünde net.
- **apple-touch-icon.png** — 180×180, beyaz marka, `#0a0a0c` zemin, %9 kenar boşluğu.
- **og.png** — marka sağ üst köşeye yerleştirildi; sol üstteki "SEDAT ONAT" yazısıyla
  dengeleniyor. Paylaşım önizlemesinde artık logo da görünüyor.

Not: Elde yapılmış temiz bir vektör (AI/SVG) varsa onu koymak daha iyi olur —
izleme, fırça kenarlarını yaklaşık olarak yeniden çiziyor.
