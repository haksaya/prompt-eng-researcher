# Prompt Mühendisliği Eğitimi – Ders 3

## İleri Prompt Teknikleri: Sistem Mesajları, Çoklu Deneme, Görsel Düzenleme ve Görsel–Metin Entegrasyonu (Yaklaşık 2,5 Saat)

---

## Ders 3 – 150 Dakika

### Önceki Dersle Bağlantı

Önceki derste promptlarımızı **bağlam + rol + görev + çıktı biçimi** yapısına oturttuk, akademik tonu ve formatı kontrol ettik, modele hakem ve yöntem uzmanı gibi roller verdik ve adım adım düşündürdük. Ama bir sorun fark ettik: Her yeni sohbette araştırma konumuzu, sorumuzu ve yazım kurallarımızı **yeniden** yazmak zorunda kaldık.

Bu derste bu tekrarı ortadan kaldıran **sistem mesajlarını ve kalıcı talimatları** öğreneceğiz ve kendi araştırma asistanımızı tanımlayacağız. Sonra tek bir cevapla yetinmeyip **birden fazla çıktı üretip karşılaştırmayı** göreceğiz. Dersin ikinci yarısında metinden görsele geçeceğiz: Yapay zekâ ile görsel düzenlemeyi, akademik çalışmalarda bunun etik sınırlarını ve bir araştırmayı kamuoyuna anlatan **akademik blog yazısını** uygun görseliyle birlikte hazırlamayı öğreneceğiz.

### Dersin Hedefleri

Bu dersin sonunda öğrenci:

- Sistem mesajı, kullanıcı mesajı ve özel talimat kavramlarını ayırt edebilecek.
- Bir tez veya araştırma için kalıcı bir talimat seti (proje talimatı) yazabilecek.
- Aynı görev için birden fazla çıktı üretip ölçütlere göre karşılaştırabilecek.
- Yapay zekâ ile bir görseli düzenleme (anonimleştirme, stil değiştirme, eskizden görsel) promptları yazabilecek.
- Akademik çalışmalarda görsel düzenlemenin etik sınırlarını bilecek.
- Bir akademik blog yazısını ve ona uygun görseli tutarlı şekilde üretebilecek.

### Süre Planı

| Bölüm | Süre |
|---|---|
| Giriş ve önceki dersin tekrarı | 10 dk |
| Konu 1: Sistem mesajları ve talimatlar | 35 dk |
| Konu 2: Çoklu deneme ve çıktı karşılaştırma | 30 dk |
| Konu 3: Yapay zekâ ile görsel düzenleme | 30 dk |
| Konu 4: Görsel ve metin entegrasyonu + Uygulama: Blog yazısı ve görseli | 35 dk |
| Ders özeti, mini quiz ve ders sonu uygulaması | 10 dk |
| **Toplam** | **150 dk** |

### Derse Hazırlık

- Görsel üretebilen ve düzenleyebilen bir araç açık olsun: ChatGPT (görsel üretimi GPT Image modeliyle yapılır), Gemini veya benzeri. Ücretsiz sürümlerde görsel sayısı sınırlı olabilir.
- Derse kendi çektiğiniz bir saha fotoğrafı (bir cephe, bir sokak veya bir iç mekân) ve elle çizilmiş basit bir eskizin fotoğrafını getirin.

---

### Giriş ve Tekrar (10 dk)

**Soru:** Prompt yapısının dört bileşeni nelerdir?

**Cevap:** Bağlam, rol, görev, çıktı biçimi.

**Soru:** Geçen ders araştırma konunuzu ve sorunuzu kaç kez yeniden yazdınız?

**Cevap:** Büyük ihtimalle "her promptta". Bu, bugünkü ilk konunun çıkış noktasıdır: **Tekrar eden bilgiyi bir kez yazıp kalıcı hâle getirmek.**

---

### Konu 1: Sistem Mesajları ve Talimatlar (35 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir enstitüye kayıt olan tez öğrencisine ilk gün bir **tez yazım kılavuzu** verilir: sayfa düzeni, başlık numaralandırma, atıf biçimi, kaynakça kuralları. Öğrenci bütün tez boyunca bu kuralları uygular. Her bölüm yazılırken yeniden anlatılmaz.

**Basit açıklama:** Sistem mesajı, yapay zekâya sohbetin başında **bir kez** verilen ve bütün sohbet boyunca geçerli olan temel talimatlardır. Sonraki mesajlarınız (kullanıcı mesajları) bu temel kuralların üzerine eklenir.

**Teknik tanım:** Dil modelleriyle yapılan konuşmalar farklı **rollere** sahip mesajlardan oluşur:

| Mesaj türü | Kim yazar? | Ne işe yarar? |
|---|---|---|
| Sistem mesajı (system / developer) | Uygulamayı kuran kişi veya kullanıcı (ayarlar üzerinden) | Modelin genel davranışını, kimliğini, kurallarını belirler |
| Kullanıcı mesajı (user) | Siz | O anki soru veya istek |
| Asistan mesajı (assistant) | Model | Modelin cevabı |

Sistem mesajı genellikle kullanıcı mesajından **daha yüksek öncelikli** kabul edilir ve bütün sohbet boyunca geçerlidir.

#### Sohbet Araçlarında Sistem Mesajına Karşılık Gelen Özellikler

Sohbet uygulamalarında sistem mesajını doğrudan yazamayız; ama aynı işi gören özellikler vardır:

| Özellik | Nerede? | Ne işe yarar? |
|---|---|---|
| Özel talimatlar / kişiselleştirme | ChatGPT ve Claude ayarları | Bütün sohbetlerde geçerli genel tercihler (dil, ton, uzunluk) |
| Projeler | ChatGPT Projects, Claude Projects | Belirli bir iş için talimatlar + dosyalar; o projedeki bütün sohbetlerde geçerli |
| Gem / özel asistan | Gemini Gems, ChatGPT'deki özel asistanlar | Belirli bir görev için kayıtlı, tekrar kullanılabilir asistan |
| API'de sistem mesajı | Ders 6'da göreceğiz | Kod ile yazılan uygulamalarda doğrudan `instructions` veya `system` alanı |

> **Dikkat:** Uygulamaların menü isimleri ve yerleri sık değişir. Bir özelliği bulamazsanız uygulamanın ayarlar menüsüne veya yardım sayfasına bakın. Önemli olan kavramdır: **Kalıcı talimat + o anki istek.**

#### Neden Öğreniyoruz?

- **Tez ve makale yazımında:** Araştırmanın konusu, sorusu, yöntemi, yazım kuralları ve terim sözlüğü bir kez tanımlanır; her çalışma oturumunda otomatik geçerli olur.
- **Akademik dürüstlükte:** "Kaynak uydurma" yasağı ve "emin değilsen işaretle" kuralı her sohbette geçerli olur.
- **Tutarlılık:** Aylar süren bir tez çalışmasında terimler ve üslup tutarlı kalır.
- **Zaman:** Her prompt kısalır.

#### Temel Kavramlar

**Kavram: Kimlik talimatı**

- Basit açıklama: Modelin kim olduğunu söyleyen kısım.
- Örnek: "Sen bu yüksek lisans tezinin araştırma ve akademik yazım asistanısın."

**Kavram: Kalıcı kurallar**

- Basit açıklama: Her cevapta uyulması gereken kurallar.
- Örnek: "Asla kaynak, künye veya doğrudan alıntı uydurma. Emin değilsen belirt."

**Kavram: Varsayılan biçim**

- Basit açıklama: Aksi söylenmedikçe kullanılacak format.
- Örnek: "Aksi istenmedikçe Türkçe ve en fazla 300 kelime ile cevap ver."

**Kavram: Bilgi tabanı**

- Basit açıklama: Projeye yüklenen ve modelin başvurabileceği dosyalar.
- Örnek: Tez önerisi, bölüm planı, terim sözlüğü, enstitünün tez yazım kılavuzu, okuma notları.

#### Basit Örnek

Sistem mesajı olmadan, her seferinde:

```text
Kentsel dönüşüm alanlarında komşuluk ilişkileri üzerine bir yüksek lisans tezi yazıyorum.
Akademik ve temkinli yaz. Kaynak uydurma. Şu paragrafı düzelt: ...
```

Sistem mesajı (proje talimatı) ile, bir kez:

```text
Sen kentsel dönüşüm alanlarında komşuluk ilişkileri üzerine yazılan bir yüksek lisans tezinin
akademik yazım asistanısın. Akademik ve temkinli yazarsın. Asla kaynak uydurmazsın.
```

Sonra her seferinde sadece:

```text
Şu paragrafı düzelt: ...
```

#### Birlikte Uygulayalım: Bir Araştırma İçin Kalıcı Talimat Yazmak

**Amaç:** Bir araştırma için tekrar kullanılabilir bir sistem talimatı yazmak ve bir proje/özel asistan içinde kullanmak.

**Senaryo:** Geleneksel konuttan apartmana geçişte mekân kullanımının dönüşümünü inceleyen bir araştırmanın bütün yazım ve okuma çalışmaları tek bir projede toplanacak.

**Adımlar:**

1. Bir metin dosyası açın ve adını `arastirma_proje_talimati.txt` koyun.
2. Aşağıdaki talimatı dosyaya yazın. Kendi araştırmanıza göre köşeli parantezli yerleri değiştirin.

```text
# KİMLİK
Sen [araştırmanın kısa adı] konulu araştırmanın araştırma ve akademik yazım asistanısın.
Araştırmacıyla birlikte çalışan titiz bir akademik editör ve araştırma asistanı gibi davranırsın.

# ARAŞTIRMA HAKKINDA
- Konu: Geleneksel Türk evinden 20. yüzyıl apartman dairesine geçişte mekân kullanımının dönüşümü.
- Araştırma sorusu: Ev mekânının değişimiyle gündelik hayat pratikleri nasıl değişti?
- Yöntem: Plan arşivleri ve dönem konut dergilerinin incelenmesi, sözlü tarih görüşmeleri.
- Çıktı türü: Hakemli dergi makalesi ve sempozyum bildirisi.

# KESİN KURALLAR
1. Asla kaynak, künye, sayfa numarası, DOI veya doğrudan alıntı uydurma.
2. Emin olmadığın tarih, isim veya sayı için "[DOĞRULANMALI]" etiketi koy.
3. Atıf gereken ama kaynağı verilmemiş iddialar için "[ATIF]" etiketi koy.
4. Araştırmacının metnini düzeltirken anlamı ve atıfları değiştirme; değişiklikleri listele.
5. Mimari terimleri, metin disiplinlerarası bir okura yönelikse ilk geçtiği yerde açıkla.

# YAZIM KURALLARI
- Yüzyıllar rakamla yazılır: 18. yüzyıl.
- Yabancı terimler italik yazılır.
- Cümleler mümkünse 25 kelimeyi geçmez.
- Birinci çoğul şahıs kullanılmaz; nesnel ve temkinli akademik dil kullanılır.
- Atıf biçimi: APA 7 (yazar, yıl).

# VARSAYILAN CEVAP BİÇİMİ
- Dil: Türkçe.
- Aksi istenmedikçe en fazla 300 kelime.
- Bir görev belirsizse, cevap vermeden önce en fazla 3 netleştirici soru sor.
```

3. Kullandığınız araçta proje veya özel asistan oluşturun:
   - **ChatGPT:** Sol menüden yeni bir proje oluşturun, proje ayarlarında talimatlar (instructions) alanına bu metni yapıştırın.
   - **Claude:** Projects bölümünden yeni proje oluşturun, proje talimatları alanına yapıştırın.
   - **Gemini:** Yeni bir Gem oluşturun ve talimat alanına yapıştırın.
4. Varsa projeye araştırma önerinizi veya bölüm planınızı içeren bir dosya yükleyin.
5. Projenin içinde yeni bir sohbet açın ve yalnızca şunu yazın:

```text
Şu paragrafı düzelt:
Onsekizinci yüzyılda inşa edilen bu evlerde hayat, ailenin bütün gününü geçirdiği bir mekandı ve biz bu evlerin en önemli özelliğinin 1785 yılında yapılan ilk örneklerinde görülen ahşap direklerle çevrili olması olduğunu görüyoruz.
```

6. **Tahmin sorusu:** Model talimattaki hangi kuralları uygulayacak?
7. Cevabı inceleyin.

**Beklenen sonuç:**

- "Onsekizinci yüzyıl" → "18. yüzyıl" düzeltilmesi,
- "biz ... görüyoruz" ifadesinin nesnel bir yapıya çevrilmesi,
- "1785 yılında yapılan ilk örnekler" ifadesine "[DOĞRULANMALI]" etiketi konması,
- Kaynağı verilmemiş iddiaya "[ATIF]" etiketi konması,
- Uzun cümlenin bölünmesi,
- Değişikliklerin listelenmesi.

**Açıklama:** Biz yalnızca "düzelt" dedik; diğer bütün kuralları sistem talimatı sağladı. "1785" gibi spesifik ve kaynaksız bir tarihin işaretlenmesi, Ders 1'de öğrendiğimiz uydurma riskine karşı kalıcı bir güvenlik önlemidir.

#### Gerçek Hayat Senaryosu: Terim Tutarlılığı

**Senaryo:** Bir tezin farklı bölümlerinde aynı mekân için farklı kelimeler kullanılmış: "sofa", "hol", "orta salon", "divanhane".

**Problem nedir?** Okur (ve jüri) bunların aynı mekân mı, farklı mekânlar mı olduğunu anlayamaz; bu, kavramsal tutarsızlık olarak eleştirilir.

**Nasıl çözeceğiz?** Proje talimatına bir **terimler sözlüğü** ekleyeceğiz.

**Hangi bilgileri kullanacağız?** Araştırmacının kavramsal çerçevede yaptığı terim tercihleri.

**Adımlar:**

1. Proje talimatının sonuna şu bölümü ekleyin:

```text
# TERİMLER SÖZLÜĞÜ (bu terimleri tutarlı kullan)
- sofa: Geleneksel evde odaların açıldığı ortak alan. "Hol" kelimesini yalnızca apartman dairesi için kullan.
- hayat: Bir yanı açık, sofa işlevli yarı açık mekân. "Balkon" ile karıştırma.
- salon: Apartman dairesindeki temsil/misafir odası.
- divanhane: Sadece büyük konaklardaki baş oda için kullan; sofa yerine kullanma.
```

2. Kaydedin.
3. Proje içinde şu isteği yazın:

```text
Aşağıdaki iki paragrafı terimler sözlüğüne göre kontrol et. Tutarsız kullanımları tablo hâlinde göster:
Satır | Kullanılan terim | Olması gereken | Neden

[iki paragraf]
```

**Beklenen sonuç:** Terim tutarsızlıklarını gösteren bir tablo.

#### Sıra Sizde 1 (15 dk)

**Amaç:** Kendi ihtiyacına göre sistem talimatı yazmak.

**Görev:** Bir **literatür okuma asistanı** için ayrı bir proje talimatı yazın. Bu asistan, okuduğunuz makaleleri özetleyecek ve literatür tablosuna eklenecek satırlar üretecek.

**İstenenler:**

- Kimlik bölümü
- En az 3 kesin kural (biri uydurma yasağı olmalı)
- Varsayılan cevap biçimi (Ders 2'deki okuma notu yapısını kullanabilirsiniz)
- Projeyi oluşturup bir makale özetiyle test edin.

**Beklenen sonuç:** Sadece makale metnini yapıştırarak standart bir okuma notu ve tablo satırı alınabilen bir proje.

**İpucu:** Ders 2'deki okuma notu şablonunun "ROL" ve "ÇIKTI BİÇİMİ" kısımlarını talimata taşıyın; "GÖREV" kısmını kısa bırakın.

#### Çözüm

```text
# KİMLİK
Sen mimarlık tarihi ve konut çalışmaları alanında deneyimli bir araştırma asistanısın.
Görevin, araştırmacının yapıştırdığı akademik metinlerden standart okuma notları çıkarmak.

# KESİN KURALLAR
1. Yalnızca yapıştırılan metne dayan. Metinde olmayan bilgi ekleme.
2. Kaynak, künye, alıntı veya sayfa numarası uydurma.
3. Metinde bulunmayan alanlara "Metinde belirtilmemiş" yaz.
4. Yorumlarını bulgulardan ayır: Yorumlarını "Asistan yorumu:" ile başlat.

# VARSAYILAN CEVAP BİÇİMİ
Her metin için şu başlıklarla okuma notu hazırla:
- Künye (araştırmacının verdiği bilgiyle; eksikse [EKSİK])
- Ana iddia (1 cümle)
- Yöntem ve veri (1–2 cümle)
- Temel bulgular (en fazla 3 madde)
- Önemli kavramlar
- Sorgulanabilecek nokta
En sonda, notu literatür tablosuna eklenmek üzere tek satırlık bir tablo satırı olarak da ver:
| Yazar (Yıl) | Ana iddia | Yöntem | Temel kavram |
```

#### Sık Yapılan Hatalar

**Hata 1: Sistem talimatını aşırı uzun ve çelişkili yazmak**

- Neden hata? Çok fazla ve birbiriyle çelişen kural, modelin hangisine uyacağını karıştırır.
- Düzeltme: Kuralları başlıklar altında toplayın, önceliği belirtin ("KESİN KURALLAR" her şeyden önce gelir).

**Hata 2: Proje dışında yeni sohbet açıp talimatın geçerli olduğunu sanmak**

- Neden hata? Proje talimatı sadece o projenin içindeki sohbetlerde geçerlidir.
- Düzeltme: Araştırmayla ilgili sohbetleri her zaman proje içinden açın.

**Hata 3: Talimatı hiç güncellememek**

- Neden hata? Araştırma ilerledikçe soru, yöntem ve terimler değişir.
- Düzeltme: Her önemli aşamadan (örneğin saha çalışması bitince) sonra talimatı gözden geçirin.

**Hata 4: Hassas verileri talimata veya bilgi tabanına koymak**

- Neden hata? Katılımcı adları, görüşme kayıtları, yayımlanmamış ham veri gereksiz yere paylaşılmış olur; etik kurul taahhütleriyle çelişebilir.
- Düzeltme: Yalnızca işin gerektirdiği bilgileri bulundurun; kişisel verileri anonimleştirin.

---

### Konu 2: Çoklu Deneme ve Çıktı Karşılaştırma (30 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir araştırmacı makalesinin özetini tek seferde yazmaz. Birkaç farklı sürüm dener: probleme vurgu yapan, bulguya vurgu yapan, literatürdeki boşluğa vurgu yapan. Sonra bunları derginin beklentisine göre karşılaştırıp en iyisini seçer ya da iyi yanlarını birleştirir.

**Basit açıklama:** Yapay zekâ aynı prompta her seferinde biraz farklı cevap verir. Bu bir sorun değil, bir fırsattır: Birden fazla seçenek üretip karşılaştırarak en iyisini seçebilir veya en iyi parçaları birleştirebiliriz.

**Teknik tanım:** Dil modelleri cevap üretirken her adımda olası kelimeler arasından olasılığa dayalı bir seçim yapar. Bu rastgelelik, **sıcaklık (temperature)** gibi ayarlarla kontrol edilir. Aynı promptla birden fazla çıktı üretip (sampling) belirli ölçütlerle karşılaştırma ve seçme yöntemine çoklu deneme denir.

#### Neden Öğreniyoruz?

- **Başlık, özet, araştırma sorusu** gibi işlerde tek seçenek nadiren en iyisidir.
- **Önemli bilgilerde** farklı cevapların ortak noktaları daha güvenilirdir; ayrıştıkları yerler doğrulanması gereken yerlerdir.
- **Prompt iyileştirmede** iki farklı promptun sonuçlarını karşılaştırmak, hangi promptun daha iyi olduğunu gösterir.

#### Temel Kavramlar

**Kavram: Yeniden üretme (regenerate)**

- Basit açıklama: Aynı mesaja yeni bir cevap üretme. Sohbet araçlarında genellikle cevabın altında yuvarlak ok simgesiyle yapılır.
- Örnek: Bir başlık önerisini beğenmediğinizde yeniden üretmek.

**Kavram: Sıcaklık (temperature)**

- Basit açıklama: Cevabın ne kadar "yaratıcı / rastgele" olacağını belirleyen ayar. Düşük değer daha tutarlı, yüksek değer daha çeşitli cevaplar verir.
- Not: Sohbet uygulamalarında genellikle doğrudan ayarlanamaz; API'de ve bazı geliştirici araçlarında ayarlanabilir. Yeni modellerin bir kısmında bu ayar sınırlıdır.

**Kavram: Değerlendirme ölçütü (rubrik)**

- Basit açıklama: Seçenekleri karşılaştırmak için önceden belirlenen puanlama kriterleri.
- Örnek: "Netlik (1–5), bulgulara sadakat (1–5), kelime sınırına uygunluk (Evet/Hayır)."

**Kavram: A/B prompt testi**

- Basit açıklama: İki farklı promptu aynı görev için deneyip sonuçlarını karşılaştırmak.

#### Çoklu Deneme Yöntemleri

| Yöntem | Nasıl yapılır? | Ne zaman? |
|---|---|---|
| Tek promptta çok seçenek | "Birbirinden farklı 5 seçenek yaz." | Başlık, araştırma sorusu, anahtar kelime |
| Yeniden üretme | Aynı promptu tekrar çalıştırmak | Çeşitlilik görmek |
| Farklı modeller | Aynı promptu ChatGPT, Claude, Gemini'de denemek | Önemli metinler, farklı üsluplar |
| A/B prompt testi | İki farklı promptu denemek | Prompt iyileştirme |
| Modeli hakem yapmak | Seçenekleri modele ölçütlerle puanlatmak | Çok sayıda seçenek olduğunda |

> **Dikkat:** Modeli hakem yaptığınızda bile son karar sizindir. Model, özellikle kendi ürettiği metinleri değerlendirirken yanlı olabilir.

#### Basit Örnek

```text
1950–1980 arasında apartman dairelerinde salonun temsil mekânına dönüşmesini inceleyen
makalem için birbirinden belirgin şekilde farklı 5 başlık öner: 1 tanesi "Ana başlık: Alt başlık"
biçiminde, 1 tanesi soru biçiminde, 1 tanesi bir kavramı öne çıkaran, 1 tanesi dönemi ve yeri
belirten açıklayıcı, 1 tanesi bir nesneye odaklı olsun.
```

**Tahmin sorusu:** "Birbirinden farklı" yerine sadece "5 başlık öner" deseydik ne olurdu?

**Cevap:** Başlıklar büyük ihtimalle birbirine benzerdi (örneğin hepsi "Apartman Dairesinde Salon: ..." ile başlardı). Çeşitlilik istemek ve türleri tanımlamak, benzer seçeneklerin önüne geçer.

#### Birlikte Uygulayalım: Makale Özeti Karşılaştırması

**Amaç:** Birden fazla çıktı üretmek, ölçütle karşılaştırmak ve en iyi parçaları birleştirmek.

**Senaryo:** Bir sempozyuma gönderilecek bildirinin 250 kelimelik özeti hazırlanacak.

**Adımlar:**

1. Araştırma projesinin içinde yeni bir sohbet açın.
2. Önce değerlendirme ölçütlerini belirleyin ve not edin:

| Ölçüt | Açıklama | Puan |
|---|---|---|
| Netlik | Araştırma sorusu ve katkı ilk okumada anlaşılıyor mu? | 1–5 |
| Sadakat | Bulgularda olmayan iddia var mı? | 1–5 |
| Yapı | Amaç–yöntem–bulgular–sonuç sırası var mı? | 1–5 |
| Uzunluk | 230–250 kelime arasında mı? | Evet/Hayır |

3. Şu promptu yazın:

```text
Aşağıdaki bilgilere dayanarak 3 farklı bildiri özeti yaz. Her biri 230–250 kelime olsun.
Seçenek A: Literatürdeki boşlukla başlasın.
Seçenek B: Gündelik hayattan somut bir gözlemle başlasın.
Seçenek C: Araştırma sorusuyla doğrudan başlasın.
Her seçeneğin altına kelime sayısını yaz.
Verilen bulgular dışında bulgu ekleme. "Önemli", "kapsamlı" gibi içi boş sıfatlardan kaçın.

Bilgiler:
- Soru: 1950–1980 döneminde orta sınıf apartman dairelerinde salonun temsil mekânına dönüşmesi gündelik hayatı nasıl etkiledi?
- Yöntem: İstanbul ve Ankara'da yayımlanan dönem konut dergilerindeki 120 daire planının ve ev ilanlarının incelenmesi.
- Bulgular: Salon planda girişe en yakın ve en büyük oda olarak konumlanmış; ilanlarda "misafir salonu" ifadesi yaygınlaşmış; gündelik yaşam mutfak ve küçük oturma odasına kaymış.
```

4. Üç seçeneği okuyun ve ölçüt tablosuna göre birlikte puanlayın.
5. Aynı promptu farklı bir modelde (örneğin ChatGPT kullandıysanız Claude veya Gemini'de) çalıştırın.
6. Toplam 6 seçenek arasından en yüksek puanlıları belirleyin.
7. Birleştirme promptu yazın:

```text
Aşağıdaki iki bildiri özetinin güçlü yanlarını birleştir:
A'nın açılış cümlesini ve C'nin yöntem anlatımını kullan. 250 kelimeyi geçme.
Bulgulara yeni bilgi ekleme.

A: [metin]
C: [metin]
```

8. Kelime sayısını kendiniz bir sayaçla kontrol edin.

**Beklenen sonuç:** Ölçütlerle seçilmiş ve birleştirilmiş, 250 kelimelik nihai bir bildiri özeti.

**Açıklama:** Tek bir denemeyle yetinseydik, sadece modelin ilk "tahmin"ini görecektik. Çoklu deneme ve ölçütle karşılaştırma, kaliteyi belirgin şekilde artırır. Önceden ölçüt belirlemek ise seçimi duygusal olmaktan çıkarır.

> **Dikkat:** Modeller kelime saymada sık yanılır. Kelime sınırı olan metinleri (özet, bildiri) mutlaka kendiniz sayın.

#### Gerçek Hayat Senaryosu: Tutarlılık Testiyle Bilgi Kontrolü

**Senaryo:** Bir makalenin giriş bölümünde "İstanbul'daki ilk apartmanlar ne zaman yapıldı?" sorusuna değinilecek.

**Problem nedir?** Model bu tür tarih sorularında yanılabilir.

**Nasıl çözeceğiz?** Aynı soruyu 3 kez (yeniden üreterek veya farklı modellerde) soracağız. Cevaplar tutarsızsa bu, bilginin mutlaka kaynaktan doğrulanması gerektiğinin işaretidir.

**Adımlar:**

1. Şu soruyu sorun:

```text
İstanbul'da apartman tipi konutların ortaya çıkışı hangi döneme tarihlenir?
Hangi semtlerde yoğunlaşmıştır? Emin olmadığın kısımları belirt.
```

2. Cevabı yeniden üretin (veya farklı bir modelde sorun). Toplam 3 cevap alın.
3. Şu tabloyu doldurun:

| Bilgi | Cevap 1 | Cevap 2 | Cevap 3 | Tutarlı mı? |
|---|---|---|---|---|
| Dönem | | | | |
| Semtler | | | | |
| İlk örnek olarak adı geçen yapı | | | | |

4. Tutarlı olan bilgileri "muhtemelen doğru, yine de doğrula", tutarsız olanları "mutlaka kaynaktan doğrula" olarak işaretleyin.

**Açıklama:** Genel bilgiler (örneğin 19. yüzyılın ikinci yarısı, Pera/Beyoğlu çevresi) cevaplarda tutarlı çıkarken; belirli bir "ilk apartman" adı veya kesin yıl cevaplar arasında değişebilir. Değişen bilgi, modelin emin olmadığı bilgidir.

> **Dikkat:** Tutarlılık doğruluk garantisi değildir. Model aynı yanlışı üç kez de tekrarlayabilir. Tutarlılık testi sadece **önceliklendirme** aracıdır: Akademik metinde kullanılacak her bilgi kaynaktan doğrulanmalı ve atıfla verilmelidir.

#### Sık Yapılan Hatalar

**Hata 1: Ölçütü sonradan belirlemek**

- Neden hata? Seçenekleri gördükten sonra ölçüt belirlemek, ilk beğendiğiniz seçeneği haklı çıkarmaya yol açar.
- Düzeltme: Ölçütleri önceden yazın.

**Hata 2: "Farklı" seçenek istemeyip benzer çıktılar almak**

- Hatalı: "5 başlık öner."
- Doğru: "Birbirinden belirgin şekilde farklı 5 başlık öner: ..."

**Hata 3: Çok fazla seçenek üretip karar verememek**

- Neden hata? 30 seçenek, karar yorgunluğu yaratır.
- Düzeltme: 3–6 seçenek üretip ölçütle eleyin; gerekirse ikinci tur yapın.

---

### Konu 3: Yapay Zekâ ile Görsel Düzenleme (30 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir saha fotoğrafında kişilerin yüzlerini veya araç plakalarını gizlemek için eskiden fotoğraf düzenleme programında uzun süre çalışırdınız. Artık "Fotoğraftaki kişilerin yüzlerini bulanıklaştır" yazarak benzer bir sonucu hızla alabilirsiniz.

**Basit açıklama:** Yapay zekâ ile görsel düzenleme, mevcut bir görseli yazılı talimatla değiştirmektir: nesne eklemek veya kaldırmak, bir bölgeyi bulanıklaştırmak, stil değiştirmek, bir eskizi daha anlaşılır bir görsele dönüştürmek.

**Teknik tanım:** Görüntü düzenleme modelleri (image editing models), girdi olarak bir veya birkaç görsel ve bir metin talimatı alır; görselin talimatla ilgili kısımlarını yeniden üretirken geri kalanını korumaya çalışır. Bazı araçlarda düzenlenecek bölge bir **maske** (fırçayla boyanan alan) ile seçilir; buna **inpainting** denir. Görselin sınırlarını genişletmeye **outpainting** denir.

Bu işler için kullanılan araçlara örnekler:

| Araç | Ne yapar? |
|---|---|
| ChatGPT (GPT Image modeli) | Görsel yükleyip sohbetle düzenleme, eskizden görsel |
| Gemini | Görsel yükleyip sohbetle düzenleme |
| Adobe Photoshop (Üretken Dolgu) | Seçili alanı metinle doldurma veya silme |
| Midjourney (Editör) | Görselin bir bölümünü yeniden üretme, genişletme |
| Canva | Basit nesne silme, arka plan değiştirme |

> **Not:** OpenAI'ın eski görsel modeli DALL·E artık kullanımdan kaldırılmıştır; ChatGPT ve OpenAI API'de görsel üretimi ve düzenleme **GPT Image** modelleriyle yapılır. Araçların sürümleri hızla değiştiği için kullandığınız aracın güncel özelliklerini kontrol edin.

#### Neden Öğreniyoruz?

- **Sunum ve poster:** Konferans sunumu ve akademik poster için şematik, anlaşılır görseller hazırlamak.
- **Araştırma etiği:** Saha fotoğraflarında kişileri tanınmaz hâle getirmek (anonimleştirme).
- **Kavramsal anlatım:** Bir kavramı veya karşılaştırmayı gösteren şematik çizimler (örneğin "sofalı plan ile koridorlu planın karşılaştırması").
- **Akademik iletişim:** Araştırmayı kamuoyuna anlatan yazılar için görseller.

#### Etik Sınırlar: Akademik Çalışmada Görsel Düzenleme

Bu konu akademik çalışmalar için çok önemlidir. Temel ilke: **Kanıt olarak sunulan görsel değiştirilmez; açıklayıcı olarak sunulan görselin niteliği açıkça belirtilir.**

| Durum | Uygun mu? | Neden? |
|---|---|---|
| Saha fotoğrafında kişilerin yüzlerini bulanıklaştırmak | Uygun (ve çoğu zaman gerekli) | Katılımcı mahremiyeti. Belge niteliği taşıyan fotoğraflarda yalnızca bulanıklaştırma yapılmalı, başka hiçbir şey değiştirilmemelidir. |
| Bir yapının mevcut durumunu gösteren fotoğraftan nesne silip "mevcut durum" diye sunmak | **Uygun değil** | Veriyi değiştirmek, araştırma etiği ihlalidir. |
| Rölöve veya restitüsyon gibi gösterilen bir yapay zekâ görseli | **Uygun değil** (açıkça belirtilmedikçe) | Bilimsel bir çizim gibi algılanır ama ölçüye dayanmaz. |
| "Temsili şema, yapay zekâ ile üretilmiştir" notuyla kavramsal görsel | Uygun | Okur görselin niteliğini bilir. |
| Başkasının telifli fotoğrafını yükleyip düzenleyip yayımlamak | **Uygun değil** | Telif hakkı ihlali olabilir; izin ve atıf gerekir. |
| Arşiv fotoğrafını "renklendirip" orijinalmiş gibi kullanmak | **Uygun değil** | Belgenin özgünlüğünü bozar; yapılacaksa açıkça belirtilmelidir. |

> **Dikkat:** Yapay zekâ ile üretilmiş veya düzenlenmiş görselleri altyazıda belirtin. Örneğin: *"Şekil 3. Sofalı ve koridorlu plan şemalarının karşılaştırması (temsili; yapay zekâ ile üretilmiştir)."* Ayrıca derginin görsel ve yapay zekâ politikalarını kontrol edin.

> **Dikkat – Anonimleştirme:** Yapay zekâ düzenlemesi, fotoğrafın başka kısımlarını da fark ettirmeden değiştirebilir. Belge niteliğindeki fotoğraflarda anonimleştirme için klasik bulanıklaştırma araçları (fotoğraf düzenleme programlarındaki bulanıklaştırma fırçası) daha güvenlidir. Yapay zekâyı burada daha çok sunum ve poster görselleri için kullanın.

#### Görsel Düzenleme Promptunun Yapısı

İyi bir düzenleme promptu dört şey söyler:

1. **Neyi değiştir?** (Hedef)
2. **Nasıl değiştir?** (Yeni durum)
3. **Neyi koru?** (Korunacaklar)
4. **Hangi üslupta?** (Stil, ışık – gerekiyorsa)

Örnek:

```text
Bu fotoğraftaki bütün insanların yüzlerini tanınmayacak şekilde bulanıklaştır.
Binanın cephesini, pencereleri, renkleri ve ışığı aynen koru; başka hiçbir şeyi değiştirme.
```

**Neden "neyi koru" önemli?** Modeller düzenleme sırasında istemediğiniz yerleri de değiştirebilir (pencere sayısı, cephe oranları). Korunacakları açıkça yazmak bu riski azaltır, ama ortadan kaldırmaz; sonucu mutlaka orijinalle karşılaştırın.

#### Birlikte Uygulayalım: Saha Fotoğrafından Sunum Şemasına

**Amaç:** Bir saha fotoğrafını adım adım işleyerek konferans sunumunda kullanılabilecek, niteliği açıkça belirtilmiş bir şemaya dönüştürmek.

**Senaryo:** Bir saha çalışmasında çekilen geleneksel konut (veya erken dönem apartman) cephesi fotoğrafı, bir konferans sunumunda cephe düzenini anlatmak için kullanılacak.

**Adımlar:**

1. ChatGPT veya Gemini'de yeni bir sohbet açın.
2. Ataş (dosya ekleme) simgesine tıklayın ve cephe fotoğrafını yükleyin.
3. Önce görseli **analiz ettirin** (düzenlemeden önce modelin ne gördüğünü anlamak için):

```text
Bu fotoğraftaki yapıyı mimari açıdan tarif et: kat sayısı, cephe elemanları,
malzeme, pencere düzeni. Fotoğrafta tanınabilir kişi, araç plakası veya
kişisel bilgi içeren tabela olup olmadığını listele.
```

4. Modelin listesine bakın. Tanınabilir kişi veya plaka varsa, sunumda fotoğrafın kendisi de kullanılacaksa bunları önce bir fotoğraf düzenleme programıyla bulanıklaştırın.
5. Şimdi fotoğraftan bir şema üretin:

```text
Bu fotoğraftaki cepheyi, bir konferans sunumunda cephe düzenini anlatmak için kullanılacak
sade bir şematik çizime dönüştür:
- Beyaz zemin üzerine ince siyah çizgiler.
- Sadece mimari öğeler: kat çizgileri, pencereler, cumba, çatı saçağı. İnsan, araç, tabela, kablo yok.
- Kat sayısını, pencere sayısını ve cumbanın yerini fotoğraftakiyle aynı tut.
- Gölge ve doku kullanma.
```

6. Sonucu orijinalle karşılaştırın. **Kontrol listesi:** Pencere sayısı aynı mı? Cumba aynı yerde mi? Kat sayısı aynı mı?
7. Bir sorun varsa düzeltin:

```text
Sağ üstteki pencere kaybolmuş. Fotoğraftaki gibi 3. kattaki 4 pencereyi geri getir.
```

8. Şema doğrulandıktan sonra, anlatmak istediğiniz öğeyi vurgulatın:

```text
Bu şemada sadece cumbayı soluk turuncu renkle vurgula. Başka hiçbir şeyi değiştirme.
```

9. Sonucu indirin ve dosya adını `sunum_cephe_semasi.png` olarak kaydedin.
10. Altyazıyı yazın: *"Şekil 2. Örnek konutun cephe düzeni (temsili şema; yazarın fotoğrafından yapay zekâ ile üretilmiştir)."*

**Beklenen sonuç:** Fotoğraftaki cephe düzenine sadık, dikkat dağıtıcı unsurlardan arındırılmış, anlatılmak istenen öğeyi vurgulayan ve niteliği altyazıda belirtilmiş bir şema.

**Açıklama:** Düzenlemeyi tek seferde değil, **adım adım** yaptık: önce analiz, sonra şema, sonra vurgu. Her adımda oranları fotoğrafla karşılaştırdık. Şemayı "fotoğraf" olarak değil, açıkça "temsili şema" olarak etiketledik; böylece okur onu kanıt değil, açıklama aracı olarak okur.

#### Sıra Sizde 2 (15 dk): Eskizden Sunum Görseline

**Amaç:** Bir el eskizini düzenleme talimatıyla daha anlaşılır bir sunum görseline dönüştürmek.

**Görev:** Elle çizdiğiniz basit bir iç mekân eskizini (örneğin bir sofanın perspektifi) fotoğraflayıp yükleyin ve bir sunumda kullanılacak, temsili bir iç mekân görseline dönüştürün.

**İstenenler:**

- Önce eskizi modele tarif ettirin.
- Dönüştürme promptunda: malzeme (ahşap tavan, kireç sıva), ışık (öğleden sonra, pencereden giren güneş), korunacaklar (perspektif, açıklık yerleri) belirtilsin.
- En az bir düzeltme turu yapın.
- Sonucu, kullandığınız promptları ve görselin altyazısını kaydedin.

**Beklenen sonuç:** Eskizin kompozisyonunu koruyan, malzeme ve ışık bilgisi eklenmiş, altyazısında temsili olduğu belirtilmiş bir görsel.

**İpucu:** "Eskizdeki perspektifi, kapı ve pencerelerin yerini ve sayısını aynen koru" ifadesi, modelin kompozisyonu değiştirmesini azaltır.

#### Çözüm

Analiz promptu:

```text
Bu el eskizinde ne görüyorsun? Mekânın türünü, perspektif tipini, açıklıkların (kapı, pencere)
yerlerini ve sayısını tarif et.
```

Dönüştürme promptu:

```text
Bu eskizi, geleneksel bir Türk evinin sofasını gösteren temsili bir iç mekân görseline dönüştür.
Görsel bir konferans sunumunda mekân kurgusunu anlatmak için kullanılacak.
- Perspektifi, kapı ve pencerelerin yerini ve sayısını aynen koru.
- Malzemeler: ahşap çıtalı tavan, beyaz kireç sıvalı duvarlar, ahşap döşeme, sedirler üzerinde kilim.
- Işık: öğleden sonra, sol taraftaki pencerelerden giren yumuşak güneş ışığı.
- İnsan figürü ekleme.
- Sade, okunaklı bir illüstrasyon üslubu; abartılı renkler olmasın.
```

Düzeltme örneği:

```text
Tavan çok yüksek olmuş; eskizdeki gibi daha alçak bir oran kullan.
Sedirlerin yüksekliği diz hizasında olsun.
```

Altyazı örneği: *"Şekil 4. Sofalı plan tipinde iç mekân kurgusu (temsili; yazarın eskizinden yapay zekâ ile üretilmiştir)."*

#### Sık Yapılan Hatalar

**Hata 1: Korunacakları söylememek**

- Hatalı: "Fotoğrafı şemaya çevir."
- Doğru: "Fotoğrafı şemaya çevir. Pencere sayısını, kat sayısını ve oranları koru."

**Hata 2: Düzenlenmiş görseli kanıt gibi sunmak**

- Neden hata? Okuru yanıltır; araştırma etiği ihlalidir.
- Düzeltme: Altyazıda yapay zekâ kullanımını belirtin; kanıt niteliğindeki görselleri (anonimleştirme dışında) düzenlemeyin.

**Hata 3: Mimari doğruluğu kontrol etmemek**

- Neden hata? Modeller merdivenleri, kemerleri, taşıyıcı sistemi mantıksız çizebilir (havada asılı kirişler, sayısı değişen pencereler).
- Düzeltme: Her görseli orijinalle ve mimari mantıkla kontrol edin; gerekirse düzeltme isteyin veya elle düzeltin.

**Hata 4: Tek seferde çok fazla değişiklik istemek**

- Neden hata? Hangi değişikliğin sorun çıkardığı anlaşılmaz.
- Düzeltme: Değişiklikleri sırayla, adım adım isteyin.

---

### Konu 4: Görsel ve Metin Entegrasyonu – Yapay Zekâ ile İçerik Üretimi (35 dk)

#### Konu Nedir?

**Günlük hayat örneği:** İyi bir akademik posterde metin ile görsel birbirini tamamlar. Metin "salonun girişe en yakın oda olarak konumlandığını" söylerken yanındaki şema tam bunu gösterir. Kötü bir posterde ise görsel ile metin birbiriyle konuşmaz.

**Basit açıklama:** Görsel–metin entegrasyonu, metni ve görseli birbirinden bağımsız değil, **birbirine göre** üretmektir. Önce metni yazar, sonra metnin ana fikrinden görsel promptu çıkarırız (veya tersi).

**Teknik tanım:** Çok kipli (multimodal) içerik üretimi; metin, görsel, ses gibi farklı türdeki içeriklerin tutarlı bir mesaj etrafında birlikte üretilmesidir. Çok kipli modeller hem metni hem görseli anlayabildiği için, bir metinden görsel promptu çıkarmak veya bir görselden metin üretmek mümkündür.

#### Neden Öğreniyoruz?

- **Akademik iletişim:** Araştırmayı kamuoyuna anlatan blog yazıları, üniversite haber bültenleri.
- **Konferans:** Posterler ve sunum slaytları.
- **Tutarlı görsel dil:** Bir sunumdaki veya posterdeki bütün görsellerin aynı üslupta olması.

#### Temel Kavramlar

**Kavram: Görsel prompt**

- Basit açıklama: Görsel üretmek için yazılan metin talimatı. Ders 4'te ayrıntılı yapısını öğreneceğiz.

**Kavram: Stil rehberi (görsel kimlik)**

- Basit açıklama: Bütün görsellerde tekrar eden üslup kuralları: renk paleti, çizim tekniği, ışık, kompozisyon.
- Örnek: "Beyaz zemin, ince çizgi, tek vurgu rengi, insan figürü yok, görselde yazı yok."

**Kavram: Alt metin (alt text)**

- Basit açıklama: Görseli göremeyen kişiler (ekran okuyucu kullananlar) ve arama motorları için görselin yazılı açıklaması.
- Neden önemli? Erişilebilirlik sağlar; birçok dergi ve üniversite web sitesi artık alt metin istemektedir.

#### Entegrasyon Akışı

1. **Metni yaz:** Ana fikir netleşir.
2. **Görsel ihtiyacını belirle:** Metnin hangi anı görselleştirilmeli?
3. **Metinden görsel prompt çıkar:** Modelden yardım alınabilir.
4. **Stil rehberini ekle:** Görsel kimlik korunur.
5. **Görseli üret ve kontrol et.**
6. **Altyazı ve alt metin yaz.**

#### Birlikte Uygulayalım: Blog Yazısı İçin Yapay Zekâ Metni ve Uygun Görsel Oluşturma

**Amaç:** Bir akademik blog yazısını ve ona uygun görseli birbirine bağlı şekilde üretmek.

**Senaryo:** Yayımlanmış bir araştırmanın bulguları, üniversitenin araştırma blogunda kamuoyuna anlatılacak. Yazının konusu: **"Evlerimizdeki kayıp mekân: Sofa"**.

**Problem nedir?** Hem akademik bulgulara sadık hem de alan dışından okurun anlayacağı bir yazı ile yazıyla uyumlu bir görsel gerekiyor.

**Nasıl çözeceğiz?** Önce yazıyı yazdıracağız, sonra yazının ana fikrinden görsel promptu çıkaracağız, sonra görseli üretip altyazı ve alt metin yazacağız.

**Hangi bilgileri kullanacağız?** Araştırmanın bulguları, görsel stil rehberi, blog okurunun profili.

**Adımlar:**

1. Araştırma projesinin içinde yeni bir sohbet açın.
2. Blog yazısı promptunu yazın:

```text
## GÖREV
Üniversitenin araştırma blogu için bir yazı yaz. Başlık: "Evlerimizdeki Kayıp Mekân: Sofa"

## OKUR
Alan dışından, meraklı yetişkin okurlar.

## İÇERİK
Yazı şu araştırma bulgularına dayanmalı; başka bulgu ekleme:
- Geleneksel evde sofa, odaları birbirine bağlayan bir dolaşım alanı ve ailenin buluştuğu ortak bir mekândı.
- Apartman dairesinde bu işlev koridor (dolaşım) ve salon (toplanma) arasında bölündü.
- Bugünkü açık plan daireler, sofanın birleştirici işlevini farklı bir biçimde yeniden üretiyor olabilir.

Yapı:
- Okuru gündelik bir sahneyle karşılayan bir açılış
- Bulguların sade bir dille anlatımı
- Kapanışta okura bir soru ve araştırmanın yayımlandığı yere yönlendiren tek bir cümle ([MAKALE BAĞLANTISI] yaz)

## BİÇİM
- 500–600 kelime
- 3 ara başlık
- Kısa paragraflar (en fazla 4 cümle)
- Kesin tarih ve isim kullanma; gerekiyorsa [DOĞRULANMALI] koy.
```

3. Yazıyı okuyun; bulgulara sadık mı, abartı var mı kontrol edin ve gerekiyorsa bir düzeltme turu yapın.
4. Görsel stil rehberini yazın ve Prompt Defterim'e kaydedin:

```text
GÖRSEL STİL REHBERİ (Araştırma sunumları ve blog)
- Teknik: Beyaz zemin üzerine ince siyah çizgi + hafif sulu boya dokusu
- Renkler: Sıcak toprak tonları, krem, tek vurgu rengi olarak soluk turkuaz
- Işık: Yumuşak, doğal gün ışığı
- Kompozisyon: Göz hizasından iç mekân perspektifi veya sade şema
- İnsan figürü: Yok veya çok küçük ve silüet
- Yazı/metin: Görselde yazı olmasın
```

5. Yazıdan görsel prompt çıkarmasını isteyin:

```text
[STİL REHBERİ]

Bu blog yazısının ana fikrini en iyi anlatan görsel sahneyi seç. Bu sahne için, yukarıdaki görsel
stil rehberine uygun, ayrıntılı bir görsel üretim promptu yaz (en fazla 80 kelime).
Promptta mekânın öğelerini (sedir, pencereler, tavan, döşeme, ışık) açıkça belirt.
```

6. Model örneğin şöyle bir prompt üretebilir:

```text
Geleneksel bir Türk evinin geniş sofası, göz hizasından iç mekân perspektifi. Sağ ve solda
odalara açılan ahşap kapılar, uçta cumbalı pencere önünde kilim serili alçak sedir.
Ahşap çıtalı tavan, geniş ahşap döşeme tahtaları. Pencerelerden süzülen yumuşak öğleden
sonra ışığı. Beyaz zemin üzerine ince siyah çizgi ve hafif sulu boya; sıcak toprak
tonları, krem ve soluk turkuaz vurgu. İnsan figürü yok, görselde yazı yok.
```

7. Bu promptla görseli üretin (aynı sohbette "Bu prompta göre görseli oluştur" diyebilirsiniz).
8. Görseli kontrol edin: Stil rehberine uyuyor mu? Mimari açıdan mantıklı mı (kapılar, pencereler, tavan)?
9. Gerekiyorsa düzeltme isteyin.
10. Altyazı ve alt metin isteyin:

```text
Bu görsel için:
1. Blog yazısında görselin altında yer alacak 1 cümlelik altyazı yaz (sonunda "Temsili illüstrasyon; yapay zekâ ile üretilmiştir." notu olsun).
2. Ekran okuyucular için 1–2 cümlelik alt metin yaz.
```

**Beklenen sonuç:**

- Bulgulara sadık, 500–600 kelimelik, 3 ara başlıklı bir blog yazısı,
- Yazının ana fikrini gösteren, stil rehberine uygun bir illüstrasyon,
- Altyazı ve alt metin.

**Açıklama:** Görseli yazıdan bağımsız üretseydik, yazı "sofanın birleştirici işlevinden" bahsederken görsel alakasız bir sahne gösterebilirdi. Görsel promptunu **yazının kendisinden** çıkarmak ve **stil rehberi** eklemek, metin ile görselin aynı mesajı vermesini sağladı. Stil rehberi sayesinde aynı araştırmanın sunumu, posteri ve blog yazıları da aynı görsel kimliği taşıyacak.

#### Sık Yapılan Hatalar

**Hata 1: Blog yazısında bulguları abartmak**

- Neden hata? Kamuoyu için yazarken model bulguları "kanıtlandı", "her evde" gibi genellemelere dönüştürebilir.
- Düzeltme: "Bulguları abartma, genelleme yapma; 'olabilir', 'işaret ediyor' gibi ifadeler kullan" deyin ve yazıyı makaleyle karşılaştırın.

**Hata 2: Her görselde farklı üslup**

- Neden hata? Sunum, poster ve blog dağınık görünür.
- Düzeltme: Stil rehberini her görsel promptuna ekleyin.

**Hata 3: Görselde yazı istemek**

- Neden hata? Görsel modelleri yazıyı eskisine göre çok daha iyi üretse de hâlâ harf hataları yapabilir, özellikle Türkçe karakterlerde (ğ, ş, ı).
- Düzeltme: Yazıyı görselin içine değil, sunum veya poster programında ayrı katman olarak ekleyin.

**Hata 4: Alt metni unutmak**

- Neden hata? Erişilebilirlik ve web'de bulunabilirlik kaybolur.
- Düzeltme: Her görsel için alt metin yazın.

---

### Ders Özeti

Bu derste promptlarımızı kalıcı hâle getirmeyi öğrendik: Sistem mesajları ve proje talimatlarıyla araştırmanın konusu, sorusu, yöntemi, yazım kuralları ve uydurma yasağı her sohbette otomatik geçerli oldu. Başlık ve bildiri özeti gibi işlerde tek cevapla yetinmeyip birden fazla seçenek ürettik, önceden belirlediğimiz ölçütlerle karşılaştırdık ve en iyi parçaları birleştirdik. Görsel tarafta, saha fotoğraflarından ve eskizlerden adım adım sunum şemaları ürettik ve akademik çalışmada kanıt niteliğindeki görselin değiştirilemeyeceğini, açıklayıcı görselin ise niteliğinin altyazıda belirtilmesi gerektiğini gördük. Son olarak bir akademik blog yazısı ile ona uygun görseli, bir stil rehberi kullanarak birbirine bağlı şekilde ürettik.

### Bu Derste Neler Öğrendik?

- Sistem, kullanıcı ve asistan mesajlarının farkını öğrendik.
- Bir araştırma için kalıcı bir talimat seti ve terimler sözlüğü yazdık.
- Proje / Gem gibi özelliklerle talimatları kalıcı hâle getirdik.
- Bildiri özeti üzerinde çoklu deneme ve ölçütle karşılaştırma yaptık.
- Tutarlılık testiyle doğrulanması gereken bilgileri belirledik.
- Görsel düzenleme promptunun yapısını (hedef, yeni durum, korunacaklar, üslup) öğrendik.
- Akademik çalışmada görsel düzenlemenin etik sınırlarını, anonimleştirmeyi ve altyazı kullanımını gördük.
- Görsel stil rehberi hazırladık.
- Bir akademik blog yazısı ile uygun görselini birlikte ürettik.

### Mini Quiz

1. **(Çoktan seçmeli)** Sistem mesajının temel işlevi nedir?
   - a) Modelin internette arama yapmasını sağlamak
   - b) Bütün sohbet boyunca geçerli olacak temel davranış ve kuralları belirlemek
   - c) Görsel üretmek
   - d) Cevabı hızlandırmak
2. **(Doğru / Yanlış)** Bir proje talimatı, o projenin dışında açılan sohbetlerde de geçerlidir.
3. **(Kısa cevap)** Çoklu denemede değerlendirme ölçütlerini neden seçenekleri görmeden önce belirlemeliyiz?
4. **(Kısa cevap)** Görsel düzenleme promptunda hangi dört bilgi bulunmalıdır?
5. **(Doğru / Yanlış)** Bir yapının mevcut durumunu gösteren saha fotoğrafından istenmeyen nesneleri yapay zekâ ile silip makalede "mevcut durum" fotoğrafı olarak kullanmak uygundur.
6. **(Çoktan seçmeli)** Aynı soruya üç farklı cevapta farklı tarihler geliyorsa bu ne gösterir?
   - a) Modelin bozuk olduğunu
   - b) Bilginin mutlaka kaynaktan doğrulanması gerektiğini
   - c) Ortalamanın doğru olduğunu
   - d) Sorunun yanlış sorulduğunu
7. **(Küçük problem)** "Fotoğrafı sunum için güzelleştir" promptunu iyi bir düzenleme promptuna dönüştürün.
8. **(Kısa cevap)** Görsel–metin entegrasyonunda stil rehberi ne işe yarar?

### Mini Quiz Cevapları

1. **b.**
2. **Yanlış.** Proje talimatı sadece proje içindeki sohbetlerde geçerlidir.
3. Seçenekleri gördükten sonra belirlenen ölçütler, ilk beğenilen seçeneği haklı çıkarmaya yönelik olur; tarafsız karşılaştırma bozulur.
4. Neyi değiştir (hedef), nasıl değiştir (yeni durum), neyi koru, hangi üslupta.
5. **Yanlış.** Kanıt niteliğindeki görseli değiştirmek araştırma etiği ihlalidir; okuru yanıltır.
6. **b.**
7. Örnek: "Bu cephe fotoğrafını, sunumda cephe düzenini anlatmak için beyaz zemin üzerine ince siyah çizgili bir şemaya dönüştür. Kat sayısını, pencere sayısını ve oranları aynen koru; insan, araç ve tabela ekleme." (Altyazıda temsili şema olduğu belirtilir.)
8. Bütün görsellerde aynı tekniğin, renk paletinin, ışığın ve kompozisyonun kullanılmasını sağlayarak sunum, poster ve yazılarda tutarlı bir görsel kimlik oluşturur.

### Ders Sonu Uygulaması

**Senaryo:** Aynı araştırmanın ikinci bulgusu için ikinci bir blog yazısı hazırlanacak: **"Misafir Salonu: Evin En Güzel Ama En Az Kullanılan Odası"**. Bu kez başlık da çoklu deneme ile seçilecek.

**Yapılacaklar:**

1. Araştırma projesinin içinde çalışın (sistem talimatı aktif olsun).
2. Birbirinden farklı 5 başlık seçeneği ürettirin; önceden belirlediğiniz 3 ölçütle puanlayıp birini seçin.
3. Seçilen başlıkla, verilen bulgulara dayanan 400–500 kelimelik blog yazısını yazdırın.
4. Stil rehberini kullanarak yazıdan görsel prompt çıkarttırın ve görseli üretin.
5. Görseli mimari açıdan kontrol edin, en az bir düzeltme turu yapın.
6. Altyazı ve alt metin yazdırın.

Kullanılacak bulgular:

- Salon, dönem planlarında girişe en yakın ve en büyük oda olarak konumlanmıştır.
- Dönem ilanlarında "misafir salonu" ifadesi yaygınlaşmıştır.
- Ailenin gündelik yaşamı mutfak ve küçük oturma odasına kaymıştır.

**Beklenen sonuç:** Puanlama tablosu, seçilmiş başlık, bulgulara sadık blog yazısı, stil rehberine uygun görsel, altyazı ve alt metin.

**İpuçları:**

- Başlık türlerini çeşitlendirin (soru, kavram odaklı, nesne odaklı...).
- Görsel promptunda "vitrin, dantel örtü, kapalı kapı, kullanılmamış koltuklar" gibi yazıdaki nesneleri kullanın.
- Stil rehberini her görsel promptunun başına yapıştırın.

### Ders Sonu Uygulaması – Çözüm

**Ölçüt tablosu (önceden):**

| Ölçüt | Puan |
|---|---|
| Merak uyandırma | 1–5 |
| Bulguyu yansıtma | 1–5 |
| Kısalık (en fazla 8 kelime) | 1–5 |

**Başlık promptu:**

```text
"Apartman dairesinde misafir salonu" konulu, araştırma bulgularını kamuoyuna anlatan bir blog yazısı
için birbirinden belirgin şekilde farklı 5 başlık öner:
1 soru, 1 kavram odaklı, 1 nesne odaklı, 1 tek kelime + alt başlık, 1 karşıtlık kuran.
Her biri en fazla 8 kelime olsun. Bulguları abartan ifadeler kullanma.
```

**Örnek seçim:** "Girmek Yasaktı: Misafir Salonunun Kısa Tarihi" (Merak 5, Bulgu 4, Kısalık 4).

**Yazı promptu:** Konu 4'teki blog promptu; başlık, verilen üç bulgu ve 400–500 kelime sınırıyla güncellenir. "Bulgularda olmayan bilgi ekleme, genelleme yapma" yönergesi korunur.

**Görsel prompt (beklenen tür):**

```text
1970'lerin bir apartman dairesinde kapısı yarı aralık misafir salonu, göz hizasından görünüm.
Dantel örtülü takım koltuklar, camlı vitrinde dizili fincanlar, duvarda çerçeveli tablo,
yerde desenli halı, tül perdeden süzülen yumuşak ışık. Beyaz zemin üzerine ince siyah çizgi
ve hafif sulu boya; sıcak toprak tonları, krem ve soluk turkuaz vurgu.
İnsan figürü yok, görselde yazı yok.
```

**Düzeltme örneği:**

```text
Vitrin pencerenin önünü kapatıyor; vitrini yan duvara al. Pencere oranını koru.
```

**Altyazı:** "Kapısı çoğu zaman kapalı tutulan misafir salonu. (Temsili illüstrasyon; yapay zekâ ile üretilmiştir.)"

**Alt metin:** "Dantel örtülü koltukları, fincanlarla dolu camlı vitrini ve tül perdesiyle 1970'ler tarzı bir apartman salonunun sulu boya illüstrasyonu."

> **Sonraki derste:** Bugün görsel düzenlemeye ve metinle uyumlu görsel üretmeye giriş yaptık. Bir sonraki derste görsel prompt yazımını derinleştireceğiz: **Midjourney ve GPT Image ile görsel üretim, tarz, ışık, perspektif gibi görsel prompt bileşenleri,** sunum ve poster görselleri, ses ve video araçları. Ayrıca yapay zekânın arkasındaki **yapay sinir ağlarının** nasıl çalıştığını, kâğıt üzerinde küçük bir sinir ağını hesaplayarak öğreneceğiz.
