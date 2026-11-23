Online alışverişte satın alma niyeti

E-ticaret oturumlarının satın alma niyetiyle ilişkisini UCI Online Shoppers Purchasing Intention verisi üzerinde inceleyen BIL545 proje deposu.

## İçindekiler

- [Veri kümesi](#veri-kümesi)
- [Proje 1: Öznitelik seçimi ve kararlılığı](#proje-1-öznitelik-seçimi-ve-kararlılığı)
- [Proje 2: Oturum analizi](#proje-2-oturum-analizi)
- [Sonuç özeti](#sonuç-özeti)
- [Sınırlılıklar](#sınırlılıklar)

## Öğrenci ve grup

| İsim Soyisim | Okul numarası |
|---|---:|
| Şahin Güngördü | 264312011 |

## Proje dosyaları

- [`proje1/BIL545_Proje1_EkPaket2_OznitelikSecimi.ipynb`](proje1/BIL545_Proje1_EkPaket2_OznitelikSecimi.ipynb): Proje 1 Ek Paket 2 için bağımsız öznitelik seçimi ve kararlılık bölümü. Tam Proje 1 defteri bulunmadığı için resmî teslimden önce bu bölüm tam Proje 1 Colab defterine eklenmelidir.
- [`proje2/BIL545_Proje2_OnlineShoppers.ipynb`](proje2/BIL545_Proje2_OnlineShoppers.ipynb): Öğretim üyesinin Proje 2 taslağından doldurulan notebook; Bölüm 1–3 ile Ek Paket 1 ve Ek Paket 2 / Seçenek A bölümlerini içerir.

## Veri kümesi

- **Kaynak:** [UCI Machine Learning Repository — Online Shoppers Purchasing Intention](https://archive.ics.uci.edu/dataset/468/online)
- **İçerik:** 12.330 oturum, 17 öznitelik; hedef sütunu `Revenue`.
- **Lisans:** CC BY 4.0.
- **Veriyi alma:** `online_shoppers_intention.csv` dosyası depoya eklenmez. Notebook çalışma dizininde CSV varsa onu okur; yoksa UCI dataset id 468'den indirir.

## Proje 1: Öznitelik seçimi ve kararlılığı

Filtre (F-skoru), sarmalayıcı (RFE) ve gömülü (ExtraTrees) seçiciler aynı 5-katlı, 3-tekrarlı çapraz doğrulamayla karşılaştırıldı. Seçim sıklığı ayrıca 100 tabakalı %70 alt örneklemde ölçüldü; yönergedeki ölçüte göre %80'den fazla seçilme kararlı kabul edildi.

| Hat | Average Precision (ortalama ± std) |
|---|---:|
| Seçimsiz geçici Random Forest | 0.748 ± 0.014 |
| Filtre (F-skoru) | 0.740 ± 0.015 |
| RFE | 0.705 ± 0.017 |
| ExtraTrees | 0.741 ± 0.015 |

`ExitRates`, `PageValues`, `Month` ve `VisitorType` üç seçicide de 100/100 alt örneklemde seçildi.

## Proje 2: Oturum analizi

- **Bölüm 1 — Kümeleme:** KMeans için k=3 en yüksek alt örneklem kararlılığını verdi (ARI 0.953; silhouette 0.307). DBSCAN seçilen ayarda tek yoğun küme buldu ve örneklemin %5.1'ini gürültü saydı.
- **Bölüm 2 — Aykırı oturumlar:** Isolation Forest ve LOF sıralamalarının Spearman uyumu 0.345 oldu. Eğitim oturumlarının en aykırı %2'sini çıkarmak sonuçları yalnızca sınırlı ölçüde değiştirdi.
- **Bölüm 3 — Alt gruplar:** Month, VisitorType ve Weekend gruplarındaki hata ölçüleri karşılaştırıldı. Hassas demografik değişkenler bulunmadığından bu sonuçlar adillik garantisi değildir.
- **Ek Paket 1:** Kümeyi sınıflandırma özelliği olarak eklemek CV Average Precision'ı değiştirmedi (0.378); ayrı küme modellerinin test AP'si global modelden düşük çıktı (0.350 ve 0.362).
- **Ek Paket 2 / Seçenek A:** Bağlam-only, PageValues hariç web/oturum-only ve birleşik hatların CV Average Precision değerleri sırasıyla 0.256, 0.305 ve 0.378 oldu.

Proje 2 sonuçları geçici class-weighted Random Forest referansına dayanıyor; Proje 1'in nihai modeli ve öğretim üyesi geri bildirimi paylaşılmadığı için bu ölçümler gerçek Proje 1 modeliyle yenilenmelidir.

## Sonuç özeti

Öznitelik seçimi yöntemleri bu geçici modelde seçimsiz hatta göre Average Precision artışı sağlamadı. Proje 2'de web/oturum özellikleri bağlam özelliklerine ek öngörü sinyali verdi. `PageValues` sonuçları ana modelden ayrı tutuldu; bu değişken hedefe çok yakın bilgi taşıyabileceğinden tahmin anında kullanılabilirliği doğrulanmalıdır.

## Sınırlılıklar

Veri tek bir tarihsel e-ticaret bağlamından oturum özetleri içerir. Analizler nedensel etkiyi veya güncel/farklı sitelere genellemeyi göstermez. Proje 1'in gerçek modeli ve geri bildirimi paylaşılmadığından iki notebook'taki sınıflandırma karşılaştırmaları geçicidir. Grup katkı beyanı, öğrencinin gerçek çalışması ve sunum kısmıyla teslimden önce tamamlanmalıdır.

## Çalıştırma

1. İlgili notebook bağlantısını açıp Colab'a aktarın.
2. CSV kullanacaksanız `online_shoppers_intention.csv` dosyasını çalışma dizinine yükleyin. Yüklemezseniz veri UCI'dan indirilir.
3. **Çalışma zamanı → Tümünü çalıştır** ile hücreleri baştan sona çalıştırın.
4. Proje 1 Ek Paket 2 notebook'unu tam Proje 1 defterine ekleyin. GitHub ve STIX'e aynı `.ipynb` kopyasını yükleyin.

## Katkı ve yapay zekâ beyanı

| İsim Soyisim | Okul numarası | Katkı beyanı |
|---|---:|---|
| Şahin Güngördü | 264312011 | Veri kümesini ve proje kapsamını paylaştı. Kod ve analiz taslağında ChatGPT kullanıldı; nihai doğrulama ve sunum katkısı teslim öncesi gerçek çalışmaya göre tamamlanmalıdır. |

**Yapay zekâ kullanımı:** ChatGPT yönergeyi sınıflandırma, analiz planı, notebook kod/yazı taslağı ve bu README'yi hazırlama aşamalarında kullanıldı. Kullanım ve sonuç doğrulaması notebook içinde de beyan edilmiştir.
