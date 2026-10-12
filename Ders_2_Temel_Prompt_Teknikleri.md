# Prompt Mühendisliği Eğitimi – Ders 2

## Temel Prompt Teknikleri, Rol Atama ve Adım Adım Düşünme (Yaklaşık 2,5 Saat)

---

## Ders 2 – 150 Dakika

### Önceki Dersle Bağlantı

Önceki derste dil modelinin bağlama göre en olası devamı tahmin ettiğini, bu yüzden iyi bir promptun "ne, neden, kim için, ne bilgiyle, nasıl, ne olmasın" sorularını cevaplaması gerektiğini öğrendik. Ayrıca modelin kaynak uydurabileceğini ve akademik çalışmada her bilginin doğrulanması gerektiğini gördük.

Bu derste bu soruları **düzenli bir prompt yapısına** dönüştüreceğiz: **bağlam + rol + görev + çıktı biçimi.** Ardından akademik tonu, üslubu ve biçimi kontrol etmeyi, modele hakem veya editör gibi roller vermeyi ve onu adım adım düşündürmeyi öğreneceğiz. Bu dersin sonunda bir makaleyi okuma notuna dönüştüren ve bir literatür paragrafı yazdıran **yeniden kullanılabilir prompt şablonlarımız** olacak.

### Dersin Hedefleri

Bu dersin sonunda öğrenci:

- Bir promptu bağlam, rol, görev ve çıktı biçimi bileşenlerine ayırabilecek.
- Açık, ölçülebilir ve uygulanabilir yönergeler yazabilecek.
- Aynı bulguyu akademik, alan dışı okura yönelik ve sosyal medya tonlarında yazdırabilecek.
- Cevabın biçimini (tablo, madde, başlık, kelime sayısı) kontrol edebilecek.
- Modele hakem, editör gibi roller atayarak cevabın bakış açısını değiştirebilecek.
- Karmaşık bir araştırma kararını modele adım adım düşündürebilecek.
- Bir makaleden düzenli bir okuma notu (özet) çıkarabilecek.

### Süre Planı

| Bölüm | Süre |
|---|---|
| Giriş ve önceki dersin tekrarı | 10 dk |
| Konu 1: Prompt yapısı – bağlam + rol + görev + çıktı biçimi | 35 dk |
| Konu 2: Doğru yönergeler yazma | 20 dk |
| Konu 3: Ton, üslup ve formatlama | 30 dk |
| Konu 4: Rol atama | 20 dk |
| Konu 5: Chain of thought – adım adım düşünme | 20 dk |
| Ders özeti, mini quiz ve ders sonu uygulaması | 15 dk |
| **Toplam** | **150 dk** |

---

### Giriş ve Tekrar (10 dk)

Hızlı bir tekrar yapalım:

**Soru:** Yapay zekâya "Bana bu konuda 10 kaynak ver" demek neden risklidir?

**Cevap:** Model gerçekçi görünen ama var olmayan kaynaklar uydurabilir (halüsinasyon).

**Soru:** "Prompt Defterim" dosyasına hangi promptları kaydettik? Birini okuyalım.

**Cevap:** Ders sonu uygulamasındaki promptlardan birini okuyalım ve bu promptun hangi kontrol sorularını cevapladığını birlikte bulalım. Bu, bugünkü konuya doğal bir geçiş sağlar.

---

### Konu 1: Prompt Yapısı – Bağlam + Rol + Görev + Çıktı Biçimi (35 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir araştırma projesinde asistana iş verirken genellikle şöyle konuşursunuz:

> "Kentsel dönüşüm projemiz için (**bağlam**), bugün bir sosyolog gözüyle bak (**rol**), topladığımız 10 görüşmenin ana temalarını çıkar (**görev**), her tema için bir tablo satırı ve iki kısa alıntıyla (**çıktı biçimi**)."

Bu cümlede asistanın işi doğru yapması için gereken her şey var. Prompt yapısı da tam olarak budur.

**Basit açıklama:** İyi bir prompt dört yapı taşından oluşur:

1. **Bağlam:** Durum nedir? Arka plan bilgisi nedir?
2. **Rol:** Model kim gibi davranmalı?
3. **Görev:** Ne yapılacak?
4. **Çıktı biçimi:** Sonuç hangi şekilde teslim edilecek?

**Teknik tanım:** Yapılandırılmış prompt (structured prompt), modelin talimatı doğru yorumlaması için bilgiyi işlevlerine göre ayrılmış bölümler hâlinde sunan prompt tasarımıdır. Bölümlerin ayrılması, modelin hangi bilginin arka plan, hangisinin talimat olduğunu karıştırmasını önler.

#### Neden Öğreniyoruz?

- **Tekrar kullanılabilirlik:** Bir kere iyi bir yapı kurduğunuzda, yalnızca görevi veya metni değiştirerek onlarca kez kullanabilirsiniz.
- **Tutarlılık:** Okunan 30 makalenin notları aynı formatta çıkar; literatür tablosu kendiliğinden oluşur.
- **Hata ayıklama:** Cevap kötü geldiğinde hangi parçanın eksik olduğunu bulmak kolaylaşır.
- **Şeffaflık:** Yöntem bölümünde yapay zekânın nasıl kullanıldığını açıklamak kolaylaşır.

#### Temel Kavramlar

**Kavram: Bağlam**

- Basit açıklama: Modelin bilmesi gereken arka plan.
- Neden kullanılır? Model sizi, çalışmanızı ve amacınızı bilmez.
- Örnek: "Kentsel dönüşüm alanlarında komşuluk ilişkileri üzerine bir yüksek lisans tezi yazıyorum. Şu an literatür bölümündeyim."

**Kavram: Rol**

- Basit açıklama: Modelin hangi uzmanlıkla, hangi gözle bakacağı.
- Neden kullanılır? Kelime seçimini, ayrıntı düzeyini ve bakış açısını değiştirir.
- Örnek: "Sen mimarlık alanında hakemli bir derginin deneyimli hakemisin."

**Kavram: Görev**

- Basit açıklama: Yapılacak iş, tercihen bir fiille başlar: yaz, özetle, karşılaştır, listele, düzelt.
- Neden kullanılır? Belirsiz görev, belirsiz sonuç doğurur.
- Örnek: "Aşağıdaki makale özetini 3 maddede özetle."

**Kavram: Çıktı biçimi**

- Basit açıklama: Sonucun şekli, uzunluğu, bölümleri.
- Neden kullanılır? Sonucu doğrudan kullanılabilir hâle getirir.
- Örnek: "Tablo olarak ver: Kavram | Tanım | Hangi kuramcıyla ilişkili?"

#### Basit Örnek

Aynı isteğin yapı taşları eklendikçe nasıl değiştiğini görelim:

| Sürüm | Prompt |
|---|---|
| Sadece görev | "Cumbayı anlat." |
| + Çıktı biçimi | "Cumbayı 100 kelimeyle anlat." |
| + Bağlam | "Osmanlı kent dokusu üzerine bir makalenin literatür bölümünü yazıyorum. Cumbayı 100 kelimeyle anlat." |
| + Rol | "Sen Osmanlı sivil mimarisi üzerine çalışan bir mimarlık tarihçisisin. Osmanlı kent dokusu üzerine bir makalenin literatür bölümünü yazıyorum. Cumbayı 100 kelimeyle anlat." |

**Tahmin sorusu:** Dört sürümü sırayla denersek cevaplar nasıl değişir?

**Cevap:** İlk sürüm uzun ve ansiklopedik olabilir. İkincisi kısalır. Üçüncüsü akademik bir dile yaklaşır. Dördüncüsü kavramı kent dokusu ve sokak ilişkisi gibi uzmanlık bağlamlarına yerleştirir.

#### Birlikte Uygulayalım: Dört Sürüm Deneyi

**Amaç:** Prompt bileşenlerinin cevaba etkisini gözle görmek.

**Senaryo:** Bir makalenin literatür bölümü için cumba kavramını tanımlayan bir paragraf hazırlıyoruz.

**Adımlar:**

1. Yeni bir sohbet açın.
2. Yukarıdaki tablonun 1. sürümünü yazın ve cevabı okuyun.
3. **Yeni bir sohbet** açın ve 2. sürümü yazın. (Her sürüm için yeni sohbet açmak, önceki cevabın etkisini ortadan kaldırır.)
4. Aynı şekilde 3. ve 4. sürümleri ayrı sohbetlerde deneyin.
5. Dört cevabı bir belgeye yan yana kopyalayın.
6. Her cevap için şu tabloyu doldurun:

| Sürüm | Uzunluk uygun mu? | Dil akademik mi? | Makalede kullanılabilir mi? |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |

**Beklenen sonuç:** 4. sürüm akademik kullanıma en yakın metni üretmelidir.

**Açıklama:** Her bileşen modelin bir tahmin alanını kapattı. Rol, anlatımın uzmanlık düzeyini; bağlam, metnin nerede kullanılacağını; çıktı biçimi uzunluğu belirledi.

> **Dikkat:** 4. sürümün cevabı ne kadar iyi olursa olsun, içindeki olgusal bilgiler (tarihler, yapı adları) makalede kullanılmadan önce kaynaktan doğrulanmalıdır.

#### Gerçek Hayat Senaryosu: Makale Okuma Notu Şablonu

**Senaryo:** Bir literatür taraması sırasında her hafta 3–4 makale okunuyor ve notlar dağınık kalıyor. Her makale için aynı yapıda bir okuma notu isteniyor.

**Problem nedir?** Notların farklı formatlarda olması, sonradan karşılaştırmayı ve literatür tablosunu oluşturmayı zorlaştırıyor.

**Nasıl çözeceğiz?** Dört bileşenli bir şablon prompt hazırlayacağız ve her makalede yalnızca metni değiştireceğiz.

**Hangi bilgileri kullanacağız?** Makalenin özeti veya giriş/sonuç bölümleri, araştırma sorumuz.

**Şablon prompt:**

```text
## BAĞLAM
Şu araştırma sorusu için literatür okuyorum:
[araştırma sorunuz]

## ROL
Sen mimarlık tarihi ve konut çalışmaları alanında deneyimli bir araştırma asistanısın.
Titiz, tarafsız ve kısa yazarsın.

## GÖREV
Aşağıdaki makale metnini oku ve bir okuma notu hazırla.
Sadece metinde yazanlara dayan. Metinde olmayan bilgi ekleme.
Metinde bulunmayan bir alan için "Metinde belirtilmemiş" yaz.

## ÇIKTI BİÇİMİ
Aşağıdaki başlıkları kullan:
- Ana iddia (1 cümle)
- Yöntem ve veri (1–2 cümle)
- Temel bulgular (en fazla 3 madde)
- Kullanılan önemli kavramlar (virgülle ayrılmış liste)
- Araştırma sorumla bağlantısı (1–2 cümle)
- Sorgulanabilecek nokta (1 cümle)

## MAKALE METNİ
[buraya metni yapıştır]
```

**Adım adım uygulama:**

1. Şablonu "Prompt Defterim" dosyasına kopyalayın.
2. `[araştırma sorunuz]` kısmına Ders 1'de netleştirdiğiniz soruyu yazın.
3. Elinizdeki bir makalenin özetini veya giriş + sonuç bölümünü kopyalayın.
4. Şablondaki `[buraya metni yapıştır]` yerine metni yapıştırın.
5. Promptu yapay zekâya gönderin.
6. Çıkan okuma notunu kontrol edin: Ana iddia gerçekten makalede var mı?
7. İkinci bir makale için 3–5 arasındaki adımları tekrarlayın.
8. İki okuma notunu karşılaştırın. Aynı yapıda olduklarını görün.

> **Dikkat:** Uzun PDF'leri doğrudan yükleyebilen araçlarda (ChatGPT, Claude, Gemini) dosyayı ekleyip "## MAKALE METNİ" kısmına "Ekteki PDF" yazabilirsiniz. Yine de modelin her sayfayı eşit dikkatle okumayabileceğini unutmayın; önemli bulguları sayfa numarasıyla kontrol edin.

**Not:** Promptta `##` işaretleri, bölümleri ayırmak için kullanılır. Model bunları başlık olarak anlar. `BAĞLAM:` gibi etiketler veya XML benzeri `<baglam>` etiketleri de kullanılabilir. Önemli olan bölümlerin net ayrılmasıdır.

#### Sıra Sizde 1 (15 dk)

**Amaç:** Dört bileşenli prompt yazmayı pekiştirmek.

**Görev:** "Geleneksel konutta çok amaçlı oda: Batılı mobilyanın eve girişiyle odaların tek işlevli hâle gelmesi" konulu bir makale için bir **makale yapı planı** istemek üzere dört bileşenli bir prompt yazın.

**İstenenler:**

- Bağlam: Makalenin konusu, türü ve gönderileceği dergi türü.
- Rol: Uygun bir uzman rolü.
- Görev: Makale yapı planı hazırlamak.
- Çıktı biçimi: Bölüm başlıkları, her bölüm altında 2–3 cümlelik açıklama, tahmini kelime sayısı.

**Beklenen sonuç:** Giriş, literatür, yöntem, bulgular/tartışma ve sonuç bölümlerinden oluşan düzenli bir plan.

**İpucu:** Geleneksel konutta odanın aynı anda oturma, yemek ve yatma için kullanıldığını bağlama ekleyin.

#### Çözüm

```text
## BAĞLAM
Mimarlık tarihi alanında hakemli bir dergiye 7.000 kelimelik bir makale hazırlıyorum.
Konu: Geleneksel Türk evinde odanın gün içinde oturma, yemek ve yatma için kullanılan
çok amaçlı bir mekân olmasından; 19. yüzyıl sonundan itibaren Batılı mobilyanın eve
girmesiyle odaların tek işlevli hâle gelmesine geçiş.
Kaynaklarım: rölöve çizimleri, dönem dergileri, seyahatnameler.

## ROL
Sen mimarlık tarihi alanında hakemli dergilerde çok sayıda makale yayımlamış ve
dergi editörlüğü yapmış bir akademisyensin.

## GÖREV
Bu makale için bir yapı planı hazırla. Anlatım kronolojik değil, tematik ilerlesin.

## ÇIKTI BİÇİMİ
- Giriş, kavramsal çerçeve, yöntem ve kaynaklar, 2–3 tematik bulgu bölümü, tartışma, sonuç
- Her bölüm başlığının altında 2–3 cümlelik içerik açıklaması
- Her bölüm için tahmini kelime sayısı
- En sonda toplam kelime sayısı (7.000'i geçmemeli)
```

**Beklenen çıktı örneği (kısaltılmış):**

1. Giriş – Problem, araştırma sorusu ve makalenin katkısı (700 kelime)
2. Kavramsal Çerçeve: Çok Amaçlı Mekân ve İşlevsel Ayrışma (1.000 kelime)
3. Yöntem ve Kaynaklar (600 kelime)
4. Bulgu 1: Yüklük, Sedir ve Sini – Odayı Çok Amaçlı Kılan Donatılar (1.200 kelime)
5. …

#### Sık Yapılan Hatalar

**Hata 1: Bağlamı görevle karıştırmak**

Hatalı:

```text
Tez yazıyorum ve konut ve sofa ve özetle şunu ve hakem okuyacak bu metni.
```

Doğru: Bilgileri ayrı bölümlere koyun (BAĞLAM, GÖREV, ÇIKTI BİÇİMİ).

Neden? Model hangi kısmın talimat, hangi kısmın bilgi olduğunu karıştırır.

**Hata 2: Rol verip görevi unutmak**

Hatalı: "Sen bir mimarlık tarihçisisin." (ve başka bir şey yok)

Doğru: "Sen bir mimarlık tarihçisisin. Aşağıdaki paragraftaki dayanaksız genellemeleri işaretle."

**Hata 3: Çıktı biçimini çok gevşek bırakmak**

Hatalı: "Kısa bir özet."

Doğru: "En fazla 150 kelimelik, tek paragraflık bir özet."

Neden? "Kısa" kişiden kişiye değişir; sayı değişmez.

**Hata 4: Metni yapıştırmayı unutmak**

Neden hata? "Aşağıdaki makaleyi özetle" yazıp makaleyi eklemezseniz model ya sizden ister ya da (daha kötüsü) hayali bir makale özetler.

Düzeltme: Göndermeden önce promptun sonuna metnin gerçekten eklendiğini kontrol edin.

---

### Konu 2: Doğru Yönergeler Yazma (20 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir derginin yazım kılavuzunda "Makale kısa olsun" yazmaz; "Makale kaynakça dahil 8.000 kelimeyi geçmemelidir, özet 150–250 kelime olmalıdır" yazar. İlki yoruma açıktır; ikincisi ölçülebilir ve kontrol edilebilir.

**Basit açıklama:** Yönerge (talimat), modele ne yapacağını söyleyen cümlelerdir. Doğru yönerge; açık, ölçülebilir, olumlu ifadeli ve sıralı olmalıdır.

#### Neden Öğreniyoruz?

Akademik metinler belirli kurallara uymak zorundadır: derginin yazım kılavuzu, kelime sınırları, atıf biçimi, terim tutarlılığı. Doğru yönergeler, bu kuralların modele aktarılmasını sağlar.

#### İyi Yönergenin 5 Özelliği

| Özellik | Zayıf yönerge | Güçlü yönerge |
|---|---|---|
| Açık | "Biraz düzenle." | "Paragrafları en fazla 6 cümleye indir." |
| Ölçülebilir | "Kısa tut." | "En fazla 250 kelime." |
| Olumlu ifadeli | "Günlük dil kullanma." | "Nesnel, üçüncü şahıs ağzından, temkinli bir akademik dil kullan." |
| Sıralı | Karışık istekler | "1. Düzelt. 2. Özetle. 3. Başlık öner." |
| Gerekçeli | "Terimleri açıkla." | "Dergi disiplinlerarası olduğu için mimari terimleri ilk geçtiği yerde açıkla." |

**Gerekçe vermek neden önemli?** Model gerekçeyi bildiğinde, yönergeyi yazmadığınız durumlara da doğru şekilde uygular. "Dergi disiplinlerarası" bilgisini alan model, sadece terimleri açıklamakla kalmaz; alan içi kısaltmaları da açar.

#### Örnekle Gösterim (Few-shot / Örnekli Yönerge)

Bazen bir kuralı anlatmak yerine örnek göstermek daha etkilidir.

**Günlük hayat örneği:** Bir araştırma asistanına "Kaynakçayı şöyle yaz" deyip örnek bir künye göstermek.

```text
Tezimin "Kavramlar" ekindeki her terim için kısa bir tanım maddesi yazacaksın.
Aşağıdaki örneğin biçimini ve uzunluğunu aynen izle.

Örnek:
**Sofa** – Geleneksel Türk evinde odaların açıldığı ortak alan. Hem dolaşım hem toplanma mekânıdır. Plan tipolojisinde belirleyici öğedir.

Şimdi şu terimler için madde yaz: eyvan, cumba, hayat, yüklük, seki.
```

**Tahmin sorusu:** Model "eyvan" maddesini hangi uzunlukta yazar?

**Cevap:** Örnekteki gibi yaklaşık 3 kısa cümle. Model örneğin kalıbını taklit eder.

Bu tekniğe **few-shot prompting** (birkaç örnekli prompt) denir. Hiç örnek vermemeye **zero-shot**, bir örnek vermeye **one-shot** denir.

#### Birlikte Uygulayalım: Dergi Yazım Kılavuzuna Göre Düzeltme

**Amaç:** Birden fazla ölçülebilir yönergeyi aynı anda uygulatmak.

**Senaryo:** Makalenin gönderileceği dergi şu kuralları istiyor: Yüzyıllar rakamla ("18. yüzyıl"), yabancı terimler italik, cümleler en fazla 25 kelime, birinci çoğul şahıs ("biz", "görüyoruz") kullanılmayacak.

**Adımlar:**

1. Yeni sohbet açın.
2. Şu promptu yazın:

```text
Aşağıdaki paragrafı dergimin yazım kurallarına göre düzelt.

Kurallar:
1. Yüzyılları rakamla yaz (örnek: on sekizinci yüzyıl → 18. yüzyıl).
2. Yabancı dildeki terimleri *italik* yaz (Markdown yıldız işaretiyle).
3. 25 kelimeden uzun cümleleri böl.
4. "Biz", "görüyoruz", "diyebiliriz" gibi birinci çoğul şahıs ifadelerini edilgen veya üçüncü şahıs yapılarla değiştir.
5. Anlamı ve içeriği değiştirme.

Önce düzeltilmiş paragrafı ver. Sonra her kural için yaptığın değişiklikleri madde madde listele.

Paragraf:
On dokuzuncu yüzyılın ikinci yarısından itibaren İstanbul'un bazı semtlerinde görmeye başladığımız apartman tipi konutlar, Avrupa'daki immeuble de rapport örneklerinden etkilenmiş olup geleneksel sofalı plan şemasının yerini koridorlu plana bırakmasıyla birlikte ev içindeki mahremiyet anlayışının da değiştiğini düşünebiliriz.
```

3. **Tahmin sorusu:** Model kaç cümle üretecek? Hangi kelime italik olacak?
4. Cevabı okuyun ve her kuralı tek tek kontrol edin.

**Beklenen sonuç:**

> 19. yüzyılın ikinci yarısından itibaren İstanbul'un bazı semtlerinde apartman tipi konutlar görülmeye başlanır. Bu konutlar, Avrupa'daki *immeuble de rapport* örneklerinden etkilenmiştir. Geleneksel sofalı plan şeması yerini koridorlu plana bırakmıştır. Bu değişimle birlikte ev içindeki mahremiyet anlayışının da dönüştüğü düşünülebilir.

**Açıklama:** Her kural ölçülebilir olduğu için model uygulayabildi, biz de kontrol edebildik. Değişiklik listesi istemek, modelin neyi neden değiştirdiğini görmemizi sağlar.

#### Sık Yapılan Hatalar

**Hata 1: Çelişen yönergeler**

Hatalı: "Literatürü çok ayrıntılı tartış ama 100 kelimeyi geçme."

Doğru: Önceliği belirtin: "100 kelimeyi geçme; bu sınır içinde en önemli 2 tartışmaya odaklan."

**Hata 2: Yönergeyi metnin içine gömmek**

Neden hata? Uzun bir metnin ortasına yazılan talimat gözden kaçabilir.

Düzeltme: Talimatları metinden önce, ayrı bir bölümde verin.

**Hata 3: Örneği fazla özel seçmek**

Neden hata? Few-shot örneğinizde hep "plan tipolojisi" ifadesi geçerse, model diğer maddelere de gereksiz yere eklemeye çalışabilir.

Düzeltme: Birden fazla, birbirinden farklı örnek verin.

---

### Konu 3: Ton, Üslup ve Formatlama (30 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Aynı araştırma bulgusunu bir tez jürisine, bir sempozyum oturumuna ve bir gazeteciye anlatırken farklı kelimeler kullanırsınız. Bulgu aynıdır; anlatım değişir.

**Basit açıklama:**

- **Ton:** Metnin tavrı (nesnel, temkinli, ikna edici, samimi).
- **Üslup:** Metnin yazılış biçimi (kısa cümleli, kavram yoğun, betimleyici).
- **Format:** Metnin görsel düzeni (paragraf, liste, tablo, başlık).

**Teknik tanım:** Ton ve üslup kontrolü, modelin dil kayıtını (register), cümle yapısını ve sözcük seçimini yönergeler veya örnek metinler aracılığıyla belirlemektir. Formatlama ise çıktının yapısal düzenini (Markdown, tablo, JSON, madde listesi) tanımlamaktır.

#### Neden Öğreniyoruz?

Bir araştırmacı aynı bulguyu farklı yerlerde kullanır:

- Hakemli makale veya tez (akademik ton)
- Bildiri özeti (yoğun, yapılandırılmış)
- Proje başvurusu (ikna edici, etki odaklı)
- Kamuoyu için blog veya söyleşi (anlaşılır, merak uyandıran)
- Akademik sosyal medya paylaşımı (kısa, davetkâr)

Ton kontrolünü bilen araştırmacı, bir kez ürettiği bilgiyi birçok kanala uyarlayabilir.

#### Temel Kavramlar ve Ton Tablosu

| Ton | Özellikleri | Ne zaman? | Yönerge ifadesi |
|---|---|---|---|
| Akademik | Kanıta dayalı, nesnel, terim yoğun, temkinli | Makale, tez | "Akademik bir dille, nesnel ve temkinli ifadelerle yaz." |
| Alan dışı okura yönelik | Sade, örnekli, terimleri açıklayan | Disiplinlerarası dergi, kamuoyu yazısı | "Alan dışından bir okurun anlayacağı, örnekli ve sade bir dille yaz." |
| İkna edici | Önem ve etki odaklı | Proje başvurusu | "Çalışmanın özgün değerini ve etkisini vurgulayan ikna edici bir dille yaz." |
| Samimi | Kısa, soru soran | Sosyal medya | "Kısa, davetkâr ve anlaşılır yaz." |
| Resmî | Saygılı, net, kalıplara uygun | Dergi editörüne yazışma | "Resmî akademik yazışma kurallarına uygun yaz." |

**Üslup ipucu:** Kendi yazınızdan bir örnek vermek en güçlü üslup yönergesidir:

```text
Aşağıda daha önce yazdığım bir paragraf var. Yeni metni bu paragrafın üslubuyla yaz:
cümle uzunluğu, kelime seçimi ve akış benzer olsun.

Örnek paragrafım:
[kendi paragrafınız]
```

#### Formatlama Araçları

| İstenen format | Prompt ifadesi |
|---|---|
| Tablo | "Şu sütunlarla tablo yap: ..." |
| Numaralı liste | "Numaralı liste olarak ver." |
| Başlıklı metin | "Her bölümü bir başlıkla ayır." |
| Kelime sınırı | "Tam olarak 3 paragraf, her biri 80–100 kelime." |
| Yapılandırılmış özet | "Amaç / Yöntem / Bulgular / Sonuç başlıklarıyla yaz." |
| Kaynakça biçimi | "APA 7 biçimine göre düzenle." (Künye bilgisini siz verin!) |

> **Dikkat:** "APA biçimine göre düzenle" dediğinizde künye bilgilerini **siz** vermelisiniz. Model biçimlendirmede iyidir ama eksik bilgiyi (sayfa numarası, cilt, DOI) uydurabilir. Ona "Eksik bilgi varsa [EKSİK] yaz" deyin. Kaynakça için Zotero veya Mendeley gibi kaynak yönetim programları daha güvenilirdir.

#### Basit Örnek: Aynı Bulgu, Üç Ton

Bulgu: *"Apartman dairelerinde salon, uzun yıllar misafir için ayrılmış ve günlük hayatta pek kullanılmayan bir oda olarak kaldı."*

- **Akademik:** "1960'lı yıllardan itibaren orta sınıf apartman dairelerinde salonun gündelik kullanımdan ayrılarak bir temsil mekânına dönüştüğü gözlemlenmektedir."
- **Alan dışı okura yönelik:** "Birçok apartman dairesinde salonun kapısı çoğu gün kapalı dururdu. Bu oda, ailenin gündelik hayatından çok misafir ağırlamaya ayrılmıştı."
- **Sosyal medya:** "Sizin evde de 'misafir salonu' var mıydı? Yeni makalemizde bu odanın 1960–80 arasında nasıl bir 'vitrin' mekânına dönüştüğünü inceledik. 🔗"

**Soru:** Hangi metin bir makale için uygun? Hangisi bir yayın duyurusu için?

**Cevap:** Akademik ton makale için, sosyal medya tonu yayın duyurusu için uygundur.

#### Birlikte Uygulayalım: Bir Bulgu, Üç Kanal

**Amaç:** Ton ve formatı yönergelerle değiştirmek.

**Senaryo:** Bir araştırmanın ana bulgusu üç farklı kanalda kullanılacak.

**Adımlar:**

1. Yeni sohbet açın.
2. Şu promptu yazın:

```text
## BAĞLAM
Araştırmamın ana bulgusu şu:
"Apartman dairelerinde salon, 1950–1980 arasında ailenin gündelik hayatından ayrılarak
misafire ayrılmış bir temsil mekânına dönüştü. Aile ise gününü mutfak ve küçük oturma
odasında geçirmeye başladı."
Yöntem: dönem konut dergilerinin ve plan arşivlerinin incelenmesi.

## GÖREV
Bu bulguyu üç farklı çıktı olarak yaz.

## ÇIKTI BİÇİMİ
### 1. Makale paragrafı (tartışma bölümü)
Akademik ve temkinli ton, 150 kelime. Atıf gereken yerlere [ATIF] yaz.

### 2. Bildiri özeti (abstract)
Akademik ton, 200 kelime, amaç–yöntem–bulgular–sonuç sırasıyla.

### 3. Akademik sosyal medya paylaşımı
LinkedIn için, en fazla 80 kelime, okura bir soru sor, en fazla 3 hashtag kullan.
```

3. Üç çıktıyı okuyun.
4. **Soru:** "Hangisini olduğu gibi kullanırdınız, hangisini düzeltirdiniz?"
5. Düzeltilmesi gerekeni seçin ve aynı sohbette düzeltme isteyin:

```text
2 numaralı bildiri özetinde "bu çalışma" ifadesini iki kez kullanmışsın, tekrarı kaldır
ve son cümleyi daha temkinli yap ("gösterir" yerine "işaret eder" gibi).
```

**Beklenen sonuç:** Aynı bulgunun üç farklı tonda, belirtilen uzunluklarda üç versiyonu ve düzeltilmiş bir bildiri özeti.

**Açıklama:** Bulgu sabit kaldı; yalnızca ton, uzunluk ve format yönergeleri değişti. Bu, araştırmacının tek bir çalışmadan farklı kanallar için içerik üretmesini sağlar.

#### Sıra Sizde 2 (15 dk) – Özet Çıkarma Uygulaması

**Amaç:** Bir metinden farklı uzunluk ve formatta özet çıkarmak.

**Görev:** Aşağıdaki metni (veya kendi okuduğunuz bir makalenin bir bölümünü) kullanarak 3 farklı özet çıkartın.

Metin:

```text
Geleneksel Türk evinde oda, belirli bir işleve ayrılmış bir mekân değildi. Gün içinde
aynı oda oturmak, yemek yemek, misafir ağırlamak ve uyumak için kullanılırdı. Bunu mümkün
kılan, odanın donatılarıydı: Duvar boyunca uzanan sedirler oturma yerini, yüklük denilen
gömme dolaplar ise gece serilecek yatakları saklamayı sağlıyordu. Yemek, yere serilen
sofra bezinin üzerine konan sininin etrafında yenirdi. Böylece tek bir oda, eşyanın
yerleştirilip kaldırılmasıyla gün içinde birçok kez işlev değiştiriyordu. 19. yüzyılın
sonlarından itibaren Batılı mobilyanın –masa, sandalye, karyola– eve girmesiyle bu esneklik
azaldı; mobilya odaya yerleşti ve odalar tek işlevli hâle gelmeye başladı.
```

**İstenenler:**

1. Tek cümlelik özet.
2. 3 maddelik özet.
3. "Önce – Sonra" sütunlarından oluşan bir tablo özeti.

**Beklenen sonuç:** Üç farklı biçimde, metne sadık özetler.

**İpucu:** Her özet için ayrı bir biçim yönergesi yazın ve "metinde olmayan bilgi ekleme" demeyi unutmayın.

#### Çözüm

Prompt:

```text
Aşağıdaki metni üç farklı biçimde özetle. Sadece metindeki bilgileri kullan.

1. Tek cümlelik özet (en fazla 30 kelime).
2. 3 maddelik özet (her madde en fazla 15 kelime).
3. "Önce (geleneksel ev)" ve "Sonra (Batılı mobilya sonrası)" sütunlarından oluşan,
   en az 4 satırlık bir tablo.

Metin:
[metin]
```

Beklenen çıktı:

1. Geleneksel Türk evinde çok amaçlı kullanılan oda, Batılı mobilyanın eve girmesiyle esnekliğini kaybedip tek işlevli hâle geldi.
2. Maddeler:
   - Oda gün içinde oturma, yemek ve uyku için kullanılırdı.
   - Sedir, yüklük ve sini bu esnekliği sağlıyordu.
   - Batılı mobilya odaları tek işlevli hâle getirdi.
3. Tablo:

| Önce (geleneksel ev) | Sonra (Batılı mobilya sonrası) |
|---|---|
| Oda çok amaçlıydı | Oda tek işlevli oldu |
| Oturma için sedir | Oturma için sandalye ve koltuk |
| Yatak yüklükte saklanırdı | Karyola odaya sabitlendi |
| Yemek yerde, sini etrafında | Yemek masada |

#### Sık Yapılan Hatalar

**Hata 1: Ton için tek kelime kullanmak**

Hatalı: "Güzel yaz."

Doğru: "Nesnel, temkinli, üçüncü şahıs ağzından ve kısa paragraflarla yaz."

**Hata 2: Akademik metinde modelin kesin dilini olduğu gibi kabul etmek**

Neden hata? Model bazen "kuşkusuz", "açıkça kanıtlamaktadır" gibi gereğinden kesin ifadeler kullanır. Akademik dilde temkin önemlidir.

Düzeltme: "Kesin hükümlerden kaçın, 'işaret etmektedir', 'düşündürmektedir' gibi temkinli ifadeler kullan."

**Hata 3: Format isteyip içeriği kontrol etmemek**

Neden hata? Güzel bir tablo, yanlış bilgi içerebilir.

Düzeltme: Tablodaki her satırı kaynak metinle karşılaştırın.

---

### Konu 4: Rol Atama (20 dk)

> Bu konu ve bir sonraki konu, müfredattaki "İleri Prompt Teknikleri" modülünün ilk bölümüdür. Ders 3'te bu modüle devam edeceğiz.

#### Konu Nedir?

**Günlük hayat örneği:** Bir makale taslağını yayın öncesinde danışmanınıza, yöntem konusunda uzman bir meslektaşınıza ve alan dışından bir arkadaşınıza okuttuğunuzu düşünün. Her biri aynı metne farklı açıdan bakar ve farklı eleştiriler getirir.

**Basit açıklama:** Rol atama, yapay zekâya "Sen bir ... olarak davran" diyerek ona belirli bir uzmanlık, bakış açısı ve konuşma biçimi vermektir.

**Teknik tanım:** Rol atama (role prompting / persona prompting), modelin cevap üretirken belirli bir uzmanlık alanının terminolojisini, önceliklerini ve değerlendirme ölçütlerini benimsemesini sağlayan prompt tekniğidir.

> **Dikkat:** Rol vermek modele gerçek uzmanlık kazandırmaz. Model "uzman gibi konuşur" ama bilgisi yine eğitim verisiyle sınırlıdır. Rol, daha çok **bakış açısını ve önceliği** değiştirir.

#### Neden Öğreniyoruz?

Araştırmacı, metnini göndermeden önce farklı gözlerle okutmak ister: hakem, editör, yöntem uzmanı, alan dışı okur. Rol atama, bu farklı gözleri hızlıca simüle etmeyi sağlar. Böylece gerçek hakem sürecinde gelebilecek eleştirilere önceden hazırlanılabilir.

#### Temel Kavramlar: Faydalı Roller

| Rol | Ne işe yarar? | Örnek kullanım |
|---|---|---|
| Hakem | Argüman, kanıt, yöntem | Makale taslağını değerlendirme |
| Dergi editörü | Derginin kapsamına uygunluk, yapı, özgün katkı | Gönderim öncesi kontrol |
| Yöntem uzmanı | Veri toplama ve analiz | Yöntem bölümünü sınama |
| Alan dışı okur | Anlaşılırlık | "Mimarlık bilmeyen bir sosyolog olarak oku" |
| Tez jürisi üyesi | Tutarlılık, savunulabilirlik | Tez savunmasına hazırlık soruları |
| Şeytanın avukatı | Zayıf noktaları bulma | "Bu argümana karşı en güçlü itirazları yaz" |

#### Basit Örnek

```text
Sen mimarlık bilmeyen, kent sosyolojisi alanında çalışan bir araştırmacısın. Aşağıdaki paragrafı oku
ve anlamadığın her kavramı ve cümleyi listele. Dürüst ol.

Paragraf:
Hayatlı plan tipinde odalar, güneye bakan yarı açık bir sofaya dizilir; zamanla hayatın
camekânla kapatılmasıyla iç sofalı ve orta sofalı plan tiplerine geçilmiştir.
```

**Tahmin sorusu:** Model hangi kavramları anlamadığını söyler?

**Cevap:** Muhtemelen "hayatlı plan tipi", "yarı açık sofa", "camekân", "iç sofalı / orta sofalı plan" gibi terimler. Bu liste, disiplinlerarası bir dergiye gönderilecek metinde hangi terimlerin açıklanması gerektiğini gösterir.

#### Birlikte Uygulayalım: Hakem Gözüyle Okuma

**Amaç:** Aynı metni farklı rollerle değerlendirip farklı geri bildirimler almak.

**Senaryo:** Bir makalenin giriş paragrafı yazıldı. Dergiye gönderilmeden önce üç farklı gözle okutacağız.

**Adımlar:**

1. Kendi yazdığınız bir giriş paragrafını veya Ders 1'de yazdırdığınız giriş paragrafını hazırlayın.
2. Yeni sohbette şunu yazın:

```text
Aşağıdaki paragrafı üç farklı rol ile ayrı ayrı değerlendir.
Her rol için ayrı bir başlık aç ve en fazla 3 madde yaz.

Rol 1: Mimarlık alanında hakemli bir derginin hakemi (argümanın netliği, literatürdeki boşluğun gösterilmesi)
Rol 2: Yöntem uzmanı (araştırma sorusunun yöntemle cevaplanabilirliği)
Rol 3: Mimarlık dışından bir sosyal bilimci (anlaşılırlık, terimler)

En sonda, üç rolün ortak önerisini tek cümleyle yaz.

Paragraf:
[paragraf]
```

3. Üç değerlendirmeyi okuyun.
4. **Soru:** "Hangi rolün eleştirisi sizi en çok şaşırttı?"
5. Ortak öneriye göre paragrafı modelden yeniden yazmasını isteyin:

```text
Ortak öneriyi ve üç roldeki eleştirileri dikkate alarak paragrafı yeniden yaz.
Benim üslubumu ve atıflarımı koru. Değişiklikleri sonda madde madde açıkla.
```

**Beklenen sonuç:** Üç farklı bakış açısından gelen eleştiri ve bunlara göre iyileştirilmiş bir paragraf.

**Açıklama:** Hakem argümana, yöntem uzmanı soru–yöntem uyumuna, alan dışı okur anlaşılırlığa odaklandı. Tek bir "değerlendir" promptu bu çeşitliliği vermezdi.

> **Dikkat:** Size gelen gerçek bir hakem raporunu veya başkasına ait, gizli tutulması gereken bir makale taslağını (örneğin hakemliğini yaptığınız bir makaleyi) yapay zekâ araçlarına yüklemeyin. Hakemlik süreci gizlidir ve birçok dergi bunu açıkça yasaklar.

#### Sık Yapılan Hatalar

**Hata 1: Rolü çok genel vermek**

Hatalı: "Sen bir uzmansın."

Doğru: "Sen konut çalışmaları alanında 20 yıllık deneyime sahip, nitel yöntemlerle çalışan bir hakemsin."

**Hata 2: Rolün gerçek uzmanlık kazandırdığını sanmak**

Neden hata? "Sen bir profesörsün" demek, modelin uydurma yapmasını engellemez.

Düzeltme: Rolle birlikte "emin olmadığında belirt" yönergesini de verin.

**Hata 3: Eleştiri rolünde modelin aşırı kibar kalması**

Neden hata? Modeller varsayılan olarak nazik ve övücü olma eğilimindedir.

Düzeltme: "Övgüye yer verme. Sadece zayıf noktaları ve somut iyileştirme önerilerini yaz."

---

### Konu 5: Chain of Thought – Adım Adım Düşünme (20 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir örneklem büyüklüğü hesaplarken evren büyüklüğünü, güven düzeyini ve hata payını tek tek belirler, sonra formüle yerleştirirsiniz. Sonuca tek hamlede atlamak yerine adımları sırayla izlemek hatayı azaltır.

**Basit açıklama:** Chain of thought (düşünce zinciri), yapay zekâdan sonuca doğrudan atlamak yerine, düşünme adımlarını sırayla yazmasını istemektir.

**Teknik tanım:** Chain-of-thought prompting, modelin nihai cevaptan önce ara akıl yürütme adımlarını üretmesini sağlayan tekniktir. Model her adımı ürettiğinde bu adım bir sonraki tahminin bağlamına eklenir; bu da çok aşamalı problemlerde doğruluğu artırır.

> **Not:** Günümüzde bazı modeller ("düşünen" veya "reasoning" modeller) cevap vermeden önce kendi içlerinde adım adım düşünür. Bu modellerde "adım adım düşün" demek daha az fark yaratır. Ancak adımları **görünür** yazdırmak, sizin akıl yürütmeyi kontrol etmenizi sağladığı için yine faydalıdır.

#### Neden Öğreniyoruz?

- **Araştırma tasarımında:** "Hangi yöntem bu soruya uygun?" gibi birçok etkeni olan kararlarda.
- **Kuramsal tartışmalarda:** İki yaklaşımı karşılaştırırken.
- **Kontrol için:** Modelin hangi adımda hata yaptığını görmek için.
- **Planlamada:** Tez takvimi, veri toplama planı gibi işlerde.

#### Temel Kavramlar

**Kavram: Ara adım**

- Basit açıklama: Sonuca giden yoldaki her bir küçük düşünce.
- Örnek: "1. Önce araştırma sorusunun türünü belirle (betimleyici mi, açıklayıcı mı?). 2. Sonra hangi verinin gerektiğini düşün. 3. Sonra yöntem öner."

**Kavram: Adımları biz tanımlamak**

- Basit açıklama: "Adım adım düşün" demek yerine, adımları kendimiz yazmak.
- Neden? Modelin doğru yöntemle düşünmesini sağlar.

#### Basit Örnek

Adımsız:

```text
Tezimi 12 ayda bitirmem gerekiyor. Nasıl planlamalıyım?
```

Adımlı:

```text
Yüksek lisans tezimi 12 ayda bitirmem gerekiyor. Tez 5 bölümden oluşacak:
giriş, literatür, yöntem, bulgular, sonuç. Bulgular için 3 ay saha çalışması gerekiyor.
Şu adımları sırayla izle ve her adımın sonucunu yaz:
1. Etik kurul başvurusu gibi saha öncesi işlerin süresini tahmin et.
2. Saha çalışmasını takvime yerleştir.
3. Son 2 ayı bütün tezin düzeltmesi ve danışman geri bildirimi için ayır.
4. Kalan süreyi bölümlere dağıt; hangi bölümün hangisinden önce yazılması gerektiğini gerekçelendir.
5. Sonucu Ay | Yapılacak iş | Teslim edilecek ürün sütunlu bir tabloyla ver.
```

**Soru:** İkinci promptun cevabı neden daha güvenilir?

**Cevap:** Çünkü modelin varsayımları (etik kurul süresi, saha zamanlaması) ve gerekçeleri görünür. Bir adım yanlışsa hemen fark edilir ve düzeltilir.

#### Birlikte Uygulayalım: Yöntem Seçimi

**Amaç:** Karmaşık bir araştırma kararını adım adım düşündürmek.

**Senaryo:** "Kentsel dönüşüm sonrası yeni konut sitelerine taşınan ailelerin komşuluk ilişkileri nasıl değişti?" sorusu için yöntem seçilecek.

**Adımlar:**

1. Yeni sohbet açın.
2. Önce adımsız soruyu sorun:

```text
"Kentsel dönüşüm sonrası yeni konut sitelerine taşınan ailelerin komşuluk ilişkileri nasıl değişti?"
sorusu için hangi yöntemi kullanmalıyım?
```

3. Cevabı not edin.
4. Yeni sohbette adımlı soruyu sorun:

```text
Araştırma sorum: "Kentsel dönüşüm sonrası yeni konut sitelerine taşınan ailelerin komşuluk
ilişkileri nasıl değişti?"
Koşullar: Yüksek lisans tezi, 1 yıl süre, tek araştırmacı, sınırlı bütçe.

Yöntem kararı için şu adımları izle ve her adımı ayrı başlıkla yaz:
Adım 1: Sorunun türünü belirle (betimleyici, açıklayıcı, karşılaştırmalı?) ve gerekçelendir.
Adım 2: Bu soruyu cevaplamak için hangi tür veriye ihtiyaç olduğunu yaz.
Adım 3: En az 3 olası yöntemi (örneğin anket, derinlemesine görüşme, gözlem) listele.
Adım 4: Her yöntemi soruya uygunluk, uygulanabilirlik ve etik açısından tabloyla karşılaştır.
Adım 5: Bir yöntem veya yöntem birleşimi öner ve sınırlılıklarını yaz.
```

5. İki cevabı karşılaştırın.

**Beklenen sonuç:** Adımlı cevapta örneğin "derinlemesine görüşme ağırlıklı, gözlemle desteklenmiş nitel bir tasarım" gibi gerekçeli bir öneri ve karşılaştırma tablosu.

**Açıklama:** Adımsız soruda model genellikle tek bir yöntem adı verir. Adımlı soruda sorunun türünü, veri ihtiyacını ve koşulları görünür şekilde düşündüğü için karar daha savunulabilir hâle gelir. Biz de akıl yürütmeye katılıp "Ben gözlemi değil, fotoğraf-anlatı (photo-elicitation) yöntemini düşünürüm çünkü..." diyebiliriz.

#### Gerçek Hayat Senaryosu: İki Kuramsal Yaklaşımı Karşılaştırmak

**Senaryo:** Bir konut araştırmasının kuramsal çerçevesinde, evi "fiziksel bir tipoloji" olarak inceleyen yaklaşımla, evi "gündelik hayat pratikleri" üzerinden inceleyen yaklaşım arasında seçim yapılacak.

**Problem nedir?** Hangi yaklaşımın araştırma sorusuna daha uygun olduğuna karar vermek.

**Nasıl çözeceğiz?** Modeli adım adım ve ölçütlere göre düşündüreceğiz.

**Hangi bilgileri kullanacağız?** Araştırma sorusu, eldeki kaynak türleri.

**Prompt:**

```text
Araştırmamın kuramsal çerçevesi için iki yaklaşım arasında karar vermek istiyorum.

Yaklaşım 1: Evi plan tipleri ve mekân organizasyonu üzerinden inceleyen tipolojik yaklaşım.
Yaklaşım 2: Evi, içinde yaşayanların gündelik pratikleri (yemek, uyku, misafir ağırlama)
üzerinden inceleyen gündelik hayat yaklaşımı.

Araştırma sorusu: Ev mekânının değişimiyle gündelik hayat nasıl değişti?
Elimdeki kaynaklar: Plan çizimleri, dönem dergileri, sözlü tarih görüşmeleri.

Adım adım düşün:
1. Her yaklaşımın neyi görünür kıldığını yaz.
2. Her yaklaşımın neyi gözden kaçırabileceğini yaz.
3. Elimdeki kaynakların hangi yaklaşımı daha iyi desteklediğini değerlendir.
4. Araştırma sorusuna uygunluğu değerlendir.
5. Bir öneri yap. İki yaklaşımı birleştirmek mümkünse nasıl birleştirileceğini açıkla.
Emin olmadığın noktaları belirt. Kuramcı adı ve eser adı verme.
```

**Beklenen sonuç:** İki yaklaşımın gerekçeli değerlendirmesi ve büyük ihtimalle "gündelik hayat yaklaşımı ana çerçeve, tipolojik yaklaşım destekleyici analiz aracı" gibi birleştirici bir öneri.

> **Dikkat:** Model burada bir **tartışma ortağı**dır. Kuramsal tercih araştırmacının kendi kararıdır. Model kuramcı veya eser adı önerirse, bunları mutlaka orijinal kaynaklardan kontrol edin ve okumadığınız bir kaynağa atıf yapmayın.

#### Sık Yapılan Hatalar

**Hata 1: Basit sorularda gereksiz adım istemek**

Neden hata? "Eyvan nedir?" sorusu için 5 adımlı düşünce gereksizdir ve cevabı uzatır.

Düzeltme: Adım adım düşünmeyi çok etkenli kararlar ve planlamalar için kullanın.

**Hata 2: Adımları okumadan sadece sonuca bakmak**

Neden hata? Adımları yazdırmanın amacı kontrol etmektir.

Düzeltme: Her adımı okuyun; hatalı adım varsa "3. adımda etik kurul sürecini atladın" diye düzeltin.

**Hata 3: Mantıklı görünen akıl yürütmenin doğru olduğunu sanmak**

Neden hata? Model yanlış bir bilgiden başlayıp çok mantıklı bir zincir kurabilir.

Düzeltme: Zincirdeki bilgi iddialarını (tarih, isim, olay) ayrıca doğrulayın.

---

### Ders Özeti

Bu derste promptlarımızı düzenli bir yapıya kavuşturduk: **bağlam + rol + görev + çıktı biçimi.** Bu yapıyla, her makalede aynı biçimde okuma notu çıkaran bir şablon hazırladık. Doğru yönergenin açık, ölçülebilir, olumlu ifadeli, sıralı ve gerekçeli olması gerektiğini gördük ve dergi yazım kurallarını modele uygulattık. Örnek vererek (few-shot) modelin istenen kalıbı taklit etmesini sağladık. Aynı bulguyu makale, bildiri özeti ve sosyal medya için farklı tonlarda yazdırdık ve özet çıkarmayı farklı formatlarda denedik. Son olarak modele hakem, yöntem uzmanı ve alan dışı okur rolleri vererek metni üç gözle değerlendirdik ve yöntem seçimi gibi karmaşık kararları adım adım düşündürdük.

### Bu Derste Neler Öğrendik?

- Promptun dört temel bileşenini (bağlam, rol, görev, çıktı biçimi) öğrendik.
- Yeniden kullanılabilir bir "makale okuma notu" şablonu hazırladık.
- İyi yönergenin 5 özelliğini öğrendik ve dergi yazım kurallarını uygulattık.
- Zero-shot, one-shot ve few-shot kavramlarını gördük.
- Ton, üslup ve format arasındaki farkı öğrendik.
- Aynı bulguyu makale, bildiri ve sosyal medya için yazdırdık.
- Bir metinden farklı biçimlerde özet çıkardık.
- Rol atamayla metni hakem, yöntem uzmanı ve alan dışı okur gözüyle değerlendirdik.
- Chain of thought ile yöntem seçimi gibi kararları adım adım düşündürdük.

### Mini Quiz

1. **(Çoktan seçmeli)** Aşağıdakilerden hangisi prompt yapısının dört temel bileşeninden biri **değildir**?
   - a) Bağlam
   - b) Rol
   - c) Şifre
   - d) Çıktı biçimi
2. **(Doğru / Yanlış)** "Kısa yaz" yönergesi, "En fazla 150 kelime yaz" yönergesinden daha ölçülebilirdir.
3. **(Kısa cevap)** Modele 2–3 örnek göstererek aynı kalıpta çıktı üretmesini sağlamaya ne ad verilir?
4. **(Çoktan seçmeli)** "Sen hakemli bir derginin hakemisin" rolünü vermek ne sağlar?
   - a) Modelin hiç hata yapmamasını
   - b) Modelin bakış açısını ve değerlendirme ölçütlerini değiştirmeyi
   - c) Modelin internette arama yapmasını
   - d) Modelin kaynakları doğrulamasını
5. **(Kısa cevap)** Chain of thought tekniği hangi tür sorularda en çok fayda sağlar?
6. **(Küçük problem)** Şu yönergeyi olumlu ve ölçülebilir hâle getirin: "Çok uzun ve dağınık yazma."
7. **(Doğru / Yanlış)** "APA biçimine göre düzenle" dediğimizde model eksik künye bilgilerini doğru şekilde tamamlar.
8. **(Çıktı tahmini)** Şu prompta model nasıl bir çıktı verir? `Aşağıdaki iki kelimeyi örnekteki gibi yaz. Örnek: Sofa → SOFA (4 harf). Kelimeler: cumba, eyvan`

### Mini Quiz Cevapları

1. **c.** Dört bileşen bağlam, rol, görev ve çıktı biçimidir.
2. **Yanlış.** "En fazla 150 kelime" ölçülebilir; "kısa" kişiden kişiye değişir.
3. **Few-shot prompting** (birkaç örnekli prompt).
4. **b.** Rol bakış açısını değiştirir ama hatasızlık sağlamaz.
5. Birden fazla etkenin değerlendirildiği kararlar (yöntem seçimi gibi), karşılaştırmalar, planlamalar ve çok aşamalı problemler.
6. Örnek: "En fazla 200 kelime yaz. Her paragraf tek bir iddiayla başlasın, ardından kanıt ve kısa bir yorum gelsin."
7. **Yanlış.** Eksik bilgileri uydurabilir; künyeyi siz vermeli ve eksikleri [EKSİK] olarak işaretletmelisiniz.
8. Beklenen çıktı:

```text
cumba → CUMBA (5 harf)
eyvan → EYVAN (5 harf)
```

Model örnekteki kalıbı (büyük harf ve harf sayısı) taklit eder.

### Ders Sonu Uygulaması

**Senaryo:** "Konutta mutfağın dönüşümü" konusunda bir literatür bölümü yazılıyor. Bu bölüm için bir makale okundu; okuma notu çıkarılacak, notu kullanan bir literatür paragrafı yazdırılacak ve paragraf hakem gözüyle değerlendirilip revize edilecek.

**Yapılacaklar:**

1. Mutfak konusunda bulduğunuz gerçek bir makalenin özetini veya bir bölümünü alın. (Bulamazsanız Sıra Sizde 2'deki metni kullanın.)
2. Bu dersteki "makale okuma notu" şablonuyla okuma notu çıkarın.
3. Okuma notundaki bir bulgudan yola çıkarak, dört bileşenli bir promptla 150 kelimelik bir literatür paragrafı yazdırın (akademik ton).
4. Paragrafı iki rolle (hakem ve alan dışı okur) değerlendirtin.
5. Değerlendirmeye göre paragrafı yeniden yazdırın.
6. Kullandığınız promptları "Prompt Defterim" dosyasına kaydedin.

**Beklenen sonuç:** Bir okuma notu, bir paragrafın ilk ve son sürümü, iki rolün değerlendirmesi.

**İpuçları:**

- Paragraf promptunda okuma notundaki bulguyu ve makalenin yazar–yıl bilgisini bağlam bölümüne yapıştırın.
- Değerlendirme rollerine "övgüye yer verme" yönergesini ekleyin.
- Son sürümde "atıfları ve üslubumu koru" demeyi unutmayın.

### Ders Sonu Uygulaması – Çözüm

**Adım 2:** Konu 1'deki okuma notu şablonu, makale metni yapıştırılarak kullanılır.

**Adım 3 – Paragraf promptu:**

```text
## BAĞLAM
Konutta mutfağın dönüşümü üzerine bir makalenin literatür bölümünü yazıyorum.
Okuduğum bir makalenin (Yazar, Yıl) bulgusu şu:
[okuma notundaki bulgu, örneğin: "Geleneksel evlerde mutfak çoğu zaman ana yapının dışında
ya da arka kısımda yer alıyordu; apartman dairelerinde ise mutfak evin içine alınarak
küçüldü ve standartlaştı."]

## ROL
Sen konut çalışmaları alanında makaleler yayımlamış bir akademisyensin.

## GÖREV
Bu bulguyu literatüre yerleştiren bir paragraf yaz. Bulguyu (Yazar, Yıl) atfıyla aktar.
Bulguda olmayan tarih, isim veya istatistik ekleme; başka atıf gereken yerlere [ATIF] yaz.

## ÇIKTI BİÇİMİ
- 150 kelime civarı, tek paragraf
- Akademik ve temkinli ton
- Paragraf bir iddia cümlesiyle başlasın ve bir sonraki paragrafa geçişi hazırlayan bir cümleyle bitsin
```

**Adım 4 – Değerlendirme promptu:**

```text
Aşağıdaki literatür paragrafını iki rolle ayrı ayrı değerlendir. Övgüye yer verme;
her rol için en fazla 3 somut iyileştirme önerisi yaz.

Rol 1: Konut çalışmaları alanında hakemli bir derginin hakemi
Rol 2: Mimarlık dışından bir sosyal bilimci

Paragraf:
[paragraf]
```

**Adım 5 – Yeniden yazım promptu:**

```text
Bu önerileri uygulayarak paragrafı yeniden yaz. Uzunluğu, atıfları ve üslubu koru.
Sonra hangi öneriyi nasıl uyguladığını madde madde açıkla.
```

**Değerlendirme ölçütü:** Son paragraf; bulguya ve atfa sadık kalmalı, uydurma bilgi içermemeli, 150 kelime civarında olmalı, bir iddia cümlesiyle başlamalı ve sonraki paragrafa geçiş sağlamalıdır.

> **Sonraki derste:** Bugün her seferinde bağlamı ve rolü yeniden yazdık. Bir sonraki derste **sistem mesajları ve özel talimatlarla** bunu kalıcı hâle getirecek, kendi araştırma asistanımızı tanımlayacağız. Ayrıca aynı prompttan birden fazla çıktı alıp karşılaştırmayı, yapay zekâ ile görsel düzenlemeyi ve bir akademik blog yazısını uygun görseliyle birlikte üretmeyi öğreneceğiz.
