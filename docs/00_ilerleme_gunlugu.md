# 📒 İlerleme Günlüğü — Ne Yaptık?

> Projede attığımız adımların kaydı. Her anlamlı adımdan sonra güncellenir.

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

## ⏳ Sıradaki adımlar
- [ ] FAZ 2 — Power Query: tablo inceleme + eleme + tip kontrolü + temizlik (detay: `docs/02_power_query_temizlik.md`)
- [ ] FAZ 3 — Model & ilişkiler + Tarih tablosu
- [ ] FAZ 4 — DAX measure'lar
- [ ] FAZ 5-7 — 3 sayfa görselleştirme
- [ ] FAZ 8 — İçgörü & öneri metinleri
- [ ] FAZ 9 — Cila + .pbix kaydet + sunum

## 🧠 Önemli kararlar (neden böyle yaptık)
- **Sadece 6 tablo:** Proje "hepsini kapsama, en ilgilileri seç" diyor. `events` çok büyük, kopya tablo modeli bozar.
- **Veri Dönüştürme > Yükle:** Veriyi modele almadan önce temizlemek için.
- **bigquery-public-data'dan direkt okuma:** Kendi projemize kopyalamaya gerek yok; fatura `third-harbor-301722`'den düşer.
