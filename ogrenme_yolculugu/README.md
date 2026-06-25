# 🧭 Öğrenme Yolculuğu — Bu Projeyi Nasıl Öğrendim?

> Bu klasör, TheLook Power BI projesini **nasıl** öğrendiğimin detaylı kaydıdır.
> Amaç: ileride tekrar okuyup pekiştirmek + yöntemi geliştirdikçe güncellemek.
> Bu projeyle **ne** yaptığım `docs/` klasöründe; burada **nasıl öğrendiğim** anlatılıyor.

---

## 🎯 Uyguladığım Yöntem
4 kanıtlanmış tekniği birleştirdim (detay: masaüstü `OGRENME_YONTEMIM.md`):
- **Feynman** → her kavramı basit benzetmeyle anlattırdım
- **Aktif hatırlama** → ara ara "ne öğrendik" özetleri
- **Aralıklı tekrar** → öğrenme notlarına dönüp bakma
- **Yaparak öğrenme** → her adımı kendim uyguladım, sonra kontrol

**7 kuralım:** neden önce → benzetme → adım adım uygulamalı → kalıp/sistem göster → aktif hatırlama → dokümante et → proje yönetimi.

---

## 🗺️ Yolculuğun Aşamaları (ne, neden, hangi benzetme)

### 1) Kapsam & Kurulum
- **Ne:** Gereksinimleri okudum, kapsamı 5 iş alanına (Satış, Müşteri, Envanter, Web, Pazarlama) kilitledim. GitHub repo kurdum.
- **Neden:** Önce hedefi netleştirmeden başlamak = yanlış yöne kürek çekmek.
- **Ders:** İyi proje yönetimi = önce kapsam, sonra iş.

### 2) Veri İçe Aktarma (BigQuery)
- **Ne:** `bigquery-public-data.thelook_ecommerce`'ten 7 tablo çektim. "İçeri aktar" (Import) seçtim.
- **Neden:** Import = veri Power BI'a kopyalanır, hızlı; DirectQuery = her tıklamada canlı sorgu, yavaş.
- **Benzetme:** Import = malzemeyi mutfağa taşımak; bir kez taşı, sürekli kullan.

### 3) Veriyi İnceleme & Eleme (EN ÖNEMLİ DERS)
- **Ne:** 8 tabloyu Power Query'de açtım. `thelook_ecommerce-table`'ı (şemasız/bozuk) ve önce `events`'i değerlendirdim.
- **Neden:** "Bilen kişi söyledi" diye değil, **kendi gözümle görüp** karar verdim — kopya tablo gerçekten hata veriyordu.
- **Benzetme:** Doktor önce röntgen çeker, sonra teşhis koyar.
- **Ders:** İyi analist varsayımla değil, **gözlemle** karar verir.

### 4) Temizlik
- **Ne:** 7 tablonun tiplerini kontrol ettim (hepsi doğruydu). Boş tarih sütunlarına dokunmadım.
- **Neden:** `returned_at` boş = "iade edilmedi" (hata değil, bilgi).
- **Benzetme:** Boş kutu da bilgi taşır.
- **Ders:** Temizlik her zaman "değiştirmek" değil; bazen "kontrol edip sağlam olduğunu doğrulamak"tır.

### 5) Model & İlişkiler
- **Ne:** 6 ilişkilik temiz yıldız şeması kurdum. Bazı ilişkileri (çift yol yaratacağı için) bilerek kurmadım.
- **Neden:** PK (benzersiz id) ↔ FK (ona işaret eden _id). Tek aktif yol = belirsizlik yok.
- **Benzetme:** Filtre su gibi, "1" tarafından "*" tarafına akar (yıldız şeması).
- **Ders:** Az ve doğru ilişki > çok ve karışık ilişki.

### 6) Measure & Sütunlar (DAX)
- **Ne:** 14 measure + 2 segment sütunu yazdım.
- **Neden:** Ham satırlar iş sorusunu cevaplayamaz; hesaplama (measure) gerekir.
- **Benzetme:** Measure = tarif (malzemeyi anlamlı sonuca çevirir). Sütun = kavanoza etiket (her satırı sınıflandırır).
- **🔑 Büyük keşif:** DAX sonsuz ezber değil → **measure için ~5 kalıp + sütun için ~5 kalıp.** Kalıbı tanı, kelimeyi değiştir.

---

## 🧱 DAX Kalıp Hatırlatıcı (özet)
**Measure:** SUM/COUNT · DISTINCTCOUNT · AVERAGE · DIVIDE · CALCULATE (+ SUMX/RELATED)
**Sütun:** IF/SWITCH · RELATED · CALCULATE · metin & birleştirme · YEAR/FORMAT (+ aritmetik)
**Pusula:** "Toplamda ne kadar?" → measure · "Bu satır ne?" → sütun

---

## 🔁 Bunu Nasıl Tekrar Ederim? (gözden geçirme rehberi)
1. `docs/05_ogrenme_notlari.md` → benzetmeleri 5 dk oku (kavramları hatırla)
2. `docs/04_dax_kutuphanesi.md` → DAX kalıplarına bak
3. Bu dosyayı oku → yolculuğun "neden"lerini hatırla
4. Kendine sor (kapat-anlat): "Star schema neden? Measure vs sütun farkı? 5 DAX kalıbı ne?"
   - Anlatamadığın yer = tekrar bakman gereken yer (Feynman testi)

---

## 📝 Yöntem Güncelleme Günlüğü
> Öğrenme yöntemini geliştirdikçe buraya yaz (tarih + ne değişti).

- **2026-06 (ilk):** 7 kurallı yöntem TheLook projesinde ilk kez tam uygulandı. Benzetme + neden-önce + kalıp gösterme çok işe yaradı.
- _(sıradaki güncellemeni buraya ekle)_
