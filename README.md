# BIL545 | Online alışverişte satın alma niyeti

> **Ders:** Veri Madenciliğinde İleri Konular · 2026–2027 Güz
> **Veri kümesi:** UCI Online Shoppers Purchasing Intention
> **Hedef:** Oturumun satın almayla (`Revenue`) sonuçlanıp sonuçlanmadığını incelemek

## İçindekiler

- [Öğrenci ve grup](#öğrenci-ve-grup)
- [Depo içeriği](#depo-içeriği)
- [Veri kümesi ve lisans](#veri-kümesi-ve-lisans)
- [Colab'da çalıştırma](#colabda-çalıştırma)
- [Sonuç özeti](#sonuç-özeti)
- [Katkı ve yapay zekâ beyanı](#katkı-ve-yapay-zekâ-beyanı)
- [Teslim öncesi tamamlanacaklar](#teslim-öncesi-tamamlanacaklar)

## Öğrenci ve grup

| Bilgi | Değer |
|---|---|
| İsim Soyisim | Şahin Güngördü |
| Okul numarası | 264312011 |
| Grup adı | [Grup adı eklenecek] |
| Grup büyüklüğü | Ek Paket 2 ataması nedeniyle 5 kişi varsayılmıştır; doğrulanmalıdır |

Diğer grup üyelerinin adları ve okul numaraları paylaşılmadığı için eklenmemiştir.

## Depo içeriği

| Klasör | İçerik |
|---|---|
| [`proje1/`](proje1/) | Proje 1 Ek Paket 2: öznitelik seçimi ve kararlılığı için bağımsız notebook. Proje 1'in tam defteri mevcut olmadığından resmî teslimden önce bu bölüm tam Proje 1 Colab defterine eklenmelidir. |
| [`proje2/`](proje2/) | Öğretim üyesinin Proje 2 taslağından doldurulan notebook: Bölüm 1–3, Ek Paket 1 ve Ek Paket 2 / Seçenek A. |

Yönergeye göre her proje kodu, çıktıları ve yazılı yanıtları tek bir Colab defterinde bulunmalı; GitHub'daki ve STIX'e yüklenen defterler aynı olmalıdır. Bu depoda Proje 1 için şu anda yalnızca istenen bağımsız Ek Paket 2 bölümü vardır.

## Veri kümesi ve lisans

- **Kaynak:** [UCI Machine Learning Repository — Online Shoppers Purchasing Intention](https://archive.ics.uci.edu/dataset/468/online)
- **Boyut:** 12.330 oturum, 17 öznitelik ve `Revenue` hedefi.
- **Lisans:** CC BY 4.0; veri kaynağı notebook'larda da belirtilmiştir.
- **Dosya:** `online_shoppers_intention.csv` GitHub deposuna eklenmez. Notebook çalışma dizininde bu CSV varsa onu okur; yoksa UCI dataset id 468'i indirir.

## Colab'da çalıştırma

1. Açmak istediğiniz notebook bağlantısına tıklayın:
   - [Proje 1 Ek Paket 2'yi Colab'da aç](https://colab.research.google.com/github/sahingngrdu/Sat-n-alma-Niyeti/blob/main/proje1/BIL545_Proje1_EkPaket2_OznitelikSecimi.ipynb)
   - [Proje 2'yi Colab'da aç](https://colab.research.google.com/github/sahingngrdu/Sat-n-alma-Niyeti/blob/main/proje2/BIL545_Proje2_OnlineShoppers.ipynb)
2. Kendi CSV kopyanızı kullanacaksanız `online_shoppers_intention.csv` dosyasını Colab çalışma dizinine yükleyin. Yüklemezseniz notebook UCI'dan indirir.
3. **Çalışma zamanı → Tümünü çalıştır** ile hücreleri baştan sona çalıştırın.
4. Notebook içindeki grup, katkı ve Proje 1'den devralınan model/geri bildirim alanlarını gerçek bilgilerle tamamlayın.

## Sonuç özeti

### Proje 1 · Ek Paket 2 — öznitelik seçimi ve kararlılığı

Filtre (F-skoru), sarmalayıcı (RFE) ve gömülü (ExtraTrees) seçiciler; aynı 5-katlı, 3-tekrarlı CV bölmelerinde karşılaştırıldı. Her seçici ayrıca 100 tabakalı %70 alt örneklemde tekrarlandı; yönergedeki ölçüte uygun olarak **%80'den fazla** seçilme kararlı kabul edildi.

| Hat | Average Precision (ortalama ± std) |
|---|---:|
| Seçimsiz geçici Random Forest | 0.748 ± 0.014 |
| Filtre (F-skoru) | 0.740 ± 0.015 |
| RFE | 0.705 ± 0.017 |
| ExtraTrees | 0.741 ± 0.015 |

`ExitRates`, `PageValues`, `Month` ve `VisitorType` üç yöntemde de 100/100 alt örneklemde seçildi. PageValues'ın tahmin anında kullanılabilirliği doğrulanmadığından bu kararlılık tek başına güvenli kullanım kanıtı sayılmamalıdır.

### Proje 2 · Bölüm 1–3 ve ek paketler

- **Bölüm 1 — Kümeleme:** Alt örneklem kararlılığında k=3 en yüksek ARI'yi verdi (0.953); KMeans örneklem silhouette değeri 0.307 oldu. DBSCAN seçilen ayarda tek yoğun küme ve %5.1 gürültü buldu.
- **Bölüm 2 — Aykırı gözlem:** Isolation Forest ve LOF sıralamalarının Spearman uyumu 0.345'tir. Eğitim verisinin en aykırı %2'sini çıkarmak, sabit test kümesindeki sonuçları yalnızca sınırlı ölçüde değiştirdi.
- **Bölüm 3 — Alt grup analizi:** Month, VisitorType ve Weekend gruplarındaki hata ölçüleri raporlandı. Veri hassas demografik özellikler içermediğinden bu analiz adillik garantisi vermez.
- **Ek Paket 1:** Küme bilgisini eklemek CV'de Average Precision'ı değiştirmedi (0.378); küme başına modeller global modelden daha düşük test AP verdi (0.350 ve 0.362).
- **Ek Paket 2 / Seçenek A:** Bağlam-only, PageValues hariç web/oturum-only ve birleşik hatların CV Average Precision değerleri sırasıyla 0.256, 0.305 ve 0.378 oldu. PageValues içeren sonuçlar yalnızca duyarlılık analizi olarak tutuldu.

Proje 2 ölçümleri, Proje 1'in nihai modeli ve öğretim üyesi geri bildirimi paylaşılmadığı için geçici class-weighted Random Forest referansına dayanır; nihai Proje 1 modeliyle yenilenmelidir.

## Katkı ve yapay zekâ beyanı

Katkı beyanı, grup üyelerinin gerçekten yaptığı kodlama, analiz, yorum ve sunum işlerini ve anlattıkları alt başlıkları göstermelidir. Grup üyeleri/paylaşımı henüz sağlanmadığı için katkılar uydurulmamıştır; tablo teslimden önce doldurulmalıdır.

| Üye | Okul numarası | Gerçek katkı ve sunum alt başlığı |
|---|---|---|
| Şahin Güngördü | 264312011 | [Kendi yaptığı işleri ve sunum kısmını yazın] |
| Üye 2 | [Eklenecek] | [Gerçek katkı ve sunum kısmı] |
| Üye 3 | [Eklenecek] | [Gerçek katkı ve sunum kısmı] |
| Üye 4 | [Eklenecek] | [Gerçek katkı ve sunum kısmı] |
| Üye 5 | [Eklenecek] | [Gerçek katkı ve sunum kısmı] |

**Yapay zekâ beyanı:** ChatGPT, yönergeyi sınıflandırma, analiz planı, notebook kod taslağı ve README metni hazırlamada kullanıldı. Grup üyeleri kodu ve sonuçları incelemeli; katkı beyanı ile sunumu kendi gerçek çalışmalarına göre tamamlamalıdır.

## Teslim öncesi tamamlanacaklar

- Grup adını ve tüm üyelerin ad/numaralarını ekleyin; grup büyüklüğünü doğrulayın.
- Katkı tablosunu GitHub commit geçmişi ve sunumla tutarlı gerçek işlerle tamamlayın.
- Gerçek Proje 1 modelini/geri bildirimini paylaşarak geçici model kullanılan analizleri yenileyin; Proje 1 Ek Paket 2'yi tam Proje 1 notebook'una ekleyin.
- Her notebook'u sıfırdan **Tümünü çalıştır** ile çalıştırın; aynı `.ipynb` dosyalarını GitHub'a ve STIX'e teslim edin.
