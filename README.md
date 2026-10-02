# Kesme

Şekli tek bir çizgiyle mümkün olduğunca eşit iki alana böldüğünüz Türkçe günlük oyun.
Uygulama `index.html` içinde çalışır; derleme veya çalışma zamanı bağımlılığı yoktur.

## 500 günlük + 300 ayrı antrenman silueti

Hayvanlar, gündelik nesneler, taşıtlar, ünlü yapılar, bitkiler ve fantastik
figürlerden oluşan 800 farklı tasarım bulunur. Koleksiyon 200 nesne/figür
çizimini ve 600 farklı nesne çiftiyle oluşturulan sahne kompozisyonunu içerir.
Eyfel, Galata, Kız Kulesi, Tac Mahal ve Sidney Opera Binası bunlara dahildir.
Sayıyı artırmak için aynı şeklin döndürülmüş kopyaları kullanılmaz.

- **Günlük sıra:** Türkiye takvimine göre 2 Ekim 2026'da Kahkaha kulübü ile başlar;
  ilk 100 şekil ve tarihleri aynen korunur. 13 Şubat 2028'de 500. şekle ulaşır.
  Bu sürede tekrar yoktur. 14 Şubat 2028'de 500 günlük döngü yeniden başlar.
- **Antrenman:** Yeni turlar, günlük havuzdan farklı 300 şekillik
  `ANTRENMAN_POOL` içinden mevcut rastgele seçim davranışıyla seçilir.
  Daha önce tamamlanan antrenman sonucu kendi eski şekliyle geri yüklenebilir.
- **Arşiv:** 1 Ekim 2026'dan başlar; takvimde ve gün geçişinde daha eski tarihlere
  gidilemez. Mevcut günlük şekil sırası ve kayıtlar korunur.
- **Boşluklar:** Göz, ağız, kulp ve iç içe konturlar gerçek boşluklardır;
  çizimde, kesim kontrolünde, alan hesabında ve arşiv küçük resimlerinde korunur.
- **Eski oyunlar:** 2 Ekim öncesi arşiv ve daha önce tamamlanmış günlük/antrenman
  kayıtları eski şekilleriyle açılır; istatistik ve seri anahtarları değişmez.
  Güncellemeden önce 2 Ekim oyununu tamamlayan oyuncu o gün eski sonucunu görür.

## İçerik bakımı

`POOL`, kalıcı `siluet-001` … `siluet-500` kimliklerine sahip günlük koleksiyondur.
`ANTRENMAN_POOL`, `antrenman-001` … `antrenman-300` kimliklerini kullanır.
Her şeklin `c` alanı konturları içerir: `s: 1` dolu dış sınır, `s: -1` boşluk;
`p` kapalı sınırın noktalarıdır. İç içe konturlar `evenodd` ile çizilir.
`gununSekli` günlük oyun ve arşiv için aynı tarih seçimini yapar.

`POOL` sırasını, kimliklerini ve uzunluğunu mevcut tarihler için değiştirmeyin;
yeni bir koleksiyon için ayrı başlangıç tarihi tanımlayın. `ESKI_POOL` sırası da
eski indeks tabanlı kayıtların doğru açılması için sabittir. Yeni kayıtlar
`shapeId` taşır; eski kayıtlarda bu alanın bulunmaması desteklenir.

## Yerel önizleme

`index.html` dosyasını tarayıcıda açın veya klasörü statik olarak sunun:

```sh
python3 -m http.server 8000
```

Ardından `http://localhost:8000` adresini açın. Build, lint veya paket kurulumu gerekmez.
