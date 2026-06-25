# 🚀 TheLook E-ticaret — Power BI Yapım Kılavuzu (1 Günde Teslim)

> **Hedef:** 3 sayfalık, içgörü + öneri içeren bir Power BI raporu.
> **Kapsam:** (1) Satış Performansı · (2) Müşteri Davranışı · (3) Ürün Performansı
> Her DAX/adım kopyala-yapıştır hazır. Sırayla git, kutucukları işaretle.

---

## ✅ İLERLEME TAKİP LİSTESİ
- [ ] FAZ 1 — Veri içe aktarma (BigQuery veya CSV)
- [ ] FAZ 2 — Power Query temizlik
- [ ] FAZ 3 — Model & ilişkiler + Tarih tablosu
- [ ] FAZ 4 — Measure'lar (DAX)
- [ ] FAZ 5 — Sayfa 1: Satış
- [ ] FAZ 6 — Sayfa 2: Müşteri
- [ ] FAZ 7 — Sayfa 3: Ürün
- [ ] FAZ 8 — İçgörü & öneri metinleri + cila
- [ ] FAZ 9 — Sunum / teslim

---

## FAZ 1 — Veri İçe Aktarma

**Kullanacağımız 6 tablo:** `orders`, `order_items`, `products`, `users`, `inventory_items`, `distribution_centers`
(`events` tablosunu KULLANMIYORUZ — çok büyük ve seçtiğimiz 3 vaka için gerekmiyor.)

### Seçenek A — BigQuery (proje gereksinimi, sende kurulu)
1. Power BI Desktop → **Ana Sayfa > Veri Al > Daha Fazla > Google BigQuery**.
2. Google hesabınla giriş yap.
3. `bigquery-public-data` > `thelook_ecommerce` altından yukarıdaki **6 tabloyu** seç.
4. **Yükle** değil → **Verileri Dönüştür** (Power Query açılsın, FAZ 2 için).

> ⚠️ BigQuery bağlantısı auth/yavaşlık sorunu çıkarırsa → **Seçenek B**'ye geç (5 dk).

### Seçenek B — Kaggle CSV (yedek, en hızlı)
1. https://www.kaggle.com/datasets/mustafakeser4/looker-ecommerce-bigquery-dataset → indir.
2. Power BI → **Veri Al > Metin/CSV** → 6 CSV'yi tek tek ekle.
3. Her birinde **Verileri Dönüştür**.

---

## FAZ 2 — Power Query Temizlik

Her tablo için Power Query'de kontrol et:

1. **Veri tipleri doğru mu?**
   - `created_at`, `shipped_at`, `delivered_at`, `returned_at`, `sold_at` → **Tarih/Saat**
   - `sale_price`, `cost`, `retail_price`, `product_retail_price` → **Ondalık Sayı**
   - `id`, `user_id`, `order_id`, `product_id` → **Tam Sayı**
2. **Boş/null:** `returned_at`, `sold_at`, `delivered_at` boş olması NORMAL (iade edilmemiş / satılmamış / teslim edilmemiş demek). Silme!
3. **Metin temizliği:** `category`, `brand`, `status` sütunlarında → **Dönüştür > Biçim > Kırp (Trim)** + **Temizle (Clean)**.
4. **Gereksiz sütun yok** — hepsini tut, sonra gizleriz.
5. Bitince **Ana Sayfa > Kapat ve Uygula**.

---

## FAZ 3 — Model & İlişkiler

**Model görünümü**ne geç. Şu ilişkileri kontrol et / kur (hepsi *Bir-Çok*, tek yön):

| Bir (1) tarafı | Çok (*) tarafı |
|---|---|
| `orders[order_id]` | `order_items[order_id]` |
| `users[id]` | `order_items[user_id]` |
| `users[id]` | `orders[user_id]` |
| `products[id]` | `order_items[product_id]` |
| `products[id]` | `inventory_items[product_id]` |
| `distribution_centers[id]` | `products[distribution_center_id]` |

> İlişki kurmak için: bir alanı sürükleyip diğerinin üzerine bırak. Çift tıklayıp yönü **Tek (Single)** yap.

### Tarih Tablosu (önerilir — trend grafiklerini düzgün yapar)
**Modelleme > Yeni Tablo:**
```DAX
Tarih =
ADDCOLUMNS(
    CALENDAR(DATE(2019,1,1), DATE(2024,12,31)),
    "Yıl", YEAR([Date]),
    "Ay No", MONTH([Date]),
    "Ay", FORMAT([Date], "MMM"),
    "Yıl-Ay", FORMAT([Date], "YYYY-MM"),
    "Çeyrek", "Ç" & FORMAT([Date], "Q")
)
```
Sonra: `Tarih[Date]` (1) → `order_items[created_at]` (*) ilişkisi kur.
`Tarih` tablosunu **Tarih Tablosu Olarak İşaretle** (Tablo araçları > Tarih tablosu olarak işaretle > Date).

---

## FAZ 4 — Measure'lar (DAX)

`order_items` tablosuna sağ tık > **Yeni ölçü**. Her birini tek tek yapıştır.

```DAX
Toplam Satış = SUM('order_items'[sale_price])
```
```DAX
Net Satış (İptal Hariç) =
CALCULATE(
    SUM('order_items'[sale_price]),
    NOT 'order_items'[status] IN {"Cancelled", "Returned"}
)
```
```DAX
Sipariş Sayısı = DISTINCTCOUNT('order_items'[order_id])
```
```DAX
Müşteri Sayısı = DISTINCTCOUNT('order_items'[user_id])
```
```DAX
Ortalama Sipariş Değeri = DIVIDE([Toplam Satış], [Sipariş Sayısı])
```
```DAX
Ortalama Satış Fiyatı = AVERAGE('order_items'[sale_price])
```
```DAX
Toplam Maliyet = SUMX('order_items', RELATED('products'[cost]))
```
```DAX
Toplam Kâr = [Toplam Satış] - [Toplam Maliyet]
```
```DAX
Kâr Marjı % = DIVIDE([Toplam Kâr], [Toplam Satış])
```
```DAX
Satılan Ürün Adedi = COUNTROWS('order_items')
```
```DAX
İade Oranı =
DIVIDE(
    CALCULATE(COUNTROWS('order_items'), 'order_items'[status] = "Returned"),
    COUNTROWS('order_items'),
    0
)
```

### Müşteri segmentasyonu (HESAPLANAN SÜTUN — `users` tablosunda)
`users` tablosu > **Yeni sütun**:
```DAX
Toplam Harcama = CALCULATE(SUM('order_items'[sale_price]))
```
```DAX
Harcama Segmenti =
VAR h = 'users'[Toplam Harcama]
RETURN
    IF(ISBLANK(h), "Alışveriş Yok",
        IF(h < 100, "Düşük",
            IF(h < 500, "Orta", "Yüksek")))
```

---

## FAZ 5 — Sayfa 1: 📈 Satış Performansı

| Görsel | Alan / Measure |
|---|---|
| **KPI Kartı** ×4 | Toplam Satış · Toplam Kâr · Sipariş Sayısı · Ort. Sipariş Değeri |
| **Çizgi grafiği** (Aylık trend) | X: `Tarih[Yıl-Ay]` · Y: `Toplam Satış` |
| **Çubuk grafiği** (Top kategori) | Y: `products[category]` · X: `Toplam Satış` · Filtre: Üst 10 |
| **Çubuk grafiği** (Ort. fiyat/kategori) | Y: `products[category]` · X: `Ortalama Satış Fiyatı` |
| **Dilimleyici (Slicer)** | `Tarih[Yıl]` |

> 💡 İptal/iade siparişler trende dahil mi? Karar senin — kararını sunumda 1 cümleyle belirt.

---

## FAZ 6 — Sayfa 2: 👥 Müşteri Davranışı

| Görsel | Alan / Measure |
|---|---|
| **KPI Kartı** ×2 | Müşteri Sayısı · Ort. Sipariş Değeri |
| **Pasta/Halka** (Segment dağılımı) | Açıklama: `users[Harcama Segmenti]` · Değer: Müşteri Sayısı |
| **Yığılmış çubuk** (Cinsiyete göre satış) | Eksen: `users[gender]` · Değer: Toplam Satış |
| **Harita** (Coğrafi dağılım) | Konum: `users[country]` veya enlem/boylam · Boyut: Müşteri Sayısı |
| **Dilimleyici** | `users[age]` veya `Harcama Segmenti` |

> 🗺️ Harita çalışmazsa: Dosya > Seçenekler > Güvenlik > **Harita ve Alan Harita görsellerini kullan** ✔ (ekranını açmıştın) > Tamam > Yenile.

---

## FAZ 7 — Sayfa 3: 📦 Ürün Performansı

| Görsel | Alan / Measure |
|---|---|
| **KPI Kartı** ×2 | İade Oranı · Kâr Marjı % |
| **Çubuk** (En çok iade edilen ürün) | Y: `products[name]` · X: `İade Oranı` · Üst 10 |
| **Çubuk** (En kârlı kategori) | Y: `products[category]` · X: `Toplam Kâr` |
| **Tablo** (Marka performansı) | `products[brand]` · Toplam Satış · Kâr Marjı % · İade Oranı |
| **Top 5 Envanter kategorisi** | `inventory_items[product_category]` · Adet sayımı · Üst 5 |

---

## FAZ 8 — İçgörü & Öneri Metinleri

Her sayfaya 1 **Metin kutusu** ekle: "Bu sayfa ne anlatıyor + 1 öneri."
Son sayfa (veya sunum) için iskelet:

1. **Problem ifadesi:** "TheLook'un satış müdürü olarak hangi kategoriye yatırım yapmalıyız?"
2. **Bulgular:** En çok satan 3 kategori, en kârlı marka, en yüksek iadeli ürün.
3. **Öneriler (uygulanabilir):**
   - Yüksek marjlı + yüksek satışlı kategoriye reklam bütçesi.
   - Yüksek iadeli ürünlerde kalite/beden sorunu araştır.
   - "Yüksek" segment müşterilere sadakat programı.

---

## FAZ 9 — Cila & Teslim
- [ ] Tüm sayfalara başlık ekle
- [ ] Tutarlı renk teması (Görünüm > Temalar)
- [ ] Sayfa adlarını düzelt (Satış / Müşteri / Ürün)
- [ ] `.pbix` kaydet → proje klasörüne
- [ ] (İstenirse) PDF olarak dışa aktar: Dosya > Dışa Aktar > PDF
