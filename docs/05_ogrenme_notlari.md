# 🧠 Öğrenme Notları & Zihin Haritaları

> Bu dosya kavramları **benzetmelerle** saklar — beyin somut resme kanca atar, ezber kalıcı olur.
> Ara ara oku (spaced repetition). Her kavram: **resim → tek cümle özet.**

---

## 🌟 Star Schema (Yıldız Şeması)
**Resim:** Merkezde bir olay defteri (`order_items` = "kim neyi kaça ne zaman aldı"), çevresinde o olayı açıklayan sözlükler (`users`=kim, `products`=ne, `Tarih`=ne zaman).
**Özet:** *order_items olayları tutar; diğer tablolar o olayı açıklar.*

## 🔑 Birincil Anahtar (PK) ↔ Yabancı Anahtar (FK)
**Resim:** Her tablonun kimlik numarası (`id` = PK, benzersiz). Başka tablo bu kimliğe "işaret eden" bir not tutar (`user_id`, `product_id` = FK).
**Özet:** *PK = benzersiz kimlik (1 tarafı); FK = ona işaret eden not (çok tarafı). FK ismi hangi tabloya gittiğini söyler.*

## 🌊 Kardinalite & Çapraz Filtre Yönü
**Resim:** İlişki = tek yönlü bir yokuş. Filtre **su gibi**, benzersiz "1" tarafından, çok "*" tarafına doğru **aşağı akar.**
**Özet:** *Filtre; "1" → "*" yönünde, AKTİF ve TEK yönlü yollardan akar.*

## 🚦 Aktif / Pasif İlişki
**Resim:** Aktif = açık yol (düz çizgi). Pasif = kapalı yol (kesik çizgi), sadece özel izinle (USERELATIONSHIP) geçilir. İki yer arası tek yol açık kalır ki kafa karışmasın.
**Özet:** *İki tablo arası tek aktif yol olur; fazlası belirsizlik (ambiguity) yaratır.*

## 🍳 Measure (Ölçü) = Tarif
**Resim:** Ham satırlar = malzeme (un, yumurta). Measure = tarif ("hepsini topla"). Grafik = tabaktaki yemek. Müşteriye un servis edilmez; tarif malzemeyi anlamlı sonuca çevirir.
**Özet:** *Measure = ham satırları işin sorduğu sayıya çeviren tarif. Bir kez yaz, her grafikte kullan.*

## 📊 Measure vs Hesaplanan Sütun
**Resim:** Sütun = her ürüne yapışık etiket (sabit). Measure = kasada anlık hesaplanan fiş (ne seçtiğine göre değişir).
**Özet:** *Topluyor/oranlıyor + filtreye tepki versin → measure. Her satırı etiketliyor → sütun.*

## 🔍 "Veriyi görmeden eleme"
**Resim:** Doktor önce röntgen çeker, sonra teşhis koyar. Biz de `events` ve kopya tabloyu **açıp gördük**, sonra eledik (kopya tablo şemasız çıktı = bozuk).
**Özet:** *İyi analist varsayımla değil, gözlemle karar verir.*

## 🕳️ Anlamlı Boşluk (null)
**Resim:** `returned_at` boş = "bu ürün iade edilmedi" (hata değil, haber). Boş kutu da bilgi taşır.
**Özet:** *Her boşluk eksik veri değildir; bazen boşluğun kendisi anlamlıdır. Önce "bu boşluk ne demek?" diye sor.*

## 📦 Büyük dosya & Git
**Resim:** Repo = kod ve not defteri; bavul (.pbix 163MB) oraya sığmaz. Bavulu Drive'a koy, repoya sadece notları + fotoğrafları (PDF/ekran görüntüsü) koy.
**Özet:** *GitHub'a kod + dokümantasyon konur; büyük ikili dosyalar (.pbix) değil.*

## 🧱 DAX = ~5 Lego Parçası
**Resim:** Az sayıda Lego parçası, sonsuz yapı. DAX'ta da ~5 temel kalıp tüm KPI'ları üretir; iş kelimesi değişir, kalıp aynı kalır.
**5 temel kalıp:**
1. `SUM / COUNTROWS` → topla / say (Toplam Satış, Satılan Ürün Adedi)
2. `DISTINCTCOUNT` → benzersiz say (Sipariş Sayısı, Müşteri Sayısı, Oturum Sayısı)
3. `AVERAGE` → ortala (Ortalama Satış Fiyatı)
4. `DIVIDE` → oran/yüzde (Kâr Marjı %, İade Oranı, Dönüşüm Oranı, AOV)
5. `CALCULATE` → koşullu hesapla / filtre değiştir (Net Satış, İade Oranı, Satın Alan Oturum)
+ bonus: `SUMX + RELATED` → satır satır + başka tablodan değer çek (Toplam Maliyet)
**Özet:** *DAX sonsuz ezber değil; ~5 kalıbın iş sorusuna göre tekrarı. Kalıbı tanı, kelimeyi değiştir.*

> Not: measure'lar birbirini Lego gibi kullanır — `Toplam Kâr = [Toplam Satış] - [Toplam Maliyet]`. Önce küçük parçaları yaz, sonra birleştir.

---
> Yeni kavram öğrendikçe buraya benzetmesiyle ekle. Bu dosya senin "kalıcı hafıza"n.
