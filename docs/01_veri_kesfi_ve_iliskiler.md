# 🔍 Veri Keşfi & Tablo İlişkileri (EDA)

> TheLook e-ticaret veri seti — kullandığımız 6 tablonun sözlüğü ve aralarındaki ilişkiler.
> Amaç: "Hangi tabloda ne var, her sütun ne işe yarar, bununla hangi soruyu cevaplarız?"

## 📦 Kullandığımız tablolar (6) + atladıklarımız (2)

| Tablo | Rolü | Alıyor muyuz? |
|-------|------|:---:|
| `order_items` | **Olgu (Fact)** — satış olayları | ✅ |
| `orders` | Sipariş başlığı | ✅ |
| `users` | Müşteri (boyut) | ✅ |
| `products` | Ürün (boyut) | ✅ |
| `inventory_items` | Envanter/stok | ✅ |
| `distribution_centers` | Dağıtım merkezi (boyut) | ✅ |
| `events` | Web olayları (2M+ satır) | ❌ kapsam dışı |
| `thelook_ecommerce-table` | Denormalize kopya tablo | ❌ modeli bozar |

---

## 🌟 Veri Modeli Mantığı: Star Schema (Yıldız Şeması)

Merkezde **olay/olgu** tablosu (`order_items`), çevresinde onu **açıklayan boyut** tabloları var:

```
                 ┌──────────────┐
                 │    orders     │
                 └──────┬───────┘
                        │ order_id
        users           │            products
   ┌────────────┐       │        ┌────────────┐
   │   users    │──user_id──┐    │  products  │
   └────────────┘       │   │    └─────┬──────┘
                  ┌─────▼───▼──────────▼─────┐
                  │       order_items         │  ◄── FACT (satışlar)
                  └─────┬──────────────┬──────┘
                        │ inv_item_id  │ product_id
              ┌─────────▼────────┐     │
              │  inventory_items │─────┘
              └────────┬─────────┘
                       │ distribution_center_id
              ┌────────▼──────────┐
              │ distribution_centers │
              └────────────────────┘
```

**Tek cümleyle:** `order_items` "kim neyi kaça ne zaman aldı"yı tutar; diğer tablolar bu olayı açıklar.

---

## 📑 Tablo Tablo Veri Sözlüğü

### 1. `order_items` — ⭐ ANA OLGU TABLOSU (satılan her ürün = 1 satır)
| Sütun | Tip | Açıklama |
|-------|-----|----------|
| id | Tam sayı | Satır kimliği |
| order_id | Tam sayı | Hangi siparişe ait (→ orders) |
| user_id | Tam sayı | Hangi müşteri (→ users) |
| product_id | Tam sayı | Hangi ürün (→ products) |
| inventory_item_id | Tam sayı | Hangi stok kalemi (→ inventory_items) |
| status | Metin | Complete / Shipped / Processing / Cancelled / Returned |
| created_at | Tarih/Saat | Sipariş anı |
| shipped_at | Tarih/Saat | Kargoya verilme |
| delivered_at | Tarih/Saat | Teslim |
| returned_at | Tarih/Saat | İade (boşsa iade yok) |
| **sale_price** | Ondalık | **Satış fiyatı — gelirin kaynağı** |

**Ne öğreniriz:** Toplam satış, gelir trendi, iade oranı, ort. sipariş değeri.

---

### 2. `orders` — Sipariş başlığı (her sipariş = 1 satır)
| Sütun | Tip | Açıklama |
|-------|-----|----------|
| order_id | Tam sayı | Sipariş kimliği (→ order_items) |
| user_id | Tam sayı | Müşteri (→ users) |
| status | Metin | Sipariş durumu |
| gender | Metin | Sipariş veren cinsiyeti |
| created_at | Tarih/Saat | Sipariş tarihi |
| returned_at / shipped_at / delivered_at | Tarih/Saat | Lojistik tarihleri |
| num_of_item | Tam sayı | Siparişteki ürün adedi |

**Ne öğreniriz:** Sipariş sayısı, sepet büyüklüğü, lojistik süreleri.

---

### 3. `users` — Müşteri (her müşteri = 1 satır)
| Sütun | Tip | Açıklama |
|-------|-----|----------|
| id | Tam sayı | Müşteri kimliği (→ orders, order_items) |
| first_name / last_name | Metin | Ad soyad |
| email | Metin | E-posta |
| age | Tam sayı | Yaş |
| gender | Metin | Cinsiyet |
| state / city / country | Metin | Konum |
| street_address / postal_code | Metin | Adres |
| latitude / longitude | Ondalık | Harita için koordinat |
| traffic_source | Metin | Geliş kanalı (Search, Email, Organic…) |
| created_at | Tarih/Saat | Kayıt tarihi |

**Ne öğreniriz:** Demografi, coğrafi dağılım (harita), segmentasyon, kanal analizi.

---

### 4. `products` — Ürün (her ürün = 1 satır)
| Sütun | Tip | Açıklama |
|-------|-----|----------|
| id | Tam sayı | Ürün kimliği (→ order_items, inventory_items) |
| cost | Ondalık | **Maliyet — kâr hesabı için** |
| category | Metin | Kategori (Jeans, Tops…) |
| name | Metin | Ürün adı |
| brand | Metin | Marka |
| retail_price | Ondalık | Liste fiyatı |
| department | Metin | Men / Women |
| sku | Metin | Stok kodu |
| distribution_center_id | Tam sayı | Dağıtım merkezi (→ distribution_centers) |

**Ne öğreniriz:** Kategori/marka performansı, kâr marjı, fiyat analizi.

---

### 5. `inventory_items` — Envanter / stok kalemleri
| Sütun | Tip | Açıklama |
|-------|-----|----------|
| id | Tam sayı | Stok kalemi kimliği (→ order_items) |
| product_id | Tam sayı | Ürün (→ products) |
| created_at | Tarih/Saat | Stoğa giriş |
| sold_at | Tarih/Saat | Satıldığı an (**boşsa hâlâ stokta**) |
| cost | Ondalık | Maliyet |
| product_category / product_name / product_brand | Metin | Ürün bilgisi (denormalize) |
| product_retail_price | Ondalık | Perakende fiyat |
| product_department | Metin | Bölüm |
| product_sku | Metin | SKU |
| product_distribution_center_id | Tam sayı | Dağıtım merkezi |

**Ne öğreniriz:** Stoktaki ürün adedi, top 5 envanter kategorisi, stok devri.

---

### 6. `distribution_centers` — Dağıtım merkezi
| Sütun | Tip | Açıklama |
|-------|-----|----------|
| id | Tam sayı | Merkez kimliği (→ products, inventory_items) |
| name | Metin | Merkez adı (ör. Memphis TN) |
| latitude / longitude | Ondalık | Konum |

**Ne öğreniriz:** Lojistik dağılımı, merkez bazında performans.

---

### 7. `events` — Web olayları (Sayfa 4-5'te kullanıldı)
Her satır = bir web etkileşimi. Anahtar sütun `event_type` (ziyaretçi ne yaptı):

| event_type | Anlamı | Mağaza benzetmesi |
|-----------|--------|-------------------|
| `home` | Ana sayfa ziyareti | Kapıdan girdi |
| `department` | Bölüm/reyon sayfasına baktı | "Kadın Giyim" reyonuna yöneldi |
| `product` | Ürün sayfasına baktı | Bir ürünü eline alıp inceledi |
| `cart` | Sepete ekledi | Sepete koydu |
| `purchase` | Satın aldı | Kasada ödedi |
| `cancel` | İptal etti | Vazgeçti |

Diğer sütunlar: `session_id` (oturum), `user_id` (kullanıcı — anonimse boş), `created_at`, `browser`, `traffic_source` (geliş kanalı), `city`/`state`.
**Gerçek yolculuk sırası:** home → department → product → cart → purchase. (Huni grafiği bunları sayıya göre dizer, akış sırasına göre değil.)
**Ne öğreniriz:** Oturum sayısı, dönüşüm oranı, sepet terki, trafik kaynağı analizi.

## 🔗 Kurulacak İlişkiler (Model görünümü)

Hepsi **Bir-Çok (1→*)**, tek yönlü:

| Bir (1) | → | Çok (*) |
|---------|---|---------|
| `orders[order_id]` | → | `order_items[order_id]` |
| `users[id]` | → | `orders[user_id]` |
| `users[id]` | → | `order_items[user_id]` |
| `products[id]` | → | `order_items[product_id]` |
| `products[id]` | → | `inventory_items[product_id]` |
| `inventory_items[id]` | → | `order_items[inventory_item_id]` |
| `distribution_centers[id]` | → | `products[distribution_center_id]` |
| `distribution_centers[id]` | → | `inventory_items[product_distribution_center_id]` |

> ⚠️ Power BI bazı ilişkileri otomatik kurar ama hepsini kontrol et. Yanlış/çift ilişki varsa düzelt. `users` → `order_items` ile `users` → `orders` → `order_items` arasında çift yol oluşursa birini pasif yap.

---

## 💡 EDA'dan İlk Gözlemler (analiz için potansiyel alanlar)
- **Satış:** `order_items.sale_price` + `created_at` → zaman trendi, mevsimsellik.
- **Kategori:** `products.category` en güçlü kırılım ekseni.
- **İade:** `status = "Returned"` → ürün kalite/beden sorunu sinyali.
- **Müşteri:** `users` demografi + `traffic_source` → segment + kanal ROI.
- **Kâr:** `sale_price - products.cost` → marj analizi.
