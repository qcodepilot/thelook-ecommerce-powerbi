# 🛍️ TheLook E-ticaret — Power BI Veri Analizi & İçgörü Çıkarma

> Workintech Veri Analitiği Bootcamp — Proje 1
> Power BI kullanarak TheLook e-ticaret veri setinin analizi, KPI hesaplama ve işletmeye yönelik uygulanabilir öneriler.

## 📊 Proje Hakkında
TheLook, kurgusal bir e-ticaret giyim perakendecisidir. Bu projede müşteri, ürün, sipariş, envanter ve web verileri analiz edilerek iş kararlarını destekleyecek içgörüler çıkarılmıştır.

**Veri kaynağı:** Google BigQuery `bigquery-public-data.thelook_ecommerce`
([Kaggle mirror](https://www.kaggle.com/datasets/mustafakeser4/looker-ecommerce-bigquery-dataset)) · **7 tablo** (events dahil)

## 🎯 Analiz Kapsamı (5 sayfa)
| Sayfa | Odak | İçerik |
|-------|------|--------|
| 1 | 📈 Satış Performansı | Aylık trend, top kategoriler, ort. fiyat, hafta içi/sonu |
| 2 | 👥 Müşteri Davranışı | Harcama segmenti, coğrafya, cinsiyet, yaş, tek-seferlik/tekrar-eden |
| 3 | 📦 Envanter / Ürün | İade oranı, kâr/kategori, top 5 stok, stok-satış uyumsuzluğu |
| 4 | 🌐 Web Sitesi | Oturum, dönüşüm oranı, dönüşüm hunisi, tarayıcı |
| 5 | 📣 Pazarlama | Kanal→satış, kanal→müşteri, kanal performans tablosu |

## 💡 Öne Çıkan İçgörüler
- **Büyüme:** Satış 2019→2026 istikrarlı yükselişte; kâr marjı sağlıklı **%52**.
- **Şampiyon kategori:** Outerwear & Coats hem en çok satan hem en kârlı.
- **Sadakat altın:** Tekrar eden müşteriler (%38) cironun **%60'ını** üretiyor; müşteri başına **2,5x** değerli.
- **Envanter uyumsuzluğu:** Intimates fazla stokta beklerken, en kârlı Outerwear stok-out riskinde.
- **Sepet terki:** Ziyaretçiler sepete kadar geliyor ama ödemede kaçıyor (web hunisi).
- **Pazarlama:** Search açık ara en güçlü kanal; kanal kalitesi homojen (~136$/müşteri).

## 🚀 Öneriler
1. Yüksek değerli kategorilere (Outerwear, Jeans) yatırımı sürdür; Intimates stoğunu azalt.
2. **Müşteri elde tutmaya** odaklan: ilk alışveriş sonrası sadakat programı + ikinci-sipariş indirimi.
3. **Sepet terkini** azalt: ödeme adımlarını sadeleştir + terk edenlere retargeting.
4. Search/SEO'ya yatırımı koru; Email/Display gibi verimli küçük kanalları büyüt.

## 🧮 Kullanılan Teknikler
- **Power Query:** Veri inceleme, tip kontrolü, kalite doğrulama
- **Veri modelleme:** Star schema (6 ilişki), Tarih tablosu, PK↔FK
- **DAX:** 14 measure + 6 hesaplanan sütun (Toplam Satış, Kâr Marjı, İade Oranı, Dönüşüm Oranı, segmentasyon, müşteri tipi…)
- **Görselleştirme:** KPI kartı, çizgi/çubuk, halka, treemap, huni, tablo, cross-filter

## 📁 Dosyalar & Dokümantasyon
- `TheLook_Analiz.pbix` — Power BI rapor dosyası (büyük dosya; repoda değil)
- [`YAPIM_KILAVUZU.md`](YAPIM_KILAVUZU.md) — adım adım tam yapım kılavuzu
- [`docs/`](docs/) — detaylı dokümantasyon:
  - [00 İlerleme günlüğü](docs/00_ilerleme_gunlugu.md)
  - [01 Veri sözlüğü & ilişkiler](docs/01_veri_kesfi_ve_iliskiler.md)
  - [02 Power Query temizlik](docs/02_power_query_temizlik.md)
  - [03 Model & ilişkiler](docs/03_model_iliskiler.md)
  - [04 DAX kütüphanesi](docs/04_dax_kutuphanesi.md)
  - [05 Öğrenme notları (benzetmeler)](docs/05_ogrenme_notlari.md)
  - [06 Sunum anlatım scripti](docs/06_sunum_anlatimi.md)
  - [07 Soru kapsama belgesi](docs/07_soru_kapsama.md)
- [`ogrenme_yolculugu/`](ogrenme_yolculugu/) — bu projeyi nasıl öğrendiğimin kaydı

---
👤 **Hazırlayan:** Ömür Yalçın Mutlu · Workintech Veri Analitiği
