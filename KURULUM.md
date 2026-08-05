# Jekyll kurulumu — ne nerede?

Bu site GitHub Pages tarafından otomatik derlenir. Ek bir program kurmanız gerekmez.

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

- Depoda `.nojekyll` adlı bir dosya OLMAMALI (varsa silin, yoksa Jekyll çalışmaz).
- `CNAME` dosyası (alan adı için) yerinde kalsın.
- Fotoğraflar kök dizine: `rumeysaerdogdu.jpeg`, `rumeysaerdogduofis.jpeg`, `rumeysaerdogdu2.jpeg`

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
