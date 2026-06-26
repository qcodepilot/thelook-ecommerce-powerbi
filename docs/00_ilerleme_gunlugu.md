# 📒 İlerleme Günlüğü — Ne Yaptık?

> Projede attığımız adımların kaydı. Her anlamlı adımdan sonra güncellenir.

## 📍 KALDIĞIMIZ YER (buradan devam)
**Tamamlanan:** FAZ 1-4 (veri+model+measure) + **Sayfa 1 Satış** (5 KPI, trend, top kategori, ort. fiyat) + **Sayfa 2 Müşteri** (segment halkası, müşteri başı gelir, coğrafi treemap, cinsiyet, yaş). Tüm içgörüler `docs/06_sunum_anlatimi.md`'de.
**Sıradaki adım:** Sayfa 5 — Pazarlama (kanal→satış, kanal→müşteri, trafik kaynağı→oturum). Son sayfa! Sonra cila + teslim. Sayfa 4 (Web) tamam: Oturum/Dönüşüm KPI, dönüşüm hunisi (sepet terki bulgusu), tarayıcı.
**Önemli teknik not:** Tarih tablosu ilişkisi datetime/date sorunu yaşattı; çözüm = grafiklerde `order_items[created_at]` veya `Sipariş Ay` (FORMAT) sütununu doğrudan kullan, Tarih ilişkisine güvenme. Hafta içi/sonu için order_items'a DAX sütun eklenebilir.
**Not:** `.pbix` yerelde kayıtlı (GitHub'da değil — büyük dosya). Azure harita bölge kısıtı → coğrafya için treemap kullanıldı.

## ✅ Tamamlanan
| # | Adım | Açıklama |
|---|------|----------|
| 1 | Proje kurulumu | Gereksinimler okundu, kapsam belirlendi: **3 sayfa** (Satış, Müşteri, Ürün) |
| 2 | GitHub repo | `thelook-ecommerce-powerbi` oluşturuldu, README + .gitignore + kılavuz push edildi |
| 3 | Veri kaynağı | Power BI → Google BigQuery → `bigquery-public-data.thelook_ecommerce` bağlandı |
| 4 | Tablo seçimi | 6 tablo seçildi (`order_items, orders, users, products, inventory_items, distribution_centers`); `events` ve kopya tablo dışlandı |
| 5 | Veri keşfi (EDA) | Veri sözlüğü + ilişki haritası dokümante edildi → `docs/01_veri_kesfi_ve_iliskiler.md` |
| 6 | 8 tablo Power Query'ye alındı | Öğrenme amacıyla 8 tablonun hepsi içe aktarıldı; 2'sini (events + kopya tablo) **inceleyerek** eleme kararı verilecek |
| 7 | EDA araçları açıldı | Görünüm > Sütun kalitesi / dağılımı / profili aktif edildi (veri kalitesi kontrolü) |
| 8 | FAZ 2 tamamlandı | 7 tablo tip kontrolü yapıldı (hepsi doğru); veri temiz (tekrar/eksik sorunu yok); events tutuldu, kopya tablo silindi |

## ⏳ Sıradaki adımlar
- [x] FAZ 2 — Power Query: inceleme + tip kontrolü tamam (detay: `docs/02_power_query_temizlik.md`)
- [x] Kapat ve Uygula → 7 tablo modele yüklendi
- [x] FAZ 3 (ilişkiler) — 6 ilişkilik temiz star schema kuruldu (detay: `docs/03_model_iliskiler.md`)
- [x] FAZ 3 (devam) — Tarih tablosu oluşturuldu + order_items[created_at]'e bağlandı ("tarih tablosu olarak işaretle" opsiyonel, atlandı)
- [x] FAZ 4 — 14 measure + 2 segment sütunu yazıldı (referans: `docs/04_dax_kutuphanesi.md`)
- [x] FAZ 5 — Sayfa 1 Satış Performansı: 4 KPI + aylık trend + top kategoriler + ort. fiyat/kategori. İçgörüler script'te.
- [ ] FAZ 6 — Sayfa 2: Müşteri Davranışı
- [ ] FAZ 3 — Model & ilişkiler + Tarih tablosu
- [ ] FAZ 4 — DAX measure'lar
- [ ] FAZ 5-7 — 3 sayfa görselleştirme
- [ ] FAZ 8 — İçgörü & öneri metinleri
- [ ] FAZ 9 — Cila + .pbix kaydet + sunum

## 🧠 Önemli kararlar (neden böyle yaptık)
- **Kapsam: 5 alan (tam build):** Proje 2-3 seç diyor ama bu 3 kişilik ekip projesi; Ömür hepsini öğrenmek için tek başına yapıyor, sonra kendi payını çekecek. Herkes kendi .pbix'ini yapıyor.
- **events TUTULUYOR:** Web Sitesi + Pazarlama alanları için gerekli. (Önceki "devre dışı" kararı, kapsam genişleyince güncellendi.)
- **thelook_ecommerce-table silindi:** Şemasız/bozuk (DataSource hatası), yüklenemiyor.
- **Veri Dönüştürme > Yükle:** Veriyi modele almadan önce temizlemek için.
- **bigquery-public-data'dan direkt okuma:** Kendi projemize kopyalamaya gerek yok; fatura `third-harbor-301722`'den düşer.
