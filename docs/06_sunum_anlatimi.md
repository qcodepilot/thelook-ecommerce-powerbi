# 🎤 Sunum Anlatım Scripti

> Her bulguyu "sahnede nasıl anlatırım" diliyle yazıyoruz. Pratik için sesli oku.
> Kural (projeden): Grafik sayısı değil, **yorum** önemli. Rolün veriyi anlamlandırmak.
> Her sayfa: **Ne görüyoruz → Ne anlama geliyor → Ne öneriyoruz.**

---

## 🎬 Açılış (sunuma başlarken)
> "Merhaba. Ben TheLook e-ticaret verisini bir veri analisti gözüyle inceledim.
> Bugün size satıştan müşteriye, üründen pazarlamaya kadar işin 5 yönünü ve
> bunlardan çıkardığım uygulanabilir önerileri sunacağım. Hadi satış performansıyla başlayalım."

---

## 📈 SAYFA 1 — Satış Performansı

### KPI'lar (künye rakamları)
> "Önce büyük resme bakalım. TheLook toplamda **10,9 milyon dolar** ciro yapmış ve
> bundan **5,6 milyon dolar kâr** elde etmiş. Yani kâr marjı yaklaşık **%52** —
> bu, perakende için oldukça sağlıklı bir oran; şirket sattığı her 100 dolardan
> 52 dolarını kâr olarak tutuyor.
>
> Bu satışlar **125 bin sipariş**ten geliyor ve müşteriler sipariş başına ortalama
> **87 dolar** harcıyor. Bu ortalama sipariş değeri, kampanya ve paket-satış
> stratejilerimiz için bir kıyas noktası olacak."

### 💡 Analist notu (neden güveniyoruz?)
> "Rakamların tutarlılığını da kontrol ettim: Toplam satışı sipariş sayısına böldüğümde
> çıkan 87 dolar, ayrı hesapladığım ortalama sipariş değeriyle birebir uyuşuyor.
> Yani verdiğim sayılar birbirini doğruluyor."

### 📊 Aylık Trend
> "Satışların zaman içindeki seyrine baktığımızda net bir **büyüme trendi** görüyoruz.
> 2019'da aylık ~130 bin dolar civarındayken, 2026 ortasına gelindiğinde aylık satış
> **850 bin doları** aşmış. Yani şirket küçülen değil, **istikrarlı büyüyen** bir
> işletme. Bu büyüme özellikle son 1-2 yılda hızlanmış — bu da bize pazarlama ve
> envanter yatırımını artırmanın doğru zamanı olduğunu söylüyor."
>
> _Teknik not (analist için): KPI'daki 10,9M toplam = tüm ayların toplamı; grafikteki
> her nokta tek bir ayın dilimi. Parçalar bütünü doğruluyor._

### 📅 Hafta İçi / Hafta Sonu (normalize etme dersi)
> "Satışların haftanın günlerine dağılımına baktığımızda ilk bakışta hafta içi ezici
> görünüyor: toplam satışın %72'si hafta içi, %28'i hafta sonu. Ama burada dikkatli
> olmak gerekiyor — hafta içi 5 gün, hafta sonu sadece 2 gün. Adil karşılaştırma için
> **gün başına** bakalım: hafta içi günde ~1,56 milyon, hafta sonu günde ~1,55 milyon.
> Yani **gün başına neredeyse aynı!**
>
> Demek ki satışlarımız haftanın her gününe eşit dağılmış; belirgin bir hafta içi/sonu
> etkisi yok. Bu yüzden güne özel (örneğin yalnızca hafta sonu) kampanyalara gerek yok;
> talep hafta boyu sabit. (Not: gerçek perakendede genelde hafta sonu bir zirve görülür;
> buradaki düzlük veri setinin kurgusal olmasından kaynaklanıyor olabilir.)"

### 🏆 Top Kategoriler
> "Peki bu satışlar hangi ürünlerden geliyor? En çok ciro getiren üç kategori:
> **Outerwear & Coats, Jeans ve Sweaters** — yani montlar, kotlar ve kazaklar.
> Listenin en altında ise çorap, tayt gibi düşük fiyatlı ürünler var.
>
> Buradaki desen önemli: ciroyu **birim fiyatı yüksek üst-giyim ürünleri** sürüklüyor.
> Bir çorap ile bir mont aynı adette satılsa bile, mont ciroya çok daha fazla katkı
> yapıyor. Bu da bize yatırımı nereye yönlendireceğimiz konusunda ilk ipucunu veriyor:
> yüksek değerli kategoriler."

### 💲 Kategori Bazında Ortalama Fiyat (çapraz analiz)
> "Şimdi en çok ciro getiren kategorilerle, en pahalı kategorileri yan yana koyalım —
> burada işin inceliği ortaya çıkıyor:
>
> • **Outerwear & Coats** hem en pahalı hem en çok satan kategori. Yani yüksek fiyat
>   ve yüksek hacmi birleştiriyor — bizim **şampiyon kategorimiz.**
> • **Jeans** orta fiyatlı ama ciroda ikinci; demek ki ciroyu **yüksek hacimle**
>   yakalıyor — çok sayıda adet satılıyor.
> • **Suits** ise pahalı ama az satıyor — yani burada **kullanılmamış bir potansiyel**
>   var; doğru pazarlamayla hacmi artırılabilir.
>
> Kısacası aynı ciro iki farklı yoldan gelebiliyor: ya pahalı satarsın, ya çok satarsın.
> En değerlisi ikisini birleştiren Outerwear kategorisi."

### İade Deseni (kategori)
> "İade oranlarını kategori bazında incelediğimizde, en yüksek iadeli kategoriler
> Leggings, Pants ve Swim — ama dikkat çekici olan şu: oranlar birbirine **çok yakın**,
> hepsi %9-10 bandında. Yani belirli bir 'sorunlu kategori' yok; iade **sistemik bir %10.**
> Bu da çözümün kategoriye özel değil **genel** olması gerektiğini söylüyor: net beden
> tabloları, daha iyi ürün görselleri, beden öneri aracı gibi tüm siteyi kapsayan
> iyileştirmeler. (Dürüst not: oranların bu denli homojen olması veri setinin kurgusal
> üretiminden kaynaklanıyor olabilir.)"

### 🏷️ Marka Performansı
> "Markaları satış, kâr marjı ve iade oranıyla birlikte incelediğimizde: satış liderleri
> Calvin Klein, Diesel ve Carhartt. En yüksek marjlar ise premium/outdoor markalarda —
> Ray-Ban, Canada Goose, The North Face, Arc'teryx %56-58 bandında.
>
> Buradaki yıldız **Canada Goose**: hem yüksek marj (%56) hem de **en düşük iade oranı (%5)** —
> yani hem kârlı hem müşteri memnuniyeti yüksek. Bu profildeki markaları vitrinde öne
> çıkarmak mantıklı. Tersine Quiksilver ve Mountain Hardwear %11 iade alıyor; bu markalarda
> beden/kalite sorununu araştırmak gerekiyor."

### ✅ Sayfa 3 Önerisi (Envanter/Ürün)
> "Ürün ve envanter tarafındaki önerilerim: (1) En kârlı kategoriler aynı zamanda en çok
> satanlar — Outerwear, Jeans, Sweaters'a yatırımı sürdürün. (2) Intimates ve Tops & Tees'te
> fazla stok var; sipariş azaltıp indirimle eritin. (3) Outerwear stoğunu artırın, stok
> tükenmesini önleyin. (4) %10'luk iadeyi düşürmek için genel beden/görsel iyileştirmeleri yapın."

### ✅ Sayfa 1 Önerisi
> "Satış tarafındaki önerim net: **Outerwear & Coats ve Jeans** kategorilerine
> öncelik verelim — biri hem pahalı hem çok satıyor, diğeri hacim devi. Pazarlama
> bütçesi ve envanter yatırımı öncelikle buralara gitmeli. Suits gibi pahalı ama
> az satan kategoriler için ise hedefli kampanyalarla hacmi büyütmeyi deneyebiliriz."

---

## 👥 SAYFA 2 — Müşteri Davranışı

### Harcama Segmentasyonu
> "Müşterilerimizi toplam harcamalarına göre üç gruba ayırdık. Tablo şöyle:
> müşterilerin **%54'ü düşük** (100 doların altında), **%43'ü orta** harcayan.
> Yüksek harcayanlar — yani 500 doları aşanlar — ise yalnızca **%2,5**.
>
> Bu çok tanıdık bir tablo: küçük bir azınlık, muhtemelen cironun büyük kısmını
> getiriyor (klasik 80/20 kuralı). Buradan iki net fırsat çıkıyor:
> birincisi, 35 bin kişilik **orta segmenti** sadakat ve üst-satış kampanyalarıyla
> yukarı taşımak; ikincisi, o değerli ama küçük **yüksek segmenti** özel programlarla
> elde tutmak — çünkü değerli bir müşteriyi kaybetmek, yenisini kazanmaktan pahalıdır."

### Coğrafi Dağılım
> "Müşterilerimiz coğrafi olarak nerede yoğunlaşıyor? En büyük müşteri tabanımız
> **Çin ve ABD**'de; ardından Brezilya, İngiltere, Güney Kore, Fransa ve Almanya
> geliyor. Yani uluslararası bir işletmeyiz, ama müşteriler **birkaç büyük ülkede
> toplanmış.** Bu da pazarlama bütçesini her yere eşit dağıtmak yerine, bu yüksek
> yoğunluklu ülkelere odaklamamız gerektiğini söylüyor."
>
> _(Not: Coğrafi dağılım, ülke bazlı bir ağaç haritasıyla gösterildi — Azure harita
> servisi bölge kısıtı nedeniyle kullanılamadı; treemap aynı bilgiyi güvenilir şekilde verir.)_

### Cinsiyet Kırılımı
> "Cinsiyete baktığımızda erkek müşteriler yaklaşık 6 milyon dolar, kadın müşteriler
> 5 milyon dolar civarında satış getiriyor — yani **dengeli bir tablo**, hafif erkek
> ağırlıklı (%55'e %45). Bu da bize tek bir cinsiyete odaklanmak yerine **her iki
> kitleye de** hitap eden kampanyalar yürütmemiz gerektiğini söylüyor."

### Yaş Dağılımı
> "Yaş tarafında ilginç bir tablo var: müşteriler 12 yaştan 70'e kadar **neredeyse eşit
> dağılmış** — belirgin bir yaş grubu öne çıkmıyor. Bu da TheLook'un belli bir kuşağa
> değil, **geniş bir yaş yelpazesine** hitap ettiğini gösteriyor; dolayısıyla pazarlamayı
> yaşa göre daraltmak yerine genele yaymak daha mantıklı.
> (Dürüst not: Bu kadar düz bir dağılım, veri setinin kurgusal üretiminden kaynaklanıyor
> olabilir; gerçek bir e-ticarette yaş genelde belirli aralıklarda yoğunlaşır.)"

### ⭐ Müşteri Yaşam Süresi: Tek Seferlik vs Tekrar Eden (en güçlü bulgu)
> "Şimdi sunumun en çarpıcı bulgusuna geliyoruz. Müşterilerimizi tek seferlik ve tekrar
> eden diye ayırdık:
> • Tekrar eden müşteriler: 30 bin kişi — yani müşterilerin sadece **%38'i** — ama
>   cironun **%60'ını** (6,6 milyon dolar) üretiyorlar.
> • Tek seferlik müşteriler: 50 bin kişi (%62) ama cironun yalnızca %40'ı.
>
> Müşteri başına çevirdiğimizde fark daha da net: tekrar eden bir müşteri **218 dolar**
> değerinde, tek seferlik ise **86 dolar** — yani tekrar eden müşteri **2,5 kat** daha değerli.
> (İlginç: tek seferlik müşteri başı 86 dolar, ortalama sipariş değerimizle neredeyse aynı —
> mantıklı, çünkü tek sipariş veriyorlar.)
>
> Bunun anlamı çok net: en yüksek kaldıraçlı büyüme stratejimiz **müşteri elde tutma
> (retention).** Bir tek-seferlik müşteriyi tekrar edene dönüştürmek, o müşterinin değerini
> 2,5 katına çıkarıyor — bu, sürekli yeni müşteri avlamaktan çok daha kârlı. Önerim: ilk
> alışverişten sonra sadakat programı, kişiselleştirilmiş e-posta ve ikinci-sipariş indirimi
> ile tek seferlik müşterileri geri kazanmaya odaklanmak."

### ✅ Sayfa 2 Önerisi
> "Müşteri tarafındaki önerilerim: (1) 35 binlik orta segmenti sadakat programıyla yukarı
> taşıyın, (2) değerli yüksek segmenti özel avantajlarla elde tutun, (3) pazarlama bütçesini
> Çin, ABD ve Brezilya gibi yoğun ülkelere yönlendirin, (4) yaş ve cinsiyet dengeli olduğu
> için kampanyaları geniş kitleye kurun."

## 📦 SAYFA 3 — Envanter / Ürün

### Kârlılık & Satış Örtüşmesi
> "Ürün tarafında en kârlı kategorilere baktığımızda çarpıcı bir uyum görüyoruz:
> kâr sıralaması, satış sıralamasıyla neredeyse birebir aynı — yine Outerwear & Coats,
> Jeans ve Sweaters önde. Bu da marjlarımızın kategoriler arasında **tutarlı (~%52)**
> olduğunu, yani 'çok satan ama kâr getirmeyen' tuzak bir kategorimiz olmadığını gösteriyor.
> En çok satan kategoriler aynı zamanda en kârlı olanlar — bu kategoriler **çift değerli.**"

### İade Oranı
> "Genel iade oranımız **%10** — yani her 10 üründen biri geri dönüyor. Bu, göz ardı
> edilmeyecek bir oran; hangi ürünlerin daha çok iade edildiğini incelemek, beden/kalite
> sorunlarını yakalamak için önemli."

### Stok–Satış Uyumsuzluğu (kritik envanter bulgusu)
> "Şimdi önemli bir noktaya geliyoruz. Stokta en çok bulunan 5 kategori: Intimates,
> Jeans, Tops & Tees, Fashion Hoodies ve Swim. Ama en çok satan ve en çok kâr eden
> kategorilerimiz Outerwear, Jeans ve Sweaters'dı. Bu iki listede yalnızca **Jeans**
> ortak!
>
> Yani **Intimates ve Tops & Tees** depolarımızı dolduruyor ama satışta öne çıkmıyor —
> bu, **rafta bekleyen, paraya dönüşmeyen fazla stok** demek. Tersine, en kârlı
> kategorimiz Outerwear, en çok stoklananlar arasında değil; demek ki hızlı tükeniyor
> ve **stok tükenmesi riski** taşıyor.
>
> Önerim net: Intimates ve Tops & Tees için sipariş miktarlarını azaltıp eldeki stoğu
> indirimle eritelim; buna karşılık Outerwear & Coats stoğunu artıralım. Böylece hem
> bağlı sermayeyi azaltır, hem de en kârlı üründe satış kaçırmayı önleriz."

## 🌐 SAYFA 4 — Web Sitesi Performansı

### Dönüşüm Hunisi
> "Sitemizde 683 bin oturum gerçekleşmiş ve bunların %27'si satın almayla sonuçlanmış.
> Huniye baktığımızda yolculuk şöyle: insanlar çok sayıda ürün görüntülüyor, ciddi
> miktarda sepete ekleme yapıyor — ama burada kritik bir düşüş var: sepete eklenen
> olayların sayısı 596 bin iken, satın alma 183 bine iniyor. Üstüne 125 bin de iptal var.
>
> Yani en büyük sorunumuz **sepet terki** — müşteriler ürünü beğenip sepete atıyor ama
> ödeme adımında kaçıyor. Bu, e-ticaretin en yaygın gelir kaybı noktası.
>
> Önerim: (1) ödeme sürecini sadeleştirip adım sayısını azaltmak, (2) sepetini terk
> edenlere hatırlatma e-postası ve retargeting reklamı göndermek, (3) iptalleri azaltmak
> için kargo ve iade koşullarını baştan netleştirmek.
> (Dürüst not: %27'lik dönüşüm oranı gerçek e-ticaret için olağandışı yüksek — gerçekte
> %2-3 beklenir; bu, veri setinin kurgusal olmasından kaynaklanıyor.)"

### Etkileşim Metrikleri
> "Ziyaretçi etkileşimine baktığımızda, oturum başına ortalama **3,57 sayfa** görüntüleniyor —
> yani insanlar siteye girip birkaç ürün/sayfa geziyor, sağlıklı bir etkileşim. Sitede
> geçirilen süreyi de events zaman damgalarından hesaplamayı denedik; ancak sentetik veride
> bir oturuma ait olaylar zamanda çok dağıldığı için gerçekçi bir değer çıkmadı (ortalama
> ~7 saat gibi anlamsız bir sonuç). Bu yüzden etkileşimi sayfa görüntüleme üzerinden
> değerlendirdik. Gerçek bir veride oturum süresi dakikalarla ölçülür ve satışla
> ilişkilendirilebilirdi."

### Kaynağa Göre Dönüşüm
> "Dönüşüm oranını trafik kaynağına göre kırdığımızda ilginç bir sonuç çıkıyor: tüm
> kanallarda dönüşüm neredeyse aynı (~%27). Yani hangi kanaldan gelirlerse gelsinler
> ziyaretçiler benzer oranda satın alıyor — kanal seçimi dönüşüm *kalitesini* değil,
> yalnızca *hacmini* etkiliyor. (Gerçek e-ticarette kanala göre dönüşüm farklılaşır;
> buradaki eşitlik veri setinin kurgusal olmasından kaynaklanıyor.)"

### Tarayıcı Dağılımı
> "Ziyaretçilerimizin tarayıcı tercihine baktığımızda Chrome açık ara önde — neredeyse
> yarısı Chrome kullanıyor; ardından Safari ve Firefox geliyor, IE ise yok denecek kadar
> az. Bu, mühendislik kaynağımızı nereye ayıracağımızı söylüyor: siteyi önce Chrome'da
> kusursuz çalışacak şekilde test edelim, Safari ve Firefox'u ikinci öncelik yapalım,
> eski IE için ekstra çaba harcamayalım."

### ✅ Sayfa 4 Önerisi (Web)
> "Web tarafındaki öncelik: sepet terkini azaltmak. Ödeme adımlarını sadeleştirip,
> sepetini terk edenlere retargeting yaparsak dönüşümü doğrudan artırırız. Teknik tarafta
> ise Chrome öncelikli test stratejisi izleyelim."

## 📣 SAYFA 5 — Pazarlama Etkinliği

### Kanal Analizi
> "Müşterilerimiz hangi kanaldan geliyor ve hangisi para getiriyor? İki grafiği yan yana
> koyduğumuzda çarpıcı bir uyum var: hem müşteri sayısı hem satış sıralaması aynı —
> **Search açık ara önde**, ardından Organic, sonra Facebook, Email ve Display.
>
> İki grafiğin aynı şekilde olması şu anlama geliyor: kanallar arasında müşteri kalitesi
> benzer; yani hiçbir kanal 'çok ama değersiz' ya da 'az ama altın' müşteri getirmiyor.
> Search sadece en büyük musluk.
>
> Önerim: (1) Search'e (SEO + arama reklamları) yatırımı sürdürün, en çok getiren kanal o.
> (2) Organic ikinci ve maliyetsiz — içerik üretimiyle besleyin. (3) Email, Facebook ve
> Display şu an küçük; bunlar büyütülebilir potansiyel, küçük test bütçeleriyle ölçeklemeyi
> deneyin.
> Bunu bir tabloyla da doğruladık: her kanalın müşteri başına ortalama geliri 134-138 dolar
> arasında — neredeyse aynı, yani kanal kalitesi homojen (~136 dolar/müşteri). İlginç ayrıntı:
> en küçük kanal Display aslında en yüksek müşteri başı gelire (138) sahip; Display ve Email
> gibi küçük ama verimli kanalları ölçeklemek mantıklı olabilir.
> (Dürüst not: TheLook'ta reklam harcaması verisi olmadığı için gerçek ROI ve müşteri
> kazanım maliyeti hesaplanamıyor; kanalları gelir ve müşteri sayısıyla vekil olarak değerlendirdik.)"

---

## 🎬 Kapanış
> "Özetle: TheLook yüksek marjlı, sağlıklı bir işletme. Önerilerim şu üç başlıkta
> toplanıyor: [1...], [2...], [3...]. Veriyi sadece raporlamadım; karar almanıza
> yardımcı olacak şekilde yorumladım. Teşekkürler."

> Not: Kapanıştaki 3 öneriyi tüm sayfalar bitince netleştireceğiz.
