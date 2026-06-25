# 📚 DAX Kütüphanesi (tekrar kullanılabilir)

> Bu projede yazdığımız tüm DAX kodları. Her biri başka projelerde de kullanılabilir.
> Kopyala-yapıştır hazır. Türkçe Power BI ayıracı `;` isterse virgülleri `;` yap.

---

## 📅 Tarih (Calendar) Tablosu — HER PROJEDE KULLANILIR ⭐
Modelleme > Yeni Tablo. Tek başına bir takvim üretir; tarih aralığını verine göre ayarla.
```DAX
Tarih =
ADDCOLUMNS(
    CALENDAR(DATE(2019,1,1), DATE(2026,12,31)),
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
**Kurulum:** `Tarih[Date]` → `order_items[created_at]` ilişkisi + "Tarih tablosu olarak işaretle".
**Neden:** Zaman analizi (aylık trend, mevsimsellik, hafta içi/sonu) ve zaman-zekası fonksiyonları için ayrı takvim şart.

---

## 📈 Satış Measure'ları
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

## 💰 Kâr Measure'ları
```DAX
Toplam Maliyet = SUMX('order_items', RELATED('products'[cost]))
```
```DAX
Toplam Kâr = [Toplam Satış] - [Toplam Maliyet]
```
```DAX
Kâr Marjı % = DIVIDE([Toplam Kâr], [Toplam Satış])
```

## 👥 Müşteri
```DAX
Müşteri Sayısı = DISTINCTCOUNT('order_items'[user_id])
```
```DAX
Müşteri Başına Ort. Gelir = DIVIDE([Toplam Satış], [Müşteri Sayısı])
```
Hesaplanan sütun (`users` tablosunda):
```DAX
Toplam Harcama = CALCULATE(SUM('order_items'[sale_price]))
```
```DAX
Harcama Segmenti =
VAR h = 'users'[Toplam Harcama]
RETURN IF(ISBLANK(h), "Alışveriş Yok",
    IF(h < 100, "Düşük", IF(h < 500, "Orta", "Yüksek")))
```

## 📦 Envanter / Ürün
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

## 🌐 Web / 📣 Pazarlama
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

> **Durum:** Tarih tablosu ✅ oluşturuldu. Measure'lar FAZ 4'te tek tek eklenecek (yukarıdakiler hazır referans).
