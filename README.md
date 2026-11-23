# BIL545 — Online alışverişte satın alma niyeti

## Öğrenci bilgileri

- **İsim Soyisim:** Şahin Güngördü
- **Okul numarası:** 264312011

Bu depo, aynı UCI Online Shoppers Purchasing Intention veri kümesiyle hazırlanan iki ayrı ders çıktısını içerir. CSV veri dosyası GitHub'a eklenmez; iki notebook da çalışma dizininde CSV varsa onu okur, yoksa UCI dataset id 468'den indirir.

## İçerik

- `proje1-ek-paket2/BIL545_Proje1_EkPaket2_OznitelikSecimi.ipynb`: Proje 1 Ek Paket 2 için bağımsız öznitelik seçimi/kararlılık bölümü. Filtre, RFE ve gömülü ExtraTrees yöntemlerini, aynı CV bölmelerini ve 100 tabakalı %70 alt örneklemi kullanır. Resmî teslimde gerçek Proje 1 notebook'una eklenmelidir.
- `proje2/BIL545_Proje2_OnlineShoppers.ipynb`: Öğretim üyesinin Proje 2 taslağının doldurulmuş hali; zorunlu Bölüm 1–3, Ek Paket 1 ve veri yapısına uygun Ek Paket 2 / Seçenek A içerir. 5 kişilik grup kapsamı varsayılmıştır.

## Colab'da çalıştırma

1. İlgili `.ipynb` dosyasını Colab'da açın.
2. CSV kullanacaksanız `online_shoppers_intention.csv` dosyasını notebook çalışma dizinine yükleyin. Yüklemezseniz notebook UCI'dan indirir.
3. **Çalışma zamanı → Tümünü çalıştır** ile hücreleri sırayla çalıştırın.
4. Proje 1'in gerçek modelini/öğretim üyesi geri bildirimini, grup adını ve üyeleri, öğrenci numaralarını ve katkı beyanını gerçek bilgilerle tamamlayın. Proje 2 taslağı 5 kişilik gruplar için iki ek paketi de istediğinden grup kapsamını doğrulayın.
5. Teslim öncesi notebook'u baştan sona tekrar çalıştırıp STIX'e de yükleyin.

## Veri ve tahmin sınırı

Veri 12.330 e-ticaret oturumu, 17 öznitelik ve `Revenue` hedefini içerir. PageValues'ın tahmin anında güvenli biçimde mevcut olduğu doğrulanmadığından Proje 2 ana referans modeline katılmamış, yalnızca duyarlılık karşılaştırmasında gösterilmiştir. Proje 1 Ek Paket 2 seçici frekanslarında ise sütun veri kümesinin parçası olduğu için yer alır; bu bulgu zamanlama/sızıntı riskini ortadan kaldırmaz.

Kaynak: [UCI Online Shoppers Purchasing Intention](https://archive.ics.uci.edu/dataset/468/online) (CC BY 4.0).
