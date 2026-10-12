# Prompt Mühendisliği Eğitimi – Ders 4

## Görsel ve Multimedya Promptları, Yapay Sinir Ağları ve Üretken Yapay Zekâ (Yaklaşık 2,5 Saat)

---

## Ders 4 – 150 Dakika

### Önceki Dersle Bağlantı

Önceki derste sistem talimatlarıyla kendi araştırma asistanımızı tanımladık, çoklu deneme ile en iyi bildiri özetini seçtik, saha fotoğraflarından sunum şemaları ürettik ve bir akademik blog yazısını uygun görseliyle birlikte hazırladık. Görsel promptlarımızı bir **stil rehberi** ile tutarlı tuttuk.

Bu dersin ilk yarısında görsel promptları bir mimarın diliyle derinleştireceğiz: **tarz, ışık, perspektif, malzeme, kompozisyon.** Midjourney ve ChatGPT'nin görsel modeli ile sunum ve poster görselleri üreteceğiz, ses ve video araçlarını araştırma sürecine (özellikle sözlü tarih ve görüşmeler) bağlayacağız ve yayımlanan bir makale için sosyal medya duyuru seti hazırlayacağız.

Dersin ikinci yarısında perdenin arkasına bakacağız: Bütün bu araçların temelindeki **yapay sinir ağları** nasıl çalışır? Kâğıt kalemle küçük bir sinir ağını kendimiz hesaplayacağız ve Ders 1'de gördüğümüz "bir sonraki kelimeyi tahmin etme" fikrinin prompt mühendisliğine nasıl yön verdiğini anlayacağız.

### Dersin Hedefleri

Bu dersin sonunda öğrenci:

- Görsel prompt yapısının bileşenlerini (konu, mekân, tarz, ışık, perspektif, malzeme, kompozisyon, teknik parametreler) kullanabilecek.
- Midjourney ve ChatGPT (GPT Image) ile görsel üretim promptları yazabilecek ve temel parametreleri bilecek.
- Ses ve video araçlarının araştırma ve akademik iletişim süreçlerindeki kullanımını açıklayabilecek.
- Yayımlanan bir araştırma için tutarlı bir sosyal medya duyuru seti hazırlayabilecek.
- Yapay sinir ağının ne olduğunu ve temel prensiplerini sade bir dille açıklayabilecek.
- Basit bir yapay nöronun hesabını elle yapabilecek.
- Token tahmini kavramının prompt yazımına etkisini açıklayabilecek.
- Yapay sinir ağlarının sağlık, finans ve otomotiv sektörlerindeki kullanımına örnek verebilecek.

### Süre Planı

| Bölüm | Süre |
|---|---|
| Giriş ve önceki dersin tekrarı | 5 dk |
| Konu 1: Görsel prompt yapıları, Midjourney ve GPT Image ile görsel üretim | 35 dk |
| Konu 2: ChatGPT + ses + video entegrasyonları | 15 dk |
| Uygulama: Sosyal medya için içerik üretme | 20 dk |
| Konu 3: Yapay sinir ağları nedir? Temel prensipler, insan zekâsıyla benzerlik | 25 dk |
| Konu 4: Sinir ağı ile veri sınıflandırma (elle hesap) | 20 dk |
| Konu 5: Token tahmini, prompt mühendisliği yaklaşımı ve üretken yapay zekâ devrimi | 15 dk |
| Konu 6: Sağlık, finans, otomotiv ve gerçek hayatta yapay zekâ kullanım örnekleri | 10 dk |
| Ders özeti, mini quiz | 5 dk (ders sonu uygulaması evde) |
| **Toplam** | **150 dk** |

### Derse Hazırlık

- ChatGPT veya Gemini'de görsel üretim özelliği açık olsun.
- Midjourney ücretli bir abonelik gerektirir. Abonelik yoksa Midjourney promptlarını ChatGPT veya Gemini ile deneyebilirsiniz; parametre kısımlarını (`--ar` gibi) çıkarıp oranı cümleyle yazmanız yeterlidir.
- Konu 4 için kâğıt, kalem ve hesap makinesi hazırlayın.

---

### Giriş ve Tekrar (5 dk)

**Soru:** Görsel düzenleme promptunun dört bileşeni neydi?

**Cevap:** Neyi değiştir, nasıl değiştir, neyi koru, hangi üslupta.

**Soru:** Geçen ders hazırladığımız stil rehberinde hangi bilgiler vardı?

**Cevap:** Teknik (mürekkep + sulu boya), renk paleti, ışık, kompozisyon, insan figürü ve görselde yazı olmaması.

---

### Konu 1: Görsel Prompt Yapıları ve Midjourney / GPT Image ile Görsel Üretim (35 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir görselleştirme ofisine render siparişi verdiğinizi düşünün. Yalnızca "Evin bir görselini istiyorum" demezsiniz. Kamera açısını, saati, güneşin yönünü, malzemeleri, atmosferi ve görselin hangi formatta olacağını belirtirsiniz. Mimari görselleştirmenin bu dili, görsel prompt yazmanın da temelidir; görsel prompt yazmak bu dili yapay zekâya aktarmaktır.

**Basit açıklama:** Görsel prompt, bir görsel üretim modeline ne çizeceğini ve nasıl çizeceğini anlatan metindir. İyi bir görsel prompt; konuyu, ortamı, tarzı, ışığı, bakış açısını ve kompozisyonu tarif eder.

**Teknik tanım:** Metinden görsele (text-to-image) modeller, metin promptunu sayısal bir temsile dönüştürür ve bu temsile uygun bir görüntüyü adım adım üretir. Promptta geçen kavramlar (örneğin "aksonometrik", "altın saat ışığı") modelin eğitildiği görsel–metin çiftlerindeki karşılıklarına göre yorumlanır.

#### Neden Öğreniyoruz?

- **Makale ve tez:** Kavramsal şemalar, karşılaştırmalı diyagramlar (temsili olduğu belirtilerek).
- **Akademik sunum:** Konferans sunumları ve posterler için atmosfer görselleri.
- **Mimarlık pratiği:** Konsept aşamasında hızlı atmosfer ve malzeme denemeleri.
- **Akademik iletişim:** Yayın duyuruları, araştırma blogu ve proje web sayfası görselleri.

#### Temel Kavramlar: Görsel Promptun Bileşenleri

| Bileşen | Soru | Mimari örnek |
|---|---|---|
| Konu | Ne görünüyor? | Geleneksel bir Türk evinin sofası |
| Ortam / bağlam | Nerede, ne zaman? | 19. yüzyıl, Safranbolu, sonbahar |
| Tarz / teknik | Nasıl çizilmiş? | Sulu boya, karakalem, fotogerçekçi, aksonometrik çizim |
| Işık | Işık nasıl? | Öğleden sonra yumuşak güneş, bulutlu gün, altın saat |
| Perspektif / kamera | Nereden bakıyoruz? | Göz hizası, kuş bakışı, kurbağa bakışı, geniş açı, kesit perspektif |
| Malzeme ve doku | Yüzeyler neden yapılmış? | Ahşap çıtalı tavan, kireç sıva, kerpiç |
| Kompozisyon | Elemanlar nasıl yerleşmiş? | Simetrik, merkezde pencere, ön planda sedir |
| Renk paleti | Hangi renkler? | Toprak tonları, krem, soluk turkuaz |
| Atmosfer | Hangi duygu? | Sakin, nostaljik, terk edilmiş |
| Teknik parametreler | Oran, kalite, sürüm | 3:2 oran, yüksek çözünürlük |

**Mimari çizim terimleri sözlüğü:**

| Türkçe kavram | Promptta işe yarayan ifade |
|---|---|
| Plan | "architectural floor plan, top view, black lines on white" |
| Kesit | "architectural section drawing" / "sectional perspective" |
| Aksonometri | "axonometric drawing", "isometric view" |
| Patlatılmış aksonometri | "exploded axonometric diagram" |
| Rölöve havası | "measured drawing style, fine ink lines" |
| Eskiz | "loose architectural sketch, pen and ink" |
| Maket fotoğrafı | "white cardboard architectural model photograph" |

> **Not:** Modellerin çoğu Türkçe promptları anlar; ancak teknik mimari terimlerde İngilizce karşılıkları kullanmak bazen daha isabetli sonuç verir. Türkçe yazıp sonuç beklentinizi karşılamazsa İngilizce deneyin; bu da bir çoklu deneme yöntemidir.

#### İki Ana Araç: Midjourney ve ChatGPT (GPT Image)

| Özellik | Midjourney | ChatGPT – GPT Image |
|---|---|---|
| Erişim | midjourney.com (web) ve Discord, ücretli abonelik | ChatGPT içinde (ücretsiz sürümde sınırlı), OpenAI API'de `gpt-image` modelleri |
| Güçlü yanı | Estetik, atmosfer, sanatsal üslup | Talimata sadakat, sohbetle düzenleme, görseldeki yazılar |
| Prompt biçimi | Kısa-orta uzunlukta tarif + parametreler (`--ar 3:2`) | Doğal dilde, uzun ve ayrıntılı tarif |
| Düzenleme | Editör, varyasyon, yeniden üretme | Sohbetle "şunu değiştir" |
| Tutarlılık araçları | Stil referansı (`--sref`), kişiselleştirme, moodboard | Referans görsel yüklemek, aynı sohbette devam etmek |

> **Not:** Bu araçlar çok hızlı güncelleniyor. 2026 itibarıyla Midjourney'in varsayılan modeli V8 ailesindendir; ChatGPT'de görsel üretimi GPT Image modeliyle yapılır ve eski DALL·E modelleri kullanımdan kaldırılmıştır. Parametrelerin güncel listesi için Midjourney'in kendi belgelerine bakın.

**Sık kullanılan Midjourney parametreleri:**

| Parametre | Ne yapar? | Örnek |
|---|---|---|
| `--ar` | En-boy oranı | `--ar 3:2` (yatay), `--ar 4:5` (Instagram dikey) |
| `--s` (stylize) | Midjourney'in kendi estetiğinin ne kadar baskın olacağı (0–1000) | `--s 50` (talimata sadık), `--s 500` (daha sanatsal) |
| `--c` (chaos) | Dört görsel arasındaki çeşitlilik (0–100) | `--c 30` |
| `--no` | İstenmeyen öğe | `--no people, text` |
| `--seed` | Sonucu tekrarlanabilir kılmaya yardım eden sayı | `--seed 1234` |
| `--raw` | Daha az "süslenmiş", daha fotoğrafik/sade sonuç | `--raw` |
| `--sref` | Bir görselin üslubunu referans almak | `--sref [görsel bağlantısı]` |

#### Basit Örnek

Zayıf görsel prompt:

```text
Türk evi
```

Güçlü görsel prompt (Midjourney):

```text
Interior of a traditional Ottoman Turkish house, central sofa hall with low wooden divans
covered in kilims, carved wooden ceiling, white lime-plastered walls, bay window (cumba)
at the end, soft afternoon light, eye-level view, watercolor and fine ink line architectural
illustration, warm earth tones, calm and nostalgic --ar 3:2 --s 100 --no people, text
```

Aynı istek GPT Image için (doğal dil, Türkçe):

```text
Geleneksel bir Osmanlı-Türk evinin sofasının iç mekân illüstrasyonu. Göz hizasından bakış.
Sofanın iki yanında odalara açılan ahşap kapılar, uçta cumbalı pencere ve önünde kilim serili
alçak sedirler. Oymalı ahşap tavan, kireç sıvalı beyaz duvarlar. Öğleden sonra pencereden giren
yumuşak ışık. Beyaz kâğıt üzerine ince mürekkep çizgi ve sulu boya; sıcak toprak tonları.
Sakin ve nostaljik bir atmosfer. Yatay 3:2 oran. İnsan figürü ve yazı olmasın.
```

**Tahmin sorusu:** İki promptun içeriği aynı. Sizce Midjourney ile GPT Image sonuçları aynı mı olur?

**Cevap:** Hayır. Midjourney genellikle daha "sanatsal" ve atmosferik yorumlar; GPT Image ise listedeki öğelere (cumba, sedir, kapılar) daha sadık kalma eğilimindedir. Bu yüzden önemli görsellerde iki aracı da denemek bir çoklu deneme stratejisidir.

#### Birlikte Uygulayalım: Bir Mekân, Dört Temsil

**Amaç:** Görsel promptta tarz ve perspektif bileşenlerini değiştirerek aynı mekânın farklı temsillerini üretmek.

**Senaryo:** Bir konferans sunumunda "hayatlı ev" plan tipi anlatılacak. Dinleyicilerin mekânı anlaması için aynı evi dört farklı temsil biçiminde göstermek istiyoruz.

**Adımlar:**

1. ChatGPT'de (veya Gemini'de) yeni bir sohbet açın.
2. **Temel tarif** yazın ve Prompt Defterim'e kaydedin (her denemede bunu kullanacağız):

```text
TEMEL TARİF: İki katlı, geleneksel bir Anadolu evi. Üst katta güneye bakan, bir yanı ahşap
direklerle açık "hayat" (yarı açık sofa). Hayata açılan iki oda. Ahşap karkas üst kat,
taş zemin kat, kiremit çatı, geniş saçaklar.
```

3. **Deneme 1 – Göz hizası atmosfer görseli:**

```text
[TEMEL TARİF] Avludan, göz hizasından bakış. Yaz sabahı, yumuşak ışık. Sulu boya ve ince mürekkep
illüstrasyon, sıcak toprak tonları. İnsan figürü ve yazı yok. Yatay 3:2.
```

4. **Deneme 2 – Kesit perspektif:**

```text
[TEMEL TARİF] Evin hayattan ve bir odadan geçen kesit perspektifi. İç mekânlar görünür olsun:
hayattaki sedir, odadaki yüklük ve ocak. Beyaz zemin üzerine siyah ince çizgi, sadece hayat
alanı soluk okra renkle vurgulansın. Teknik ama okunaklı bir mimari çizim üslubu.
```

5. **Deneme 3 – Aksonometrik diyagram:**

```text
[TEMEL TARİF] Üst katın patlatılmış aksonometrik diyagramı: çatı yukarı kaldırılmış, hayat ve
odalar görünür. Hayat alanı turuncu, odalar açık gri. Beyaz arka plan, yazı ve etiket yok.
```

6. **Deneme 4 – Maket fotoğrafı:**

```text
[TEMEL TARİF] Beyaz mukavva ve balsa ağacından yapılmış bir mimari maketin fotoğrafı.
Masa üzerinde, yandan yumuşak stüdyo ışığı, sığ alan derinliği.
```

7. Dört görseli yan yana koyun.
8. Mimar gözüyle değerlendirin:

| Görsel | Hayat mekânı anlaşılıyor mu? | Mimari hata var mı? | Sunumda nerede kullanılır? |
|---|---|---|---|
| Atmosfer | | | |
| Kesit | | | |
| Aksonometri | | | |
| Maket | | | |

**Beklenen sonuç:** Aynı mekânın dört farklı temsili. Atmosfer görseli sunumun giriş slaytına, kesit ve aksonometri plan tipini açıklayan slaytlara, maket görseli posterin ana görseline uygun olabilir.

**Açıklama:** Temel tarif sabit kaldı; sadece **tarz** ve **perspektif** bileşenleri değişti. Bu yöntem, bir mimarın aynı projeyi plan, kesit, perspektif ve maketle anlatmasıyla aynıdır.

> **Dikkat:** Yapay zekâ ile üretilen kesit ve aksonometriler **ölçülü teknik çizim değildir.** Duvar kalınlıkları, kat yükseklikleri, taşıyıcı sistem tutarsız olabilir. Sunumda ve yayında "şematik / temsili" olarak etiketlenmelidir. Gerçek rölöve çizimlerinin yerini tutmaz.

#### Sıra Sizde 1 (10 dk)

**Amaç:** Görsel prompt bileşenlerini kullanarak tutarlı bir illüstrasyon serisi üretmek.

**Görev:** "Konutta mutfağın dönüşümü" konulu bir akademik poster için üç görsellik bir seri üretin: geleneksel evin mutfağı, 1960'ların apartman mutfağı, bugünün açık mutfağı.

**İstenenler:**

- Üç görselde de aynı tarz, ışık ve perspektif kullanılsın (sadece konu değişsin).
- Ders 3'teki stil rehberini kullanın.
- Her görsel için mimari kontrol yapın.

**Beklenen sonuç:** Yan yana konduğunda zamansal dönüşümü anlatan, aynı görsel dilde üç illüstrasyon.

**İpucu:** Önce "sabit kısım" (tarz + ışık + perspektif) yazın, sonra her görsel için sadece konu cümlesini değiştirin.

#### Çözüm

Sabit kısım:

```text
Göz hizasından, mutfağın kapısından içeriye bakış. Sabah ışığı, pencereden giren yumuşak güneş.
Beyaz kâğıt üzerine ince siyah mürekkep çizgi ve hafif sulu boya; sıcak toprak tonları, krem ve
soluk turkuaz vurgular. İnsan figürü ve yazı yok. Yatay 3:2.
```

Konu cümleleri:

1. "Geleneksel bir Anadolu evinin ana yapıdan ayrı, avluya açılan mutfağı: duvarda ocak, isli tavan, yerde bakır kaplar, tahta raflarda çömlekler."
2. "1960'lar Türkiye'sinde bir apartman dairesinin küçük, kapalı mutfağı: tezgâh üstü fırın, emaye lavabo, duvarda fayans, küçük bir masa ve iki tabure."
3. "Günümüzde bir apartman dairesinde salona açılan açık mutfak: ada tezgâh, bar tabureleri, gömme ankastre cihazlar, arka planda salon koltuğu."

Her görsel için şöyle yazılır: `[konu cümlesi] + [sabit kısım]`.

#### Sık Yapılan Hatalar

**Hata 1: Sadece konu yazıp tarzı ve ışığı belirtmemek**

- Hatalı: "Bir mutfak."
- Doğru: Konu + tarz + ışık + perspektif + renk.

**Hata 2: Birbiriyle çelişen tarzlar**

- Hatalı: "Fotogerçekçi sulu boya eskiz."
- Doğru: Bir ana tarz seçin: "Sulu boya eskiz" veya "fotogerçekçi render".

**Hata 3: Seride sabit kısmı değiştirmek**

- Neden hata? Seri dağınık görünür.
- Düzeltme: Sabit kısmı Prompt Defterim'den kopyalayın, elle yeniden yazmayın.

**Hata 4: Gerçek mimarların veya yaşayan sanatçıların adlarıyla üslup kopyalamak**

- Neden hata? Telif ve etik sorunlara yol açabilir; araçlar bazı isimleri engelleyebilir.
- Düzeltme: Üslubu tarif edin: "ince mürekkep çizgi, sade geometri, beyaz zemin."

---

### Konu 2: ChatGPT + Ses + Video Entegrasyonları (15 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir araştırmacı, eski bir ev sahibesiyle yaptığı bir saatlik sözlü tarih görüşmesini eskiden günlerce dinleyip deşifre ederdi. Bugün kaydı bir yapay zekâ aracına vererek dakikalar içinde metne dönüştürebilir, sonra bu metni özetletebilir.

**Basit açıklama:** Yapay zekâ yalnızca metin ve görselle değil, sesle ve videoyla da çalışabilir: konuşmayı yazıya çevirebilir (transkripsiyon), yazıyı sese çevirebilir (seslendirme), sesli sohbet edebilir ve kısa videolar üretebilir.

**Teknik tanım:**

| Teknoloji | İngilizce adı | Ne yapar? |
|---|---|---|
| Konuşmadan metne | Speech-to-Text (STT), transkripsiyon | Ses kaydını yazıya döker |
| Metinden konuşmaya | Text-to-Speech (TTS) | Yazıyı doğal sesle okur |
| Sesli asistan | Voice mode | Konuşarak sohbet etmeyi sağlar |
| Metinden videoya | Text-to-Video | Prompttan kısa video üretir |
| Görselden videoya | Image-to-Video | Durağan bir görseli hareketlendirir |

#### Neden Öğreniyoruz?

Araştırma ve akademik iletişim sürecinde ses ve video şu noktalarda işe yarar:

| İhtiyaç | Araç türü | Örnek kullanım |
|---|---|---|
| Sözlü tarih görüşmesi | Transkripsiyon + özetleme | Eski apartman sakinleriyle görüşmeleri yazıya dökmek |
| Saha notları | Sesli not + transkripsiyon | Saha gezisinde konuşarak not almak, sonra düzenletmek |
| Düşünceyi sesli geliştirme | Sesli sohbet | Yürürken bir argümanı yapay zekâyla konuşarak sınamak |
| Ders ve seminer kayıtları | Transkripsiyon + özetleme | Bir seminerin kaydından not çıkarmak |
| Akademik iletişim | Seslendirme | Araştırma blogu yazısının sesli sürümü, kısa podcast tanıtımı |
| Video özet (video abstract) | Görselden video, seslendirme | Makale için kısa tanıtım videosu |

**Örnek araçlar:** ChatGPT, Gemini ve Claude mobil uygulamalarındaki sesli sohbet; toplantı ve görüşme transkripsiyonu yapan uygulamalar; ElevenLabs gibi seslendirme araçları; Runway, Google Veo gibi video üretim araçları. Araç seçenekleri hızla değiştiği için kullanmadan önce güncel durumu kontrol edin.

#### Birlikte Uygulayalım: Görüşme Kaydından Okuma Notuna

**Amaç:** Bir ses kaydını metne dönüştürüp araştırma notuna çevirmek.

**Senaryo:** Apartmanlaşma üzerine bir sözlü tarih araştırmasının pilot çalışmasında, 1970'lerde bir apartman dairesinde büyümüş bir kişiyle kısa bir deneme görüşmesi yapıldı.

**Adımlar:**

1. Telefonun ses kayıt uygulamasıyla, ders sırasında iki kişi arasında 2–3 dakikalık kısa bir "deneme görüşmesi" kaydedin. Konu: "Çocukluğunuzdaki evin salonunu anlatır mısınız?"
2. ChatGPT veya Gemini mobil uygulamasında yeni bir sohbet açın ve ses dosyasını yükleyin (veya uygulamanın sesli not/transkripsiyon özelliğini kullanın).
3. Şu promptu yazın:

```text
Bu ses kaydını Türkçe olarak yazıya dök. Konuşmacıları "Görüşmeci" ve "Katılımcı" olarak ayır.
Anlaşılmayan yerlere [anlaşılmıyor] yaz. Hiçbir cümleyi düzeltme veya özetleme; olduğu gibi aktar.
```

4. Transkripti kontrol edin: Kaçırılan veya yanlış duyulan kelime var mı?
5. Ardından şu promptu yazın:

```text
Bu transkriptten bir sözlü tarih okuma notu çıkar:
- Bahsedilen mekânlar ve eşyalar (liste)
- Mekânların kullanım biçimleri (kim, ne zaman, ne için?)
- Duygusal ifadeler (katılımcının kendi kelimeleriyle kısa alıntılar)
- Hangi araştırma sorusuna veya temaya veri sağlıyor?
Transkriptte olmayan hiçbir bilgiyi ekleme.
```

**Beklenen sonuç:** Konuşmacıları ayrılmış bir transkript ve araştırma temalarıyla ilişkilendirilmiş bir okuma notu.

**Açıklama:** Transkripsiyon ve özetlemeyi **iki ayrı adımda** yaptık. Önce ham metni elde ettik ve kontrol ettik, sonra yorumlattık. Tek adımda "kaydı özetle" deseydik, transkripsiyon hatalarını göremezdik.

> **Dikkat:** Sözlü tarih görüşmelerinde katılımcıdan **kayıt ve yapay zekâ ile işleme için açık izin** alın. Kişisel verileri (tam isim, adres) içeren kayıtları yüklemeden önce kullandığınız aracın veri politikasını kontrol edin. Akademik çalışmalarda etik kurul gereklilikleri de söz konusu olabilir.

#### Sık Yapılan Hatalar

**Hata 1: Transkripti kontrol etmeden kullanmak**

- Neden hata? Özel isimler, yer adları ve mimari terimler (örneğin "yüklük", "cumba") yanlış yazılabilir.
- Düzeltme: Transkripti kayıtla karşılaştırarak düzeltin.

**Hata 2: Katılımcının sözlerini modelin "düzelttiği" hâliyle alıntılamak**

- Neden hata? Alıntı, katılımcının gerçek sözlerini yansıtmalıdır.
- Düzeltme: "Olduğu gibi aktar, düzeltme" yönergesini verin.

**Hata 3: Üretilen videoları belge gibi kullanmak**

- Neden hata? Yapay zekâ videosu tarihsel bir kayıt değildir.
- Düzeltme: "Temsili, yapay zekâ ile üretilmiştir" notunu ekleyin.

---

### Uygulama: Sosyal Medya İçin İçerik Üretme (20 dk)

#### Birlikte Uygulayalım: Yayımlanan Bir Makale İçin 3 Gönderilik Duyuru Serisi

**Amaç:** Metin, görsel ve tutarlı görsel kimliği birleştirerek bir akademik sosyal medya serisi üretmek.

**Senaryo:** "Apartman dairesinde salonun temsil mekânına dönüşümü" konulu bir makale hakemli bir dergide yayımlandı. Makalenin daha fazla araştırmacıya ve ilgili okura ulaşması için LinkedIn ve Instagram'da 3 gönderilik bir duyuru serisi hazırlanacak.

**Problem nedir?** Her platformun okuru ve dili farklı; ama mesaj bulgulara sadık ve görsel kimlik tutarlı olmalı.

**Nasıl çözeceğiz?** Önce bir içerik planı tablosu, sonra her gönderi için görsel ve iki platforma göre metin üreteceğiz.

**Hangi bilgileri kullanacağız?** Makalenin özeti ve ana bulguları, Ders 3'teki stil rehberi, platform özellikleri.

**Platform özellikleri:**

| Platform | Okur | Ton | Görsel oranı | Metin uzunluğu |
|---|---|---|---|---|
| LinkedIn | Akademisyenler, mimarlar, kurumlar | Profesyonel, bulgu odaklı | 1.91:1 yatay veya 1:1 | 120–180 kelime |
| Instagram | Alanla ilgilenen geniş kitle, öğrenciler | Anlaşılır, merak uyandıran, soru soran | 4:5 dikey | 60–100 kelime + hashtag |

**Adımlar:**

1. Araştırma projesi içinde yeni sohbet açın ve makalenin özetini yapıştırın.
2. İçerik planı isteyin:

```text
Yukarıdaki makale özetine dayanarak 3 gönderilik bir duyuru serisi planla:
1. gönderi: Makalenin yayımlandığının duyurusu ve araştırma sorusu
2. gönderi: En dikkat çekici bulgu
3. gönderi: Yöntem ve kaynaklar (dönem dergileri, plan arşivleri)
Tablo olarak ver: Gönderi no | Ana mesaj (1 cümle) | Görsel fikri (1 cümle) | Okura sorulacak soru
Özette olmayan hiçbir bulguyu ekleme.
```

3. Tabloyu inceleyin ve gerekiyorsa düzeltin.
4. 1. gönderi için görsel üretin:

```text
[STİL REHBERİ]
1. gönderi için görsel üret: [tablodaki görsel fikri]. Yatay 1.91:1 oran.
Görselin sol kısmında, sonradan makale başlığı eklenebilmesi için sade bir boşluk bırak. Görselde yazı olmasın.
```

5. Aynı gönderi için iki platform metnini isteyin:

```text
1. gönderi için iki metin yaz:
A) LinkedIn: profesyonel, 150 kelime civarı, makalenin yayımlandığını ve araştırma sorusunu duyur,
   derginin adı için [DERGİ], bağlantı için [DOI BAĞLANTISI] yaz, en fazla 3 hashtag.
B) Instagram: anlaşılır ve merak uyandıran, 80 kelime civarı, okura tablodaki soruyu sor,
   sonunda 5 Türkçe hashtag.
Bulguları abartma; özette olmayan bilgi ekleme.
```

6. 2. ve 3. gönderiler için 4. ve 5. adımları tekrarlayın.
7. Üç görseli yan yana koyun: Aynı seriden oldukları anlaşılıyor mu?
8. Metinleri makalenin özetiyle karşılaştırın: Abartılmış ya da özette olmayan bir iddia var mı?

**Beklenen sonuç:** 3 görsel + 6 metin (her gönderi için LinkedIn ve Instagram), tutarlı görsel kimlik, bulgulara sadık mesajlar.

**Açıklama:** İçerik planını önce tablo hâlinde yapmak, serinin bütününü görmemizi sağladı. Stil rehberi görsel tutarlılığı, platform tablosu ise metinlerin doğru tona sahip olmasını sağladı. Ders 2'deki ton bilgimiz ve Ders 3'teki görsel–metin entegrasyonu burada birleşti. Son kontrol adımı, akademik iletişimde en sık yapılan hatayı (bulguyu abartmayı) önler.

#### Sıra Sizde 2 (Evde, 20 dk)

**Amaç:** Duyuru serisini bağımsız olarak tamamlamak.

**Görev:** Seriye 4. bir gönderi ekleyin: "Bu araştırmadan sonra ne çalışılabilir?" (gelecek araştırma önerileri). Görseli ve iki platform metnini üretin. Ayrıca görseli bir görselden video aracıyla 5 saniyelik kısa bir hareketli görsele dönüştürmeyi deneyin (isteğe bağlı).

**İstenenler:** 1 görsel, 1 LinkedIn metni, 1 Instagram metni, isteğe bağlı kısa video.

**İpucu:** Video promptunda hareketi küçük tutun: "Pencereden giren ışık yavaşça yer değiştirsin. Kamera sabit."

#### Çözüm

Görsel promptu:

```text
[STİL REHBERİ]
Yan yana iki sade plan şeması: solda geleneksel sofalı bir ev planı, sağda koridorlu bir apartman
dairesi planı. İki planın ortasında, ileriye doğru uzanan ince kesikli bir çizgi.
Beyaz zemin, ince siyah çizgiler, ortak alanlar soluk turkuaz ile vurgulu.
Yatay 1.91:1 oran. Görselde yazı yok.
```

LinkedIn metni (örnek):

> Makalemizin bıraktığı sorulardan biri: Salonun bir "vitrin" mekânına dönüşmesi, bugünün açık plan dairelerinde nasıl bir karşılık buluyor? Çalışmamız 1950–1980 dönemine odaklandı; sonraki dönemlerin, özellikle kentsel dönüşüm konutlarının benzer bir yöntemle incelenmesi karşılaştırmalı bir tablo sunabilir. Bu alanda çalışan araştırmacılarla tartışmaktan memnuniyet duyarız. Makale: [DOI BAĞLANTISI] #KonutÇalışmaları #MimarlıkTarihi #GündelikHayat

Instagram metni: Okura "Sizin evinizde salon hâlâ misafir için mi?" diye soran, araştırmanın 1950–1980 dönemine odaklandığını ve bugünün evlerinin de incelenmeye değer olduğunu söyleyen 80 kelimelik bir metin.

### Konu 3: Yapay Sinir Ağları (YSA) Nedir? Temel Prensipler ve İnsan Zekâsıyla Benzerlik (25 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir çocuk "ev" kavramını nasıl öğrenir? Kimse ona "dört duvar + çatı + kapı = ev" diye kural öğretmez. Yüzlerce ev görür; bazıları ahşap, bazıları beton, bazıları çadır. Büyükler "bu ev", "bu ev değil, bu dükkân" der. Çocuk zamanla kendi kafasında "ev"i tanıyan bir sezgi geliştirir.

**Basit açıklama:** Yapay sinir ağı, bilgisayarın da örneklerden bu şekilde öğrenmesini sağlayan bir yöntemdir. Çok sayıda basit hesap biriminin (yapay nöron) birbirine bağlanmasıyla oluşur. Ağ, örnekler gördükçe bu bağlantıların gücünü ayarlar ve doğru cevap vermeyi öğrenir.

**Teknik tanım:** Yapay sinir ağı (YSA, Artificial Neural Network – ANN); girdileri ağırlıklarla çarpıp toplayan ve sonucu bir aktivasyon fonksiyonundan geçiren yapay nöronların katmanlar hâlinde birbirine bağlanmasıyla oluşan bir hesaplama modelidir. Ağ, eğitim verisiyle tahmin hatasını en aza indirecek şekilde ağırlıklarını güncelleyerek öğrenir.

#### Neden Öğreniyoruz?

"Ben prompt yazacağım, sinir ağını neden öğreniyorum?" sorusu çok doğal. Cevap:

- Modelin neden **kendinden emin ama yanlış** cevap verebildiğini anlamak için,
- Neden **örnek vermenin** (few-shot) bu kadar etkili olduğunu anlamak için,
- Görsel modellerin neden "sık görülen" üsluplarda daha başarılı olduğunu anlamak için,
- Akademik metinlerde yapay zekâdan bahsederken doğru kavramları kullanmak için.

#### Temel Kavramlar

**Kavram: Yapay nöron**

- Basit açıklama: Birkaç sayı alan, her birini bir önem katsayısıyla çarpıp toplayan ve "eşik aşıldı mı?" diye karar veren küçük bir hesap birimi.
- Benzetme: Bir jüri üyesi düşünün. Projeye bakarken işlev, estetik ve maliyete farklı önem verir. Puanları önem dereceleriyle çarpıp toplar; toplam belli bir eşiği geçerse "geçti" der.

**Kavram: Ağırlık (weight)**

- Basit açıklama: Her girdinin ne kadar önemli olduğunu gösteren sayı.
- Örnek: Jüri üyesi için "işlev" ağırlığı 3, "estetik" ağırlığı 2 olabilir.

**Kavram: Eşik / sapma (bias)**

- Basit açıklama: Nöronun "evet" demesi için aşılması gereken seviyeyi ayarlayan sayı.
- Örnek: Sıkı bir jüri üyesinin eşiği yüksektir.

**Kavram: Aktivasyon fonksiyonu**

- Basit açıklama: Toplamı bir karara dönüştüren kural. En basit hâli: "Toplam 0'dan büyükse 1, değilse 0."

**Kavram: Katman (layer)**

- Basit açıklama: Yan yana dizilmiş nöron grubu. Girdi katmanı, gizli katmanlar ve çıktı katmanı vardır.
- Benzetme: Bir yarışmada ön eleme jürisi, teknik jüri ve ana jüri gibi aşamalı değerlendirme.

**Kavram: Eğitim (training)**

- Basit açıklama: Ağın örnekler görüp hata yaptıkça ağırlıklarını düzeltmesi.
- Benzetme: Bir öğrencinin her kritikte aldığı geri bildirimle bir sonraki projesini düzeltmesi.

**Kavram: Derin öğrenme (deep learning)**

- Basit açıklama: Çok sayıda gizli katmanı olan sinir ağlarıyla yapılan öğrenme. Bugünkü dil ve görsel modellerinin tamamı derin öğrenme modelleridir.

#### Yapay Sinir Ağının Temel Prensipleri

1. **Örnekten öğrenme:** Kurallar yazılmaz; örnekler verilir.
2. **Ağırlıklı toplama:** Her nöron girdileri önem derecesine göre toplar.
3. **Katmanlı soyutlama:** İlk katmanlar basit özellikleri (çizgi, kenar), sonraki katmanlar karmaşık özellikleri (pencere, cephe, bina türü) yakalar.
4. **Hatadan öğrenme:** Tahmin yanlışsa ağırlıklar küçük adımlarla düzeltilir.
5. **Genelleme:** İyi eğitilmiş ağ, hiç görmediği örnekler hakkında da doğru tahmin yapabilir.

#### Yapay Zekâ ve İnsan Zekâsının Benzerliği ve Farkları

| Konu | İnsan beyni | Yapay sinir ağı |
|---|---|---|
| Temel birim | Biyolojik nöron | Matematiksel nöron (sayılarla hesap) |
| Bağlantı | Sinapslar, güçlenir veya zayıflar | Ağırlıklar, eğitimle değişir |
| Öğrenme | Az örnekle, deneyimle, bedenle, duyguyla | Çok fazla örnekle, sayısal optimizasyonla |
| Enerji | Çok düşük enerjiyle çalışır | Eğitimi çok yüksek enerji ve donanım ister |
| Anlam | Dünyayı deneyimleyerek anlar | Örüntüleri istatistiksel olarak yakalar |
| Hata farkındalığı | Çoğu zaman "emin değilim" diyebilir | Kendinden emin şekilde yanılabilir |
| Esneklik | Bir alandan diğerine kolayca aktarır | Eğitildiği verinin dışına çıkınca zorlanabilir |

> **Dikkat:** "Yapay sinir ağı beyin gibi çalışır" ifadesi bir **ilham benzetmesidir**, birebir eşleşme değildir. Akademik metinlerde bu benzetmeyi kullanırken sınırlarını belirtmek doğru olur.

**Soru:** Bir mimarlık öğrencisi "Türk evi"ni tanımak için kaç örnek görmeye ihtiyaç duyar? Bir yapay sinir ağı?

**Cevap:** İnsan birkaç güçlü örnek ve açıklamayla kavramı yakalayabilir. Yapay sinir ağı genellikle binlerce örneğe ihtiyaç duyar. Bu fark, yapay zekâya prompt yazarken **örnek ve bağlam vermenin** neden bu kadar önemli olduğunu da açıklar.

---

### Konu 4: Sinir Ağı ile Veri Sınıflandırma – Kâğıt Üzerinde Hesap (20 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir arşivde binlerce eski ev fotoğrafı var ve bunları "geleneksel ev" ve "apartman" olarak iki klasöre ayırmak gerekiyor. Bunu elle yapmak günler sürer. Bir sinir ağı bu ayrımı öğrenip otomatik yapabilir.

**Basit açıklama:** Sınıflandırma, bir şeyi önceden belirlenmiş gruplardan birine yerleştirmektir. Sinir ağı, özelliklere bakarak bir karar verir.

**Teknik tanım:** Sınıflandırma (classification), bir modelin girdi özelliklerine dayanarak örneği belirli bir sınıfa atadığı gözetimli öğrenme görevidir. En basit sinir ağı sınıflandırıcısı tek bir yapay nörondan oluşan **algılayıcıdır (perceptron).**

#### Birlikte Uygulayalım: Tek Nöronlu Ev Sınıflandırıcısı

**Amaç:** Bir yapay nöronun nasıl karar verdiğini ve nasıl öğrendiğini elle hesaplayarak görmek.

**Senaryo:** Arşivdeki ev kayıtlarını "Geleneksel ev (1)" ve "Apartman (0)" olarak sınıflandıran tek nöronlu bir model kuruyoruz.

**Girdiler (özellikler):** Her özellik var ise 1, yok ise 0.

| Özellik | Sembol |
|---|---|
| Plan şemasında sofa var mı? | x1 |
| Plan şemasında koridor var mı? | x2 |
| Ahşap karkas yapı mı? | x3 |

**Başlangıç ağırlıkları ve eşik:**

| Parametre | Değer |
|---|---|
| w1 (sofa) | 2 |
| w2 (koridor) | -2 |
| w3 (ahşap karkas) | 1 |
| b (sapma) | -1 |

**Hesap kuralı:**

```text
toplam = (x1 × w1) + (x2 × w2) + (x3 × w3) + b
Eğer toplam > 0 ise tahmin = 1 (Geleneksel ev)
Değilse tahmin = 0 (Apartman)
```

**Adımlar:**

1. Tahtaya özellik tablosunu ve ağırlıkları yazın.
2. **Ev A:** Sofa var, koridor yok, ahşap karkas.
   - x1 = 1, x2 = 0, x3 = 1
   - **Tahmin sorusu:** Hesaplamadan önce sorun: "Sizce model ne diyecek?"
   - toplam = (1 × 2) + (0 × -2) + (1 × 1) + (-1) = 2 + 0 + 1 - 1 = **2**
   - 2 > 0 → Tahmin: **1 (Geleneksel ev)** ✔
3. **Ev B:** Sofa yok, koridor var, ahşap karkas değil (betonarme).
   - x1 = 0, x2 = 1, x3 = 0
   - toplam = 0 + (1 × -2) + 0 + (-1) = **-3**
   - -3 > 0 değil → Tahmin: **0 (Apartman)** ✔
4. **Ev C:** Sofa yok, koridor yok, ahşap karkas (örneğin küçük bir köy evi).
   - x1 = 0, x2 = 0, x3 = 1
   - toplam = 0 + 0 + 1 - 1 = **0**
   - 0 > 0 değil → Tahmin: **0 (Apartman)** ✘ (Gerçekte geleneksel ev)
5. **Soru:** "Model neden yanıldı?"
   - **Cevap:** Ahşap karkasın ağırlığı (1), eşiği (-1) aşmaya yetmedi. Model "sofa yoksa geleneksel ev değildir" gibi davranıyor.
6. **Öğrenme adımı:** Hata yapınca ağırlıkları güncelleyelim. Basit kural:

```text
hata = gerçek değer - tahmin
yeni ağırlık = eski ağırlık + (hata × ilgili girdi)
yeni sapma = eski sapma + hata
```

   - hata = 1 - 0 = 1
   - w1 = 2 + (1 × 0) = **2**
   - w2 = -2 + (1 × 0) = **-2**
   - w3 = 1 + (1 × 1) = **2**
   - b = -1 + 1 = **0**
7. Ev C'yi yeni ağırlıklarla tekrar hesaplayın:
   - toplam = 0 + 0 + (1 × 2) + 0 = **2** → Tahmin: **1 (Geleneksel ev)** ✔
8. Ev B'yi yeni ağırlıklarla kontrol edin (öğrenme diğer örnekleri bozmuş mu?):
   - toplam = 0 + (1 × -2) + 0 + 0 = **-2** → Tahmin: **0 (Apartman)** ✔
9. Ev A'yı kontrol edin:
   - toplam = 2 + 0 + 2 + 0 = **4** → **1** ✔

**Beklenen sonuç:**

| Ev | x1 | x2 | x3 | Gerçek | İlk tahmin | Güncelleme sonrası tahmin |
|---|---|---|---|---|---|---|
| A | 1 | 0 | 1 | 1 | 1 ✔ | 1 ✔ |
| B | 0 | 1 | 0 | 0 | 0 ✔ | 0 ✔ |
| C | 0 | 0 | 1 | 1 | 0 ✘ | 1 ✔ |

**Açıklama:** Model bir hata yaptı ve hatasına göre ağırlıklarını küçük bir adımla düzeltti. Artık ahşap karkas özelliğine daha fazla önem veriyor. Gerçek yapay sinir ağları bu işlemi **milyarlarca ağırlık** ve **milyarlarca örnek** üzerinde, çok daha gelişmiş matematikle yapar. Ama temel fikir aynıdır: **tahmin et → hatayı ölç → ağırlıkları düzelt → tekrar et.**

#### Sıra Sizde 3 (5 dk)

**Amaç:** Nöron hesabını pekiştirmek.

**Görev:** Güncellenmiş ağırlıklarla (w1 = 2, w2 = -2, w3 = 2, b = 0) şu evi sınıflandırın:

- **Ev D:** Sofa var, koridor var, ahşap karkas değil (geçiş dönemi bir konut).

**İstenenler:** Toplamı hesaplayın, tahmini yazın, sonucun mantıklı olup olmadığını yorumlayın.

**İpucu:** Sofa ve koridor birbirinin etkisini götürüyor mu?

#### Çözüm

- x1 = 1, x2 = 1, x3 = 0
- toplam = (1 × 2) + (1 × -2) + (0 × 2) + 0 = 2 - 2 + 0 + 0 = **0**
- 0 > 0 değil → Tahmin: **0 (Apartman)**

**Yorum:** Ev D tam bir geçiş örneği: hem geleneksel (sofa) hem modern (koridor) özellik taşıyor. Modelin kararı sınırda (toplam tam 0). Bu durum gerçek modellerde de olur: Sınırda kalan örneklerde model kararsızdır ve hata ihtimali yüksektir. Bu yüzden yapay zekâ çıktılarında "emin misin?" sorusu ve doğrulama önemlidir.

---

### Konu 5: Token Tahmini, Prompt Mühendisliği Yaklaşımı ve Üretken Yapay Zekâ Devrimi (15 dk)

#### Token Prediction (Token Tahmini)

**Günlük hayat örneği:** Ders 1'deki otomatik tamamlama oyununu hatırlayın. Şimdi bunu sayılarla görelim.

**Basit açıklama:** Dil modeli bir metni okurken her adımda "sıradaki token ne olabilir?" sorusuna bir **olasılık listesi** üretir ve bu listeden bir seçim yapar. Seçilen token metne eklenir ve süreç tekrar eder.

**Teknik tanım:** Büyük dil modelleri, kendinden önceki token dizisine koşullu olarak bir sonraki token'ın olasılık dağılımını hesaplayan otoregresif modellerdir. Cevap, bu dağılımdan art arda örnekleme yapılarak üretilir.

**Örnek:** Model şu metni gördü: *"Geleneksel Türk evinde sofa, odaların açıldığı ortak bir ..."*

| Olası sonraki token | Olasılık (temsili) |
|---|---|
| alan | %45 |
| mekândır | %30 |
| yaşam | %12 |
| holdür | %5 |
| diğerleri | %8 |

Model genellikle yüksek olasılıklı seçeneklerden birini seçer. **Sıcaklık** ayarı yüksekse daha düşük olasılıklı seçenekler de seçilebilir (daha yaratıcı ama daha riskli).

#### Prompt Mühendisliği Yaklaşımıyla Bağlantı

Bu bilgi prompt mühendisliğini şu şekilde açıklar:

| Prompt tekniği | Token tahmini açısından neden işe yarar? |
|---|---|
| Bağlam vermek | Olasılık dağılımını konuyla ilgili kelimelere kaydırır ("sofa" → mobilya değil, mekân). |
| Rol atamak | O uzmanlık alanında sık geçen kelime ve kalıpların olasılığını artırır. |
| Örnek vermek (few-shot) | Modelin örnekteki kalıbı devam ettirme olasılığını çok yükseltir. |
| Çıktı biçimi belirtmek | Tablo başladığında bir sonraki token'ın "|" olma olasılığı artar. |
| Adım adım düşündürmek | Her ara adım, bir sonraki adım için daha zengin bağlam oluşturur. |
| "Emin değilsen belirt" demek | "Emin değilim" ifadesinin olası bir devam olmasını sağlar. |

**Neden uydurma oluyor?** Bir kaynak künyesi istediğinizde model "gerçek bir künyeye benzeyen" token dizisini üretir. Yazar adları, dergi adları ve yıllar sık görülen örüntüler olduğu için, ortaya gerçekçi ama hayali bir künye çıkabilir. Model "bu kaynak gerçekten var mı?" diye kontrol etmez; sadece olası devamı üretir.

**Soru:** Bu bilgiye göre, uydurma kaynak riskini azaltmanın en iyi yolu nedir?

**Cevap:** Modele gerçek kaynak metnini vermek (bağlam) ve sadece o metne dayanmasını istemek; ya da web araması yapan ve bağlantı gösteren araçları kullanıp bağlantıları kontrol etmek.

#### Üretken Yapay Zekâ Devrimi

**Basit açıklama:** Eskiden yapay zekâ çoğunlukla **sınıflandırıyordu** (bu e-posta spam mı, bu fotoğrafta kedi var mı?). Son yıllarda yapay zekâ **üretmeye** başladı: metin, görsel, ses, video, kod.

Bu dönüşümü mümkün kılan başlıca gelişmeler:

1. **Transformer mimarisi (2017):** Modellerin bir metindeki bütün kelimeler arasındaki ilişkiye aynı anda "dikkat" etmesini sağlayan sinir ağı yapısı. Bugünkü dil modellerinin temelidir.
2. **Ölçek:** Çok daha büyük veri, çok daha büyük modeller ve güçlü donanım (GPU).
3. **İnsan geri bildirimiyle eğitim:** Modellerin insanların tercih ettiği, yardımcı ve güvenli cevaplar vermeye yönlendirilmesi.
4. **Çok kiplilik:** Aynı modelin metin, görsel ve sesi birlikte anlayıp üretebilmesi.
5. **Ajanlar:** Modellerin sadece cevap vermekle kalmayıp araç kullanarak görev yapması (Ders 5'te göreceğiz).

**Akademik çalışmalar için anlamı:** Literatür taraması, veri işleme, yazım ve görselleştirme süreçlerinin her biri artık yapay zekâ ile desteklenebiliyor. Ama araştırmacının **yargısı, doğrulama sorumluluğu, etik yükümlülükleri ve özgün katkısı** her zamankinden daha önemli.

---

### Konu 6: Sağlık, Finans ve Otomotiv Sektöründe Yapay Sinir Ağları ve Gerçek Hayatta Kullanım Örnekleri (10 dk)

#### Sektörel Örnekler

| Sektör | Yapay sinir ağı ne yapar? | Sınıflandırma örneğimizle bağlantısı |
|---|---|---|
| Sağlık | Röntgen, MR ve patoloji görüntülerinde şüpheli bulguları işaretleyerek hekime yardımcı olur | Ev sınıflandırıcısı gibi, görüntüyü "normal / incelenmeli" sınıfına atar |
| Finans | Kredi kartı işlemlerinde olağandışı (dolandırıcılık şüphesi taşıyan) işlemleri fark eder; kredi risk değerlendirmesine destek verir | İşlemi "olağan / şüpheli" sınıfına atar |
| Otomotiv | Sürücü destek sistemlerinde kamera görüntüsündeki yayaları, şeritleri, trafik işaretlerini tanır | Görüntüdeki nesneleri "yaya / araç / işaret" sınıflarına ayırır |
| Mimarlık ve inşaat | Tarihi yapı fotoğraflarında hasar tespiti, cephe görüntülerinden yapı tipi sınıflandırma, enerji tüketimi tahmini | Doğrudan bizim örneğimizin genişletilmiş hâli |
| Kültürel miras ve arşiv | Arşiv fotoğraflarının etiketlenmesi, el yazısı belgelerin metne dönüştürülmesi | Arşiv kayıtlarını otomatik sınıflandırma |

> **Dikkat:** Sağlık ve finans gibi alanlarda yapay zekâ kararları **insan uzmanın denetimiyle** kullanılır. Bir model sınırda kalan örneklerde (Ev D gibi) yanılabilir; bu alanlarda hatanın bedeli yüksektir.

#### Gerçek Hayatta Yapay Zekâ Kullanım Örnekleri (Tartışma)

**Soru:** Gün içinde farkında olmadan hangi yapay zekâ sistemlerini kullanıyoruz?

**Cevap:** Telefonun yüz tanıma kilidi, harita uygulamasında trafik tahmini, e-postada spam filtresi, müzik ve video önerileri, fotoğraf galerisinde yüz ve nesne arama, klavyede kelime önerisi, otomatik çeviri.

**Soru:** Araştırma sürecinizde bu dersten sonra hangi üç yapay zekâ kullanımını deneyeceksiniz?

**Cevap (örnek):** Sözlü tarih görüşmelerini yazıya dökmek, sunum ve poster şemalarını tutarlı bir seri hâlinde üretmek, arşiv fotoğraflarını sınıflandırıp etiketlemek.

---

### Ders Özeti

Bu derste görsel promptları bir mimarın diliyle yazmayı öğrendik: konu, ortam, tarz, ışık, perspektif, malzeme, kompozisyon ve teknik parametreler. Aynı mekânı atmosfer görseli, kesit, aksonometri ve maket fotoğrafı olarak ürettik ve bu görsellerin teknik çizim olmadığını, temsili olarak etiketlenmesi gerektiğini gördük. Ses ve video araçlarıyla sözlü tarih görüşmelerini nota dönüştürmeyi ve yayımlanan bir makale için sosyal medya duyuru serisi hazırlamayı denedik. Dersin ikinci yarısında yapay sinir ağlarının temel mantığını öğrendik, tek bir nöronu kâğıt üzerinde hesaplayıp hatasından öğrenmesini izledik. Son olarak token tahmini fikrinin prompt tekniklerinin neden işe yaradığını ve modellerin neden uydurabildiğini nasıl açıkladığını gördük.

### Bu Derste Neler Öğrendik?

- Görsel promptun 10 bileşenini ve mimari terimlerin promptta nasıl kullanılacağını öğrendik.
- Midjourney ve GPT Image arasındaki farkları ve temel Midjourney parametrelerini gördük.
- Aynı mekânı farklı temsil biçimlerinde ürettik.
- Ses kaydını transkripte ve okuma notuna dönüştürdük.
- Bir yayın için platformlara göre tutarlı bir sosyal medya duyuru serisi hazırladık.
- Yapay nöron, ağırlık, sapma, aktivasyon ve katman kavramlarını öğrendik.
- Tek nöronlu bir sınıflandırıcıyı elle hesapladık ve öğrenme adımını uyguladık.
- Token tahmininin prompt teknikleriyle ilişkisini kurduk.
- Üretken yapay zekâ devrimini mümkün kılan gelişmeleri öğrendik.
- Yapay sinir ağlarının sağlık, finans, otomotiv ve mimarlıktaki kullanımlarını gördük.

### Mini Quiz

1. **(Çoktan seçmeli)** Aşağıdakilerden hangisi görsel promptta "perspektif / kamera" bileşenine örnektir?
   - a) Sulu boya
   - b) Kuş bakışı
   - c) Toprak tonları
   - d) Nostaljik
2. **(Kısa cevap)** Midjourney'de `--ar 4:5` parametresi ne işe yarar?
3. **(Doğru / Yanlış)** Yapay zekâ ile üretilmiş bir kesit perspektif, ölçülü bir rölöve çiziminin yerine kullanılabilir.
4. **(Kısa cevap)** Bir ses kaydını yazıya dökme işlemine ne ad verilir?
5. **(Kod çıktısı tahmini / hesap)** w1 = 2, w2 = -2, w3 = 1, b = -1 iken x1 = 1, x2 = 1, x3 = 1 olan evin toplamı ve tahmini nedir? (Toplam > 0 ise 1)
6. **(Çoktan seçmeli)** Yapay sinir ağında "ağırlık" neyi temsil eder?
   - a) Modelin dosya boyutunu
   - b) Bir girdinin karara etkisinin büyüklüğünü
   - c) Görselin çözünürlüğünü
   - d) Eğitim süresini
7. **(Kısa cevap)** Few-shot prompting'in işe yaramasını token tahmini ile açıklayın.
8. **(Doğru / Yanlış)** Bugünkü büyük dil modellerinin temelinde transformer mimarisi vardır.
9. **(Küçük problem)** "Güzel bir apartman çiz" promptunu en az 5 görsel prompt bileşeni içerecek şekilde yeniden yazın.

### Mini Quiz Cevapları

1. **b.**
2. Görselin en-boy oranını 4:5 (dikey) yapar; Instagram dikey gönderileri için uygundur.
3. **Yanlış.** Yapay zekâ görselleri ölçüye dayanmaz; sadece temsili olarak kullanılabilir.
4. **Transkripsiyon** (konuşmadan metne, speech-to-text).
5. toplam = 2 + (-2) + 1 + (-1) = **0** → 0 > 0 değil → Tahmin: **0 (Apartman)**.
6. **b.**
7. Model, promptta gördüğü kalıbı devam ettirmeye yatkındır. Örnekler, istenen kalıptaki token'ların olasılığını yükseltir; model de bu kalıbı izleyen token'ları seçer.
8. **Doğru.**
9. Örnek: "1960'lar İstanbul'unda beş katlı bir apartmanın sokak cephesi (konu + ortam). Mozaik kaplı giriş, ince profilli balkon korkulukları, yatay bant pencereler (malzeme ve ayrıntı). Karşı kaldırımdan göz hizası bakış (perspektif). İkindi güneşi, sıcak ışık (ışık). Hafif soluk, eski fotoğraf renkleri (renk paleti). Belgesel fotoğraf üslubu (tarz). Yatay 3:2, yazı ve insan figürü yok."

### Ders Sonu Uygulaması

**Senaryo:** "Konutta mekânın dönüşümü" konulu bir araştırma, bir sempozyumda poster olarak sunulacak. Posterin ana görseli için 3 farklı konsept denenecek. Ayrıca sempozyumun web sayfasında yayımlanmak üzere 60 saniyelik sesli bir araştırma özeti hazırlanacak.

**Yapılacaklar:**

1. Poster ana görseli için 3 konsept belirleyin (örneğin: "sofadan salona uzanan tek çizgi", "aynı pencereden iki dönem", "plan şemalarının karşılaştırması").
2. Her konsept için görsel prompt bileşenlerini içeren bir prompt yazın. Görselin üst üçte birinde poster başlığı için boşluk bırakılmasını isteyin.
3. Görselleri en az iki araçta (örneğin ChatGPT ve Midjourney ya da Gemini) üretip karşılaştırın; önceden belirlediğiniz 3 ölçütle puanlayın.
4. Araştırma için 60 saniyelik (yaklaşık 130–150 kelime) bir sesli özet metni yazdırın.
5. (İsteğe bağlı) Metni bir seslendirme aracıyla seslendirin veya kendi sesinizle kaydedin.

**Beklenen sonuç:** 3 poster görseli konsepti, karşılaştırma tablosu, seslendirmeye hazır bir araştırma özeti metni.

**İpuçları:**

- Dikey poster oranı için `--ar 2:3` veya `--ar 3:4` (Midjourney) ya da "dikey 2:3 oran" (GPT Image) kullanın.
- Görsellerde yazı istemeyin; başlık ve metinler poster tasarım programında eklenecek.
- Sesli metinde kısa cümleler ve okunuşu kolay kelimeler kullanmasını isteyin.

### Ders Sonu Uygulaması – Çözüm

**Ölçütler:** Araştırma fikrini iletme (1–5), posterde okunabilirlik / sadelik (1–5), görsel kimliğe uygunluk (1–5).

**Konsept 2 promptu (GPT Image):**

```text
Akademik poster için konsept illüstrasyon. Ortada tek bir pencere; pencerenin sol yarısında
geleneksel bir Türk evinin ahşap kafesli penceresi ve dışarıda kiremit çatılar, sağ yarısında
aynı pencerenin 1970'ler apartman penceresine dönüşmüş hâli, dışarıda beton apartmanlar.
İki yarı ortada yumuşak bir geçişle birleşiyor. Beyaz zemin üzerine ince siyah çizgi ve
hafif sulu boya; sıcak toprak tonları, soluk turkuaz vurgu. Dikey 2:3 oran. Görselin üst üçte biri
sade krem renkli boşluk olsun. Görselde yazı yok.
```

**Aynı konsept Midjourney için:**

```text
Academic poster concept illustration, a single window split in two halves: left half a traditional
Ottoman wooden lattice window with tiled roofs outside, right half the same window turned into a
1970s apartment window with concrete apartment blocks outside, soft transition in the middle,
fine black ink lines and light watercolor on white paper, warm earth tones with pale turquoise
accent, empty cream space in the top third --ar 2:3 --s 100 --no text, letters, people
```

**Sesli araştırma özeti promptu:**

```text
Aşağıdaki makale özetine dayanarak, sempozyum web sayfasında yayımlanacak 60 saniyelik
(130–150 kelime) bir sesli araştırma özeti metni yaz.
Kısa cümleler kullan, okunuşu zor kelimelerden ve kısaltmalardan kaçın.
Dinleyiciye bir soruyla başla: "Çocukluğunuzun evinde en çok hangi odada vakit geçirirdiniz?"
Ardından araştırma sorusunu, yöntemi tek cümleyle ve en önemli bulguyu anlat.
Özette olmayan bulgu ekleme; bulguları abartma.

Makale özeti:
[özet]
```

> **Sonraki derste:** Şimdiye kadar öğrendiğimiz bütün teknikleri farklı sektörlere uygulayacağız: **yazılım geliştirme** (kod yazdırma ve hata ayıklama), **eğitim** (ders materyali ve quiz), **pazarlama** (reklam metni, slogan, SEO) ve **tasarım.** Ardından yapay zekânın sadece cevap vermekle kalmayıp görev yapan bir yardımcıya dönüştüğü **yapay zekâ ajanlarını** tanıyacak ve kod yazmadan kendi araştırma asistanı ajanımızı kuracağız.
