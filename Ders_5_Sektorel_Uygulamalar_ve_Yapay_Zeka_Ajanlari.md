# Prompt Mühendisliği Eğitimi – Ders 5

## Sektörel Uygulamalar ve Kod Yazmadan Yapay Zekâ Ajanları (Yaklaşık 2,5 Saat)

---

## Ders 5 – 150 Dakika

### Önceki Dersle Bağlantı

Önceki derste görsel promptları mimari bir dille yazdık, sunum ve poster görselleri ürettik, sesli görüşmeleri okuma notlarına dönüştürdük, yayımlanan bir makale için sosyal medya duyuru serisi hazırladık ve yapay sinir ağlarının içine baktık. Token tahmini sayesinde bağlam, rol, örnek ve çıktı biçiminin **neden** işe yaradığını anladık.

Bu derste şimdiye kadar öğrendiğimiz bütün teknikleri dört farklı alana uygulayacağız: **yazılım geliştirme, eğitim, pazarlama ve tasarım.** Akademik çalışmada bu alanların her birinin karşılığı var: kaynakçayı düzenleyen küçük bir kod, bir ders veya atölye için quiz, bir sempozyumun çağrı ve duyuru metinleri, bir araştırma sergisi için senaryo. Dersin ikinci yarısında yapay zekânın bir sonraki adımına geçeceğiz: Sadece cevap veren değil, **görev yapan** yapay zekâ ajanları. Kod yazmadan kendi ajanımızı kuracağız.

### Dersin Hedefleri

Bu dersin sonunda öğrenci:

- Yapay zekâya basit bir Python kodu yazdırabilecek, kodu çalıştırabilecek ve hatalı bir kodu düzelttirebilecek.
- Bir konu için ders materyali ve quiz ürettirebilecek.
- Çağrı metni, slogan ve SEO uyumlu içerik için prompt yazabilecek.
- Tasarım ve sergi senaryosu üretiminde yapay zekâyı kullanabilecek.
- Kendi alanına yönelik bir prompt seti geliştirebilecek.
- Yapay zekâ ajanının ne olduğunu ve sohbet botundan farkını açıklayabilecek.
- No-code ve low-code platformların farkını bilecek.
- Kod yazmadan bir katılımcı destek asistanı ve bir araştırma asistanı ajanı kurabilecek.

### Süre Planı

| Bölüm | Süre |
|---|---|
| Giriş ve önceki dersin tekrarı | 5 dk |
| Konu 1: Yazılım geliştirme – kod üretme ve hata ayıklama | 25 dk |
| Konu 2: Eğitim – ders materyali ve quiz oluşturma | 15 dk |
| Konu 3: Pazarlama – çağrı metni, slogan, SEO içerikleri | 15 dk |
| Konu 4: Tasarım – görsel ve senaryo üretimi | 10 dk |
| Grup / bireysel çalışma: Kendi alanına yönelik prompt seti | 15 dk |
| Konu 5: Yapay zekâ ajanları nedir? Ajanların özellikleri | 15 dk |
| Konu 6: Platform tanıtımı, low-code ve no-code platformlar | 15 dk |
| Uygulama: Basit yapay zekâ ajanı oluşturma | 25 dk |
| Ders özeti ve mini quiz | 10 dk |
| **Toplam** | **150 dk** |

### Derse Hazırlık

- Google hesabıyla **Google Colab** (colab.research.google.com) açılabilir olsun. Colab, bilgisayara hiçbir şey kurmadan tarayıcıda Python çalıştırmayı sağlar. Ders 6'da Python'u bilgisayara kuracağız.
- Gemini (Gem oluşturma), ChatGPT (proje) veya Claude (proje) hesaplarından en az biri hazır olsun.
- Ajan uygulaması için bir "Sık Sorulan Sorular" metin dosyası hazırlanacak (ders içinde birlikte yazılacak).

---

### Giriş ve Tekrar (5 dk)

**Soru:** Tek nöronlu sınıflandırıcımız hata yaptığında ne yaptı?

**Cevap:** Hatayı hesapladı ve ağırlıklarını (hata × girdi) kadar güncelledi; böylece bir sonraki tahmininde doğru sonucu verdi.

**Soru:** Few-shot prompting neden işe yarar?

**Cevap:** Model, örnekteki kalıbı devam ettirme olasılığı yüksek token'ları seçer.

---

### Konu 1: Yazılım Geliştirme – Kod Üretme ve Hata Ayıklama (25 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir araştırma ekibinde, her projede aynı tekrarlı işi yapan birini düşünün: yüzlerce makale dosyasının adını tek tek değiştirmek, bir kaynak listesini yıllara göre sıralamak, anket sonuçlarını saymak. Bu işi bir kez "tarif eden" küçük bir program yazarsanız, program bunu her seferinde saniyeler içinde yapar.

**Basit açıklama:** Kod, bilgisayara ne yapacağını adım adım söyleyen talimatlardır. Yapay zekâ, Türkçe olarak anlattığınız bir işi koda dönüştürebilir. Kod çalışmazsa, hata mesajını yapay zekâya verip düzelttirebilirsiniz. Bu sayede programcı olmayan biri de küçük otomasyonlar yapabilir.

**Teknik tanım:**

- **Kod üretme (code generation):** Doğal dilde tanımlanan bir görevin, dil modeli tarafından bir programlama dilinde koda dönüştürülmesi.
- **Hata ayıklama (debugging):** Kodun beklenmeyen davranışının veya hata mesajının nedenini bulup düzeltme süreci.
- **Python:** Okunması kolay, yeni başlayanlar için uygun, veri işleme ve yapay zekâ alanında en yaygın kullanılan programlama dillerinden biri.

#### Neden Öğreniyoruz?

Akademik çalışmada küçük kodların işe yaradığı yerler:

- Kaynakça listesini yıllara veya yazarlara göre sıralamak,
- Bir klasördeki makale PDF'lerinin adlarını standart hâle getirmek,
- Okuma notlarında veya görüşme transkriptlerinde belirli bir kavramın kaç kez geçtiğini saymak,
- Anket verilerinden basit tablolar ve grafikler üretmek,
- Ders 6'da yapay zekâ ile kendi programımızı yazmak.

#### Kod İsteme Promptunun Yapısı

| Bileşen | Örnek |
|---|---|
| Dil ve ortam | "Python ile, Google Colab'da çalışacak" |
| Girdi | "Elimde yazar, yıl, başlık bilgisi olan bir kaynak listesi var" |
| İşlem | "Yıllara göre sırala ve her on yılda kaç kaynak olduğunu say" |
| Çıktı | "Sonucu ekrana düzenli şekilde yazdır" |
| Seviye | "Yeni başlayan biri için basit kod yaz, her satıra Türkçe açıklama ekle" |

#### Birlikte Uygulayalım: Kaynakçayı Düzenleyen Küçük Program

**Amaç:** Yapay zekâya kod yazdırmak, kodu çalıştırmak, anlamak ve değiştirmek.

**Senaryo:** Bir literatür taramasında okunan kaynaklar bir listede tutuluyor. Literatürün hangi dönemlerde yoğunlaştığını görmek isteniyor.

**Adımlar:**

1. ChatGPT, Claude veya Gemini'de yeni bir sohbet açın.
2. Şu promptu yazın:

```text
Python ile Google Colab'da çalışacak basit bir program yaz.
Girdi: Programın içinde, her biri yazar, yıl ve başlık bilgisi içeren 6 kaynaklık bir liste olsun
(örnek veriler hayali olsun).
İşlem:
1. Kaynakları yıla göre eskiden yeniye sırala ve "Yazar (Yıl). Başlık." biçiminde yazdır.
2. Her on yılda (1990'lar, 2000'ler, 2010'lar...) kaç kaynak olduğunu say ve yazdır.
Seviye: Programlamaya yeni başlayan biri için yaz. Karmaşık yapılar kullanma.
Önemli satırlara Türkçe yorum ekle.
```

3. Model aşağıdakine benzer bir kod üretecektir. (Derste herkesin aynı kodla ilerlemesi için bu kodu kullanın.)

```python
# Kaynak listemiz: Her kaynak bir sözlük (dictionary) olarak tutuluyor.
# Not: Bu veriler örnek amaçlı ve hayalidir.
kaynaklar = [
    {"yazar": "Demir, A.", "yil": 2008, "baslik": "Sofalı Evlerde Gündelik Hayat"},
    {"yazar": "Kaya, B.", "yil": 1995, "baslik": "Anadolu Konutunda Plan Tipleri"},
    {"yazar": "Arslan, C.", "yil": 2016, "baslik": "Apartman ve Orta Sınıf"},
    {"yazar": "Şahin, D.", "yil": 2001, "baslik": "Yüklükten Gardıroba"},
    {"yazar": "Yıldız, E.", "yil": 2019, "baslik": "Misafir Odasının Sosyolojisi"},
    {"yazar": "Çelik, F.", "yil": 1998, "baslik": "Cumba ve Sokak"},
]

# 1. Adım: Kaynakları yıla göre sırala
# sorted() listeyi sıralar; key ile neye göre sıralanacağını söylüyoruz.
sirali_kaynaklar = sorted(kaynaklar, key=lambda kaynak: kaynak["yil"])

print("Kaynaklar (eskiden yeniye):")
for kaynak in sirali_kaynaklar:
    # Her kaynağı "Yazar (Yıl). Başlık." biçiminde yazdır
    print(kaynak["yazar"] + " (" + str(kaynak["yil"]) + "). " + kaynak["baslik"] + ".")

# 2. Adım: Her on yılda kaç kaynak var, say
on_yillar = {}  # Boş bir sözlük: anahtar = on yıl, değer = kaynak sayısı

for kaynak in kaynaklar:
    on_yil = (kaynak["yil"] // 10) * 10  # Örnek: 2008 -> 2000
    if on_yil in on_yillar:
        on_yillar[on_yil] = on_yillar[on_yil] + 1
    else:
        on_yillar[on_yil] = 1

print()
print("On yıllara göre kaynak sayısı:")
for on_yil in sorted(on_yillar):
    print(str(on_yil) + "'ler: " + str(on_yillar[on_yil]) + " kaynak")
```

4. Tarayıcıda colab.research.google.com adresini açın ve Google hesabınızla giriş yapın.
5. **Yeni not defteri** (New notebook) seçeneğine tıklayın.
6. Açılan kod hücresine kodu yapıştırın.
7. **Tahmin sorusu:** Çalıştırmadan önce düşünelim: "Listenin en başında hangi kaynak yazacak? 2000'lerde kaç kaynak var?"
8. Hücrenin solundaki ▶ (çalıştır) düğmesine tıklayın.
9. Çıktıyı inceleyin.

**Beklenen çıktı:**

```text
Kaynaklar (eskiden yeniye):
Kaya, B. (1995). Anadolu Konutunda Plan Tipleri.
Çelik, F. (1998). Cumba ve Sokak.
Şahin, D. (2001). Yüklükten Gardıroba.
Demir, A. (2008). Sofalı Evlerde Gündelik Hayat.
Arslan, C. (2016). Apartman ve Orta Sınıf.
Yıldız, E. (2019). Misafir Odasının Sosyolojisi.

On yıllara göre kaynak sayısı:
1990'ler: 2 kaynak
2000'ler: 2 kaynak
2010'ler: 2 kaynak
```

> **Not:** Türkçede doğrusu "2010'lar"dır, ama program her sayıya aynı `'ler` ekini yapıştırdığı için "2010'ler" yazar. Bilgisayar ses uyumunu bilmez; kod ne söylerse onu yapar. İsterseniz yapay zekâdan bu eki düzelten bir ek kod isteyebilirsiniz (iyi bir ek alıştırma).

#### Kod Nasıl Çalışıyor?

`kaynaklar = [ ... ]`

Köşeli parantez bir **liste** oluşturur. Listenin her elemanı süslü parantez içinde bir **sözlüktür.** Sözlük, bir kütüphane kataloğundaki kart gibidir: "yazar", "yil", "baslik" alanları ve bunların değerleri vardır.

`sirali_kaynaklar = sorted(kaynaklar, key=lambda kaynak: kaynak["yil"])`

`sorted()` listeyi sıralar. `key=lambda kaynak: kaynak["yil"]` kısmı "her kaynağın yıl alanına bakarak sırala" demektir. `lambda`, tek satırlık küçük bir tarif gibidir.

`for kaynak in sirali_kaynaklar:`

Bu bir **döngüdür.** Listedeki her kaynak için alttaki girintili satırları tekrar eder.

`str(kaynak["yil"])`

Yıl bir sayıdır (2008). Metinle (`"("`) birleştirmek için önce `str()` ile metne çeviriyoruz.

`on_yil = (kaynak["yil"] // 10) * 10`

`//` tam sayı bölmesidir: 2008 // 10 = 200. Sonra 200 × 10 = 2000. Böylece yıl, ait olduğu on yıla yuvarlanır.

`if on_yil in on_yillar:`

Bu on yıl sözlükte zaten varsa sayıyı bir artırır, yoksa 1'den başlatır.

#### Kod Üzerinde Değişiklik Yapalım

1. Listeye kendi hayali kaynağınızı ekleyin: `{"yazar": "Aydın, G.", "yil": 2023, "baslik": "Açık Mutfak"},` – Programı tekrar çalıştırın. 2020'ler satırı çıktı mı?
2. **Soru:** `str()` kısmını silip `kaynak["yil"]` yazarsak ne olur?
   - **Cevap:** Hata alırız: `TypeError: can only concatenate str (not "int") to str`. Python, metin ile sayıyı `+` ile birleştiremez.
3. Sıralamayı yeniden eskiye doğru yapmak için modele sorun: "Sıralamayı yeniden eskiye nasıl çeviririm?" (Cevap: `sorted(..., reverse=True)`.)

#### Hata Ayıklama: Hatalı Kodu Düzelttirmek

Aşağıdaki kod hatalıdır. Önce Colab'da çalıştırıp hata mesajını görün:

```python
kaynaklar = [
    {"yazar": "Demir, A.", "yil": 2008},
    {"yazar": "Kaya, B.", "yil": 1995},
]

for kaynak in kaynaklar
    print(kaynak["yazar"] + " (" + kaynak["yil"] + ")")
```

**Tahmin sorusu:** Sizce kaç hata var?

Hata ayıklama promptu:

```text
Aşağıdaki Python kodu çalışmıyor. Aldığım hata mesajı şu:
[hata mesajını buraya yapıştır]

Kod:
[kodu buraya yapıştır]

1. Hatanın nedenini yeni başlayan birine anlatır gibi açıkla.
2. Düzeltilmiş kodun tamamını ver.
3. Kodda başka hata varsa onları da göster.
```

**Beklenen düzeltme:**

```python
kaynaklar = [
    {"yazar": "Demir, A.", "yil": 2008},
    {"yazar": "Kaya, B.", "yil": 1995},
]

for kaynak in kaynaklar:  # 1. hata: for satırının sonunda iki nokta (:) eksikti
    print(kaynak["yazar"] + " (" + str(kaynak["yil"]) + ")")  # 2. hata: sayı str() ile metne çevrilmeli
```

**Beklenen çıktı:**

```text
Demir, A. (2008)
Kaya, B. (1995)
```

**Açıklama:** İlk çalıştırmada Python sadece ilk hatayı (`SyntaxError`, eksik iki nokta) gösterir. Onu düzeltince ikinci hata (`TypeError`) ortaya çıkar. "Başka hata varsa onları da göster" demek, iki hatayı tek turda bulmamızı sağlar.

#### Sık Yapılan Hatalar

**Hata 1: Hata mesajını vermeden "çalışmıyor" demek**

- Hatalı: "Kodum çalışmıyor, düzelt."
- Doğru: Kodu ve hata mesajının tamamını yapıştırın.

**Hata 2: Anlamadığı kodu çalıştırmak**

- Neden hata? Özellikle dosya silen veya değiştiren kodlar veri kaybına yol açabilir; araştırma verisi geri getirilemeyebilir.
- Düzeltme: "Bu kod bilgisayarımda neyi değiştirir?" diye sorun; önce dosyaların kopyası üzerinde deneyin.

**Hata 3: Girinti (boşluk) hatası**

Hatalı:

```python
for kaynak in kaynaklar:
print(kaynak["yazar"])
```

Doğru:

```python
for kaynak in kaynaklar:
    print(kaynak["yazar"])
```

Neden? Python'da döngünün içindeki satırlar 4 boşlukla içeri kaydırılmalıdır.

**Hata 4: Seviye belirtmemek**

- Neden hata? Model ileri seviye, anlaşılması zor kod yazabilir.
- Düzeltme: "Yeni başlayan biri için, açıklamalı" deyin.

---

### Konu 2: Eğitim – Ders Materyali ve Quiz Oluşturma (15 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir araştırma görevlisi, mimarlık fakültesinde "Geleneksel konutta sofa ve plan tipleri" konulu 90 dakikalık bir atölye yürütecek. Bir ders planına, okuma listesine ve kısa bir quize ihtiyacı var.

**Basit açıklama:** Yapay zekâ, bir konu için ders planı, anlatım metni, alıştırma ve quiz hazırlamada hızlı bir yardımcıdır. Dersi veren kişi içeriği kontrol eder ve sınıfına uyarlar.

#### Neden Öğreniyoruz?

- Ders, atölye, seminer hazırlığı,
- Bir makale okuma grubu için tartışma soruları hazırlamak,
- Tez savunmasına hazırlık için olası jüri sorularını çıkarmak,
- Kendi öğrenmenizi test etmek (okuduğunuz makaleden quiz ürettirmek).

#### Birlikte Uygulayalım: Atölye Planı ve Quiz

**Amaç:** Tek bir prompt dizisiyle ders planı ve quiz üretmek.

**Adımlar:**

1. Yeni sohbet açın ve yazın:

```text
## ROL
Sen mimarlık fakültesinde ders veren deneyimli bir öğretim üyesisin.

## BAĞLAM
Mimarlık 2. sınıf öğrencilerine "Geleneksel Türk evinde sofa ve plan tipleri" konulu
90 dakikalık bir atölye yürüteceğim. Öğrenciler plan okuyabiliyor ama konuyu bilmiyor.

## GÖREV
Bir atölye planı hazırla.

## ÇIKTI BİÇİMİ
Tablo: Süre | Etkinlik | Dersi veren ne yapar? | Katılımcılar ne yapar?
Atölyede en az bir eskiz etkinliği ve bir grup tartışması olsun.
Toplam süre tam 90 dakika olsun; sonunda süreleri toplayarak kontrol et.
```

2. Planı inceleyin. Sürelerin toplamı 90 mı?
3. Aynı sohbette quiz isteyin:

```text
Bu atölye için 6 soruluk bir quiz hazırla:
- 3 çoktan seçmeli (4 seçenekli, tek doğru)
- 2 doğru/yanlış
- 1 kısa cevaplı (bir plan şemasını tarif etmelerini isteyen)
Cevap anahtarını ayrı başlık altında ver ve her cevabın neden doğru olduğunu tek cümleyle açıkla.
Sadece genel kabul görmüş bilgilerden soru sor; tartışmalı tarih veya isim sorma.
```

4. Quizi kontrol edin: Her sorunun tek doğru cevabı var mı? Yanlış seçenekler mantıklı mı?
5. Aynı mantıkla tez savunmasına hazırlık için deneyin:

```text
Aşağıdaki tez özetini oku. Bir tez jürisinin sorabileceği 8 soru yaz:
3 yöntem sorusu, 3 bulgu ve yorum sorusu, 2 literatüre katkı sorusu.
Her sorunun yanına jürinin bu soruyla neyi sınadığını tek cümleyle yaz.

Tez özeti:
[özet]
```

**Beklenen sonuç:** 90 dakikalık tablo hâlinde bir atölye planı, cevap anahtarlı 6 soruluk quiz ve olası jüri soruları listesi.

**Açıklama:** "Süreleri toplayarak kontrol et" ifadesi, modelin kendi çıktısını doğrulamasını sağlar (Ders 2'deki adım adım düşünmenin küçük bir uygulaması). "Tartışmalı tarih veya isim sorma" ifadesi uydurma riskini azaltır.

> **Dikkat:** Yapay zekâ quizlerinde en sık hata, birden fazla doğru cevabı olan sorular ve yanlış cevap anahtarıdır. Her soruyu kendiniz cevaplayarak kontrol edin.

---

### Konu 3: Pazarlama – Çağrı Metni, Slogan, SEO İçerikleri (15 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Araştırmacılar her gün onlarca sempozyum çağrısı, proje duyurusu ve yayın bildirimi alır. Bir çağrı metni ilk iki satırda ilgi uyandırmazsa okunmadan geçilir.

**Basit açıklama:** Akademik dünyada "pazarlama", bir çalışmanın, etkinliğin veya projenin doğru kişilere, doğru mesajla ulaşması demektir: sempozyum çağrıları, proje duyuruları, araştırma bloglarının bulunabilirliği. Yapay zekâ bu metinlerin taslaklarını üretmekte çok yardımcıdır.

**Teknik terim – SEO:** Search Engine Optimization, yani **arama motoru optimizasyonu.** Bir web sayfasının Google gibi arama motorlarında, ilgili aramalarda üst sıralarda çıkması için içeriğin düzenlenmesidir.

- **Benzetme:** Bir makalenin doğru anahtar kelimelerle dizinlenmesi gibi. Makale ne kadar iyi olursa olsun yanlış anahtar kelimelerle kaydedildiyse bulunamaz.
- **Neden kullanılır?** Okurların ve araştırmacıların "Türk evi sofa" gibi aramalarda araştırma blogunu veya proje sayfasını bulması için.
- **Temel kavramlar:** Anahtar kelime (insanların aradığı ifade), başlık etiketi (sayfa başlığı), meta açıklama (arama sonucunda görünen kısa özet), ara başlıklar.

> **Not:** Makalelerin kendisi için de benzer bir mantık geçerlidir: Akademik veri tabanları ve Google Scholar, makaleyi başlık, özet ve anahtar kelimelerden bulur. İyi bir başlık ve özet, makalenin bulunabilirliğini artırır.

#### Birlikte Uygulayalım: Sempozyum Duyuru Metin Seti

**Senaryo:** "Konut ve Gündelik Hayat" adlı küçük bir sempozyum düzenleniyor (hayali). Çağrı metni, slogan ve sempozyum web sayfası için içerik hazırlanacak.

**Adımlar:**

1. Yeni sohbet açın.
2. Slogan isteyin:

```text
"Konut ve Gündelik Hayat" adlı disiplinlerarası bir sempozyum için birbirinden farklı 8 slogan öner.
Her biri en fazla 6 kelime olsun.
2'si soru biçiminde, 2'si bir kavramı öne çıkaran, 2'si kelime oyunu içeren, 2'si sade ve ciddi olsun.
"Eşsiz", "muhteşem" kelimelerini kullanma.
```

3. Çağrı metni isteyin:

```text
Bu sempozyum için 2 farklı bildiri çağrısı metni yaz (her biri 120 kelime):
A) Mimarlık ve şehir planlama araştırmacılarına yönelik
B) Sosyoloji, antropoloji ve tarih alanındaki araştırmacılara yönelik
Her metin 4 alt tema içersin ve "Özet gönderim tarihi: [TARİH]" satırıyla bitsin.
Tarih, yer, ücret gibi bilgileri uydurma; köşeli parantezle yer tutucu bırak.
```

4. SEO uyumlu web sayfası planı isteyin:

```text
Sempozyumun web sayfası için SEO uyumlu bir sayfa planı hazırla:
- İnsanların Google'da arayabileceği 5 anahtar kelime öner (ana ve yan anahtar kelimeler)
- 60 karakteri geçmeyen bir sayfa başlığı
- 155 karakteri geçmeyen bir meta açıklama
- 4 ara başlık (en az ikisinde anahtar kelime geçsin)
Karakter sayılarını yanlarına yaz.
```

5. Karakter sayılarını bir karakter sayacıyla (veya Word'ün sözcük sayımı aracıyla) kontrol edin.

**Beklenen sonuç:** 8 slogan, iki farklı akademik topluluğa yönelik 2 çağrı metni, bir SEO sayfa planı.

> **Dikkat:** Modeller karakter ve kelime saymada sık hata yapar (çünkü metni token olarak görür, harf harf değil). Sınırlı alanlar için (meta açıklama, özet) mutlaka kendiniz sayın.

**Not:** Modelin önerdiği anahtar kelimelerin gerçekten aranıp aranmadığı, Google Trends veya anahtar kelime araçlarıyla kontrol edilmelidir. Model gerçek arama hacmi verisine sahip değildir.

---

### Konu 4: Tasarım – Görsel ve Senaryo Üretimi (10 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir araştırma projesinin sonunda bulgular küçük bir sergiyle kamuoyuna sunulacak: "Bir Evin Hafızası: Konutta Gündelik Hayatın Dönüşümü". Serginin mekân kurgusu, ziyaretçi rotası ve panolardaki metinler planlanmalı.

**Basit açıklama:** Tasarım alanında yapay zekâ; konsept geliştirme, senaryo (anlatı akışı) yazma, görsel üretme ve alternatif fikirler üretmede kullanılır. Ders 4'te görsel üretimi gördük; burada **senaryo** kısmına odaklanıyoruz.

**Senaryo nedir?** Tasarımda senaryo, kullanıcının (ziyaretçinin, katılımcının, izleyicinin) deneyimi adım adım nasıl yaşayacağını anlatan kurgudur. Bir film senaryosunun mekân deneyimindeki karşılığıdır.

#### Birlikte Uygulayalım: Araştırma Sergisi Senaryosu

```text
## ROL
Sen deneyimli bir sergi tasarımcısı ve küratörsün.

## BAĞLAM
Bir araştırma projesinin bulgularını sunan küçük bir sergi tasarlıyorum:
"Bir Evin Hafızası: Konutta Gündelik Hayatın Dönüşümü". Alan: 120 m², dikdörtgen, tek giriş.
Sergi, geleneksel evden apartmana dönüşümü araştırmanın bulguları üzerinden anlatacak.
Malzeme: plan çizimleri, dönem dergilerinden ilanlar, sözlü tarih görüşmelerinden kısa ses kayıtları.
Bütçe düşük.

## GÖREV
Bir ziyaretçi deneyimi senaryosu yaz.

## ÇIKTI BİÇİMİ
- 5 durak. Her durak için: Durak adı | Ziyaretçi ne görür? | Ne duyar veya ne yapar? |
  Hangi araştırma malzemesi kullanılır? | Pano metni (en fazla 40 kelime)
- Ziyaretçinin rotasını tek paragrafta tarif et.
- Düşük bütçe için 3 öneri.
- Pano metinlerinde verilen malzemede olmayan bulgu iddiası kullanma.
```

Ardından bir durağın atmosfer görselini Ders 3'teki stil rehberiyle üretin.

**Beklenen sonuç:** 5 duraklı bir sergi senaryosu tablosu, rota açıklaması ve bir durağın görseli.

---

### Grup / Bireysel Çalışma: Kendi Alanına Yönelik Prompt Seti (15 dk)

> Bu çalışmada her katılımcı kendi çalışma alanına yönelik bir prompt seti geliştirir.

#### Sıra Sizde 1

**Amaç:** Bütün teknikleri kendi iş akışına uygulamak.

**Görev:** Kendi akademik çalışma alanınız için 5 promptluk bir **prompt seti** hazırlayın. Her prompt, iş akışınızda gerçekten tekrar eden bir işi çözmeli.

**İstenenler:**

- Her prompt için: Adı, ne zaman kullanılır, prompt metni (bağlam + rol + görev + çıktı biçimi), değiştirilecek yerler köşeli parantezle işaretli.
- En az bir promptta few-shot örnek kullanın.
- En az bir promptta adım adım düşünme kullanın.
- Her promptu bir kez deneyin.

**Beklenen sonuç:** Prompt Defterim'e eklenen, tekrar kullanılabilir 5 prompt.

**İpucu:** Geçen haftanızı düşünün: Hangi işi üç kez yaptınız?

#### Çözüm – Örnek Prompt Seti (Akademik Çalışma)

| No | Prompt adı | Ne zaman? |
|---|---|---|
| 1 | Makale okuma notu | Her yeni makale okunduğunda (Ders 2 şablonu) |
| 2 | Terim tutarlılık kontrolü | Her bölüm veya makale taslağı bittiğinde (Ders 3 terimler sözlüğü) |
| 3 | Makale yapı planı eleştirisi | Yeni bir makaleye başlarken |
| 4 | Sunum görsel serisi | Konferans sunumu veya poster için (Ders 4 sabit kısım) |
| 5 | Hakem yanıt mektubu taslağı | Revizyon sürecinde hakem yorumlarına yanıt verirken |

Prompt 3 örneği (adım adım düşünme):

```text
Aşağıdaki makale yapı planını değerlendir. Şu adımları izle:
1. Makalenin araştırma sorusunu tek cümleyle yaz.
2. Her bölümün bu soruya katkısını değerlendir.
3. Eksik kalan bir bölüm veya tartışma var mı (örneğin sınırlılıklar)?
4. Bölüm sırası mantıklı mı?
5. En önemli 3 öneriyi madde madde yaz.
Övgüye yer verme.

Yapı planı:
[plan]
```

Prompt 5 örneği (few-shot):

```text
Aşağıdaki hakem yorumuna, örnekteki biçimi izleyerek kibar, net ve yapılan değişikliği
gösteren bir yanıt taslağı yaz. Yapmadığım bir değişikliği yapmış gibi gösterme;
yapılan değişiklik için [YAPILAN DEĞİŞİKLİK] yer tutucusu bırak.

Örnek:
Hakem yorumu: "Yöntem bölümünde örneklemin nasıl seçildiği açık değil."
Yanıt: "Değerli yorumunuz için teşekkür ederiz. Örneklem seçim ölçütleri Yöntem bölümüne
(s. 7) eklenmiştir: [YAPILAN DEĞİŞİKLİK]."

Şimdi bu yoruma yanıt yaz:
[hakem yorumu]
```

> **Dikkat:** Hakem yanıtı yazarken size gelen hakem raporunu yapay zekâ aracına yapıştırmadan önce derginin politikasını kontrol edin. Raporun yalnızca ilgili yorumunu, kişisel bilgi içermeden kullanmak daha güvenlidir.

---

### Konu 5: Yapay Zekâ Ajanları Nedir? Ajanların Özellikleri (15 dk)

#### Konu Nedir?

**Günlük hayat örneği:** İki farklı yardımcı düşünün.

- **Birinci yardımcı (sohbet botu):** Ona "Bu hafta hangi makaleleri okumalıyım?" diye sorarsınız; size bir öneri söyler. Gerisini siz yaparsınız.
- **İkinci yardımcı (ajan):** Ona "Bu hafta konut ve gündelik hayat konusunda yeni yayımlanan makaleleri bul, özetlerini çıkar, literatür tablomun sonuna ekle ve bana cuma günü özet gönder" dersiniz. O da arama yapar, dosyaları açar, tabloyu günceller ve size haber verir.

İkinci yardımcı bir **ajan**dır.

**Basit açıklama:** Yapay zekâ ajanı, bir hedefi gerçekleştirmek için kendi başına adım planlayan, araç kullanan (web araması, dosya okuma, e-posta, takvim gibi) ve sonucu kontrol ederek ilerleyen yapay zekâ sistemidir.

**Teknik tanım:** Yapay zekâ ajanı (AI agent); bir dil modelini karar mekanizması olarak kullanan, çevresinden bilgi alıp (algı), araçlar aracılığıyla eylemde bulunan (eylem), sonuçları gözlemleyerek bir sonraki adımı belirleyen (döngü) ve belirli bir hedefe ulaşana kadar bu döngüyü sürdüren yazılımdır.

#### Sohbet Botu ile Ajan Arasındaki Fark

| Özellik | Sohbet botu | Yapay zekâ ajanı |
|---|---|---|
| Ne yapar? | Soruya cevap verir | Görevi yerine getirir |
| Araç kullanımı | Yok veya sınırlı | Web, dosya, e-posta, takvim, tablo vb. |
| Adım sayısı | Genelde tek adım | Çok adımlı, kendi planlar |
| Özerklik | Her adımda sizin isteğinizi bekler | Belirlenen sınırlar içinde kendi ilerler |
| Hafıza | Sohbetle sınırlı | Kalıcı bilgi tabanı / hafıza olabilir |
| Benzetme | Danışabileceğiniz bilgili bir meslektaş | İş verebileceğiniz bir araştırma asistanı |

#### Ajanların Özellikleri

**1. Hedef odaklılık**

- Basit açıklama: Ajan tek bir soruya değil, bir hedefe çalışır.
- Örnek: "Sempozyum katılımcılarının sorularını SSS dosyasına göre cevapla."

**2. Talimatlar (sistem mesajı)**

- Basit açıklama: Ajanın kimliği, kuralları ve sınırları. Ders 3'te öğrendiğimiz sistem talimatı ajanın "iş tanımı"dır.

**3. Bilgi tabanı (knowledge)**

- Basit açıklama: Ajanın başvurduğu dosyalar.
- Örnek: Sempozyumun SSS dosyası, programı, yazım kuralları.

**4. Araçlar (tools)**

- Basit açıklama: Ajanın dış dünyada iş yapmasını sağlayan yetenekler.
- Örnek: Web araması, Google Drive'dan dosya okuma, e-posta gönderme, tabloya satır ekleme.

**5. Planlama ve döngü**

- Basit açıklama: Ajan görevi adımlara böler, bir adımı yapar, sonucu görür, sonraki adıma karar verir.

**6. Hafıza**

- Basit açıklama: Önceki etkileşimleri veya bilgileri hatırlama.

**7. Sınırlar ve insan onayı**

- Basit açıklama: Ajanın ne yapamayacağı ve hangi adımlarda insandan onay isteyeceği.
- Örnek: "Katılımcılara e-posta göndermeden önce taslağı bana göster."

> **Dikkat:** Ajanlar ne kadar çok araca ve özerkliğe sahipse, hata yaptıklarında etkisi o kadar büyük olur. Ajanlara özellikle **dosya silme, para harcama, adınıza e-posta gönderme** gibi yetkileri dikkatle verin ve önemli adımlarda onay isteyin. Ayrıca ajanın okuduğu web sayfaları veya dosyalar içinde gizlenmiş kötü niyetli talimatlar olabileceğini (buna "prompt injection" denir) unutmayın.

**Soru:** Bir sempozyum katılımcı destek asistanının hangi araçlara ihtiyacı olur? Hangi yetkiler ona verilmemeli?

**Cevap:** Sempozyumun SSS dosyasını ve programını okuma yeterlidir. Bildiri kabul veya ret kararı bildirme, ücret indirimi verme, düzenleme kurulu adına söz verme veya katılımcıların kişisel bilgileriyle işlem yapma yetkisi verilmemelidir.

---

### Konu 6: Platform Tanıtımı, Low-Code ve No-Code Platformlar (15 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir anket yapmanın üç yolu olduğunu düşünün:

- **Hazır anket aracı (no-code):** Formu sürükle-bırak ile kurar, bağlantıyı paylaşırsınız. Hızlı ama esnekliği sınırlı.
- **Hazır araç + biraz özelleştirme (low-code):** Ana yapı hazır, ama bazı hesaplamaları veya mantık kurallarını kendiniz eklersiniz.
- **Kendi yazılımınız (kod):** Tam esneklik ama uzmanlık ve zaman gerektirir.

**Basit açıklama:**

- **No-code (kodsuz) platform:** Hiç kod yazmadan, menüler, formlar ve sürükle-bırak ile yapay zekâ asistanı veya otomasyon kurmayı sağlar.
- **Low-code (az kodlu) platform:** Çoğu iş görsel arayüzle yapılır, gerektiğinde küçük kod parçaları eklenir.
- **Kodlu yaklaşım (API):** Her şeyi programlayarak yaparsınız. Ders 6'nın konusu.

#### Platform Türleri

| Tür | Örnek platformlar | Ne için uygun? | Seviye |
|---|---|---|---|
| Sohbet tabanlı özel asistan | ChatGPT projeleri ve özel asistanları, Claude Projects, Gemini Gems | Talimat + dosyalarla çalışan kişisel asistan | No-code |
| Kaynak temelli araştırma asistanı | Google NotebookLM | Yüklediğiniz kaynaklara dayanarak soru cevaplama, özet, sesli özet | No-code |
| Ajan modu | Sohbet uygulamalarının web'de gezinip görev yapabilen ajan özellikleri | Çok adımlı web görevleri | No-code |
| İş akışı otomasyonu | Zapier, Make, n8n | "Şu olunca şunu yap" zincirleri, yapay zekâ adımlarıyla | No-code / Low-code |
| Kurumsal ajan oluşturucular | Microsoft Copilot Studio, Google'ın kurumsal ajan araçları | Kurum içi bilgiyle çalışan ajanlar | Low-code |

> **Not:** Bu alan çok hızlı değişiyor; platformların adları, fiyatları ve özellikleri sık güncelleniyor. Kullanmadan önce platformun güncel belgelerine bakın. Ayrıca üniversitenizin hangi araçları onayladığını ve araştırma verileri için hangi kuralları koyduğunu kontrol edin. Kavramlar (talimat, bilgi tabanı, araç, tetikleyici) ise platformdan bağımsızdır.

#### İş Akışı Otomasyonunun Mantığı

Zapier, Make ve n8n gibi platformlar şu mantıkla çalışır:

```text
TETİKLEYİCİ (Trigger)  →  EYLEM 1  →  EYLEM 2  →  ...
"Bir şey olduğunda"       "şunu yap"   "sonra şunu yap"
```

**Araştırmacı için örnek akış:**

```text
Tetikleyici: Google Drive'daki "Okunacaklar" klasörüne yeni bir PDF eklendi
Eylem 1:     PDF'in metnini çıkar
Eylem 2:     Yapay zekâ adımı: Ders 2'deki okuma notu promptuyla özetle
Eylem 3:     Özeti Google Sheets'teki "Literatür Tablosu"na yeni satır olarak ekle
Eylem 4:     Bana "Yeni okuma notu hazır" e-postası gönder
```

**Soru:** Bu akışta prompt mühendisliği bilgisi nerede kullanılıyor?

**Cevap:** Eylem 2'deki yapay zekâ adımında. Otomasyonun kalitesi, o adıma yazılan promptun kalitesine bağlıdır. Kötü bir promptla kurulan otomasyon, her yeni PDF'de kötü sonucu otomatik olarak tekrarlar.

---

### Uygulama: Basit Yapay Zekâ Ajanı Oluşturma (25 dk)

#### Birlikte Uygulayalım: Sempozyum Katılımcı Destek Asistanı

**Amaç:** Kod yazmadan; talimat, bilgi tabanı ve sınırlarla çalışan bir müşteri hizmetleri (katılımcı destek) asistanı kurmak.

**Senaryo:** "Konut ve Gündelik Hayat Sempozyumu" (hayali) için çağrı yayımlandı. Düzenleme kuruluna her gün benzer sorular geliyor: "Özet gönderim tarihi ne zaman?", "Özet kaç kelime olmalı?", "Çevrim içi katılım var mı?", "Bildiriler yayımlanacak mı?" Düzenleme kurulu bu soruları cevaplayan bir asistan istiyor.

**Problem nedir?** Tekrarlayan soruları hızlı, tutarlı ve doğru cevaplamak; bilinmeyen sorularda uydurmamak; kabul/ret gibi kurul kararlarına karışmamak.

**Nasıl çözeceğiz?** Bir SSS dosyası hazırlayıp, talimatlarla birlikte bir özel asistana (Gem / proje) yükleyeceğiz.

**Hangi bilgileri kullanacağız?** Sempozyum bilgileri, tarihler, kurallar, iletişim bilgileri (dersteki örnekte hayali).

**Adımlar:**

1. Bilgisayarda bir metin dosyası açın, adını `sss_sempozyum.txt` koyun ve aşağıdaki içeriği yazın (bilgiler hayalidir):

```text
KONUT VE GÜNDELİK HAYAT SEMPOZYUMU – SIK SORULAN SORULAR (HAYALİ)

Genel bilgiler
- Sempozyumun adı: Konut ve Gündelik Hayat Sempozyumu
- Tarih: 12–13 Mart, İstanbul (yüz yüze)
- Çevrim içi katılım: Yalnızca dinleyici olarak mümkündür; bildiri sunumu yüz yüze yapılır.
- Alt temalar: Geleneksel konut; Apartmanlaşma; Kentsel dönüşüm; Konut ve toplumsal cinsiyet

Bildiri özeti
- Özet gönderim son tarihi: 15 Aralık
- Özet uzunluğu: 250–300 kelime, Türkçe veya İngilizce
- Özette amaç, yöntem, bulgular ve sonuç yer almalıdır.
- Kabul sonuçları: 15 Ocak'ta e-posta ile bildirilir.

Yayın
- Kabul edilen bildirilerin genişletilmiş özetleri bildiri kitabında yayımlanacaktır.

İletişim
- Sorular için: sempozyum@ornek-universite.edu.tr (hayali)
```

2. Talimat metnini hazırlayın:

```text
# KİMLİK
Sen "Konut ve Gündelik Hayat Sempozyumu"nun katılımcı destek asistanısın. Katılımcıların sorularını
kibar, kısa ve net bir dille cevaplarsın.

# BİLGİ KAYNAĞI
Sadece yüklenen "sss_sempozyum.txt" dosyasındaki bilgileri kullan.

# KURALLAR
1. Dosyada olmayan bir bilgi sorulursa uydurma. Şunu söyle: "Bu konuda elimde bilgi yok.
   Lütfen sempozyum@ornek-universite.edu.tr adresine yazın."
2. Bildiri kabul veya ret konusunda hiçbir tahmin ve söz verme; kararların düzenleme kurulu
   tarafından verildiğini söyle.
3. Ücret, indirim veya son tarih uzatması konusunda söz verme.
4. Bir bildiri özetinin içeriği değerlendirilmesi istenirse değerlendirme yapma; özetin
   uzunluk ve yapı kurallarını hatırlat.
5. Cevapların 3 cümleyi geçmesin.
6. Katılımcı hangi dilde yazarsa o dilde cevap ver.
```

3. Platformda asistanı oluşturun (kullandığınız araca göre):
   - **Gemini:** Gem yöneticisinden yeni Gem oluşturun → Ad: "Sempozyum Katılımcı Destek" → Talimatlar alanına talimatı yapıştırın → Bilgi (knowledge) bölümüne SSS dosyasını yükleyin → Kaydedin.
   - **ChatGPT:** Yeni bir proje oluşturun → Proje talimatlarına talimatı yapıştırın → Proje dosyalarına SSS dosyasını ekleyin.
   - **Claude:** Yeni bir proje oluşturun → Proje talimatlarına yapıştırın → Proje bilgisine SSS dosyasını ekleyin.
4. Asistanı test edin. Aşağıdaki test sorularını tek tek sorun ve sonuçları tabloya yazın:

| No | Test sorusu | Beklenen davranış | Gerçekleşen | Doğru mu? |
|---|---|---|---|---|
| 1 | Özet son tarihi ne zaman? | 15 Aralık | | |
| 2 | Çevrim içi sunum yapabilir miyim? | Hayır; çevrim içi yalnızca dinleyici | | |
| 3 | Katılım ücreti ne kadar? | Bilgi yok, iletişim adresine yönlendir | | |
| 4 | Özetim kabul edilir mi sizce? | Tahmin ve söz vermez; kararı kurul verir | | |
| 5 | Son tarihi bir hafta uzatabilir misiniz? | Söz vermez, iletişim adresine yönlendirir | | |
| 6 | Can I submit my abstract in English? | İngilizce cevap: Evet, Türkçe veya İngilizce | | |
| 7 | Şu özetimi değerlendirir misin? | Değerlendirme yapmaz; uzunluk ve yapı kurallarını hatırlatır | | |

5. **Tahmin sorusu:** "Katılım ücreti ne kadar?" sorusunda asistan ne yapacak?
6. Hatalı davranan bir test varsa talimatı güncelleyin. Örneğin asistan 3. soruda tahmini bir ücret verirse:

```text
7. Ücret sorulursa kesinlikle tahmini bir tutar verme; iletişim adresine yönlendir.
```

7. Talimatı kaydedip başarısız olan testi tekrar çalıştırın.

**Beklenen sonuç:** 7 testin hepsinde beklenen davranışı gösteren bir katılımcı destek asistanı.

**Açıklama:** Kod yazmadan bir müşteri hizmetleri asistanı kurduk. Asistanın üç bileşeni vardı: **talimat** (kimlik ve kurallar), **bilgi tabanı** (SSS dosyası) ve **test** (beklenen davranış tablosu). Özellikle 3, 4, 5 ve 7 numaralı testler, asistanın bilmediği şeyi uydurmamasını ve yetkisi olmayan konularda (kabul kararı, süre uzatma, bilimsel değerlendirme) söz vermemesini kontrol etti. Bu test tablosu, gerçek hayatta bir asistan yayına alınmadan önce mutlaka yapılması gereken bir **kalite kontrolüdür.**

#### Sıra Sizde 2 (Ders sonunda veya evde, 20 dk): Araştırma Asistanı Ajanı

**Amaç:** Kendi araştırma süreci için bilgi tabanlı bir asistan kurmak.

**Görev:** Okuduğunuz 3–5 makalenin PDF'ini (veya okuma notlarınızı) yükleyerek bir "Araştırma Asistanı" kurun.

**İstenenler:**

- Talimatta: Yalnızca yüklenen kaynaklara dayan; her bilgide hangi kaynaktan geldiğini belirt; kaynaklarda yoksa "yüklenen kaynaklarda yok" de.
- En az 5 test sorusu hazırlayın; bunlardan 2'si kaynaklarda **olmayan** bir bilgi sorsun.
- Testleri tabloya kaydedin.

**Beklenen sonuç:** Kaynak belirterek cevap veren, kaynaklarda olmayan bilgiyi uydurmayan bir araştırma asistanı.

**İpucu:** Google NotebookLM bu iş için özellikle uygundur, çünkü cevaplarında yüklenen kaynaklara atıf gösterir. Gem veya proje de kullanılabilir.

#### Çözüm

Talimat:

```text
# KİMLİK
Sen bu literatür taramasının araştırma asistanısın.

# KURALLAR
1. Sadece yüklenen kaynakları kullan. Genel bilgini kullanma.
2. Her bilginin sonunda parantez içinde kaynağın dosya adını yaz. Örnek: (Kaya_1995.pdf)
3. Kaynaklarda olmayan bir şey sorulursa: "Yüklenen kaynaklarda bu bilgi yok." de ve
   başka bir şey ekleme.
4. Kaynaklar arasında çelişki varsa iki görüşü de kaynağıyla birlikte göster.
5. Doğrudan alıntı yaparken kaynaktaki ifadeyi değiştirme ve tırnak içinde ver.
```

Test tablosu örneği:

| No | Soru | Beklenen |
|---|---|---|
| 1 | Kaynaklarda sofa hangi işlevleriyle anlatılıyor? | Kaynak adıyla cevap |
| 2 | Hangi kaynak apartmanlaşmadan bahsediyor? | Dosya adlarıyla liste |
| 3 | Kaynaklar arasında görüş ayrılığı var mı? | Varsa iki görüş + kaynak |
| 4 | İzmir'deki Levanten evleri hakkında ne deniyor? (kaynaklarda yoksa) | "Yüklenen kaynaklarda bu bilgi yok." |
| 5 | Sedad Hakkı Eldem'in doğum yılı nedir? (kaynaklarda yoksa) | "Yüklenen kaynaklarda bu bilgi yok." |

#### Sık Yapılan Hatalar

**Hata 1: Asistanı test etmeden kullanmak veya paylaşmak**

- Neden hata? Asistan uydurabilir veya yetkisi olmayan sözler verebilir.
- Düzeltme: Beklenen davranış tablosuyla test edin; özellikle "bilmediği" sorularla.

**Hata 2: Bilgi tabanını güncellememek**

- Neden hata? Son tarih uzatıldı ama SSS dosyası eski kaldıysa asistan yanlış bilgi verir.
- Düzeltme: Bilgi değiştiğinde dosyayı güncelleyin ve yeniden yükleyin.

**Hata 3: Talimatta sadece "yapılacakları" yazmak**

- Neden hata? "Yapılmayacaklar" (ücret söyleme, uydurma, kabul sözü verme) yazılmazsa model varsayılan olarak yardımcı olmaya çalışıp sınırları aşabilir.
- Düzeltme: Kurallar bölümüne açık sınırlar ekleyin.

**Hata 4: Kişisel veya gizli belgeleri düşünmeden yüklemek**

- Neden hata? Paylaşılan bir asistana yüklenen dosyaların içeriği (örneğin katılımcı listesi, hakem raporları), asistanı kullanan diğer kişilere sızabilir.
- Düzeltme: Paylaşılacak asistanlara yalnızca kamuya açık olabilecek bilgileri yükleyin.

---

### Ders Özeti

Bu derste prompt tekniklerini dört farklı alana uyguladık. Yazılımda, Türkçe tarif ettiğimiz bir işi Python koduna dönüştürdük, Google Colab'da çalıştırdık, kodu değiştirdik ve hatalı bir kodu hata mesajıyla birlikte düzelttirdik. Eğitimde atölye planı, quiz ve olası tez jürisi soruları; akademik iletişimde sempozyum sloganı, çağrı metni ve SEO planı; tasarımda bir araştırma sergisi senaryosu ürettik. Ardından kendi akademik iş akışımıza özel bir prompt seti hazırladık. Dersin ikinci yarısında yapay zekâ ajanlarını tanıdık: Hedefe göre çalışan, araç kullanan, planlayan ve sınırlar içinde hareket eden sistemler. No-code ve low-code platformları ve otomasyon mantığını öğrendik. Son olarak kod yazmadan bir sempozyum katılımcı destek asistanı kurduk ve onu bir test tablosuyla kontrol ettik.

### Bu Derste Neler Öğrendik?

- Kod isteme promptunun bileşenlerini (dil, girdi, işlem, çıktı, seviye) öğrendik.
- Python'da liste, sözlük, döngü ve sıralama kavramlarını bir örnek üzerinden gördük.
- Google Colab'da kod çalıştırdık ve hatalı kodu hata mesajıyla düzelttirdik.
- Atölye planı, quiz ve tez jürisi soruları ürettik; süre ve cevap anahtarını kontrol ettik.
- SEO kavramını ve modellerin karakter saymadaki zayıflığını öğrendik.
- Bir araştırma sergisi senaryosu yazdırdık.
- Kendi alanımıza özel 5 promptluk bir set hazırladık.
- Sohbet botu ile ajan arasındaki farkı ve ajanların 7 özelliğini öğrendik.
- No-code, low-code ve kodlu yaklaşımın farkını ve otomasyon mantığını (tetikleyici → eylem) gördük.
- Kod yazmadan bir katılımcı destek asistanı kurup test ettik.

### Mini Quiz

1. **(Kod çıktısı tahmini)** Aşağıdaki kodun çıktısı nedir?

```python
yil = 2008
on_yil = (yil // 10) * 10
print(on_yil)
```

2. **(Kısa cevap)** Aşağıdaki kod neden hata verir?

```python
yil = 1995
print("Yayın yılı: " + yil)
```

3. **(Çoktan seçmeli)** SEO'nun amacı nedir?
   - a) Görselleri büyütmek
   - b) Sayfanın arama motorlarında ilgili aramalarda üst sıralarda çıkmasını sağlamak
   - c) Metni başka dile çevirmek
   - d) Kodu hızlandırmak
4. **(Doğru / Yanlış)** Dil modelleri karakter saymada her zaman kusursuzdur.
5. **(Kısa cevap)** Bir yapay zekâ ajanını sohbet botundan ayıran iki özelliği yazın.
6. **(Çoktan seçmeli)** "Google Drive'a yeni PDF eklenince özetle ve tabloya ekle" gibi akışlar hangi tür platformla kurulur?
   - a) Görsel üretim aracı
   - b) İş akışı otomasyon platformu (Zapier, Make, n8n gibi)
   - c) Kelime işlemci
   - d) Video düzenleyici
7. **(Küçük problem)** Katılımcı destek asistanına "Sempozyumda konaklama ayarlanıyor mu?" diye soruldu ve SSS'de bu bilgi yok. Asistan ne yapmalıdır? Talimattaki hangi kural bunu sağlar?
8. **(Doğru / Yanlış)** No-code platformlarda yapay zekâ adımının kalitesi yine yazılan promptun kalitesine bağlıdır.

### Mini Quiz Cevapları

1. `2000` (2008 // 10 = 200; 200 × 10 = 2000)
2. `yil` bir sayıdır (int); metinle `+` ile birleştirilemez. `str(yil)` kullanılmalıdır: `print("Yayın yılı: " + str(yil))`
3. **b.**
4. **Yanlış.** Modeller metni token olarak işlediği için karakter ve kelime saymada hata yapabilir.
5. Araç kullanabilmesi, çok adımlı planlama yapabilmesi, belirli sınırlar içinde özerk hareket etmesi, kalıcı bilgi tabanı/hafıza (herhangi ikisi).
6. **b.**
7. Bilgi uydurmamalı ve "Bu konuda elimde bilgi yok, lütfen iletişim adresine yazın" diyerek yönlendirmelidir. Bunu talimattaki 1. kural (dosyada olmayan bilgiyi uydurma, iletişim adresine yönlendir) sağlar.
8. **Doğru.**

### Ders Sonu Uygulaması

**Senaryo:** Bir literatür taraması boyunca okunan kaynakları takip etmek için bir "Literatür Takip Sistemi" kurulacak. Bu sistem; küçük bir kod, bir prompt ve bir asistanın birleşimi olacak.

**Yapılacaklar:**

1. Yapay zekâya, bu dersteki kaynakça kodunu genişleten bir kod yazdırın: Her kaynağa `"tema"` alanı eklensin (örneğin "Sofa", "Mutfak") ve program her tema için kaç kaynak olduğunu yazdırsın.
2. Kodu Colab'da çalıştırın; hata alırsanız hata ayıklama promptuyla düzelttirin.
3. Programın çıktısına bakarak en az kaynağı olan temayı belirleyin.
4. Sıra Sizde 2'deki araştırma asistanına, bu tema için hangi alt konularda kaynak eksik olduğunu sorun.
5. Bu eksik alt konular için Ders 1'deki anahtar kelime promptunu kullanarak arama kelimeleri ürettirin.

**Beklenen sonuç:** Temalara göre kaynak sayısını gösteren çalışan bir kod, literatürde zayıf kalan temanın tespiti ve o tema için arama stratejisi.

**İpuçları:**

- Kod promptunda "on yıllara göre sayma kısmını temalara göre sayma ile değiştir" diyebilirsiniz.
- Sözlükle sayma mantığı aynıdır; sadece anahtar `on_yil` yerine `tema` olur.

### Ders Sonu Uygulaması – Çözüm

```python
# Kaynak listemiz: Her kaynağa "tema" alanı eklendi. (Veriler hayalidir.)
kaynaklar = [
    {"yazar": "Demir, A.", "yil": 2008, "baslik": "Sofalı Evlerde Gündelik Hayat", "tema": "Sofa"},
    {"yazar": "Kaya, B.", "yil": 1995, "baslik": "Anadolu Konutunda Plan Tipleri", "tema": "Sofa"},
    {"yazar": "Arslan, C.", "yil": 2016, "baslik": "Apartman ve Orta Sınıf", "tema": "Apartman"},
    {"yazar": "Şahin, D.", "yil": 2001, "baslik": "Yüklükten Gardıroba", "tema": "Odalar"},
    {"yazar": "Yıldız, E.", "yil": 2019, "baslik": "Misafir Odasının Sosyolojisi", "tema": "Salon"},
    {"yazar": "Çelik, F.", "yil": 1998, "baslik": "Cumba ve Sokak", "tema": "Sofa"},
    {"yazar": "Aydın, G.", "yil": 2023, "baslik": "Açık Mutfak", "tema": "Mutfak"},
]

# Her temada kaç kaynak var, say
tema_sayilari = {}  # anahtar = tema adı, değer = kaynak sayısı

for kaynak in kaynaklar:
    tema = kaynak["tema"]
    if tema in tema_sayilari:
        tema_sayilari[tema] = tema_sayilari[tema] + 1
    else:
        tema_sayilari[tema] = 1

print("Temalara göre kaynak sayısı:")
for tema in tema_sayilari:
    print(tema + ": " + str(tema_sayilari[tema]) + " kaynak")

# En az kaynağı olan temayı bul
en_az_tema = ""
en_az_sayi = 1000  # Başlangıçta çok büyük bir sayı veriyoruz

for tema in tema_sayilari:
    if tema_sayilari[tema] < en_az_sayi:
        en_az_sayi = tema_sayilari[tema]
        en_az_tema = tema

print()
print("En az kaynağı olan tema: " + en_az_tema + " (" + str(en_az_sayi) + " kaynak)")
```

**Beklenen çıktı:**

```text
Temalara göre kaynak sayısı:
Sofa: 3 kaynak
Apartman: 1 kaynak
Odalar: 1 kaynak
Salon: 1 kaynak
Mutfak: 1 kaynak

En az kaynağı olan tema: Apartman (1 kaynak)
```

**Kod Nasıl Çalışıyor?**

- `tema_sayilari` sözlüğü, ders içindeki `on_yillar` sözlüğüyle aynı mantıkla çalışır: Tema adı ilk kez görülürse 1 ile başlatılır, sonra her görüldüğünde 1 artırılır.
- `en_az_sayi = 1000` satırında başlangıç değeri olarak çok büyük bir sayı verdik. Döngü her temayı bununla karşılaştırır; daha küçük bir sayı bulunca onu yeni "en az" olarak kaydeder.
- Birden fazla temanın sayısı eşitse (burada 1), ilk karşılaşılan (Apartman) seçilir. `<` yerine `<=` kullanılırsa son karşılaşılan (Mutfak) seçilirdi.

**Adım 4 promptu:**

```text
Literatür taramamda "Apartman" teması için elimde sadece 1 kaynak var. Yüklenen kaynaklara bakarak
bu temanın hangi alt konularının hiç desteklenmediğini listele. Sonra bu alt konular için
genel bilgine dayanarak (kaynak adı vermeden) hangi tür kaynaklara (dönem dergileri, imar
mevzuatı, tezler, plan arşivleri) bakmam gerektiğini öner.
```

**Adım 5:** Ders 1'deki anahtar kelime promptu, "Apartman" temasına uyarlanarak kullanılır.

> **Sonraki derste:** Bugün kod yazmadan bir asistan kurduk. Bir sonraki ve son derste perdenin bir katmanını daha kaldıracağız: **API** ile yapay zekâya doğrudan kendi programımızdan bağlanacağız. Bilgisayarımıza Python ve Anaconda'yı kuracak, OpenAI API ile ilk sohbetimizi yapacak, birden fazla makale özetini tek seferde okuma notuna çeviren bir program yazacak, fine-tuning verisinin nasıl hazırlandığını görecek ve kendi **chatbot'umuzu** yazacağız. Kursu bütün dersleri birleştiren bir final projesiyle bitireceğiz.
