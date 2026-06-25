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

### İnceleme sonuçları
| Tablo | Satır | Gözlem | Karar |
|-------|-------|--------|-------|
| order_items | _doldurulacak_ | Ana olgu tablosu | ✅ Tut |
| orders | _doldurulacak_ | Sipariş başlığı | ✅ Tut |
| users | ~100k | Müşteri demografisi | ✅ Tut |
| products | _doldurulacak_ | Ürün/kategori/marka | ✅ Tut |
| inventory_items | _doldurulacak_ | Stok | ✅ Tut |
| distribution_centers | _doldurulacak_ | Dağıtım merkezi | ✅ Tut |
| events | _doldurulacak_ | Web olayları | ⏳ inceleniyor |
| thelook_ecommerce-table | _doldurulacak_ | Uyarı ⚠️ ikonu var — kopya/denormalize? | ⏳ inceleniyor |

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
