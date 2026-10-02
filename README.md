# Kesme

Şekli tek bir çizgiyle mümkün olduğunca eşit iki alana böldüğünüz Türkçe günlük oyun.
Uygulama `index.html` içinde çalışır; derleme veya çalışma zamanı bağımlılığı yoktur.

## 100 özgün siluet

Hayvanlar, gündelik nesneler, taşıtlar, yapılar, bitkiler ve fantastik figürlerden
oluşan 100 ayrı tasarım günlük oyunda ve antrenmanda kullanılır.

- **Günlük sıra:** Türkiye takvimine göre 2 Ekim 2026'da Kahkaha kulübü ile başlar;
  9 Ocak 2027'de Yüzüncü gün pastası ile 100. şekle ulaşır. Bu sürede tekrar yoktur.
  10 Ocak 2027'de aynı 100 günlük döngü yeniden başlar.
- **Antrenman:** Mevcut rastgele seçim davranışıyla 100 şeklin tamamını kullanır.
- **Boşluklar:** Göz, ağız, kulp ve iç içe konturlar gerçek boşluklardır;
  çizimde, kesim kontrolünde, alan hesabında ve arşiv küçük resimlerinde korunur.
- **Eski oyunlar:** 2 Ekim öncesi arşiv ve daha önce tamamlanmış günlük/antrenman
  kayıtları eski şekilleriyle açılır; istatistik ve seri anahtarları değişmez.
  Güncellemeden önce 2 Ekim oyununu tamamlayan oyuncu o gün eski sonucunu görür.

## İçerik bakımı

`POOL`, kalıcı `siluet-001` … `siluet-100` kimliklerine sahip koleksiyondur.
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
