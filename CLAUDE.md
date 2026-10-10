# CLAUDE.md

Bu dosya, Claude Code'un (claude.ai/code) bu depoda çalışırken uyması gereken rehberdir.

## Proje

Klinik Psikolog Rümeysa Sağlamer'in tanıtım ve blog sitesi. **Jekyll** ile üretilir, **GitHub Pages** tarafından otomatik derlenip yayınlanır.

Yayınlama akışı: `main` dalına push → GitHub Pages depoyu derler → yayınlar. Elle yapılacak bir adım yoktur.

Alan adı `rumeysasaglamer.com`; DNS Guzel Hosting'de, apex A kayıtları GitHub Pages'e (`185.199.108–111.153`) bakar, `www` ise `ardasaglamer9.github.io`'ya. TLS sertifikasını GitHub otomatik üretir ve yeniler.

Kökteki **`CNAME` dosyası yayın için zorunludur** — GitHub Pages özel alan adını oradan okur. Silme, içeriğini değiştirme.

> Tarihçe: Site 6 Ağustos 2026'da Netlify'a taşınmıştı, sonra GitHub Pages'e geri döndü. `netlify.toml` kullanılmıyor.
>
> 10 Ekim 2026'da alan adı `rumeysaerdogdu.com` → `rumeysasaglamer.com` olarak değişti (soyadı değişikliği). Eski alan adı ayrı bir depodan yeni adrese yönlendiriliyor; DNS'i hâlâ GitHub Pages'e bakıyor ve **`MX` kaydı Guzel Hosting'de duruyor** — `info@rumeysaerdogdu.com` adresi bu sayede çalışmaya devam ediyor. Yeni posta kutusu açılınca `_config.yml` içindeki `contact.email` güncellenecek.

Sitenin tamamı Türkçe ve tek dillidir (`lang: tr`).

## Klasör yapısı

```
_config.yml          → Site bilgileri (TEK KAYNAK): başlık, açıklama, yazar, iletişim, ofis, MENÜ
_includes/
  head.html          → <head>: SEO etiketleri, Open Graph, JSON-LD yapısal veri
  nav.html           → Üst menü (site.nav üzerinden döner)
  footer.html        → Alt bilgi — iletişim/adres/sosyal (site.contact, site.office'ten okur)
  banner.html        → Sayfa başı başlık bloğu (H1 + animasyon)
  scripts.html       → Animasyonlar + otomatik İçindekiler üretimi
_layouts/
  default.html       → Genel sayfa şablonu (head + nav + içerik + footer + scripts)
  post.html          → Blog yazısı şablonu (özet, içindekiler, S.S.S., ilgili yazılar, yazar kutusu)
  redirect.html      → Eski adresten yeni adrese yönlendirme
_posts/              → BLOG YAZILARI (Markdown) — dosya adı: YYYY-AA-GG-yazi-adi.md
assets/css/style.css → (kaynak stiller)
style.css            → Kök dizindeki stil dosyası
index.html           → Ana sayfa
blog.html            → Blog listesi (adres: /blog/)
404.html             → Özel "sayfa bulunamadı"
r-*.html             → Eski adreslerden yönlendirme dosyaları — SİLME
sitemap.xml, robots.txt → SEO
CNAME                → Özel alan adı — GitHub Pages bunu okur, SİLME
netlify.toml         → Kullanılmıyor (Netlify döneminden kalma)
Gemfile              → Jekyll bağımlılıkları
*.png / *.jpeg / favicon* → Görseller, logolar, favicon'lar (kök dizinde)
```

> Kökteki `banner.html` ve `threads.html`, `_includes/` içindekilerin eski kopyalarıdır;
> hiçbir yerden çağrılmazlar ve `_config.yml`'deki `exclude:` ile yayından çıkarılmıştır.
> Gerçek olanlar `_includes/` içindedir.

> Ayrıntılı, kullanıcıya dönük kurulum notları için `KURULUM.md` dosyasına bakın. Bu dosyayla çelişecek bir değişiklik yaparsan `KURULUM.md`'yi de güncelle.

## Sık yapılan işler — ne nerede düzenlenir

### Menü
`_config.yml` içindeki `nav:` listesi. Tek değişiklik tüm sayfalara yansır — nav'ı elle bir HTML dosyasına yazma. Aktif sekme vurgusu `nav.html` içinde otomatiktir (blog yazılarında "Blog" aktif sayılır).

### İletişim ve adres bilgileri
`_config.yml` içindeki `contact:` (e-posta, Instagram) ve `office:` (ofis adı, adres) bölümleri. `footer.html` ve `head.html` içindeki yapısal veri bu değerlerden okur; bu bilgileri şablonlara elle gömme.

### Yeni blog yazısı ekleme
`_posts/` klasörüne `YYYY-AA-GG-yazi-adi.md` biçiminde bir dosya oluştur. Front matter şablonu:

```yaml
---
title: "Yazı Başlığı"
seo_title: "Arama sonucunda görünecek başlık (opsiyonel)"
description: "Google'da görünecek ~150 karakterlik açıklama."
keywords: "anahtar, kelimeler"
category_name: "Şema Terapi"        # kart etiketi / breadcrumb
thumb: sarmal                       # blog kartı deseni: halkalar | sarmal | dugum | dalga (boşsa yaprak)
thumb_color: t2                     # kart zemini: t1 yeşil | t2 altın | t3 lila | t4 kiremit (boşsa sırayla)
image: "/gorsel-adi.jpg"            # yazı başı görseli, 1280x720, kökte (opsiyonel; paylaşım kartında da kullanılır)
image_alt: "Görselin kısa tarifi"   # görsel varsa erişilebilirlik için
permalink: /yazi-adi/               # adres — .html'siz
excerpt_text: "Blog listesindeki kartta görünecek kısa özet."
summary: "Yazının başındaki Özet kutusunda görünecek metin."
faq:
  - q: "Soru?"
    a: "Cevap."
---

## İlk başlık

Metin...
```

Otomatik olan (elle yapma): İçindekiler tablosu `##` başlıklarından üretilir, okuma süresi ve tarih hesaplanır, ilgili yazılar / blog listesi / sitemap güncellenir, S.S.S. `faq:` alanından oluşur. Yazı yayınlamak için commit + push yeterli.

### Bir yazıyı taşıma / kaldırma
- **Taşıma:** yazının `permalink`'ini değiştir, eski adres için `layout: redirect` kullanan bir `r-*.html` dosyası ekle (`redirect_to` yeni adrese).
- **Kaldırma:** `_posts/` içindeki dosyayı sil. Ziyaretçi eski adrese girerse 404 görür.

## Yerelde önizleme

Zorunlu değil (GitHub Pages derler), ama değişikliği yayına vermeden görmek için kurulu:

```bash
bundle exec jekyll serve
```

Sonra `http://127.0.0.1:4000` adresini aç. Sunucu `--no-watch` ile başlatıldıysa
dosya değişikliğinden sonra yeniden başlatmak gerekir; `_config.yml` değişiklikleri
her hâlükârda yeniden başlatma ister.

Kurulum notları:
- **`Gemfile` repodadır.** Silme.
- `Gemfile.lock`, `vendor/`, `_site/`, `.bundle/` `.gitignore`'dadır.
  `Gemfile.lock` bilerek dışarıdadır: yereldeki eski Bundler (1.x) ile üretiliyor ve
  yayın ortamının daha yeni Ruby'siyle çakışabiliyor.
- Gem'ler proje içine kuruludur (`vendor/bundle`), sistem geneline değil.
- `Gemfile` içindeki `ffi`, `jekyll-sass-converter` ve `sassc` sabitleri **koşulludur**
  (`if RUBY_VERSION < "3.0"`). Yalnızca bu makinedeki eski sistem Ruby'si (2.6) için
  geçerlidir; yayın ortamı daha yeni Ruby kullandığı için orada güncel sürümler kurulur.

## GitHub Pages

- Yayın ayarı: depo → Settings → Pages. Kaynak `main` dalı, özel alan adı `rumeysasaglamer.com`, "Enforce HTTPS" açık.
- Özel alan adı kökteki `CNAME` dosyasından okunur; Settings'teki alan **o dosyayla aynı kalmalıdır**.
- GitHub Pages bir depo başına **tek** özel alan adı sunar. Bu yüzden eski alan adı ayrı bir depodan yönlendiriliyor.
- Derleme başarısız olursa: depo → Actions → `pages-build-deployment` çalışmasına bakılır.

## İçerik yazımı — dil ve ton kuralları

Bu bir ruh sağlığı sitesidir. Tüm ziyaretçiye dönük metinler (yazılar, sayfa metinleri, başlıklar, buton ve menü etiketleri, açıklamalar) aşağıdaki kurallara uymalıdır. Kod yorumları ve teknik dosyalar bu kuralın dışındadır.

### Dil
- Her ziyaretçiye dönük metin **Türkçe** yazılır. İngilizce terim, yer tutucu (`lorem ipsum`) veya çeviri kokan ifade bırakma.
- Türkçe imla ve noktalamaya dikkat et: `ş, ç, ğ, ı, İ, ö, ü` karakterleri doğru kullanılmalı. Başlıklarda ve cümle başlarında büyük "İ" (`İletişim`, `İlişkiler`).
- Sade, akıcı, gündelik ama özenli bir dil. Ağır akademik jargondan ve klinik soğukluktan kaçın; gerekiyorsa terimi açıkla.

### Ton — yargısız ve şefkatli
Yazar, örüntüleri **yargılamadan tanımaya** alan açan bir klinik psikologdur. Metin bu tonu korumalı:

- **Yargılama, etiketleme, patolojikleştirme yok.** Kişiyi ya da yaşadığını "yanlış / bozuk / hastalıklı / zayıf" gibi ifadelerle nitelendirme. "Sorunlu insanlar", "başarısızlık" gibi damgalayıcı dil kullanma.
- **Emir ve reçete değil, davet.** "Şunu yapmalısın", "yapmazsan..." yerine "birlikte bakabiliriz", "fark etmeye alan açar", "isterseniz" gibi davetkâr bir dil.
- **Kesin vaat ve garanti yok.** "Kesin çözer", "tamamen geçer", "X günde iyileşirsiniz" deme. Süreç kişiye göre değişir; belirsizliği dürüstçe ifade et (örn. "kişiye ve konuya göre değişir").
- **Korku, suçluluk ve aciliyet sömürüsü yok.** Kaygı yaratan, suçluluk bindiren veya "hemen şimdi" baskısı kuran satış dili kullanma.
- **Tıbbi/tanısal iddia yok.** Site tanı koymaz, tedavi garantisi vermez. Genel bilgi verir ve görüşmeye davet eder.
- **Kapsayıcı ve saygılı dil.** Okuyucuya saygıyla, çoğunlukla nazik "siz" hitabıyla seslen; sen/siz kullanımında mevcut yazılarla tutarlı ol.

Bir metnin tonundan emin değilsen, mevcut `_posts/` yazılarını referans al — istenen ses tonu oradadır. Yeni metni onların dili, ritmi ve şefkatli tavrıyla uyumlu yaz.

## Genel çalışma ilkeleri

- `_config.yml` tek doğruluk kaynağıdır; site bilgisini şablonlara elle gömmek yerine buradan oku.
- `r-*.html` yönlendirmelerini silme — eski adreslerden gelen ziyaretçiyi taşırlar.
- `CNAME` ve `Gemfile`'ı silme; `CNAME` olmadan alan adı, `Gemfile` olmadan derleme çalışmaz.
- Değişiklikleri yalnızca kullanıcı isteyince commit/push et.
