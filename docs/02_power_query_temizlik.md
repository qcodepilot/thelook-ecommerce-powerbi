# 🧹 FAZ 2 — Power Query: İnceleme & Temizlik

> Bu doküman biz ilerledikçe doldurulur. Amaç: veriyi modele almadan önce
> incelemek, gereksizi elemek, tipleri düzeltmek, temizlemek.

## A) EDA araçlarını açma
Görünüm sekmesi → ☑ Sütun kalitesi · ☑ Sütun dağılımı · ☑ Sütun profili
**Neden:** Her sütunun boş/hata oranını ve değer dağılımını gözle görmek için. Power Query'nin dahili veri-kalitesi aracı.

## B) Tablo inceleme — 4 kriter merceği
Bir tablo modele girmeyi hak ediyor mu?
1. **İlgi** — seçtiğim 3 vakaya (satış/müşteri/ürün) cevap veriyor mu?
2. **Boyut** — satır sayısı performansı/dosyayı zorlar mı?
3. **Tekrar** — verisi başka tabloda zaten var mı?
4. **İlişki** — modele temiz bağlanıyor mu?

### İnceleme sonuçları (gözleme dayalı)
| Tablo | Gözlem | Karar |
|-------|--------|-------|
| order_items | Ana olgu tablosu (sale_price, status, tarihler) | ✅ Tut |
| orders | Sipariş başlığı | ✅ Tut |
| users | EDA panelinde tüm sütunlar **%100 Geçerli, %0 Hata, %0 Boş** — tertemiz | ✅ Tut |
| products | Ürün/kategori/marka/maliyet | ✅ Tut |
| inventory_items | Stok kalemleri | ✅ Tut |
| distribution_centers | Dağıtım merkezi | ✅ Tut |
| **events** | Web tıklama verisi (browser, traffic_source, uri, event_type). Bizim 3 vakada kullanılmıyor; çok büyük; `user_id` önizlemede null | ⚠️ **Yükleme devre dışı** (silinmedi, kapsam dışı) |
| **thelook_ecommerce-table** | **HATA:** `DataSource.Error: Table ... does not have a schema` — şemasız/bozuk, yüklenemiyor | ❌ **Silindi** |

> 🎓 Not: Eleme kararları varsayımla değil, Power Query'de **doğrudan gözlemlenen kanıtla** verildi (hata mesajı + sütun içerikleri).

## C) Eleme yöntemi
Karar verince: sorguya sağ tık → **"Yüklemeyi etkinleştir" işaretini kaldır** (silmeden devre dışı bırakma)
veya **Sil**.
**Neden "etkinleştirmeyi kapat":** Sorgu dursun ama modele yüklenmesin → istersek geri açarız, modeli kirletmez.

## D) Tip düzeltme (her tabloda)
- Tarih sütunları (`created_at`, `shipped_at`, `delivered_at`, `returned_at`, `sold_at`) → **Tarih/Saat**
- Fiyat/maliyet (`sale_price`, `cost`, `retail_price`) → **Ondalık Sayı**
- id'ler → **Tam Sayı**
- Metin (`category`, `brand`, `status`) → **Kırp + Temizle**

## E) Bitiş
Ana Sayfa → **Kapat ve Uygula** → veri modele yüklenir.
