# Jekyll kurulumu — ne nerede?

Bu site **GitHub Pages** tarafından otomatik derlenip yayınlanır. Ek bir program kurmanız gerekmez.

Değişiklik yapmak için tek yapmanız gereken dosyayı düzenleyip GitHub'a göndermek:

```
Düzenle  →  commit  →  push  →  GitHub Pages birkaç dakikada yayınlar
```

Yayına girip girmediğini GitHub'da depo → **Actions** sekmesinden izleyebilirsiniz.

## Klasör yapısı

```
_config.yml          → Site bilgileri: isim, adres, e-posta, MENÜ. Tek yerden düzenlenir.
_includes/
  head.html          → Tüm SEO etiketleri ve yapısal veri
  nav.html           → Üst menü (bir kez düzenle, her sayfada değişir)
  footer.html        → Alt bilgi (bir kez düzenle, her sayfada değişir)
  banner.html        → Sayfa başı başlık görseli (H1 + kalem animasyonu)
  scripts.html       → Animasyonlar + otomatik İçindekiler
_layouts/
  default.html       → Genel sayfa şablonu
  post.html          → Blog yazısı şablonu (özet, içindekiler, S.S.S., ilgili yazılar)
_posts/              → BLOG YAZILARI buraya (Markdown)
assets/css/style.css → Tüm stiller tek dosyada
index.html           → Ana sayfa
blog.html            → Blog listesi (adres: /blog/)
404.html             → Özel "sayfa bulunamadı" sayfası
r-*.html             → Eski adreslerden yönlendirme dosyaları (silmeyin)
sitemap.xml          → Otomatik üretilir
robots.txt           → Otomatik üretilir
```

## Menüyü değiştirmek

`_config.yml` içindeki `nav:` listesini düzenleyin. Tek değişiklik tüm sayfalara yansır.

## İletişim / adres değiştirmek

`_config.yml` içindeki `contact:` ve `office:` bölümlerini düzenleyin.

## İletişim formu

Form `/iletisim/` sayfasında, aydınlatma metni `/aydinlatma-metni/` adresinde.

- `_config.yml` → `contact.form_action` **boşken** form, ziyaretçinin kendi
  e-posta uygulamasını dolu bir taslakla açar. Araya hiçbir servis girmez.
- Bir form servisi bağlamak için hesabı açın ve verdiği adresi
  `form_action`'a yazın (Web3Forms kullanılırsa anahtarı `form_access_key`'e).
  Servisin adını `form_provider`'a yazın; aydınlatma metninde otomatik geçer.
- Aydınlatma metnindeki aktarım ve saklama süresi kısımları avukat
  kontrolünden geçmeli; dosyanın başındaki yorumda listeli.

## Ziyaret ölçümü

Hazır ama **kapalı**. Açılınca çerez kullanmayan bir servis ziyaretleri ve
birkaç önemli tıklamayı sayar; çerez bandı gerekmez. Ayarı `_config.yml` →
`analytics:` bölümünde, kodu `_includes/analytics.html` içinde.

Önerilen servis **GoatCounter** (ücretsiz, veriler Almanya/Finlandiya'da):

1. goatcounter.com → **Sign up**. "Code" alanına kısa bir ad yazın, örneğin
   `rumeysasaglamer`; panel `https://rumeysasaglamer.goatcounter.com` olur.
2. `_config.yml` içinde:
   ```yaml
   analytics:
     provider: "goatcounter"
     goatcounter_code: "rumeysasaglamer"
   ```
3. Commit + push. Yayından sonra siteyi açın; birkaç dakika içinde ziyaret
   panelde görünür. Görünmezse sayfada sağ tık → **Sayfa kaynağını görüntüle**
   → `gc.zgo.at` geçiyor mu bakın. Reklam engelleyici açık tarayıcılar sayılmayabilir.
4. Kendi ziyaretlerinizi saymamak için her tarayıcınızda bir kez
   `https://rumeysasaglamer.com/#toggle-goatcounter` adresini açın.

Alternatif **Plausible** (ücretli, aylık yaklaşık 9 $; 30 gün deneme): site
ekleyin, kurulum kodundaki `pa-XXXX.js` içindeki `XXXX`'i `plausible_script_id`
alanına yazın, `provider: "plausible"` yapın. Umami Cloud için `provider: "umami"`
ve `umami_website_id`.

Sayılan tıklamalar (servis panelinde "Events" ya da "Goals" altında):

| Ad | Ne zaman |
|---|---|
| `form-gonderildi` | İletişim formu gönderildi (`servis`: mesaj iletildi, `eposta`: e-posta uygulaması açıldı) |
| `eposta-tik` | E-posta adresine tıklandı |
| `instagram-tik` | Instagram bağlantısına tıklandı |
| `hero-on-gorusme` | Ana sayfadaki "Ön görüşme talep edin" düğmesi |
| `menu-iletisim` | Menüdeki "İletişim" düğmesi |

Plausible'da bunların panelde görünmesi için **Goals → Add goal → Custom event**
ile aynı adla eklenmesi gerekir. Olaylara ad, e-posta ya da mesaj gibi kişisel
bilgi eklenmez.

- Ölçüm yalnızca yayındaki sitede çalışır; yerelde önizlerken sayılmazsınız.
- Kapatmak için `provider: ""` yapmanız yeterli.
- Açmadan önce aydınlatma metnine ölçümle ilgili kısa bir paragraf eklenmesi
  ve avukat kontrolü önerilir.

## Yeni blog yazısı eklemek

`_posts/` klasörüne şu isim biçiminde bir dosya oluşturun:

```
YYYY-AA-GG-yazi-adi.md
örnek: 2026-09-10-oz-sefkat-nedir.md
```

Adresler `.html` uzantısı olmadan çalışır: `permalink: /oz-sefkat-nedir/`

Dosyanın başına şu bilgileri yazın:

```yaml
---
title: "Yazı Başlığı"
description: "Google'da görünecek 150 karakterlik açıklama."
keywords: "anahtar, kelimeler"
category_name: "Kaygı"
thumb: sarmal          # kart deseni: halkalar, sarmal, dugum veya dalga (yazmazsanız yaprak çıkar)
thumb_color: t2        # kart rengi: t1 yeşil, t2 altın, t3 lila, t4 kiremit (yazmazsanız sırayla)
image: "/gorsel.jpg"   # yazı başında görünecek fotoğraf; dosyayı kök klasöre koyun (1280x720 önerilir)
image_alt: "Tarif"     # görselin kısa sözlü tarifi
permalink: /yazi-adi/
excerpt_text: "Blog listesindeki kartta görünecek kısa özet."
summary: "Yazının başındaki Özet kutusunda görünecek metin."
faq:
  - q: "Soru?"
    a: "Cevap."
---

## İlk bölüm

Metin buraya...

## İkinci bölüm

Metin buraya...
```

Sonra dosyayı commit + push edin. Otomatik olarak:
- Blog listesine eklenir
- Sitemap'e eklenir
- İçindekiler tablosu `##` başlıklarından oluşturulur
- İlgili yazılar bölümü güncellenir
- Tüm SEO etiketleri ve yapısal veri üretilir

## Dikkat

- `CNAME` ve `Gemfile` dosyalarını silmeyin — `CNAME` olmadan alan adı, `Gemfile` olmadan derleme çalışmaz.
- `r-*.html` dosyaları eski adreslerden gelen ziyaretçiyi yeni adrese taşır; silmeyin.
- Fotoğraflar kök dizine: `rumeysa-saglamer.jpeg`, `rumeysa-saglamer-2.jpeg`
- Bir şey ters giderse GitHub → depo → **Actions** → ilgili çalışmanın kaydına bakın;
  hatanın sebebi orada yazar. Ayrıca her yayının bir öncesine tek tıkla dönebilirsiniz
  (eski bir deploy'u açıp **Publish deploy**).

## Bir sayfayı taşımak / kaldırmak

**Taşımak (adres değişecek):** Yazının `permalink` satırını değiştirin, sonra eski adres için
`r-yazi-adi.html` gibi bir dosya oluşturun:

```yaml
---
layout: redirect
permalink: /eski-adres/
redirect_to: /yeni-adres/
sitemap: false
---
```

**Kaldırmak:** `_posts/` içindeki dosyayı silin. Blog listesinden ve sitemap'ten otomatik çıkar.
Ziyaretçi eski adrese girerse özel 404 sayfasını görür.
