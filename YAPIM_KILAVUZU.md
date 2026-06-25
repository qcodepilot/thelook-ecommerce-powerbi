# 🚀 TheLook E-ticaret — Power BI Yapım Kılavuzu (TAM KAPSAM)

> **Hedef:** 5 iş alanını kapsayan eksiksiz bir Power BI raporu (öğrenme amaçlı tam build).
> **Kapsam:** Satış · Müşteri · Envanter/Ürün · Web Sitesi · Pazarlama
> **Tablolar:** 7 tablo (`events` dahil) · `thelook_ecommerce-table` silindi (şemasız/bozuk)
> Her DAX kopyala-yapıştır hazır. Sırayla git, kutucukları işaretle.

---

## ✅ İLERLEME TAKİP LİSTESİ
- [x] FAZ 1 — Veri içe aktarma (7 tablo, BigQuery)
- [ ] FAZ 2 — Power Query temizlik + tipler
- [ ] FAZ 3 — Model & ilişkiler + Tarih tablosu
- [ ] FAZ 4 — Measure'lar (DAX)
- [ ] FAZ 5 — Sayfa 1: Satış Performansı
- [ ] FAZ 6 — Sayfa 2: Müşteri Davranışı
- [ ] FAZ 7 — Sayfa 3: Envanter / Ürün
- [ ] FAZ 8 — Sayfa 4: Web Sitesi Performansı
- [ ] FAZ 9 — Sayfa 5: Pazarlama Etkinliği
- [ ] FAZ 10 — İçgörü & öneri metinleri + cila + teslim

---

## FAZ 2 — Power Query Temizlik

Her tablo için kontrol et:
1. **Veri tipleri:**
   - Tarihler (`created_at`, `shipped_at`, `delivered_at`, `returned_at`, `sold_at`) → **Tarih/Saat**
   - Para (`sale_price`, `cost`, `retail_price`, `product_retail_price`) → **Ondalık Sayı**
   - `id`, `user_id`, `order_id`, `product_id`, `age`, `num_of_item` → **Tam Sayı**
2. **Boş değerler:** `returned_at`, `sold_at`, `delivered_at`, `events[user_id]` boş olabilir — NORMAL, silme.
3. **Metin temizliği:** `category`, `brand`, `status`, `traffic_source` → **Dönüştür > Biçim > Kırp + Temizle**.
4. **events tablosu yüklemesi AÇIK olmalı** (Web/Pazarlama için gerekli).
5. Bitince **Kapat ve Uygula**.

---

## FAZ 3 — Model & İlişkiler

**Model görünümü.** İlişkiler (hepsi *Bir→Çok*, tek yön):

| Bir (1) | → | Çok (*) |
|---|---|---|
| `orders[order_id]` | → | `order_items[order_id]` |
| `users[id]` | → | `orders[user_id]` |
| `users[id]` | → | `order_items[user_id]` |
| `users[id]` | → | `events[user_id]` |
| `products[id]` | → | `order_items[product_id]` |
| `products[id]` | → | `inventory_items[product_id]` |
| `inventory_items[id]` | → | `order_items[inventory_item_id]` |
| `distribution_centers[id]` | → | `products[distribution_center_id]` |
| `distribution_centers[id]` | → | `inventory_items[product_distribution_center_id]` |

> Çift yol oluşursa (ör. users→orders→order_items + users→order_items) Power BI uyarır; birini **pasif** yap veya gerektiğinde USERELATIONSHIP kullan.

### Tarih Tablosu (Modelleme > Yeni Tablo)
```DAX
Tarih =
ADDCOLUMNS(
    CALENDAR(DATE(2019,1,1), DATE(2024,12,31)),
    "Yıl", YEAR([Date]),
    "Ay No", MONTH([Date]),
    "Ay", FORMAT([Date], "MMM"),
    "Yıl-Ay", FORMAT([Date], "YYYY-MM"),
    "Çeyrek", "Ç" & FORMAT([Date], "Q"),
    "Hafta Günü No", WEEKDAY([Date], 2),
    "Hafta Günü", FORMAT([Date], "ddd"),
    "Hafta Sonu mu", IF(WEEKDAY([Date],2) >= 6, "Hafta Sonu", "Hafta İçi")
)
```
İlişki: `Tarih[Date]` (1) → `order_items[created_at]` (*). Sonra **Tarih tablosu olarak işaretle**.

---

## FAZ 4 — Measure'lar (DAX)

> İpucu: Tüm measure'ları toplamak için boş bir tablo oluştur (Veri Gir > "Ölçüler") ve measure'ları oraya koy. Düzenli durur.

### 📈 Satış
```DAX
Toplam Satış = SUM('order_items'[sale_price])
```
```DAX
Net Satış (İptal/İade Hariç) =
CALCULATE(SUM('order_items'[sale_price]),
    NOT 'order_items'[status] IN {"Cancelled","Returned"})
```
```DAX
Sipariş Sayısı = DISTINCTCOUNT('order_items'[order_id])
```
```DAX
Satılan Ürün Adedi = COUNTROWS('order_items')
```
```DAX
Ortalama Sipariş Değeri = DIVIDE([Toplam Satış], [Sipariş Sayısı])
```
```DAX
Ortalama Satış Fiyatı = AVERAGE('order_items'[sale_price])
```

### 💰 Kâr
```DAX
Toplam Maliyet = SUMX('order_items', RELATED('products'[cost]))
```
```DAX
Toplam Kâr = [Toplam Satış] - [Toplam Maliyet]
```
```DAX
Kâr Marjı % = DIVIDE([Toplam Kâr], [Toplam Satış])
```

### 👥 Müşteri
```DAX
Müşteri Sayısı = DISTINCTCOUNT('order_items'[user_id])
```
```DAX
Müşteri Başına Ort. Gelir = DIVIDE([Toplam Satış], [Müşteri Sayısı])
```
Hesaplanan sütun — `users` tablosunda:
```DAX
Toplam Harcama = CALCULATE(SUM('order_items'[sale_price]))
```
```DAX
Harcama Segmenti =
VAR h = 'users'[Toplam Harcama]
RETURN IF(ISBLANK(h), "Alışveriş Yok",
    IF(h < 100, "Düşük", IF(h < 500, "Orta", "Yüksek")))
```

### 📦 Envanter / Ürün
```DAX
İade Oranı =
DIVIDE(CALCULATE(COUNTROWS('order_items'), 'order_items'[status]="Returned"),
    COUNTROWS('order_items'), 0)
```
```DAX
Stoktaki Ürün Adedi = CALCULATE(COUNTROWS('inventory_items'), ISBLANK('inventory_items'[sold_at]))
```
```DAX
Satılan Stok Adedi = CALCULATE(COUNTROWS('inventory_items'), NOT ISBLANK('inventory_items'[sold_at]))
```

### 🌐 Web / 📣 Pazarlama (events)
```DAX
Toplam Olay = COUNTROWS('events')
```
```DAX
Oturum Sayısı = DISTINCTCOUNT('events'[session_id])
```
```DAX
Satın Alan Oturum =
CALCULATE(DISTINCTCOUNT('events'[session_id]), 'events'[event_type]="purchase")
```
```DAX
Dönüşüm Oranı = DIVIDE([Satın Alan Oturum], [Oturum Sayısı])
```
> ⚠️ **Dürüstlük notu:** TheLook'ta reklam **harcaması** verisi YOK. Bu yüzden gerçek **ROI/CAC hesaplanamaz.** Pazarlamayı kanal bazlı **gelir** ve **müşteri sayısı** ile vekil (proxy) olarak ölçeriz. Bunu sunumda belirt = analist olgunluğu.

---

## FAZ 5 — Sayfa 1: 📈 Satış Performansı
| Görsel | Alan/Measure |
|---|---|
| KPI ×4 | Toplam Satış · Toplam Kâr · Sipariş Sayısı · Ort. Sipariş Değeri |
| Çizgi (aylık trend) | X: `Tarih[Yıl-Ay]` · Y: Toplam Satış |
| Çubuk (top kategori) | Y: `products[category]` · X: Toplam Satış (Üst 10) |
| Çubuk (ort. fiyat/kategori) | Y: `products[category]` · X: Ort. Satış Fiyatı |
| Sütun (hafta içi/sonu) | X: `Tarih[Hafta Sonu mu]` · Y: Toplam Satış |
| Slicer | `Tarih[Yıl]` |

## FAZ 6 — Sayfa 2: 👥 Müşteri Davranışı
| Görsel | Alan/Measure |
|---|---|
| KPI ×2 | Müşteri Sayısı · Müşteri Başına Ort. Gelir |
| Halka (segment) | `users[Harcama Segmenti]` · Müşteri Sayısı |
| Çubuk (cinsiyet) | `users[gender]` · Toplam Satış |
| Harita (coğrafya) | Konum: `users[country]`/enlem-boylam · Boyut: Müşteri Sayısı |
| Histogram (yaş) | `users[age]` gruplu · Müşteri Sayısı |

## FAZ 7 — Sayfa 3: 📦 Envanter / Ürün
| Görsel | Alan/Measure |
|---|---|
| KPI ×2 | İade Oranı · Kâr Marjı % |
| Çubuk (en çok iade) | `products[name]` · İade Oranı (Üst 10) |
| Çubuk (en kârlı kategori) | `products[category]` · Toplam Kâr |
| Top 5 envanter kategorisi | `inventory_items[product_category]` · Stoktaki Ürün Adedi (Üst 5) |
| Tablo (marka) | `products[brand]` · Toplam Satış · Kâr Marjı % · İade Oranı |

## FAZ 8 — Sayfa 4: 🌐 Web Sitesi Performansı
| Görsel | Alan/Measure |
|---|---|
| KPI ×3 | Oturum Sayısı · Dönüşüm Oranı · Toplam Olay |
| Çizgi (oturum trendi) | X: `Tarih[Yıl-Ay]` · Y: Oturum Sayısı |
| Huni/çubuk (event_type akışı) | `events[event_type]` · Toplam Olay |
| Çubuk (tarayıcı) | `events[browser]` · Oturum Sayısı |

## FAZ 9 — Sayfa 5: 📣 Pazarlama Etkinliği
| Görsel | Alan/Measure |
|---|---|
| Çubuk (kanal→satış) | `users[traffic_source]` · Toplam Satış |
| Çubuk (kanal→müşteri) | `users[traffic_source]` · Müşteri Sayısı |
| Çubuk (trafik kaynağı→oturum) | `events[traffic_source]` · Oturum Sayısı |
| Tablo (kanal performansı) | `traffic_source` · Müşteri Sayısı · Toplam Satış · Müşteri Başına Gelir |

---

## FAZ 10 — İçgörü & Öneri + Teslim
- Her sayfaya 1 metin kutusu: "ne anlatıyor + 1 öneri"
- Son sayfa: Problem ifadesi → Bulgular → Uygulanabilir öneriler
- Tutarlı tema, başlıklar, sayfa adları
- `.pbix` kaydet → repo'ya, PDF dışa aktar
- **ÖNEMLİ:** Grafik sayısı değil, **yorum** önemli. Rolün veriyi anlamlandırmak.
