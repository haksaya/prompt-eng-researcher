# Prompt Mühendisliği Eğitimi – Ders 1

## Prompt Mühendisliğine Giriş ve Temel Kavramlar (Yaklaşık 2,5 Saat)

### Kursun Genel Planı

| Ders | Konular | Süre | Öne Çıkan Uygulamalar |
|---|---|---|---|
| Ders 1 | Yapay zekâ nedir, prompt mühendisliğinin önemi, iyi/kötü prompt, açık prompt yazma, stratejiler, model sınırları | 150 dk | Konuyu araştırma sorusuna dönüştürme, kaynak doğrulama testi |
| Ders 2 | Prompt yapısı (bağlam + rol + görev + çıktı biçimi), yönerge yazma, ton/üslup/format, rol atama, adım adım düşünme | 150 dk | Makale okuma notu şablonu, bildiri özeti, hakem gözüyle değerlendirme |
| Ders 3 | Sistem mesajları, çoklu deneme ve karşılaştırma, yapay zekâ ile görsel düzenleme, görsel–metin entegrasyonu | 150 dk | Araştırma asistanı talimatı, akademik blog yazısı + uygun görsel |
| Ders 4 | Midjourney / GPT Image ile görsel üretim, görsel prompt yapısı, ses-video, yapay sinir ağları, token tahmini, üretken yapay zekâ | 150 dk | Sunum ve poster görselleri, yayın duyurusu için sosyal medya içeriği, elle sinir ağı hesabı |
| Ders 5 | Sektörel uygulamalar (yazılım, eğitim, pazarlama, tasarım), yapay zekâ ajanları, no-code platformlar | 150 dk | Kaynakça kodu, quiz üretme, sempozyum destek asistanı, araştırma asistanı ajanı |
| Ders 6 | API, Python/Anaconda kurulumu, OpenAI API, ilk chat, fine-tuning verileri, modeli gözlemleme/silme, chatbot | 150 dk | Toplu okuma notu programı, GPT API ile chatbot; final projesi |

**Toplam:** 6 ders × 150 dakika = 900 dakika (15 saat)

> **Not:** Kurs boyunca örnekler akademik çalışmanın gerçek aşamalarından seçilmiştir: konu belirleme, literatür taraması, makale okuma ve not alma, araştırma sorusu ve yöntem, makale/tez yazımı, bildiri özeti, hakem süreci, poster ve sunum, araştırmanın kamuoyuyla paylaşılması. Örnek konular mimarlık ve konut araştırmaları alanından alınmıştır (geleneksel konut, apartmanlaşma, kentsel dönüşüm, malzeme ve yapım teknikleri gibi).

---

## Ders 1 – 150 Dakika

### Dersin Hedefleri

Bu dersin sonunda öğrenci:

- Yapay zekânın ve özellikle büyük dil modellerinin (ChatGPT, Claude, Gemini gibi) temelde nasıl çalıştığını sade bir dille açıklayabilecek.
- "Prompt" kavramını ve prompt mühendisliğinin neden önemli olduğunu anlatabilecek.
- İyi ve kötü promptları birbirinden ayırt edebilecek.
- Açık, kapsamlı ve hedefe yönelik bir prompt yazabilecek.
- Yapay zekânın neleri iyi yaptığını, nerelerde yanıldığını (özellikle uydurma kaynak üretme riskini) bilecek.
- Bir yapay zekâ sohbet aracında ilk araştırma promptlarını yazıp sonuçları değerlendirebilecek.

### Süre Planı

| Bölüm | Süre |
|---|---|
| Giriş ve beklentiler | 10 dk |
| Konu 1: Yapay zekâ nedir, nasıl çalışır? | 25 dk |
| Konu 2: Prompt mühendisliğinin önemi ve iletişimin püf noktaları | 20 dk |
| Konu 3: İyi/kötü prompt, açık ve kapsamlı prompt, hedefe yönelik stratejiler, yönlendirmeler (birlikte uygulama dahil) | 45 dk |
| Konu 4: Dil modelinin sınırları ve kapasitesi | 25 dk |
| Ders özeti ve mini quiz | 15 dk |
| Ders sonu uygulaması | 10 dk (evde tamamlanabilir) |
| **Toplam** | **150 dk** |

### Derse Hazırlık

- Bir yapay zekâ sohbet aracı açık olsun: ChatGPT (chatgpt.com), Claude (claude.ai) veya Gemini (gemini.google.com). Ücretsiz sürümler bu ders için yeterlidir.
- Herkesin aynı araçlardan birine giriş yapmış olması gerekir.
- Bir not dosyası açın (Word, Google Docs veya Not Defteri). Beğendiğimiz promptları burada saklayacağız. Bu dosyanın adı: **"Prompt Defterim"**.

---

### Giriş: Neden Buradayız? (10 dk)

**Soru:** Bugüne kadar yapay zekâya hangi soruları sordunuz? Aldığınız cevaplardan memnun kaldınız mı?

**Cevap:** Çoğu kişi "bazen çok iyi, bazen çok genel ya da yanlış cevaplar aldım" der. Bu dersin bütün amacı tam olarak bu farkın nedenini anlamaktır. Cevabın kalitesi büyük ölçüde sorunun kalitesine bağlıdır.

Bir benzetme:

> Bir tez öğrencisi danışmanına gidip yalnızca "Konut hakkında bir şey yazmak istiyorum." derse ne olur? Danışman ya çok genel bir öneri verir ya da bir sürü soru sormak zorunda kalır: Hangi dönem? Hangi şehir? Hangi kuramsal çerçeve? Hangi yöntem?
>
> Yapay zekâ çoğu zaman bu soruları sormaz; eksik bilgiyi **tahminle** doldurur. Bu yüzden iyi bir **araştırma önerisi** nasıl iyi bir tezin temeliyse, iyi bir **prompt** da iyi bir yapay zekâ cevabının temelidir.

Bu benzetme kurs boyunca sık sık karşımıza çıkacak: **Prompt = yapay zekâya verilen iyi tanımlanmış bir görev tanımı.**

---

### Konu 1: Yapay Zekâ Nedir, Nasıl Çalışır? (25 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Telefonunuzda mesaj yazarken klavye bir sonraki kelimeyi tahmin eder. "Yarın akşam" yazdığınızda "görüşürüz" ya da "yemeğe" önerisi çıkar. Klavye bunu, milyonlarca mesajda hangi kelimelerin birbirini takip ettiğini öğrendiği için yapar.

**Basit açıklama:** ChatGPT gibi sohbet araçları, bu otomatik tamamlamanın çok ama çok gelişmiş bir hâlidir. Kitaplardan, makalelerden, web sayfalarından oluşan devasa miktarda metin üzerinde eğitilmişlerdir. Siz bir şey yazdığınızda, "bu metnin ardından en uygun devam ne olur?" sorusunu art arda cevaplayarak yanıt üretirler.

**Teknik tanım:**

- **Yapay zekâ (YZ / AI – Artificial Intelligence):** Normalde insan zekâsı gerektiren işleri (dil anlama, görüntü tanıma, karar verme) yapabilen bilgisayar sistemlerinin genel adıdır.
- **Makine öğrenmesi:** Bilgisayara kuralları tek tek yazmak yerine, örneklerden kendi kendine örüntü çıkarmasını sağlayan yöntemdir.
- **Büyük dil modeli (LLM – Large Language Model):** Çok büyük metin verisiyle eğitilmiş, metin anlayan ve üreten yapay zekâ modelidir. ChatGPT'nin arkasındaki GPT modelleri, Claude, Gemini birer büyük dil modelidir.
- **Üretken yapay zekâ (Generative AI):** Yeni içerik (metin, görsel, ses, video) üretebilen yapay zekâ türüdür.

**Akademik benzetme:** Bir araştırmacının alanındaki yüzlerce makaleyi okuyarak zamanla "bu dergide makaleler genelde şu yapıda yazılır", "bu kavram genelde şu kuramcıyla birlikte anılır" gibi örüntüleri sezgisel olarak öğrenmesine benzer. Dil modeli de metinler arasında benzer örüntüleri öğrenir.

> **Dikkat:** Bu benzetmenin bir sınırı var. Araştırmacı gerçekten **anlar** ve yanlış bir şeyi fark edebilir. Dil modeli ise "hangi kelimenin gelmesi olası?" sorusuna cevap verir. Bu yüzden kulağa çok inandırıcı gelen ama yanlış olan cümleler üretebilir. Bunu Konu 4'te ayrıntılı göreceğiz.

#### Neden Öğreniyoruz?

- **Gerçek hayatta:** E-posta yazmak, uzun bir metni özetlemek, bir konuyu hızlıca anlamak.
- **Akademik çalışmada:** Okunan makaleleri özetlemek, kavramları karşılaştırmak, araştırma sorusunu netleştirmek, literatür taraması için anahtar kelime üretmek, taslak metni dil açısından düzeltmek, bildiri özetini kısaltmak.
- **İş hayatında:** Proje raporları, sunum metinleri, şartnameleri özetleme.
- **Yazılım geliştirmede:** Veri düzenleyen küçük programlar yazdırmak (Ders 5 ve 6'da göreceğiz).

Bir yapay zekânın nasıl çalıştığını bilen kişi, ondan neyi isteyebileceğini ve ona ne zaman güvenmemesi gerektiğini de bilir.

#### Temel Kavramlar

**Kavram: Model**

- Basit açıklama: Yapay zekânın "beyni" olan, eğitilmiş program.
- Neden kullanılır? Farklı modellerin farklı güçlü yanları vardır; kimi daha hızlı, kimi daha derin düşünür.
- Örnek: GPT-5.5, Claude, Gemini birer modeldir. ChatGPT ise bir **uygulamadır** ve arkasında GPT modellerini kullanır.

**Kavram: Prompt**

- Basit açıklama: Yapay zekâya yazdığınız istek, soru veya talimat.
- Neden kullanılır? Modelin ne yapacağını ancak prompt sayesinde bilir.
- Örnek: "Geleneksel Türk evinde sofa nedir? 3 cümleyle açıkla."

**Kavram: Yanıt (Çıktı / Output)**

- Basit açıklama: Yapay zekânın prompta verdiği cevap.
- Neden önemli? Değerlendirdiğimiz ve düzelttiğimiz şey budur.
- Örnek: "Sofa, geleneksel Türk evinde odaların açıldığı ortak yaşam alanıdır..."

**Kavram: Eğitim verisi**

- Basit açıklama: Modelin "okuyarak" öğrendiği metinlerin tamamı.
- Neden önemli? Model, eğitim verisinde az geçen konularda (örneğin çok yerel bir yapı ya da az bilinen bir arşiv) daha çok hata yapar.
- Örnek: Süleymaniye Camii hakkında çok metin vardır; küçük bir Kastamonu köy camisi hakkında çok az.

**Kavram: Bilgi kesim tarihi (knowledge cutoff)**

- Basit açıklama: Modelin eğitim verisinin bittiği tarih. Model bu tarihten sonra olanları bilmez (internette arama özelliği açık değilse).
- Örnek: Geçen ay yayımlanan bir makaleyi model bilmeyebilir.

#### Basit Örnek: Otomatik Tamamlama Oyunu

Şu cümleleri birlikte tamamlayalım:

**Soru:** "Mimar Sinan'ın ustalık eseri olarak bilinen yapı ......" cümlesini nasıl tamamlarsınız?

**Cevap:** Çoğu kişi "Selimiye Camii'dir" der. Çünkü bu ifade metinlerde çok sık geçer. Dil modeli de aynı mantıkla en olası devamı seçer.

**Soru:** Peki "Bir makalenin özeti genellikle amaç, yöntem, bulgular ve ......" cümlesi?

**Cevap:** "sonuçtan oluşur". Burada da en sık geçen ve anlamlı devam seçilir.

Bu küçük oyun, dil modelinin temel mantığını gösterir: **bağlama göre en uygun devamı tahmin etmek.** Bağlam ne kadar zengin olursa, tahmin o kadar isabetli olur.

#### Birlikte Uygulayalım: İlk Sohbetimiz

**Amaç:** Bir yapay zekâ sohbet aracını açmak, ilk soruyu sormak ve cevabı incelemek.

**Senaryo:** Konut araştırmalarında sık geçen "sofa" kavramının ne olduğunu öğrenmek istiyoruz.

**Adımlar:**

1. Tarayıcıyı açın ve chatgpt.com, claude.ai veya gemini.google.com adresine gidin.
2. Hesabınızla giriş yapın.
3. Ekranın altındaki mesaj kutusuna tıklayın.
4. Şu promptu yazın:

```text
Sofa nedir?
```

5. Enter tuşuna basın.
6. **Tahmin sorusu:** Cevap gelmeden önce düşünelim: "Sizce yapay zekâ hangi 'sofa'dan bahsedecek?"
7. Cevabı inceleyin. Büyük ihtimalle yapay zekâ ya oturma mobilyası olan kanepeden ya da hem kanepeden hem mimari mekândan bahsedecektir.
8. Şimdi aynı sohbette yeni bir mesaj yazın:

```text
Geleneksel Türk evi mimarisindeki "sofa" kavramını, bir mimarlık tarihi makalesinin
kavramsal çerçeve bölümünde kullanılacak şekilde 5 cümleyle tanımla.
Akademik ve nesnel bir dil kullan.
```

9. İki cevabı karşılaştırın.

**Beklenen sonuç:** İkinci cevap konu açısından çok daha isabetli, uzunluk açısından kontrollü ve akademik kullanıma daha uygun olmalıdır.

**Açıklama:** İlk promptta "sofa" kelimesinin iki anlamı vardı ve model hangisini kastettiğimizi bilemedi. İkinci promptta **bağlam** (geleneksel Türk evi mimarisi), **kullanım yeri** (makalenin kavramsal çerçeve bölümü), **ton** (akademik, nesnel) ve **uzunluk** (5 cümle) verdik. Model artık tahmin etmek zorunda kalmadı.

**Soru:** İkinci promptta hangi bilgileri ekledik?

**Cevap:** Bağlam, metnin nerede kullanılacağı, ton ve uzunluk.

---

### Konu 2: Prompt Mühendisliğinin Önemi ve Yapay Zekâ ile İletişimin Püf Noktaları (20 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir kütüphaneciye "Bana mimarlıkla ilgili bir kaynak ver." derseniz elinize rastgele bir kitap gelir. "Osmanlı sivil mimarisi üzerine, 1990 sonrası yayımlanmış, hakemli dergilerde çıkmış Türkçe makaleler arıyorum." derseniz kütüphaneci tam aradığınızı bulur.

**Basit açıklama:** Prompt mühendisliği, yapay zekâdan istediğimiz sonucu almak için talimatlarımızı bilinçli şekilde tasarlama becerisidir. "Mühendislik" kelimesi korkutmasın; burada kastedilen kod yazmak değil, **düşünerek, deneyerek ve iyileştirerek** istek yazmaktır.

**Teknik tanım:** Prompt mühendisliği (prompt engineering), bir dil modelinin çıktısının doğruluğunu, biçimini, tonunu ve faydasını artırmak için girdinin (promptun) yapısını, içeriğini ve sırasını sistematik olarak tasarlama ve test etme sürecidir.

#### Neden Öğreniyoruz?

| Alan | Prompt mühendisliği ne kazandırır? | Akademik örnek |
|---|---|---|
| Literatür taraması | Kaynakları düzenli ve karşılaştırılabilir özetlemek | 20 makaleyi aynı tabloya özetletmek |
| Akademik yazım | Dil, akış ve tutarlılık kontrolü | Tez bölümündeki tekrarları ve belirsiz ifadeleri bulmak |
| Akademik iletişim | Aynı bulguyu farklı kitlelere anlatmak | Bildiri özeti, poster metni, kamuoyu için blog yazısı |
| Görsel üretim | Sunum ve posterler için şematik görseller | Bir plan tipini anlatan diyagram |

**Soru:** Aynı yapay zekâyı kullanan iki araştırmacıdan biri harika, diğeri vasat sonuç alıyorsa fark nereden gelir?

**Cevap:** Büyük ölçüde promptlarından. Araç aynı, kullanım becerisi farklı. Tıpkı aynı veri tabanında arama yapan iki araştırmacıdan birinin doğru anahtar kelimelerle çok daha iyi sonuç bulması gibi.

#### Temel Kavramlar: İletişimin Püf Noktaları

**1. Açıklık**

- Basit açıklama: Ne istediğinizi belirsizlik bırakmadan söyleyin.
- Neden? Model belirsizliği tahminle doldurur.
- Örnek: "Bunu düzelt." yerine "Bu paragraftaki yazım hatalarını düzelt, cümle yapısını ve terimleri değiştirme."

**2. Bağlam vermek**

- Basit açıklama: Modele durumunuzu anlatın.
- Neden? Model sizi tanımaz; her sohbet onun için yeni bir başlangıçtır.
- Örnek: "Kentsel dönüşüm alanlarında mahalle ilişkileri üzerine bir yüksek lisans tezi yazıyorum. Şu an literatür bölümündeyim."

**3. Hedef okuru belirtmek**

- Basit açıklama: Metni kimin okuyacağını söyleyin.
- Neden? Aynı bulgu bir hakeme, bir jüriye ve alan dışından bir okura farklı anlatılır.
- Örnek: "Mimarlık dışından sosyal bilimcilerin okuyacağı disiplinlerarası bir dergi için."

**4. Çıktı biçimini belirtmek**

- Basit açıklama: Cevabın şeklini söyleyin: tablo, madde listesi, paragraf, kaç kelime.
- Neden? Sonucu doğrudan kullanılabilir hâle getirir.
- Örnek: "Cevabı 3 sütunlu bir tablo olarak ver: Kavram – Tanım – Hangi yaklaşımda kullanılır?"

**5. Diyalog kurmak (yinelemek)**

- Basit açıklama: İlk cevabı son cevap saymayın; düzeltme isteyin.
- Neden? İlk taslak nasıl son metin değilse, ilk cevap da son cevap değildir.
- Örnek: "Güzel ama gereğinden kesin bir dil kullanmışsın; daha temkinli akademik ifadelerle yeniden yaz."

> **Dikkat:** Yapay zekâya kibar olmak zorunda değilsiniz ama **net** olmak zorundasınız. "Lütfen" kelimesi sonucu bozmaz; ancak eksik bilgiyi de tamamlamaz.

#### Basit Örnek

| Zayıf istek | Güçlü istek |
|---|---|
| "Cumba hakkında yaz." | "Osmanlı kent dokusu üzerine bir makalenin 'sokak ve konut ilişkisi' alt başlığı için, cumbanın konut ile sokak arasındaki ilişkiyi nasıl kurduğunu anlatan 150 kelimelik bir paragraf yaz. Akademik ve temkinli bir dil kullan. Kesin tarih ve isim verme." |

**Soru:** Güçlü istekte kaç farklı bilgi var? Sayalım.

**Cevap:** Kullanım yeri (makalenin alt başlığı), konu (cumbanın sokak–konut ilişkisindeki rolü), uzunluk (150 kelime), ton (akademik, temkinli), sınır (kesin tarih ve isim verme). Beş bilgi.

---

### Konu 3: İyi ve Kötü Promptlar, Açık ve Kapsamlı Prompt Tasarlama, Hedefe Yönelik Stratejiler ve Yönlendirmeler (45 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir anket şirketine "Biraz insanlara soru sorun." demek ile örneklemi, soru formunu ve teslim tarihini içeren bir iş tanımı vermek arasındaki fark... İlki yoruma açıktır, ikincisi uygulanabilirdir.

**Basit açıklama:** İyi prompt; modelin tahmin etmesi gereken şeyleri azaltan, ne istendiğini, kimin için istendiğini ve nasıl bir sonuç beklendiğini söyleyen prompttur.

#### İyi Bir Promptun 6 Kontrol Sorusu

Bir prompt yazdıktan sonra kendinize şunları sorun:

1. **Ne?** Ne istediğimi açıkça söyledim mi? (görev)
2. **Neden?** Bunu ne için istediğimi belirttim mi? (amaç)
3. **Kim için?** Hedef okuru söyledim mi? (kitle)
4. **Ne bilgiyle?** Gerekli arka plan bilgisini verdim mi? (bağlam)
5. **Nasıl?** Biçimi, uzunluğu, tonu belirttim mi? (çıktı biçimi)
6. **Ne olmasın?** Kaçınılması gerekenleri söyledim mi? (sınırlar)

#### İyi ve Kötü Prompt Örnekleri

**Örnek 1 – Literatür taraması**

Kötü:

```text
Türk evi hakkında kaynak ver.
```

Neden kötü? Hangi açıdan, hangi dilde, hangi dönem, kaç kaynak? Daha da önemlisi: model, **var olmayan kaynaklar uydurabilir** (bunu Konu 4'te göreceğiz).

İyi:

```text
Geleneksel Türk evinin mekân organizasyonu üzerine bir literatür taraması yapmaya hazırlanıyorum.
Bana kaynak listesi verme; bunun yerine Google Scholar, DergiPark ve kütüphane kataloglarında
arama yaparken kullanabileceğim 10 Türkçe ve 10 İngilizce anahtar kelime / anahtar kelime grubu öner.
Her birinin yanına hangi alt konuyu yakalamaya yaradığını tek cümleyle yaz.
Tablo biçiminde ver.
```

Neden iyi? Görev net, amaç belli, model uydurma riskinin yüksek olduğu işi (kaynak listelemek) yapmıyor, onun yerine güçlü olduğu işi (anahtar kelime üretmek) yapıyor, biçim tanımlı.

**Örnek 2 – Akademik metin düzeltme**

Kötü:

```text
Bu paragrafı daha iyi yap: [paragraf]
```

İyi:

```text
Aşağıdaki paragraf, mimarlık alanında hakemli bir dergiye gönderilecek bir makalenin
literatür bölümünden alınmıştır. Lütfen:
- Yazım ve noktalama hatalarını düzelt,
- 30 kelimeden uzun cümleleri ikiye böl,
- Gereğinden kesin ifadeleri ("kanıtlamaktadır" gibi) temkinli ifadelerle değiştir,
- Atıfları (parantez içindeki yazar–yıl bilgilerini) olduğu gibi koru,
- Anlamı ve terimleri değiştirme.
Sonra yaptığın değişiklikleri madde madde listele.

Paragraf:
[paragraf]
```

**Örnek 3 – Makale başlığı**

Kötü:

```text
Makaleme başlık bul.
```

İyi:

```text
1950–1980 arasında İstanbul'daki orta sınıf apartman dairelerinde salonun bir temsil mekânına
dönüşmesini dönem konut dergileri üzerinden inceleyen bir makale yazıyorum.
Bana 8 makale başlığı öner. 4 tanesi "Ana başlık: Alt başlık" biçiminde olsun,
4 tanesi tek parça ve açıklayıcı olsun. Her biri en fazla 15 kelime olsun.
"Bir inceleme", "Üzerine bir çalışma" gibi kalıp ifadelerden kaçın.
```

#### Açık ve Kapsamlı Prompt Tasarlama

**Açık prompt:** Tek bir yoruma izin veren prompttur.

**Kapsamlı prompt:** Modelin işi iyi yapması için gereken bütün bilgiyi içeren prompttur.

> **Dikkat:** Kapsamlı olmak uzun ve dağınık olmak demek değildir. Bir araştırma önerisi de uzundur ama düzenlidir. Bilgileri başlıklar veya maddeler hâlinde vermek, modelin de sizin de okumasını kolaylaştırır.

Kapsamlı ama düzenli prompt şablonu:

```text
BAĞLAM: [Durumum ne?]
GÖREV: [Ne yapmanı istiyorum?]
HEDEF OKUR: [Kim okuyacak?]
BİÇİM: [Tablo / paragraf / madde, uzunluk]
TON: [Akademik / anlaşılır / tarafsız]
SINIRLAR: [Ne yapmamalı?]
```

Bu şablonu Ders 2'de "bağlam + rol + görev + çıktı biçimi" yapısı olarak ayrıntılandıracağız.

#### Hedefe Yönelik Prompt Stratejileri

Her hedefin kendine uygun bir stratejisi vardır.

| Hedef | Strateji | Örnek ifade |
|---|---|---|
| Bir kavramı anlamak | Seviyeli açıklama istemek | "Önce 1 cümleyle, sonra 1 paragrafla, sonra ayrıntılı açıkla." |
| Fikir üretmek | Çok sayıda seçenek istemek | "Bu konu için 15 farklı araştırma sorusu öner, birbirine benzemesinler." |
| Karar vermek | Karşılaştırma tablosu istemek | "İki yöntemi (anket ve derinlemesine görüşme) avantaj/dezavantaj tablosunda karşılaştır." |
| Metni iyileştirmek | Kurallar listesi vermek | "Şu 4 kurala göre düzelt..." |
| Eksikleri bulmak | Eleştirmen gibi davranmasını istemek | "Bu araştırma önerisindeki 3 zayıf noktayı söyle." |
| Kendi düşüncemi netleştirmek | Soru sordurmak | "Araştırma sorumu netleştirmem için bana 5 soru sor, cevapladıktan sonra soruyu yeniden yaz." |

Son strateji çok güçlüdür: Modelin size soru sormasını istemek, tıpkı danışmanın öğrencisine soru sorması gibi, eksik bilgiyi ortaya çıkarır.

#### Prompt Yönlendirmeleri

Yönlendirme, modelin cevabını belli bir yöne çeken küçük ifadelerdir.

| Yönlendirme | Ne işe yarar? | Örnek |
|---|---|---|
| Uzunluk | Cevabın boyunu kontrol eder | "En fazla 250 kelime." |
| Biçim | Cevabın şeklini belirler | "Numaralı liste olarak." |
| Bakış açısı | Hangi açıdan bakılacağını söyler | "Yöntem açısından değerlendir." |
| Örnek verme | Beklenen kaliteyi gösterir | "Şu örnek gibi yaz: ..." |
| Olumsuz yönlendirme | Kaçınılacak şeyi söyler | "Klişe ifadeler kullanma." |
| Belirsizlik izni | Uydurmayı azaltır | "Emin değilsen 'emin değilim' de." |

> **Dikkat:** "Belirsizlik izni" çok önemlidir. Model, bilmediği bir şeyi bilmediğini söyleme izni olduğunu açıkça duyduğunda uydurma eğilimi azalır (ama tamamen ortadan kalkmaz).

#### Birlikte Uygulayalım: Konudan Araştırma Sorusuna

**Amaç:** Belirsiz bir konuyu, yapay zekâ ile diyalog kurarak net bir araştırma sorusuna dönüştürmek.

**Senaryo:** "Apartman dairesinde salon" konusunda bir makale yazmak isteniyor ama konu çok geniş.

**Adımlar:**

1. Yeni bir sohbet açın (önceki sohbetin etkilememesi için).
2. Şu promptu yazın:

```text
Mimarlık tarihi alanında hakemli bir dergi için makale yazmak istiyorum.
Konum: apartman dairesindeki "salon" mekânı. Ama konu çok geniş.
Araştırma sorumu netleştirmem için bana tek tek 5 soru sor.
Sorularını sor ve cevaplarımı bekle; henüz araştırma sorusu yazma.
```

3. **Tahmin sorusu:** "Sizce model hangi soruları soracak?" (Olası cevaplar: dönem, şehir, sosyal sınıf, kaynak türü, kuramsal çerçeve.)
4. Modelin sorularını okuyun.
5. Soruları birlikte cevaplayın. Örnek cevaplar:

```text
1. 1950–1980 arası dönem.
2. İstanbul ve Ankara.
3. Orta sınıf aileler.
4. Mimari planlar ve dönemin konut dergilerindeki ev ilanları üzerinden.
5. Salonun "misafir odası" olarak ayrılmasının gündelik hayata etkisi beni ilgilendiriyor.
```

6. Ardından yazın:

```text
Şimdi bu cevaplara göre bana 3 farklı araştırma sorusu öner.
Her birinin altına bu soruyu cevaplamak için hangi tür kaynaklara ve hangi yönteme
ihtiyaç duyulacağını yaz.
```

7. Gelen üç sorudan en beğendiğinizi "Prompt Defterim" dosyasına kaydedin.

**Beklenen sonuç:** Örneğin "1950–1980 döneminde İstanbul ve Ankara'daki orta sınıf apartman dairelerinde salonun misafire ayrılmış bir temsil mekânına dönüşmesi, ailenin gündelik yaşam düzenini nasıl etkilemiştir?" gibi daraltılmış bir soru.

**Açıklama:** Model önce bizim düşüncemizi açığa çıkardı, sonra bu bilgiyle çalıştı. Bu yöntem, danışmanla yapılan ilk görüşmeye çok benzer.

#### Gerçek Hayat Senaryosu: Makale Okuma Yükü

**Senaryo:** Bir literatür taraması için 15 makale indirildi ama hepsini ayrıntılı okumaya vakit yok. Hangilerinin önce okunacağına karar verilmesi gerekiyor.

**Problem nedir?** Makalelerin hangisinin araştırma sorusuna en yakın olduğunu hızlıca anlamak.

**Nasıl çözeceğiz?** Her makalenin özetini (abstract) yapay zekâya verip, belirlediğimiz kriterlere göre değerlendirmesini isteyeceğiz.

**Hangi bilgileri kullanacağız?** Makale özetleri, araştırma sorusu, öncelik kriterlerimiz.

**Adım adım çözüm:**

1. Bir makalenin özetini (dergi sayfasından veya PDF'in ilk sayfasından) kopyalayın.
2. Şu promptu yazın:

```text
Araştırma sorum: 1950–1980 döneminde orta sınıf apartman dairelerinde salonun temsil mekânına
dönüşmesi gündelik hayatı nasıl etkilemiştir?
Aşağıdaki makale özetini oku ve şu tabloyu doldur:

| Ölçüt | Değerlendirme |
| Ana konu (1 cümle) | |
| Araştırma sorumla ilgisi (Yüksek / Orta / Düşük) | |
| Neden bu düzeyde? (1 cümle) | |
| Yöntemi (özette belirtildiyse) | |

Sadece özette yazanlara dayan; özette olmayan bilgi ekleme.

Özet:
[buraya makale özetini yapıştır]
```

3. Aynı promptu diğer özetler için de kullanın (sadece özeti değiştirerek).
4. Sonuçları bir tabloda toplayın ve "Yüksek" ilgili olanlardan okumaya başlayın.

> **Dikkat:** "Sadece özette yazanlara dayan" ifadesi, modelin makale hakkında kendi tahminini eklemesini sınırlar. Yine de son karar sizindir; değerlendirme bir **ön eleme** aracıdır, makaleyi okumanın yerini tutmaz.

#### Sıra Sizde 1 (15 dk)

**Amaç:** Kötü bir promptu iyi bir prompta dönüştürme becerisini pekiştirmek.

**Görev:** Aşağıdaki üç kötü promptu, 6 kontrol sorusunu kullanarak yeniden yazın ve yapay zekâda deneyin.

1. `Selimiye hakkında bilgi ver.`
2. `Bu metni özetle.`
3. `Makalem için giriş yaz.`

**İstenenler:**

- Her prompt için en az 4 kontrol sorusunu cevaplayan yeni bir sürüm yazın.
- Her iki sürümü de yapay zekâda deneyin.
- Sonuçlar arasındaki farkı 2 cümleyle not edin.

**Beklenen sonuç:** Yeni promptların cevapları daha odaklı, uzunluğu kontrollü ve hedef okura uygun olmalı.

**İpucu:** "Ne, neden, kim için, nasıl" sorularını tek tek sorun ve her birine bir cümle ekleyin.

#### Çözüm

1. Selimiye için:

```text
Bir konferans sunumunda Selimiye Camii'nin iç mekân kurgusunu anlatacağım. Dinleyiciler
mimarlık dışından sosyal bilimciler. Kubbe, ışık ve mekânın bütünlüğü üzerine 120 kelimelik,
anlaşılır bir sunum metni yaz. Kesin ölçü ve tarih verme; gerekiyorsa [DOĞRULANMALI] yaz.
Abartılı övgü sıfatlarından ("muhteşem", "eşsiz") kaçın.
```

2. Özet için:

```text
Aşağıdaki metin, bir mimarlık tarihi makalesinin giriş bölümüdür.
Yazarın ana iddiasını 1 cümleyle, kullandığı 3 temel kanıtı madde madde yaz.
Toplam 100 kelimeyi geçme. Metinde olmayan bilgi ekleme.

Metin:
[metin]
```

3. Giriş için:

```text
Kentsel dönüşüm alanlarında komşuluk ilişkilerinin değişimini inceleyen bir makalenin
giriş bölümü için ilk paragrafı yaz. Paragraf şu sırayı izlesin:
1. Konunun önemi (genel bağlam),
2. Literatürdeki boşluk,
3. Bu çalışmanın sorusu.
Akademik ve temkinli bir dil kullan, 150 kelimeyi geçme.
Hiçbir yazar adı, yıl veya istatistik uydurma; atıf gereken yerlere [ATIF] yaz.
```

#### Sık Yapılan Hatalar

**Hata 1: Tek kelimelik veya çok kısa prompt**

Hatalı:

```text
Eyvan
```

Doğru:

```text
Anadolu mimarisinde "eyvan" ne demektir? 3 cümleyle akademik bir tanım ver ve hangi yapı türlerinde görüldüğünü belirt.
```

Neden hata? Model ne istediğinizi bilemez; tanım mı, tarihçe mi, görsel mi?

**Hata 2: Birden fazla işi tek cümlede karıştırmak**

Hatalı: "Bu metni özetle, düzelt, İngilizceye çevir ve başlık bul."

Doğru: İşleri numaralandırın veya ayrı mesajlarda isteyin:

```text
Aşağıdaki metin için sırasıyla:
1. Yazım hatalarını düzelt.
2. Düzeltilmiş metni 3 cümleyle özetle.
3. Özeti İngilizceye çevir.
4. 3 başlık öner.
Her adımın sonucunu ayrı başlık altında ver.
```

**Hata 3: İlk cevabı son cevap saymak**

Neden hata? İlk cevap bir taslaktır. Düzeltme istemek zaman kaybı değil, sürecin parçasıdır.

Düzeltme: "Bu cevabı şu açıdan iyileştir: ..." diyerek devam edin.

**Hata 4: Olumsuz talimatı tek başına vermek**

Hatalı: "Dağınık yazma."

Doğru: "Her paragraf tek bir iddiayla başlasın, ardından kanıt ve kısa bir yorum gelsin."

Neden? "Dağınık yazma" belirsizdir; modelin ne yapması gerektiğini söylemek daha etkilidir.

---

### Konu 4: Dil Modeli Limitlerini ve Kapasitesini Anlama (25 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Çok bilgili ama her soruya mutlaka cevap vermek isteyen bir arkadaşınız olduğunu düşünün. Bildiği konularda harika anlatır. Bilmediği konularda ise "bilmiyorum" demek yerine kendinden emin bir şekilde uydurur. Bu arkadaşınızı seversiniz ama söylediklerini önemli konularda kontrol edersiniz.

**Basit açıklama:** Dil modelleri çok güçlüdür ama sınırları vardır. Bu sınırları bilmek, özellikle akademik çalışmalarda hayati önem taşır.

#### Neden Öğreniyoruz?

Akademik bir metinde yanlış bir tarih, uydurma bir kaynak veya yanlış atfedilmiş bir alıntı; araştırmacının güvenilirliğine ciddi zarar verir ve akademik etik ihlali sayılabilir. Yapay zekânın nerede hata yaptığını bilen araştırmacı, onu güvenle kullanabilir.

#### Temel Kavramlar

**Kavram: Halüsinasyon (uydurma)**

- Basit açıklama: Modelin, doğru olmayan bilgiyi kendinden emin bir dille üretmesi.
- Neden olur? Model "doğru olanı" değil "olası görüneni" üretir. Var olmayan bir makale adı, gerçek makale adlarına çok benzediği için olası görünebilir.
- Örnek: "Ayşe Yılmaz (2014), *Anadolu Evlerinde Sofa Tipolojisi*, METU JFA, 31(2)" gibi tamamen uydurma ama gerçekçi görünen bir kaynak.

> **Dikkat:** Akademik çalışmada en sık ve en tehlikeli hata budur. Yapay zekânın verdiği **her kaynağı** Google Scholar, DergiPark, YÖK Tez Merkezi, kütüphane kataloğu veya derginin kendi sitesinden kontrol edin. Bulamadığınız kaynağı asla kullanmayın.

**Kavram: Token**

- Basit açıklama: Modelin metni okurken kullandığı küçük parçalar. Bir kelime bir veya birkaç token olabilir.
- Neden önemli? Modelin bir seferde işleyebileceği metin miktarı ve kullanım ücretleri token ile ölçülür.
- Örnek: "mimarlık" kelimesi model tarafından "mim", "ar", "lık" gibi parçalara bölünebilir. Türkçe gibi eklemeli dillerde kelime başına token sayısı genelde İngilizceden fazladır.

**Kavram: Bağlam penceresi (context window)**

- Basit açıklama: Modelin bir sohbette aynı anda "aklında tutabildiği" metin miktarı.
- Benzetme: Çalışma masanızın büyüklüğü gibi. Masa ne kadar büyükse o kadar çok makaleyi aynı anda açıp bakabilirsiniz. Masa dolunca en eski makaleler masadan düşer.
- Örnek: Çok uzun bir sohbette model, en başta verdiğiniz talimatları unutmaya başlayabilir. Çözüm: önemli talimatları tekrar hatırlatmak veya yeni sohbet açmak.

**Kavram: Bilgi kesim tarihi**

- Model, eğitimi bittikten sonraki gelişmeleri bilmez. Bazı araçlarda "web araması" özelliği bu açığı kapatır.
- Örnek: Bu yıl yayımlanmış bir makaleyi model bilmeyebilir.

**Kavram: Tutarsızlık**

- Aynı soruya iki farklı zamanda farklı cevap gelebilir. Model her seferinde cevabı yeniden üretir.

#### Modelin Güçlü ve Zayıf Olduğu İşler

| Güçlü olduğu işler | Dikkat gerektiren işler |
|---|---|
| Verdiğiniz metni özetlemek | Kaynak, künye, sayfa numarası, DOI vermek |
| Metni farklı tona çevirmek | Kesin tarih, ölçü, istatistik vermek |
| Fikir ve araştırma sorusu üretmek | Az bilinen yerel yapılar ve arşivler hakkında bilgi |
| Yapı ve plan önermek | Doğrudan alıntı ("X şöyle demiştir") |
| Kavramları karşılaştırmak | Güncel yayınlar ve olaylar |
| Yazım ve dil düzeltmek | Etik, hukuki ve telif konularında kesin hüküm |

**Altın kural:** Modele **bilgi ürettirmek** yerine, **sizin verdiğiniz bilgiyi işletmek** daha güvenlidir. Makaleyi siz bulun, model özetlesin.

> **Dikkat – Akademik etik:** Üniversitelerin ve dergilerin büyük kısmı artık yapay zekâ kullanımına ilişkin kurallar yayımlamaktadır. Genel ilke şudur: Yapay zekâ yazar olarak gösterilmez, kullanıldığı yerler (dil düzeltme, özetleme vb.) yöntem veya teşekkür bölümünde belirtilir ve metnin bütün sorumluluğu araştırmacıdadır. Çalıştığınız kurumun ve göndereceğiniz derginin güncel kurallarını mutlaka okuyun.

#### Basit Örnek: Uydurma Kaynağı Yakalamak

**Tahmin sorusu:** Sizce yapay zekâya "Türk evinde sofa üzerine 5 akademik makale listele" dersek, verdiği makalelerin hepsi gerçek olur mu?

**Cevap:** Olmayabilir. Bazıları gerçek, bazıları yarı doğru (yazar gerçek, başlık yanlış), bazıları tamamen uydurma olabilir. Bunu birlikte test edeceğiz.

#### Birlikte Uygulayalım: Kaynak Doğrulama Testi

**Amaç:** Modelin uydurma kaynak üretme riskini kendi gözümüzle görmek ve doğrulama alışkanlığı kazanmak.

**Senaryo:** Bir literatür taraması için kaynak arıyoruz.

**Adımlar:**

1. Yeni bir sohbet açın. (Mümkünse web araması özelliğini **kapalı** tutun; testin amacı modelin kendi hafızasını görmek.)
2. Şu promptu yazın:

```text
Geleneksel Türk evinde sofa mekânı üzerine yazılmış 5 akademik makale listele.
Her biri için yazar, yıl, başlık, dergi adı ver.
```

3. Gelen listeyi kopyalayıp "Prompt Defterim" dosyasına yapıştırın.
4. Her makalenin başlığını tırnak içinde Google Scholar'da (scholar.google.com) arayın.
5. Bulamazsanız DergiPark'ta (dergipark.org.tr) arayın.
6. Her kaynak için şu tabloyu doldurun:

| Kaynak | Bulundu mu? | Bilgiler doğru mu? |
|---|---|---|
| 1 | Evet / Hayır | Yazar, yıl, dergi doğru mu? |

7. Şimdi aynı sohbete şunu yazın:

```text
Verdiğin kaynakların hangilerinden emin olmadığını belirt.
Emin olmadığın bilgiyi uydurmak yerine "emin değilim" demeni istiyorum.
```

8. Modelin cevabını inceleyin.

**Beklenen sonuç:** Listedeki kaynakların bir kısmı bulunamayabilir veya künyeleri hatalı olabilir. Model ikinci promptta bazı kaynaklardan emin olmadığını kabul edebilir.

**Açıklama:** Model gerçek kaynaklara "benzeyen" metinler üretiyor. Bu yüzden kaynak listesi için **web araması yapan araçlar** veya doğrudan akademik veri tabanları kullanılmalı; yapay zekâ ise bulunan kaynakları **özetleme ve düzenleme** için kullanılmalıdır.

> **Dikkat:** Web araması yapan araçlarda (ChatGPT'de arama, Perplexity, Claude'da web araması gibi) kaynaklar genellikle bağlantıyla birlikte gelir. Bu daha güvenlidir ama yine de bağlantıya tıklayıp **kaynağın gerçekten o bilgiyi içerdiğini** kontrol etmek gerekir.

#### Sıra Sizde 2 (10 dk)

**Amaç:** Modelin sınırlarını tanıyıp güvenli prompt yazmak.

**Görev:** Aşağıdaki riskli promptları, modelin güçlü olduğu işe yönlendirecek şekilde yeniden yazın.

1. `Sedad Hakkı Eldem'in Türk evi hakkında söylediği ünlü bir sözü alıntıla.`
2. `Safranbolu evlerinin ortalama tavan yüksekliği kaç santimetredir?`
3. `Bu konuda bana 10 kaynak ver.`

**İstenenler:** Her prompt için daha güvenli bir sürüm ve bunun neden daha güvenli olduğunu açıklayan bir cümle.

**İpucu:** Bilgiyi modelden istemek yerine, bilgiyi nerede bulacağınızı veya kendi bulduğunuz bilgiyi nasıl işleyeceğinizi sorun.

#### Çözüm

1. Doğrudan alıntı uydurulabilir. Güvenli sürüm:

```text
Sedad Hakkı Eldem'in Türk evi çalışmalarındaki temel fikirleri genel hatlarıyla özetle.
Doğrudan alıntı verme. Bu fikirleri birincil kaynaklardan doğrulamak için
hangi eser türlerine ve arşivlere bakmam gerektiğini öner.
```

Neden güvenli? Alıntı uydurma riski kaldırıldı; doğrulama yolu istendi.

2. Kesin sayısal veri uydurulabilir. Güvenli sürüm:

```text
Safranbolu evlerinin kat yükseklikleri hakkında güvenilir ölçüm verisini
hangi tür kaynaklarda (rölöve çalışmaları, tezler, koruma raporları) bulabilirim?
YÖK Tez Merkezi ve DergiPark'ta arama yapmak için anahtar kelimeler öner.
```

3. Güvenli sürüm:

```text
Bu konuda literatür taraması yapmak için Google Scholar ve DergiPark'ta
kullanabileceğim arama stratejisi öner: anahtar kelimeler, eş anlamlılar,
İngilizce karşılıklar ve VE/VEYA kullanımıyla örnek arama ifadeleri.
```

#### Sık Yapılan Hatalar

**Hata 1: Kaynak listesine körü körüne güvenmek**

- Neden hata? Uydurma kaynaklar gerçekçi görünür.
- Düzeltme: Her kaynağı bağımsız olarak doğrulayın.

**Hata 2: Çok uzun sohbette ilk talimatların hâlâ geçerli olduğunu varsaymak**

- Neden hata? Bağlam penceresi dolduğunda eski talimatlar etkisini kaybeder.
- Düzeltme: Uzun çalışmalarda önemli kuralları ara ara tekrar yazın veya yeni bir sohbet açıp özetle devam edin.

**Hata 3: Modelin "kendinden emin" dilini doğruluk işareti saymak**

- Neden hata? Model yanlış bilgiyi de aynı güvenle yazar.
- Düzeltme: Ton değil, kaynak ve doğrulama belirleyicidir.

**Hata 4: Yayımlanmamış veriyi ve kişisel verileri düşünmeden paylaşmak**

- Neden hata? Henüz yayımlanmamış araştırma verileri, görüşme kayıtları veya katılımcı bilgileri, bazı araçlarda ayarlarınıza bağlı olarak model geliştirmede kullanılabilir; kişisel veriler ayrıca etik kurul ve yasal kurallara tabidir.
- Düzeltme: Kullandığınız aracın veri ve gizlilik ayarlarını kontrol edin; kişisel verileri anonimleştirin.

---

### Ders Özeti

Bu derste yapay zekâ ile çalışmanın temelini attık. Dil modellerinin "bağlama göre en olası devamı tahmin eden" sistemler olduğunu gördük. Bu yüzden ne kadar iyi bağlam verirsek o kadar iyi sonuç aldığımızı fark ettik. Promptun iyi tanımlanmış bir görev tanımı olduğunu; iyi bir promptun ne, neden, kim için, ne bilgiyle, nasıl ve ne olmasın sorularını cevapladığını öğrendik. Son olarak modelin en büyük zayıflığının, özellikle kaynak ve alıntı konusunda uydurma bilgi üretebilmesi olduğunu, akademik çalışmada her bilginin doğrulanması ve yapay zekâ kullanımının şeffaf biçimde belirtilmesi gerektiğini gördük.

### Bu Derste Neler Öğrendik?

- Yapay zekâ, makine öğrenmesi ve büyük dil modeli kavramlarının farkını öğrendik.
- Dil modelinin bir sonraki kelimeyi tahmin ederek çalıştığını gördük.
- Prompt mühendisliğinin, istekleri bilinçli tasarlama becerisi olduğunu öğrendik.
- İyi bir promptun 6 kontrol sorusunu öğrendik.
- Kötü promptları iyi promptlara dönüştürdük.
- Hedefe göre farklı stratejiler (seçenek istemek, karşılaştırmak, soru sordurmak) kullandık.
- Yönlendirme ifadeleriyle (uzunluk, biçim, belirsizlik izni) cevabı şekillendirdik.
- Halüsinasyon, token, bağlam penceresi ve bilgi kesim tarihi kavramlarını öğrendik.
- Yapay zekânın verdiği kaynakları doğrulamayı ve akademik etik ilkelerini gördük.

### Mini Quiz

1. **(Çoktan seçmeli)** Büyük dil modeli temelde ne yapar?
   - a) İnternetteki doğru bilgiyi bulup getirir
   - b) Bağlama göre en olası devam metnini tahmin eder
   - c) İnsan gibi düşünüp anlar
   - d) Sadece önceden yazılmış cevapları gösterir
2. **(Doğru / Yanlış)** Yapay zekâ kendinden emin bir dille yazıyorsa bilgi doğrudur.
3. **(Kısa cevap)** Modelin var olmayan bir kaynağı gerçekmiş gibi üretmesine ne ad verilir?
4. **(Kısa cevap)** İyi bir promptun 6 kontrol sorusundan 4 tanesini yazınız.
5. **(Çoktan seçmeli)** Aşağıdakilerden hangisi yapay zekâ için daha güvenli bir görevdir?
   - a) "Bana 10 kaynak listele."
   - b) "Bu yapının tam inşa tarihini ver."
   - c) "Yapıştırdığım makale özetini 3 maddede özetle."
   - d) "Bu mimarın ünlü bir sözünü alıntıla."
6. **(Doğru / Yanlış)** Çok uzun bir sohbette model, başta verilen talimatları unutabilir.
7. **(Küçük problem)** Şu promptu iyileştiriniz: `Kerpiç hakkında yaz.`
8. **(Kısa cevap)** Akademik bir makalede yapay zekâ kullanıldıysa genel ilke olarak ne yapılmalıdır?

### Mini Quiz Cevapları

1. **b.** Model, bağlama göre en olası devamı tahmin eder. "Anlama" ve "doğruyu bulma" garantisi yoktur.
2. **Yanlış.** Model yanlış bilgiyi de aynı güvenle yazabilir.
3. **Halüsinasyon** (uydurma).
4. Ne? Neden? Kim için? Ne bilgiyle? Nasıl? Ne olmasın? (herhangi dördü)
5. **c.** Verilen metni özetlemek modelin güçlü olduğu, uydurma riskinin düşük olduğu bir iştir.
6. **Doğru.**
7. Örnek cevap: "Kırsal konutta yapım teknikleri üzerine bir makalenin literatür bölümü için, kerpicin Anadolu kırsal mimarisinde neden yaygın kullanıldığını iklim ve malzeme erişimi açısından tartışan 150 kelimelik akademik bir paragraf yaz. Atıf gereken yerlere [ATIF] yaz; kaynak uydurma."
8. Yapay zekâ yazar olarak gösterilmez; kullanıldığı yer ve amaç (örneğin dil düzeltme) belirtilir; içeriğin doğruluğundan araştırmacı sorumludur; kurumun ve derginin kurallarına uyulur.

### Ders Sonu Uygulaması

**Senaryo:** "Geleneksel konutta hayat ve sofa: ortak yaşam mekânları" konusunda bir makale planlanıyor. Bu ders sonu uygulamasında araştırma sorusu ve literatür taraması için ilk hazırlık yapılacak.

**Yapılacaklar:**

1. Konuyu netleştirmek için yapay zekâya size 5 soru sordurun ve cevaplayın.
2. Cevaplarınıza göre bir ana araştırma sorusu ve 3 alt soru yazdırın.
3. Google Scholar ve DergiPark'ta kullanılacak 10 anahtar kelimeyi tablo hâlinde aldırın.
4. Modelden kaynak listesi istemeyin; bunun yerine bir kaynağı kendiniz bulun, özetini kopyalayın ve Konu 3'teki tablo promptuyla değerlendirtin.
5. Kullandığınız en iyi 3 promptu "Prompt Defterim" dosyasına kaydedin.

**Beklenen sonuç:** Net bir araştırma sorusu, bir anahtar kelime tablosu, en az bir gerçek kaynağın değerlendirme tablosu ve 3 kayıtlı prompt.

**İpuçları:**

- Her promptta çalışmanın konusunu ve türünü (makale) bağlam olarak verin.
- "Sadece verdiğim metne dayan" ifadesini unutmayın.
- Model bir kaynak önerirse doğrulamadan kullanmayın.

### Ders Sonu Uygulaması – Çözüm

**Adım 1 promptu:**

```text
Mimarlık tarihi alanında hakemli bir dergi için makale hazırlıyorum.
Konu: geleneksel konutta "hayat" ve "sofa" mekânlarının ortak yaşamı nasıl örgütlediği.
Bu konunun odağını netleştirmem için bana tek tek 5 soru sor. Cevaplarımı bekle.
```

**Örnek cevaplar:**

```text
1. Odak 18. ve 19. yüzyıl Anadolu ve İstanbul konutları.
2. Hayat (yarı açık sofa) ile kapalı sofa arasındaki farkı vurgulamak istiyorum.
3. Mevsimlere göre kullanım değişikliği beni ilgilendiriyor.
4. Kadınların gündelik iş alanı olarak sofa önemli bir alt konu.
5. Kaynaklarım: rölöve çizimleri, seyahatnameler ve daha önce yapılmış sözlü tarih çalışmaları.
```

**Adım 2 promptu:**

```text
Bu cevaplara göre bir ana araştırma sorusu ve 3 alt soru yaz.
Her alt sorunun altına hangi kaynak türüyle cevaplanabileceğini yaz.
```

**Örnek sonuç:** "18. ve 19. yüzyıl Anadolu konutlarında hayat ve sofa, mevsimsel kullanım ve ev içi iş bölümü açısından ortak yaşamı nasıl örgütlemiştir?"

**Adım 3 promptu:**

```text
Bu araştırma sorusu için Google Scholar ve DergiPark'ta kullanacağım 5 Türkçe ve 5 İngilizce
anahtar kelime öner. Tablo olarak ver: Anahtar kelime | Dil | Hangi alt soruya yarar?
Kaynak listesi verme.
```

**Örnek tablo (modelden beklenen tür):**

| Anahtar kelime | Dil | Hangi alt soruya yarar? |
|---|---|---|
| "Türk evi" sofa tipolojisi | Türkçe | Mekân organizasyonu |
| hayatlı ev | Türkçe | Yarı açık mekân |
| geleneksel konut mevsimsel kullanım | Türkçe | Mevsimsel kullanım |
| konut ve toplumsal cinsiyet Osmanlı | Türkçe | Ev içi iş bölümü |
| sofa plan tipi | Türkçe | Plan tipleri |
| "Turkish house" sofa | İngilizce | Mekân organizasyonu |
| semi-open hall vernacular Anatolia | İngilizce | Yarı açık mekân |
| seasonal use vernacular dwelling | İngilizce | Mevsimsel kullanım |
| Ottoman domestic space gender | İngilizce | Ev içi iş bölümü |
| Anatolian vernacular house plan typology | İngilizce | Plan tipleri |

**Adım 4:** Konu 3'teki "makale özeti değerlendirme" promptu, bulunan gerçek bir makalenin özetiyle kullanılır (araştırma sorusu kısmı güncellenerek).

**Adım 5:** Prompt Defterim'e kaydedilecek üç prompt: soru sordurma promptu, anahtar kelime promptu, özet değerlendirme promptu. Bu üç prompt, her yeni araştırma konusu için yeniden kullanılabilir bir **literatür taraması başlangıç seti** oluşturur.

> **Sonraki derste:** Bugün iyi promptun hangi soruları cevaplaması gerektiğini gördük. Bir sonraki derste bu soruları düzenli bir yapıya oturtacağız: **bağlam + rol + görev + çıktı biçimi.** Bu yapıyla bir makale okuma notu şablonu hazırlayacak, akademik tonu kontrol edecek, metni hakem gözüyle değerlendirtecek ve yapay zekâya "adım adım düşünmeyi" öğreteceğiz.
