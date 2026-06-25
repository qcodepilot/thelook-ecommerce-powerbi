# 🔗 FAZ 3 — Veri Modeli & İlişkiler

## Kurulan ilişkiler (6) — temiz star schema

| # | Bir (1) — PK | Çok (*) — FK | Kardinalite | Yön |
|---|---|---|---|---|
| 1 | `orders[order_id]` | `order_items[order_id]` | 1:* | Tek |
| 2 | `users[id]` | `orders[user_id]` | 1:* | Tek |
| 3 | `products[id]` | `order_items[product_id]` | 1:* | Tek |
| 4 | `distribution_centers[id]` | `products[distribution_center_id]` | 1:* | Tek |
| 5 | `distribution_centers[id]` | `inventory_items[product_distribution_center_id]` | 1:* | Tek |
| 6 | `users[id]` | `events[user_id]` | 1:* | Tek |

```
   users ──1:*── orders ──1:*── order_items ──*:1── products ──*:1── distribution_centers
     │                            (FACT)                                      │
     └──1:*── events                              inventory_items ──*:1───────┘
```

## 🧠 Kararların gerekçesi (neden böyle?)
- **PK ↔ FK kuralı:** "1" tarafı boyut tablosunun benzersiz `id`'si (PK); "*" tarafı ona işaret eden `<şey>_id` (FK).
- **Bilerek KURULMAYAN ilişkiler (ambiguity önlemek için):**
  - `users → order_items` (direkt): gereksiz, çünkü `users → orders → order_items` zaten var. İkisi birden çift yol yaratır.
  - `products → inventory_items` ve `inventory_items → order_items`: `inventory_items` zaten kendi içinde `product_category`/`product_brand` denormalize tutuyor; bağlamak çift yol (loop) yaratırdı.
- **events.user_id null'ları:** Anonim ziyaretçiler. İlişki yalnızca "1" tarafının (users[id]) benzersizliğine bakar; "*" tarafındaki null'lar sorun değil, hata vermez.
- **Sonuç:** Tertemiz yıldız şeması — çift yol yok, uyarı yok. Tüm 5 analiz alanı bu zeminden beslenebilir.

## Sıradaki: Tarih tablosu
`CALENDAR` ile Tarih tablosu oluşturulup `order_items[created_at]`'e bağlanacak (zaman analizi için).
