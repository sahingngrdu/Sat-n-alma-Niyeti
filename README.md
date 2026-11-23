# **Online alışverişte satın alma niyeti**

BIL545 kapsamında UCI Online Shoppers Purchasing Intention verisiyle e-ticaret oturumlarının satın alma niyetini inceleyen proje.

## İçindekiler

- [Veri kümesi](#veri-kümesi)
- [Proje 1: Öznitelik seçimi ve kararlılığı](#proje-1-öznitelik-seçimi-ve-kararlılığı)
- [Proje 2: Oturum analizi](#proje-2-oturum-analizi)
- [Sonuç özeti](#sonuç-özeti)
- [Sınırlılıklar](#sınırlılıklar)

## Öğrenci

| İsim Soyisim | Okul numarası |
|---|---:|
| Şahin Güngördü | 264312011 |

## Proje dosyaları

- [`proje1/BIL545_Proje1_EkPaket2_OznitelikSecimi.ipynb`](proje1/BIL545_Proje1_EkPaket2_OznitelikSecimi.ipynb): Proje 1 Ek Paket 2 için bağımsız öznitelik seçimi ve kararlılık bölümü. Tam Proje 1 notebook'u mevcut olmadığından bu bölüm resmî teslimden önce tam Proje 1 Colab defterine eklenmelidir.
- [`proje2/BIL545_Proje2_OnlineShoppers.ipynb`](proje2/BIL545_Proje2_OnlineShoppers.ipynb): Öğretim üyesinin Proje 2 taslağından doldurulan notebook; Bölüm 1–3 ile Ek Paket 1 ve Ek Paket 2 / Seçenek A bölümlerini içerir.

## Veri kümesi

- **Kaynak:** [UCI Machine Learning Repository — Online Shoppers Purchasing Intention](https://archive.ics.uci.edu/dataset/468/online)
- **İçerik:** 12.330 oturum, 17 öznitelik; hedef sütunu `Revenue`.
- **Lisans:** CC BY 4.0.
- **Veriyi alma:** `online_shoppers_intention.csv` depoya eklenmez. Notebook çalışma dizininde CSV varsa onu okur; yoksa UCI dataset id 468'den indirir.

## Proje 1: Öznitelik seçimi ve kararlılığı

Filtre (F-skoru), sarmalayıcı (RFE) ve gömülü (ExtraTrees) seçiciler aynı 5-katlı, 3-tekrarlı çapraz doğrulamayla karşılaştırıldı. Seçilme sıklığı 100 tabakalı %70 alt örneklemde ölçüldü; yönergedeki **>%80** eşiği kullanıldı.

| Öznitelik kapsamı | Seçimsiz | Filtre | RFE | ExtraTrees |
|---|---:|---:|---:|---:|
| PageValues dahil AP (ortalama ± std) | 0.748 ± 0.014 | 0.740 ± 0.015 | 0.705 ± 0.017 | 0.741 ± 0.015 |
| PageValues hariç AP (ortalama ± std) | 0.377 ± 0.023 | 0.348 ± 0.015 | 0.328 ± 0.015 | 0.356 ± 0.020 |

PageValues dahil üç yöntemin ortak kararlı sütunları `ExitRates`, `PageValues`, `Month` ve `VisitorType` oldu. PageValues hariç ortak kararlı küme `ExitRates`, `Month` ve `ProductRelated_Duration` olarak değişti. Seçiciler her iki kurulumda da 15 eşleşik CV katının hiçbirinde seçimsiz hattı geçmedi. PageValues dahil AP'nin hariç duruma göre 0.371–0.392 yüksek çıkması, modelin bu sütuna duyarlı olduğunu gösterir; hedef sızıntısını tek başına kanıtlamaz.

## Proje 2: Oturum analizi

- **Bölüm 1 — Kümeleme:** k=3 en yüksek alt örneklem kararlılığını verdi (ARI 0.953; silhouette 0.307). DBSCAN seçilen ayarda tek yoğun küme ve %5.1 gürültü buldu.
- **Bölüm 2 — Aykırı oturumlar:** Isolation Forest ve LOF sıralamalarının Spearman uyumu 0.345 oldu. Eğitim oturumlarının en aykırı %2'sini çıkarmak sonuçları sınırlı ölçüde değiştirdi.
- **Bölüm 3 — Alt gruplar:** Month, VisitorType ve Weekend gruplarındaki hata ölçüleri raporlandı. Veri hassas demografik özellikler içermediğinden bu analiz adillik garantisi vermez.
- **Ek Paket 1:** Küme bilgisini eklemek CV Average Precision'ı değiştirmedi (0.378); küme başına modellerin test AP'si global modelden düşüktü (0.350 ve 0.362).
- **Ek Paket 2 / Seçenek A:** Bağlam-only, PageValues hariç web/oturum-only ve birleşik hatların CV Average Precision değerleri sırasıyla 0.256, 0.305 ve 0.378 oldu.

## Sonuç özeti

Web/oturum özellikleri bağlam özelliklerine ek öngörü sinyali verdi. Öznitelik seçimi ise bu geçici modelde AP'yi artırmadı. PageValues'ın tahmin anında erişilebilirliği doğrulanmadığından bu sütun ayrı duyarlılık analizi olarak incelenmelidir.

## Sınırlılıklar

Sınıflandırma analizleri Proje 1'in gerçek nihai modeli ve öğretim üyesi geri bildirimi paylaşılmadığı için geçici class-weighted Random Forest ile yapıldı. Gerçek modelle sonuçlar yenilenmelidir. Veri tek ve tarihsel bir siteye ait oturum özetlerinden oluşur; sonuçlar nedensel etkiyi veya farklı site/dönemlere genellemeyi göstermez. Proje 1 notebook'u şu anda yalnızca Ek Paket 2 bölümü içerir.

## Colab'da çalıştırma

1. İlgili notebook'u GitHub'dan Colab'da açın.
2. `online_shoppers_intention.csv` dosyasını çalışma dizinine eklerseniz notebook onu kullanır; eklemezseniz veri UCI'dan indirilir.
3. **Çalışma zamanı → Tümünü çalıştır** ile hücreleri baştan sona çalıştırın.
4. Proje 1'in Ek Paket 2 bölümünü tam Proje 1 notebook'una ekleyin. GitHub ve STIX'e aynı `.ipynb` dosyasını teslim edin.

## Katkı ve yapay zekâ beyanı

| İsim Soyisim | Okul numarası | Katkı beyanı |
|---|---:|---|
| Şahin Güngördü | 264312011 | Veri kümesini ve proje kapsamını paylaştı. Kod ve analiz taslağında ChatGPT kullanıldı; nihai doğrulama ve sunum katkısı gerçek çalışmaya göre tamamlanmalıdır. |

**Yapay zekâ kullanımı:** ChatGPT yönergeyi sınıflandırma, analiz planı, notebook kod/yazı taslağı ve README hazırlama aşamalarında kullanıldı. Kullanım ve sonuç doğrulaması notebook içinde de beyan edilmiştir.
