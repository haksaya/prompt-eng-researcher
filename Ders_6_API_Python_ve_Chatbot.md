# Prompt Mühendisliği Eğitimi – Ders 6

## API ile Yapay Zekâ: Python Kurulumu, OpenAI API, Fine-Tuning Verileri ve Chatbot Yapımı (Yaklaşık 2,5 Saat)

> **Bu dosyanın yapısı:** İlk bölüm 150 dakikalık Ders 6'dır. Dosyanın sonunda kursun tamamını kapsayan **Genel Tekrar, Final Mini Projesi ve Ek Alıştırmalar** yer alır. Bu bölümler ders süresinin dışında, ödev veya ek çalışma olarak planlanmıştır.

---

## Ders 6 – 150 Dakika

### Önceki Dersle Bağlantı

Önceki derste yapay zekâyı farklı alanlara uyguladık, Google Colab'da ilk Python kodlarımızı çalıştırdık ve kod yazmadan bir sempozyum katılımcı destek asistanı kurduk. O asistanın üç bileşeni vardı: **talimat, bilgi tabanı ve test.**

Bu derste aynı asistanı bu kez **kendi programımızla** kuracağız. Bunun için yapay zekâya bir web sitesi üzerinden değil, **API** adı verilen bir kapıdan bağlanacağız. Bilgisayarımıza Python'u kuracak, OpenAI API ile ilk sohbetimizi yapacak, Ders 3'te öğrendiğimiz sistem talimatını kodla verecek, birden fazla makale özetini tek seferde okuma notuna dönüştürecek, fine-tuning (ince ayar) verisinin nasıl hazırlandığını görecek ve sonunda kendi **chatbot'umuzu** yazacağız. Böylece kurs boyunca öğrendiğimiz her şey programlarımızda birleşecek.

### Dersin Hedefleri

Bu dersin sonunda öğrenci:

- API kavramını günlük hayattan bir benzetmeyle açıklayabilecek.
- OpenAI API'nin ne olduğunu, ChatGPT'den farkını ve nasıl ücretlendirildiğini bilecek.
- Anaconda ile Python kurup bir çalışma ortamı oluşturabilecek.
- API anahtarını güvenli şekilde saklayabilecek.
- OpenAI API ile ilk isteği gönderip cevabı ekrana yazdırabilecek.
- API'de talimat (sistem mesajı), model seçimi ve token kullanımı kavramlarını uygulayabilecek.
- Fine-tuning için eğitim verisinin (JSONL) nasıl hazırlandığını bilecek; ince ayar işini başlatma, izleme ve modeli silme adımlarını tanıyacak.
- Sohbet geçmişini hatırlayan basit bir chatbot yazabilecek.

### Süre Planı

| Bölüm | Süre |
|---|---|
| Giriş ve önceki dersin tekrarı | 5 dk |
| Konu 1: API nedir? OpenAI API nedir? | 20 dk |
| Konu 2: Gerekli kurulumlar (Python / Anaconda, API anahtarı) | 25 dk |
| Konu 3: API ile ilk chat | 25 dk |
| Konu 4: OpenAI API detayları (talimat, model, token, dosyadan okuma) | 15 dk |
| Konu 5: Fine-tuning verileri | 15 dk |
| Konu 6: Modeli gözlemlemek ve silmek | 10 dk |
| Uygulama: GPT API ile chatbot yapımı | 30 dk |
| Ders özeti ve mini quiz | 5 dk |
| **Toplam** | **150 dk** |

### Derse Hazırlık

- **Önemli:** Kurulum adımları (Anaconda indirme ve kurma) internet hızına göre 10–20 dakika sürebilir. Mümkünse Anaconda'yı **dersten önce** indirip kurun.
- OpenAI API kullanımı **ücretlidir** ve ChatGPT aboneliğinden ayrıdır. Derste kullanılacak işlemler çok düşük maliyetlidir (genellikle birkaç sent), ama hesaba kredi yüklenmiş olması gerekir. platform.openai.com adresinden hesap açılıp faturalama (Billing) bölümünden küçük bir kredi yüklenmelidir.
- Bir kod düzenleyici kurulu olsun. Öneri: Visual Studio Code (ücretsiz). Alternatif: Windows'ta Not Defteri, Mac'te TextEdit (düz metin modunda).

---

### Giriş ve Tekrar (5 dk)

**Soru:** Sempozyum katılımcı destek asistanının üç bileşeni neydi?

**Cevap:** Talimat (kimlik ve kurallar), bilgi tabanı (SSS dosyası), test (beklenen davranış tablosu).

**Soru:** Python'da bir sayıyı metinle birleştirmek için ne yapmamız gerekiyordu?

**Cevap:** Sayıyı `str()` ile metne çevirmek.

---

### Konu 1: API Nedir? OpenAI API Nedir? (20 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir restoranda yemek sipariş ettiğinizi düşünün. Mutfağa girip yemeği kendiniz yapmazsınız. Garsona menüden ne istediğinizi belirli bir şekilde söylersiniz; garson siparişi mutfağa götürür ve hazırlanan yemeği size getirir. Mutfağın içinde ne olduğunu bilmenize gerek yoktur.

- **Siz:** Bizim programımız
- **Menü:** API belgeleri (neyi, nasıl isteyebileceğimiz)
- **Garson:** API
- **Mutfak:** OpenAI'ın sunucularındaki yapay zekâ modeli
- **Yemek:** Modelin cevabı

**Basit açıklama:** API, iki yazılımın birbiriyle belirli kurallara göre konuşmasını sağlayan bir "kapı" veya "garson"dur. Bizim yazdığımız Python programı, OpenAI API aracılığıyla yapay zekâ modeline soru gönderir ve cevabı alır.

**Teknik tanım:** API (Application Programming Interface – Uygulama Programlama Arayüzü), bir yazılımın sunduğu işlevlere başka yazılımların erişebilmesi için tanımlanmış istek ve cevap kurallarıdır. Web API'lerinde program, internet üzerinden belirli bir adrese (endpoint) bir istek gönderir; sunucu da yapılandırılmış bir cevap (genellikle JSON biçiminde) döndürür.

**Akademik benzetme:** Bir kütüphanenin ödünç verme masası gibi. Depoda kitapların nasıl dizildiğini bilmezsiniz; masaya belirli bir formla (katalog numarası) istek verirsiniz, kitap size getirilir. Formun kuralları, API'nin kurallarıdır.

#### API Nerede Kullanılır?

- Hava durumu uygulaması, meteoroloji servisinin API'sinden veri alır.
- Kaynak yönetim programları (Zotero gibi), bir makalenin DOI numarasından künyesini otomatik olarak bulmak için yayıncıların ve veri tabanlarının API'lerini kullanır.
- Üniversite kütüphane sistemleri, veri tabanlarına API ile bağlanır.
- Bizim programımız, yapay zekâ cevabı almak için OpenAI'ın API'sini kullanacak.

#### OpenAI API Nedir? ChatGPT'den Farkı

| Özellik | ChatGPT | OpenAI API |
|---|---|---|
| Ne? | Hazır bir sohbet uygulaması | Programlardan yapay zekâya erişim kapısı |
| Kullanım | Tarayıcı veya mobil uygulama | Kod yazarak |
| Ücretlendirme | Aylık abonelik (veya ücretsiz sürüm) | Kullandığın kadar öde (token başına) |
| Özelleştirme | Talimatlar, projeler | Her şey: talimat, model, biçim, kendi arayüzün |
| Otomasyon | Sınırlı | Tam: Yüzlerce dosyayı otomatik işleyebilirsin |
| Kimin için? | Son kullanıcı | Uygulama geliştiren herkes |

**Neden API öğreniyoruz?**

- **Toplu işlem:** 50 makale özetini tek tek kopyalayıp yapıştırmak yerine, bir program hepsini sırayla aynı şablonla okuma notuna çevirebilir.
- **Tekrarlanabilirlik:** Aynı talimat ve aynı ayarlarla çalışan bir program, yöntem bölümünde açıkça tarif edilebilir.
- **Kendi aracını yapmak:** Kendi kurallarınla çalışan bir araştırma asistanı.
- **Büyük metin koleksiyonları:** Arşiv belgeleri, görüşme transkriptleri, açık uçlu anket cevapları gibi verileri sistematik olarak işlemek.

> **Dikkat:** Araştırma verilerini (özellikle kişisel veri içeren görüşme transkriptlerini) API ile işlemeden önce etik kurul izninizin ve veri koruma kurallarının buna izin verdiğinden emin olun; verileri mümkünse anonimleştirin.

#### Temel Kavramlar

**Kavram: API anahtarı (API key)**

- Basit açıklama: API'yi kullanma hakkınızı gösteren gizli bir şifre. `sk-` ile başlayan uzun bir metindir.
- Neden önemli? Bu anahtarla yapılan bütün istekler sizin hesabınızdan ücretlendirilir.
- Benzetme: Kütüphane kartınız ve şifreniz gibi. Kimseyle paylaşmazsınız.

**Kavram: İstek (request) ve cevap (response)**

- Basit açıklama: Programın gönderdiği soru (istek) ve modelin döndürdüğü yanıt (cevap).

**Kavram: Model adı**

- Basit açıklama: Hangi modelin kullanılacağını belirten ad. Örneğin `gpt-5.4-mini`.
- Not: Model adları zamanla değişir; eski modeller kullanımdan kaldırılır. Güncel liste OpenAI'ın model belgelerindedir. Akademik bir çalışmada kullandığınız model adını ve tarihini not edin; yöntem bölümünde gerekebilir.

**Kavram: Token ve ücretlendirme**

- Basit açıklama: Ders 1'de öğrendiğimiz token'lar burada para birimine dönüşür. Gönderdiğiniz metin (girdi token'ları) ve aldığınız cevap (çıktı token'ları) ayrı ayrı ücretlendirilir. Fiyatlar genellikle "1 milyon token başına" verilir.
- Örnek: Küçük modellerle yapılan bir soru-cevap genellikle bir kuruştan bile azdır; ama binlerce sayfa işlenirse maliyet birikir.

> **Dikkat:** API hesabınızda **harcama limiti** (usage limit) belirleyin. Hatalı bir döngü, farkında olmadan binlerce istek gönderebilir.

**Kavram: SDK (kütüphane)**

- Basit açıklama: API'yi kolay kullanmak için hazırlanmış kod paketi. Python için `openai` kütüphanesi.
- Benzetme: Ödünç verme masasındaki hazır istek formu. Formu doldurursunuz, gerisini kütüphane halleder.

---

### Konu 2: Gerekli Kurulumlar – Python / Anaconda ve API Anahtarı (25 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir laboratuvar deneyinden önce çalışma tezgâhınızı hazırlarsınız: cihazlar, malzemeler, kayıt defteri. Programlama için de önce "çalışma tezgâhını" kurmak gerekir.

**Basit açıklama:**

- **Python:** Kodlarımızı yazacağımız programlama dili.
- **Anaconda:** Python'u ve veri işleme için gereken araçları tek pakette kuran, ücretsiz bir dağıtım. Yeni başlayanlar için kurulumu kolaylaştırır; akademik veri analizinde de yaygın kullanılır.
- **Sanal ortam (environment):** Projenize özel, ayrı bir çalışma odası. Bir projede kurduğunuz paketler diğerini etkilemez.
- **Terminal / Anaconda Prompt:** Bilgisayara yazılı komutlar verdiğimiz pencere.

#### Birlikte Uygulayalım: Kurulum Adımları

**Amaç:** Bilgisayarda OpenAI API ile çalışmaya hazır bir Python ortamı kurmak.

**Adım 1 – Anaconda'yı indirin ve kurun**

1. Tarayıcıda anaconda.com/download adresine gidin.
2. İşletim sisteminize uygun yükleyiciyi (Windows veya macOS) indirin. (Sitede e-posta istenirse kayıt olabilir veya varsa "atla" seçeneğini kullanabilirsiniz.)
3. İndirilen dosyayı çalıştırın.
4. Kurulum sihirbazında varsayılan ayarlarla ilerleyin ("Just Me" seçeneği önerilir).
5. Kurulumun bitmesini bekleyin.

**Adım 2 – Terminali açın**

- **Windows:** Başlat menüsüne "Anaconda Prompt" yazın ve açın.
- **macOS:** "Terminal" uygulamasını açın. Kurulumdan sonra satırın başında `(base)` yazısını görmelisiniz.

**Adım 3 – Kurulumu kontrol edin**

Şu komutu yazıp Enter'a basın:

```bash
python --version
```

Beklenen çıktı (sürüm numarası farklı olabilir):

```text
Python 3.13.5
```

**Adım 4 – Projeye özel bir ortam oluşturun**

```bash
conda create -n prompt_kursu python=3.12 -y
```

Bu komut `prompt_kursu` adında, Python 3.12 içeren yeni bir çalışma ortamı oluşturur. `-y` "bütün sorulara evet" demektir.

Ortamı etkinleştirin:

```bash
conda activate prompt_kursu
```

Satırın başında artık `(prompt_kursu)` yazmalıdır.

**Adım 5 – OpenAI kütüphanesini kurun**

```bash
pip install openai
```

Kurulumu kontrol edin:

```bash
pip show openai
```

Çıktıda `Name: openai` ve bir sürüm numarası görmelisiniz.

**Adım 6 – API anahtarını oluşturun**

1. platform.openai.com adresine gidin ve giriş yapın.
2. Faturalama (Billing) bölümünden hesaba küçük bir kredi yükleyin ve bir harcama limiti belirleyin.
3. API anahtarları (API keys) bölümüne gidin.
4. "Create new secret key" (yeni gizli anahtar oluştur) düğmesine tıklayın.
5. Anahtara bir ad verin: `prompt-kursu`.
6. Oluşan anahtarı kopyalayın. **Bu anahtar bir daha tam olarak gösterilmez.**

**Adım 7 – API anahtarını güvenli şekilde kaydedin (ortam değişkeni)**

API anahtarını kodun içine yazmak yerine, bilgisayarın **ortam değişkeni** olarak kaydedeceğiz. Böylece kodu başkasıyla paylaştığınızda (örneğin bir makalenin ek materyali olarak) anahtarınız paylaşılmaz.

- **Windows (Anaconda Prompt):**

```bash
setx OPENAI_API_KEY "sk-buraya-kendi-anahtarinizi-yapistirin"
```

Ardından Anaconda Prompt'u **kapatıp yeniden açın** ve ortamı tekrar etkinleştirin:

```bash
conda activate prompt_kursu
```

- **macOS (Terminal):**

```bash
echo 'export OPENAI_API_KEY="sk-buraya-kendi-anahtarinizi-yapistirin"' >> ~/.zshrc
source ~/.zshrc
conda activate prompt_kursu
```

Kontrol edin (anahtarın ilk birkaç karakterinin göründüğünü kontrol etmek yeterli):

- Windows: `echo %OPENAI_API_KEY%`
- macOS: `echo $OPENAI_API_KEY`

**Adım 8 – Proje klasörünü oluşturun**

```bash
mkdir arastirma_asistani
cd arastirma_asistani
```

Bundan sonraki bütün dosyaları bu klasöre kaydedeceğiz.

**Beklenen sonuç:** `(prompt_kursu)` ortamı etkin, `openai` kütüphanesi kurulu, API anahtarı ortam değişkeni olarak kayıtlı ve `arastirma_asistani` klasöründeyiz.

#### Sık Yapılan Hatalar

**Hata 1: Ortamı etkinleştirmeyi unutmak**

- Belirti: `ModuleNotFoundError: No module named 'openai'`
- Neden? Kütüphane `prompt_kursu` ortamına kuruldu ama terminal `base` ortamında.
- Düzeltme: `conda activate prompt_kursu`

**Hata 2: API anahtarını koda yazıp paylaşmak**

Hatalı:

```python
client = OpenAI(api_key="sk-abc123...")
```

Doğru:

```python
client = OpenAI()  # Anahtar ortam değişkeninden otomatik okunur
```

Neden? Kodu bir meslektaşınıza gönderdiğinizde veya bir kod deposuna (örneğin GitHub) yüklediğinizde anahtarınız çalınabilir ve hesabınızdan harcama yapılabilir. Anahtarın sızdığını düşünürseniz platform üzerinden hemen silin (revoke).

**Hata 3: Windows'ta `setx` sonrası terminali yeniden açmamak**

- Belirti: Anahtar bulunamadı hatası (`OpenAIError: The api_key client option must be set...`).
- Düzeltme: Anaconda Prompt'u kapatıp yeniden açın.

**Hata 4: Faturalama yapılmamış hesap**

- Belirti: `insufficient_quota` veya 429 hata kodu.
- Düzeltme: Billing bölümünden kredi yükleyin.

---

### Konu 3: API ile İlk Chat (25 dk)

#### Birlikte Uygulayalım: İlk İstek

**Amaç:** Python programından OpenAI API'ye ilk soruyu göndermek ve cevabı ekrana yazdırmak.

**Senaryo:** Ders 1'de sohbet ekranında sorduğumuz ilk soruyu bu kez kendi programımızdan soruyoruz.

**Adımlar:**

1. Kod düzenleyicinizi (VS Code veya Not Defteri) açın.
2. Yeni bir dosya oluşturun.
3. Aşağıdaki kodu yazın.
4. Dosyayı `arastirma_asistani` klasörüne `ilk_sohbet.py` adıyla kaydedin. (Not Defteri kullanıyorsanız "Kayıt türü"nü "Tüm dosyalar" seçin ve kodlamayı UTF-8 yapın.)

```python
# ilk_sohbet.py
# OpenAI API'ye ilk sorumuzu gönderiyoruz.

from openai import OpenAI  # OpenAI kütüphanesinden OpenAI sınıfını alıyoruz

client = OpenAI()  # API'ye bağlanan "garson" nesnesi; anahtarı ortam değişkeninden okur

MODEL = "gpt-5.4-mini"  # Kullanacağımız model (güncel adları OpenAI belgelerinden kontrol edin)

cevap = client.responses.create(
    model=MODEL,
    input="Geleneksel Türk evi mimarisinde 'sofa' kavramını bir makalenin kavramsal çerçeve bölümü için 3 cümleyle akademik bir dille tanımla."
)

print(cevap.output_text)  # Modelin cevap metnini ekrana yazdır
```

5. Terminalde (ortam etkin ve `arastirma_asistani` klasöründeyken) şu komutu yazın:

```bash
python ilk_sohbet.py
```

6. **Tahmin sorusu:** Çalıştırmadan önce düşünelim: "Sizce cevap ChatGPT ekranındaki cevaba benzeyecek mi?"
7. Cevabı inceleyin.

**Beklenen çıktı (model her seferinde farklı ifadeler kullanabilir):**

```text
Sofa, geleneksel Türk evinde odaların etrafında konumlandığı ve hepsinin açıldığı ortak mekândır.
Hem dolaşım hem de toplanma işlevi üstlenerek ev içi ilişkilerin örgütlendiği merkez olarak işlev görür.
Plan tipolojisi çalışmalarında sofanın konumu, evin tipinin belirlenmesinde temel ölçüt olarak kullanılır.
```

#### Kod Nasıl Çalışıyor?

`from openai import OpenAI`

Kurduğumuz `openai` kütüphanesinden `OpenAI` adlı aracı programımıza getiriyoruz. Restoran benzetmesinde bu, sipariş formunu masaya almak gibidir.

`client = OpenAI()`

API ile konuşacak bir "garson" oluşturuyoruz ve adını `client` koyuyoruz. Parantezin içi boş, çünkü API anahtarını kütüphane `OPENAI_API_KEY` ortam değişkeninden kendisi okur.

`MODEL = "gpt-5.4-mini"`

Hangi modeli kullanacağımızı bir değişkende tutuyoruz. Büyük harfle yazmak, "bu değer program boyunca değişmeyecek" demenin bir alışkanlığıdır. Modeli değiştirmek istersek sadece bu satırı değiştiririz.

`cevap = client.responses.create(model=MODEL, input="...")`

Garsona siparişi veriyoruz: "Bu modelle, bu soruyu cevapla." `responses.create`, OpenAI'ın **Responses API** adlı uç noktasına istek gönderir. Gelen cevabın tamamı `cevap` değişkenine kaydedilir.

`print(cevap.output_text)`

Cevap nesnesinin içinde birçok bilgi vardır (model adı, token sayıları vb.). `output_text` sadece modelin yazdığı metni verir.

#### Kod Üzerinde Değişiklik Yapalım

1. `input` içindeki soruyu değiştirin: "Cumba kavramını 2 cümleyle akademik bir dille tanımla." Programı tekrar çalıştırın.
2. **Soru:** Aynı programı iki kez çalıştırırsak aynı cevabı alır mıyız?
   - **Cevap:** Büyük ihtimalle hayır. Ders 3'te gördüğümüz gibi model her seferinde cevabı yeniden üretir; anlam benzer, ifadeler farklı olur. Bu, akademik kullanımda tekrarlanabilirlik açısından önemlidir: Kullanılan promptu, modeli ve tarihi kayıt altına almak gerekir.
3. **Soru:** `print(cevap.output_text)` satırını silersek ne olur?
   - **Cevap:** Program hatasız çalışır ve API'ye istek gider (ücretlendirilir) ama ekranda hiçbir şey görmeyiz. Cevap alınır ama gösterilmez.
4. Ekrana cevabın yanında ne kadar token kullanıldığını da yazdıralım. Programın sonuna şu satırları ekleyin:

```python
print()
print("Girdi token sayısı:", cevap.usage.input_tokens)
print("Çıktı token sayısı:", cevap.usage.output_tokens)
```

Çalıştırın. Çıktı örneği:

```text
Girdi token sayısı: 38
Çıktı token sayısı: 104
```

**Açıklama:** Bu sayılar, Ders 1'deki token kavramının somut hâlidir. Ücret bu sayılara göre hesaplanır. Bazı modeller cevap vermeden önce "düşünür"; bu düşünme token'ları da çıktı token'larına dahil olabilir.

#### Sıra Sizde 1 (10 dk)

**Amaç:** API ile istek göndermeyi pekiştirmek.

**Görev:** `kavramlar.py` adlı bir program yazın. Program, Ders 2'deki few-shot kavram sözlüğü promptunu API'ye göndersin ve "eyvan, hayat, yüklük" için tanım maddelerini ekrana yazdırsın.

**İstenenler:**

- `ilk_sohbet.py` dosyasını temel alın.
- Prompt birden fazla satır olduğu için üç tırnak (`"""`) kullanın.
- Sonunda toplam token sayısını yazdırın.

**Beklenen sonuç:** Örnek biçimde üç tanım maddesi ve token bilgisi.

**İpucu:** Python'da çok satırlı metin şöyle yazılır:

```python
prompt = """Birinci satır
İkinci satır"""
```

#### Çözüm

```python
# kavramlar.py
# Few-shot prompt ile tezin kavramlar eki için tanım maddeleri üretir.

from openai import OpenAI

client = OpenAI()
MODEL = "gpt-5.4-mini"

# Çok satırlı prompt: Ders 2'deki örnekli yönerge
prompt = """Tezimin "Kavramlar" ekindeki her terim için kısa bir tanım maddesi yazacaksın.
Aşağıdaki örneğin biçimini ve uzunluğunu aynen izle.

Örnek:
**Sofa** – Geleneksel Türk evinde odaların açıldığı ortak alan. Hem dolaşım hem toplanma mekânıdır. Plan tipolojisinde belirleyici öğedir.

Şimdi şu terimler için madde yaz: eyvan, hayat, yüklük."""

cevap = client.responses.create(
    model=MODEL,
    input=prompt
)

print(cevap.output_text)
print()
print("Toplam token:", cevap.usage.total_tokens)
```

Beklenen çıktı (ifadeler değişebilir):

```text
**Eyvan** – Üç yanı kapalı, bir yanı tamamen açık, üstü örtülü mekân. Avluya veya sofaya açılır. Anadolu mimarisinde konut ve anıtsal yapılarda görülür.
**Hayat** – Geleneksel evde bir yanı açık, sofa işlevi gören yarı açık mekân. Gündelik işlerin yapıldığı yerdir. Hayatlı plan tipinin adını verdiği öğedir.
**Yüklük** – Oda duvarına gömülü, yatak ve yorganların gündüz saklandığı dolap. Odanın çok amaçlı kullanımını sağlar. Odanın işlevsel esnekliğinin temel donatısıdır.

Toplam token: 228
```

#### Sık Yapılan Hatalar

**Hata 1: Tırnak işaretini kapatmamak**

Hatalı:

```python
input="Cumba nedir?
```

Doğru:

```python
input="Cumba nedir?"
```

Neden? Python metnin nerede bittiğini bulamaz: `SyntaxError: unterminated string literal`.

**Hata 2: Parantezi kapatmamak**

Hatalı:

```python
cevap = client.responses.create(
    model=MODEL,
    input="Cumba nedir?"
```

Doğru: Sonuna `)` ekleyin.

**Hata 3: Dosya adını `openai.py` koymak**

- Neden hata? Python, `from openai import OpenAI` satırında kütüphane yerine sizin dosyanızı yükler ve hata verir.
- Düzeltme: Dosyalarınıza kütüphane adlarıyla aynı ad vermeyin.

**Hata 4: Model adını yanlış yazmak**

- Belirti: `model_not_found` hatası.
- Düzeltme: Model adını belgelerden kopyalayın; büyük-küçük harf ve tireler önemlidir.

---

### Konu 4: OpenAI API Detayları (15 dk)

#### Talimat (Sistem Mesajı) Kullanımı

Ders 3'te sohbet uygulamalarında "proje talimatı" olarak yazdığımız sistem mesajını, API'de `instructions` alanıyla veririz.

```python
# talimatli_sohbet.py
# Ders 3'teki araştırma talimatını API'de kullanır.

from openai import OpenAI

client = OpenAI()
MODEL = "gpt-5.4-mini"

# Ders 3'te yazdığımız araştırma talimatının kısaltılmış hâli
TALIMAT = """Sen geleneksel konuttan apartmana geçişte mekân kullanımının dönüşümünü inceleyen
bir araştırmanın akademik yazım asistanısın.
Kurallar:
1. Asla kaynak, künye veya doğrudan alıntı uydurma.
2. Emin olmadığın tarih, isim veya sayı için [DOĞRULANMALI] etiketi koy.
3. Atıf gereken ama kaynağı verilmemiş iddialar için [ATIF] etiketi koy.
4. Yüzyılları rakamla yaz (18. yüzyıl); birinci çoğul şahıs kullanma.
5. Metni düzeltirken anlamı değiştirme ve değişiklikleri madde madde listele."""

paragraf = """Onsekizinci yüzyılda inşa edilen bu evlerde hayat, ailenin bütün gününü geçirdiği bir mekandı
ve biz bu evlerin en önemli özelliğinin 1785 yılında yapılan ilk örneklerinde görülen ahşap direklerle
çevrili olması olduğunu görüyoruz."""

cevap = client.responses.create(
    model=MODEL,
    instructions=TALIMAT,                       # Sistem talimatı: her istekte geçerli kurallar
    input="Şu paragrafı düzelt:\n" + paragraf   # Kullanıcı isteği
)

print(cevap.output_text)
```

**Tahmin sorusu:** Ders 3'te aynı paragrafı proje içinde düzelttirmiştik. Sonuç benzer olur mu?

**Cevap:** Evet. "18. yüzyıl" düzeltmesi, "biz ... görüyoruz" ifadesinin nesnel yapıya çevrilmesi, "1785" için [DOĞRULANMALI], kaynaksız iddia için [ATIF] etiketi ve değişiklik listesi beklenir. Çünkü aynı talimat bu kez kodla verildi.

**Not:** `\n` bir **satır sonu** karakteridir. "Şu paragrafı düzelt:" yazısından sonra paragrafın yeni satırda başlamasını sağlar.

#### Dosyadan Metin Okumak

Makale notlarımızı koda yapıştırmak yerine bir dosyadan okuyabiliriz. Bu, Ders 2'deki okuma notu şablonunu yüzlerce dosyaya uygulamanın ilk adımıdır.

1. `arastirma_asistani` klasöründe `makale_ozeti.txt` adında bir dosya oluşturun ve içine bir makale özeti yapıştırın (veya Ders 2'deki "çok amaçlı oda" metnini kullanın). UTF-8 olarak kaydedin.
2. Şu programı yazın:

```python
# okuma_notu.py
# Bir metin dosyasını okuyup Ders 2'deki okuma notu biçiminde özetler.

from openai import OpenAI

client = OpenAI()
MODEL = "gpt-5.4-mini"

TALIMAT = """Sen mimarlık tarihi ve konut çalışmaları alanında titiz bir araştırma asistanısın.
Sadece verilen metne dayan. Metinde olmayan bilgi ekleme.
Bulunmayan alanlar için "Metinde belirtilmemiş" yaz."""

# Dosyayı aç ve içeriğini oku. encoding="utf-8" Türkçe karakterler için gereklidir.
with open("makale_ozeti.txt", "r", encoding="utf-8") as dosya:
    metin = dosya.read()

istek = """Aşağıdaki metinden şu başlıklarla bir okuma notu hazırla:
- Ana iddia (1 cümle)
- Yöntem ve veri (1–2 cümle)
- Temel bulgular (en fazla 3 madde)
- Önemli kavramlar

Metin:
""" + metin

cevap = client.responses.create(
    model=MODEL,
    instructions=TALIMAT,
    input=istek
)

# Sonucu hem ekrana yazdır hem de bir dosyaya kaydet
print(cevap.output_text)

with open("okuma_notu_sonuc.txt", "w", encoding="utf-8") as cikti:
    cikti.write(cevap.output_text)

print()
print("Okuma notu 'okuma_notu_sonuc.txt' dosyasına kaydedildi.")
```

**Kod Nasıl Çalışıyor?**

`with open("makale_ozeti.txt", "r", encoding="utf-8") as dosya:`

Dosyayı okuma (`"r"`, read) modunda açar. `with` yapısı, iş bitince dosyanın otomatik kapanmasını sağlar.

`metin = dosya.read()`

Dosyanın bütün içeriğini `metin` değişkenine alır.

`with open("okuma_notu_sonuc.txt", "w", encoding="utf-8") as cikti:`

Yeni bir dosyayı yazma (`"w"`, write) modunda açar. Dosya yoksa oluşturur, varsa **üzerine yazar.**

**Beklenen sonuç:** Ekranda okuma notu ve klasörde `okuma_notu_sonuc.txt` dosyası.

> **Dikkat:** `"w"` modu var olan dosyanın içeriğini siler ve yeniden yazar. Önemli dosyalarınızın adını çıktı dosyasına vermeyin.

#### Önemli API Kavramları Tablosu

| Kavram | API'deki karşılığı | Ne işe yarar? |
|---|---|---|
| Model seçimi | `model="..."` | Hız, kalite ve maliyet dengesi. Küçük ("mini", "nano") modeller ucuz ve hızlı; büyük modeller daha güçlü. |
| Sistem talimatı | `instructions="..."` | Ders 3'teki kalıcı kurallar |
| Kullanıcı isteği | `input="..."` veya mesaj listesi | O anki soru |
| Cevap metni | `cevap.output_text` | Modelin yazdığı metin |
| Token kullanımı | `cevap.usage` | Maliyet takibi |
| Sohbet geçmişi | `input` içinde mesaj listesi | Chatbot'un önceki konuşmayı hatırlaması (Uygulama bölümünde) |
| Çıktı uzunluk sınırı | `max_output_tokens=...` | Cevabın en fazla kaç token olacağı (düşünen modellerde çok düşük verilirse cevap boş kalabilir) |

> **Not:** OpenAI'ın eski ama hâlâ yaygın olan bir uç noktası daha vardır: **Chat Completions** (`client.chat.completions.create`). İnternette göreceğiniz birçok örnek bunu kullanır. Bu derste OpenAI'ın önerdiği güncel **Responses API**'yi kullanıyoruz. Mantık aynıdır: model + mesajlar → cevap.

---

### Konu 5: Fine-Tuning Verileri (15 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir araştırma projesine yeni katılan bir asistana, her seferinde "Okuma notlarını şu biçimde yaz" diye kural anlatmak yerine, daha önce yazılmış 50 iyi okuma notunu veriyorsunuz. Asistan bunları inceleyerek biçimi **kendi alışkanlığı** hâline getiriyor. Artık her seferinde anlatmanıza gerek kalmıyor.

**Basit açıklama:** Fine-tuning (ince ayar), hazır bir yapay zekâ modelini, kendi örneklerinizle ek bir eğitimden geçirerek belirli bir görevde veya biçimde daha tutarlı hâle getirmektir.

**Teknik tanım:** Fine-tuning; önceden eğitilmiş bir modelin ağırlıklarının, belirli bir göreve ait girdi–çıktı örnekleriyle (eğitim verisi) ek olarak güncellenmesidir. Ders 4'teki tek nöronlu sınıflandırıcıda ağırlıkları hatalara göre güncellemiştik; fine-tuning, aynı fikrin milyarlarca ağırlıklı bir modelde, sizin verinizle uygulanmasıdır. OpenAI'da en temel türü **denetimli ince ayardır** (supervised fine-tuning): Model, "bu girdiye bu çıktı verilmeli" örneklerinden öğrenir.

#### Prompt, Few-Shot ve Fine-Tuning Karşılaştırması

| Yöntem | Nasıl? | Ne zaman? | Maliyet / zahmet |
|---|---|---|---|
| İyi prompt | Talimatları açıkça yazmak | Her zaman ilk adım | Düşük |
| Few-shot | Promptta 2–5 örnek vermek | Biçim ve üslup tutarlılığı | Düşük |
| Bilgi tabanı / dosya yükleme | Modele kaynak belgeleri vermek | Belirli bilgilere dayanarak cevap | Düşük-orta |
| Fine-tuning | Yüzlerce örnekle modeli yeniden eğitmek | Çok sayıda tekrar eden, çok tutarlı biçim gereken işler (örneğin binlerce açık uçlu anket cevabını aynı kod şemasıyla sınıflandırmak) | Yüksek |

> **Dikkat – 2026 itibarıyla güncel durum:** OpenAI, kendi kendine hizmet veren (self-serve) fine-tuning platformunu aşamalı olarak kapatmaktadır. Mayıs 2026'dan itibaren daha önce fine-tuning yapmamış hesaplar yeni ince ayar işi başlatamamaktadır; Ocak 2027'de ise mevcut kullanıcılar için de yeni iş oluşturma sona erecektir. OpenAI bunun gerekçesi olarak yeni modellerin iyi promptlar ve örneklerle çoğu işi zaten yapabildiğini belirtmiştir. Bu nedenle bu derste fine-tuning'i **kavram ve veri hazırlığı** düzeyinde öğreniyoruz. Hazırlayacağımız veri, (1) erişimi olan hesaplarda ince ayar için, (2) başka sağlayıcıların ince ayar hizmetlerinde ve (3) **few-shot örnek havuzu** olarak her durumda kullanılabilir. Güncel durumu OpenAI belgelerinden kontrol edin.

**Fine-tuning ne zaman gerekmez?** Bir bilgiyi modele "öğretmek" için (örneğin okuduğunuz makalelerin içeriği) fine-tuning uygun değildir; bunun için bilgi tabanı / dosya yükleme kullanılır. Fine-tuning daha çok **davranış ve biçim** öğretir.

#### Eğitim Verisinin Biçimi: JSONL

**JSON nedir?** Bilgiyi "alan: değer" çiftleriyle düzenli şekilde yazmanın standart biçimi. Python sözlüklerine çok benzer.

**JSONL nedir?** "JSON Lines": Her satırda bir JSON nesnesi bulunan dosya. Her satır bir eğitim örneğidir.

OpenAI'ın sohbet modelleri için her satır şu yapıdadır:

```json
{"messages": [{"role": "system", "content": "Sistem talimatı"}, {"role": "user", "content": "Kullanıcı sorusu"}, {"role": "assistant", "content": "İdeal cevap"}]}
```

- `system`: Ders 3'teki sistem talimatı
- `user`: Örnek soru
- `assistant`: Modelin vermesini istediğimiz **ideal** cevap

**Kurallar:**

- En az 10 örnek gerekir; anlamlı iyileşme genellikle 50–100 iyi örnekle görülür.
- Örnekler gerçek kullanıma benzemeli ve çeşitli olmalıdır.
- İdeal cevaplar gerçekten ideal olmalıdır: Model hatalı örnekleri de öğrenir.

#### Birlikte Uygulayalım: Kavram Sözlüğü Eğitim Verisi Hazırlamak

**Amaç:** Python ile geçerli bir JSONL eğitim dosyası üretmek.

**Senaryo:** Bir tezin kavramlar eki için her terimi aynı biçimde açıklayan bir model istiyoruz: tanım + işlev + bugünkü karşılığı.

**Adımlar:**

1. `veri_hazirla.py` adında yeni bir dosya oluşturun ve şu kodu yazın:

```python
# veri_hazirla.py
# Fine-tuning için JSONL biçiminde eğitim verisi hazırlar.

import json  # JSON biçiminde yazmak için Python'un hazır kütüphanesi

SISTEM = "Sen bir mimarlık tarihi tezinin kavram sözlüğünü yazan asistansın. Her terimi üç kısa cümleyle açıklarsın: tanım, işlev, bugünkü karşılığı."

# Her örnek: (kullanıcı sorusu, ideal cevap)
ornekler = [
    ("Sofa nedir?",
     "Sofa, geleneksel Türk evinde odaların açıldığı ortak alandır. Hem dolaşım hem toplanma yeri olarak kullanılır. Bugünkü karşılığı: salon ile koridorun birleşimi."),
    ("Hayat nedir?",
     "Hayat, bir yanı açık, sofa işlevi gören yarı açık mekândır. Gündelik işlerin ve yaz aylarındaki yaşamın merkezidir. Bugünkü karşılığı: geniş, üstü örtülü bir balkon."),
    ("Eyvan nedir?",
     "Eyvan, üç yanı kapalı, bir yanı tamamen açık, üstü örtülü mekândır. Avluya veya sofaya açılarak gölgeli bir oturma yeri sağlar. Bugünkü karşılığı: derin, üstü kapalı bir teras."),
    ("Cumba nedir?",
     "Cumba, üst katın sokağa doğru taşan kapalı çıkmasıdır. Odaya ışık, manzara ve sokağı görme imkânı verir. Bugünkü karşılığı: kapalı balkon veya bay pencere."),
    ("Yüklük nedir?",
     "Yüklük, oda duvarına gömülü büyük dolaptır. Gündüz yatak ve yorganların saklanmasını sağlayarak odayı çok amaçlı kılar. Bugünkü karşılığı: gömme gardırop."),
    ("Sedir nedir?",
     "Sedir, oda veya sofa duvarı boyunca uzanan alçak, sabit oturma yeridir. Odanın ortasını boş bırakarak esnek kullanım sağlar. Bugünkü karşılığı: duvara yaslı köşe koltuk."),
    ("Seki nedir?",
     "Seki, oda tabanının bir kısmının yükseltilmesiyle oluşan basamaktır. Odanın giriş bölümünü oturma bölümünden ayırır. Bugünkü karşılığı: girişteki kademe veya platform."),
    ("Avlu nedir?",
     "Avlu, evin duvarlarla çevrili açık dış alanıdır. Su, bitki ve gündelik işler için korunaklı bir yaşam alanı sağlar. Bugünkü karşılığı: bahçe veya iç bahçe."),
    ("Taşlık nedir?",
     "Taşlık, zemin katta yeri taş döşeli giriş ve hizmet alanıdır. Avlu ile ev arasında geçiş ve iş alanı olarak kullanılır. Bugünkü karşılığı: giriş holü ile kiler arası bir alan."),
    ("Başoda nedir?",
     "Başoda, evin en özenli yapılmış ve genellikle en iyi manzaraya sahip odasıdır. Misafir ağırlamak ve önemli günler için kullanılır. Bugünkü karşılığı: misafir salonu."),
]

# JSONL dosyasını yaz
with open("egitim_verisi.jsonl", "w", encoding="utf-8") as dosya:
    for soru, cevap in ornekler:
        satir = {
            "messages": [
                {"role": "system", "content": SISTEM},
                {"role": "user", "content": soru},
                {"role": "assistant", "content": cevap},
            ]
        }
        # ensure_ascii=False: Türkçe karakterler (ş, ğ, ı) olduğu gibi yazılsın
        dosya.write(json.dumps(satir, ensure_ascii=False) + "\n")

print(str(len(ornekler)) + " örnek 'egitim_verisi.jsonl' dosyasına yazıldı.")

# Basit kontrol: Dosyadaki her satır geçerli JSON mu ve en az 10 satır var mı?
satir_sayisi = 0
with open("egitim_verisi.jsonl", "r", encoding="utf-8") as dosya:
    for satir in dosya:
        json.loads(satir)  # Satır geçerli JSON değilse burada hata verir
        satir_sayisi = satir_sayisi + 1

if satir_sayisi >= 10:
    print("Kontrol başarılı: " + str(satir_sayisi) + " geçerli satır var.")
else:
    print("Uyarı: En az 10 örnek gerekir. Şu an " + str(satir_sayisi) + " örnek var.")
```

2. Çalıştırın:

```bash
python veri_hazirla.py
```

**Beklenen çıktı:**

```text
10 örnek 'egitim_verisi.jsonl' dosyasına yazıldı.
Kontrol başarılı: 10 geçerli satır var.
```

3. `egitim_verisi.jsonl` dosyasını kod düzenleyicide açın ve inceleyin. Her satırın bir örnek olduğunu görün.

**Kod Nasıl Çalışıyor?**

- `ornekler` bir listedir; her elemanı `(soru, cevap)` şeklinde iki elemanlı bir **demettir** (tuple).
- `for soru, cevap in ornekler:` her demeti açar: ilk eleman `soru`, ikincisi `cevap` değişkenine gider.
- `json.dumps(...)` Python sözlüğünü tek satırlık JSON metnine çevirir.
- `+ "\n"` her örnekten sonra yeni satıra geçer; bu yüzden dosya JSONL olur.
- `json.loads(satir)` kontrol için satırı tekrar okur; hatalı bir satır varsa program burada hata verir.

> **Dikkat:** Buradaki sözlük cevapları eğitim amaçlı sadeleştirilmiş tanımlardır. Gerçek bir tez kavram sözlüğünde her tanım kaynaklarla doğrulanmalı ve atıfla verilmelidir. Model, eğitim verisindeki hataları da öğrenir.

#### İnce Ayar İşini Başlatmak (Erişimi Olan Hesaplar İçin)

Aşağıdaki kod, fine-tuning erişimi olan bir OpenAI hesabında eğitim dosyasını yükler ve bir ince ayar işi başlatır. **Erişimi olmayan hesaplarda bu kod hata verecektir;** bu durumda kodu okuyup adımları anlamak yeterlidir.

```python
# ince_ayar_baslat.py
# Eğitim dosyasını yükler ve fine-tuning işini başlatır.

from openai import OpenAI

client = OpenAI()

# 1. Eğitim dosyasını OpenAI'a yükle
egitim_dosyasi = client.files.create(
    file=open("egitim_verisi.jsonl", "rb"),  # "rb": dosyayı ikili (binary) modda oku
    purpose="fine-tune"                       # Dosyanın amacı: ince ayar
)
print("Yüklenen dosyanın kimliği:", egitim_dosyasi.id)

# 2. İnce ayar işini başlat
egitim_isi = client.fine_tuning.jobs.create(
    training_file=egitim_dosyasi.id,   # Az önce yüklediğimiz dosya
    model="gpt-4.1-mini-2025-04-14",   # İnce ayar yapılabilen bir temel model (güncel listeyi kontrol edin)
    suffix="sozluk"                    # Yeni modelin adına eklenecek etiket
)
print("İnce ayar işinin kimliği:", egitim_isi.id)
print("Durum:", egitim_isi.status)
```

Beklenen çıktı (kimlikler farklı olacaktır):

```text
Yüklenen dosyanın kimliği: file-AbC123...
İnce ayar işinin kimliği: ftjob-XyZ789...
Durum: validating_files
```

**Kod Nasıl Çalışıyor?**

- `client.files.create(...)` dosyayı OpenAI sunucularına yükler. Kimliğini (`id`) not etmeliyiz.
- `client.fine_tuning.jobs.create(...)` eğitimi başlatır. Eğitim veri boyutuna göre dakikalar ya da saatler sürebilir.
- İş tamamlandığında yeni modelin adı `ft:gpt-4.1-mini-2025-04-14:...:sozluk:...` biçiminde olur ve normal bir model gibi `model=` alanında kullanılabilir.

---

### Konu 6: Modeli Gözlemlemek ve Silmek (10 dk)

#### Konu Nedir?

**Günlük hayat örneği:** Bir laboratuvara numune analizi gönderdiğinizde süreci arada bir kontrol edersiniz: "Hangi aşamada?" Analiz bittiğinde sonuçları alırsınız; artık gerekmeyen numuneler de saklama alanında yer kaplamasın diye imha edilir.

**Basit açıklama:** İnce ayar işi başladıktan sonra durumunu izleyebilir, hangi aşamada olduğunu ve hata olup olmadığını görebiliriz. Artık kullanmadığımız ince ayarlı modelleri ve yüklediğimiz dosyaları silebiliriz.

#### İnce Ayar İşini İzlemek

```python
# ince_ayar_izle.py
# Bir fine-tuning işinin durumunu ve son olaylarını gösterir.

from openai import OpenAI

client = OpenAI()

IS_KIMLIGI = "ftjob-buraya-kendi-is-kimliginizi-yazin"

# İşin güncel durumunu al
egitim_isi = client.fine_tuning.jobs.retrieve(IS_KIMLIGI)
print("Durum:", egitim_isi.status)                     # validating_files, queued, running, succeeded, failed, cancelled
print("Oluşan model:", egitim_isi.fine_tuned_model)    # İş bitmeden None görünür

# Son 10 olayı listele (eğitimin adım adım günlüğü)
olaylar = client.fine_tuning.jobs.list_events(fine_tuning_job_id=IS_KIMLIGI, limit=10)
for olay in olaylar.data:
    print("-", olay.message)
```

Örnek çıktı:

```text
Durum: running
Oluşan model: None
- Step 20/30: training loss=0.42
- Step 10/30: training loss=0.85
- Fine-tuning job started
- Files validated, moving job to queued state
```

**Açıklama:** `training loss` (eğitim kaybı), modelin örneklere göre ne kadar hata yaptığını gösterir. Ders 4'teki sınıflandırıcıda hatayı hesaplamıştık; burada da eğitim ilerledikçe bu sayının genellikle **azalması** beklenir.

İşi iptal etmek gerekirse:

```python
client.fine_tuning.jobs.cancel(IS_KIMLIGI)
```

#### Modelleri Listelemek ve Silmek

```python
# modelleri_yonet.py
# Hesaptaki ince ayarlı modelleri listeler ve isteğe bağlı olarak birini siler.

from openai import OpenAI

client = OpenAI()

# 1. Hesaptaki bütün modelleri al ve sadece ince ayarlı olanları ("ft:" ile başlayanlar) yazdır
print("İnce ayarlı modelleriniz:")
for model in client.models.list():
    if model.id.startswith("ft:"):
        print("-", model.id)

# 2. Bir modeli silmek için aşağıdaki satırlardaki # işaretlerini kaldırın ve model adını yazın.
# DİKKAT: Silme işlemi geri alınamaz!
# SILINECEK_MODEL = "ft:gpt-4.1-mini-2025-04-14:kurumunuz:sozluk:abc123"
# sonuc = client.models.delete(SILINECEK_MODEL)
# print("Silindi mi?", sonuc.deleted)
```

Yüklenen eğitim dosyasını silmek için:

```python
client.files.delete("file-buraya-dosya-kimligi")
```

**Kod Nasıl Çalışıyor?**

- `client.models.list()` hesabınızın erişebildiği bütün modelleri döndürür; `startswith("ft:")` ile sadece ince ayarlı olanları seçeriz.
- Silme satırlarını bilerek `#` ile yorum satırı yaptık. Böylece program yanlışlıkla bir şey silmez. Bu, Ders 5'teki "ajanlara silme yetkisini dikkatle verin" ilkesinin kod karşılığıdır.

> **Dikkat:** Model silme işlemi **geri alınamaz.** Modeli kullanan bir uygulama varsa çalışmayı durdurur. Ayrıca ince ayarlı modeller, temel aldıkları model kullanımdan kaldırıldığında kullanılamaz hâle gelir. Bir araştırmada ince ayarlı model kullandıysanız, yöntem bölümünde model adını, eğitim verisini ve tarihleri kayıt altına alın; model daha sonra erişilemez olabilir.

#### Sık Yapılan Hatalar

**Hata 1: Kimlikleri not etmemek**

- Neden hata? Dosya ve iş kimlikleri olmadan izleme ve silme yapılamaz.
- Düzeltme: Programın yazdırdığı kimlikleri bir dosyaya kaydedin (veya platformun panelinden bulun).

**Hata 2: JSONL'de Türkçe karakter sorunu**

- Belirti: Dosyada `ş` gibi kodlar görünür.
- Düzeltme: `json.dumps(..., ensure_ascii=False)` ve `encoding="utf-8"` kullanın. (Kodlar teknik olarak geçerlidir ama okunması zordur.)

**Hata 3: Bilgi öğretmek için fine-tuning yapmak**

- Neden hata? Fine-tuning biçim ve davranış öğretir; olgusal bilgiyi güvenilir şekilde ekleyemez.
- Düzeltme: Bilgi için dosya / bilgi tabanı kullanın.

---

### Uygulama: GPT API ile Chatbot Yapımı (30 dk)

#### Birlikte Uygulayalım: Sempozyum Katılımcı Destek Chatbot'u

**Amaç:** Sohbet geçmişini hatırlayan, sistem talimatıyla çalışan ve bilgi dosyasını kullanan bir terminal chatbot'u yazmak.

**Senaryo:** Ders 5'te kod yazmadan kurduğumuz sempozyum katılımcı destek asistanını bu kez kendi programımızla kuruyoruz.

**Problem nedir?** Her API isteği birbirinden bağımsızdır; model önceki soruyu **hatırlamaz.** Sohbet edebilmek için geçmişi kendimiz tutmalıyız.

**Nasıl çözeceğiz?** Konuşmadaki bütün mesajları bir listede saklayıp her istekte bu listeyi modele göndereceğiz.

**Hangi bilgileri kullanacağız?** Ders 5'teki `sss_sempozyum.txt` dosyası ve talimat.

**Tahmin sorusu:** `ilk_sohbet.py` programına önce "Özetim 280 kelime" deyip ikinci çalıştırmada "Bu uzunluk uygun mu?" diye sorsaydık ne olurdu?

**Cevap:** Model hangi uzunluktan bahsettiğimizi bilemezdi. Her çalıştırma, garsona hiç tanışmamışız gibi yeni bir sipariş vermektir. Hafıza bizim tarafımızda tutulmalıdır.

**Adımlar:**

1. Ders 5'teki `sss_sempozyum.txt` dosyasını `arastirma_asistani` klasörüne kopyalayın (yoksa Ders 5'teki içerikle oluşturun).
2. `sempozyum_chatbot.py` adında yeni bir dosya oluşturun ve şu kodu yazın:

```python
# sempozyum_chatbot.py
# Sohbet geçmişini hatırlayan, SSS dosyasına dayanan katılımcı destek chatbot'u.

from openai import OpenAI

client = OpenAI()
MODEL = "gpt-5.4-mini"

# 1. Bilgi dosyasını oku
with open("sss_sempozyum.txt", "r", encoding="utf-8") as dosya:
    sss_metni = dosya.read()

# 2. Sistem talimatı: Ders 5'teki talimat + SSS metni
TALIMAT = """Sen "Konut ve Gündelik Hayat Sempozyumu"nun katılımcı destek asistanısın.
Katılımcıların sorularını kibar, kısa ve net bir dille cevaplarsın.

Kurallar:
1. Sadece aşağıdaki SSS bilgilerini kullan.
2. SSS'de olmayan bir bilgi sorulursa uydurma ve şunu söyle:
   "Bu konuda elimde bilgi yok. Lütfen sempozyum@ornek-universite.edu.tr adresine yazın."
3. Bildiri kabul veya ret konusunda tahmin ve söz verme; kararı düzenleme kurulunun verdiğini söyle.
4. Ücret, indirim veya son tarih uzatması konusunda söz verme.
5. Cevapların 3 cümleyi geçmesin.
6. Katılımcı hangi dilde yazarsa o dilde cevap ver.

SSS BİLGİLERİ:
""" + sss_metni

# 3. Sohbet geçmişini tutacağımız boş liste
gecmis = []

print("Sempozyum Katılımcı Asistanı")
print("Çıkmak için 'çıkış' yazın.")
print()

# 4. Sohbet döngüsü: Kullanıcı 'çıkış' yazana kadar devam eder
while True:
    soru = input("Siz: ")

    # Çıkış kontrolü
    if soru.lower() in ["çıkış", "cikis", "exit"]:
        print("Asistan: Görüşmek üzere, sempozyumda görüşmek dileğiyle!")
        break

    # Boş mesaj gönderilmesin
    if soru.strip() == "":
        continue

    # Kullanıcının sorusunu geçmişe ekle
    gecmis.append({"role": "user", "content": soru})

    try:
        # Bütün geçmişi modele gönder
        cevap = client.responses.create(
            model=MODEL,
            instructions=TALIMAT,
            input=gecmis
        )
        cevap_metni = cevap.output_text

        # Modelin cevabını da geçmişe ekle ki bir sonraki soruda hatırlasın
        gecmis.append({"role": "assistant", "content": cevap_metni})

        print("Asistan:", cevap_metni)
        print()

    except Exception as hata:
        # İnternet kesilmesi, anahtar hatası gibi durumlarda program çökmesin
        print("Bir hata oluştu:", hata)
        gecmis.pop()  # Cevap alınamayan soruyu geçmişten çıkar
```

3. Çalıştırın:

```bash
python sempozyum_chatbot.py
```

4. Ders 5'teki test tablosunu kullanarak şu konuşmayı yapın:

```text
Siz: Merhaba, bildiri özeti kaç kelime olmalı?
Asistan: Merhaba! Bildiri özeti 250–300 kelime olmalı ve amaç, yöntem, bulgular ile sonucu içermelidir.

Siz: Bunu İngilizce yazabilir miyim?
Asistan: Evet, özetinizi Türkçe veya İngilizce yazabilirsiniz.

Siz: Katılım ücreti ne kadar?
Asistan: Bu konuda elimde bilgi yok. Lütfen sempozyum@ornek-universite.edu.tr adresine yazın.

Siz: çıkış
Asistan: Görüşmek üzere, sempozyumda görüşmek dileğiyle!
```

**Beklenen sonuç:** İkinci soruda ("Bunu İngilizce yazabilir miyim?") model "bunu" kelimesinin bildiri özeti olduğunu önceki konuşmadan anlamalı; ücret sorusunda uydurmamalıdır.

**Açıklama:** Model kendisi hatırlamadı; biz her soruda **bütün geçmişi** yeniden gönderdik. "Bunu İngilizce yazabilir miyim?" sorusu tek başına belirsizdir ama geçmişle birlikte gönderildiğinde model bağlamı görür. Ders 1'deki **bağlam penceresi** kavramı burada somutlaşır: Sohbet uzadıkça gönderilen token sayısı ve maliyet artar.

#### Kod Nasıl Çalışıyor?

`gecmis = []`

Konuşmayı saklayacağımız boş bir liste. Her mesaj `{"role": ..., "content": ...}` biçiminde bir sözlüktür.

`while True:`

Sonsuz döngü: İçindeki satırları `break` görene kadar tekrar eder.

`soru = input("Siz: ")`

Ekranda "Siz: " yazar ve kullanıcının yazıp Enter'a basmasını bekler. Yazılan metin `soru` değişkenine gider.

`if soru.lower() in ["çıkış", "cikis", "exit"]:`

`lower()` metni küçük harfe çevirir; böylece "Çıkış" veya "ÇIKIŞ" da çalışır. Liste içinde varsa `break` ile döngüden çıkarız.

`continue`

Boş mesajda döngünün başına döner; API'ye gereksiz istek gitmez.

`gecmis.append({"role": "user", "content": soru})`

Kullanıcının sorusunu listenin sonuna ekler.

`input=gecmis`

Bu kez `input`'a tek bir metin değil, bütün mesaj listesini veriyoruz.

`try: ... except Exception as hata:`

`try` içindeki kodda bir hata olursa program çökmek yerine `except` kısmına geçer ve hatayı ekrana yazar. `gecmis.pop()` listenin son elemanını (cevabı alınamayan soruyu) siler.

#### Kod Üzerinde Değişiklik Yapalım

1. **Talimat değişikliği:** Kural 5'i "Cevapların 1 cümleyi geçmesin" yapın. Programı yeniden çalıştırıp aynı soruları sorun. Fark ne?
2. **Soru:** `gecmis.append({"role": "assistant", "content": cevap_metni})` satırını silersek ne olur?
   - **Cevap:** Model sadece kullanıcının sorularını görür, kendi önceki cevaplarını görmez. "Bunu İngilizce yazabilir miyim?" gibi sorularda karışıklık olabilir; çünkü konuşmanın yarısı eksiktir.
3. **Yeni özellik:** Her cevaptan sonra toplam token kullanımını yazdırın:

```python
print("(Bu istekte kullanılan token:", cevap.usage.total_tokens, ")")
```

Birkaç soru sorun. **Soru:** Token sayısı her soruda neden artıyor?
   - **Cevap:** Çünkü her istekte bütün geçmiş yeniden gönderiliyor; geçmiş uzadıkça girdi token'ları artar.

#### Sıra Sizde 2 (15 dk)

**Amaç:** Chatbot'u kendi ihtiyacına göre uyarlamak.

**Görev:** `sempozyum_chatbot.py`yi temel alarak bir **"Akademik Yazım Koçu"** chatbot'u yazın. Bu chatbot katılımcı sorularına değil, araştırmacının kendisine hizmet edecek: Araştırmacı paragraf yapıştıracak, chatbot Ders 3'teki dergi yazım kurallarına göre geri bildirim verecek. Ayrıca konuşma bittiğinde bütün sohbeti bir dosyaya kaydedecek.

**İstenenler:**

- Talimatı Ders 3'teki araştırma talimatına göre değiştirin (SSS dosyasına gerek yok).
- Çıkışta sohbet geçmişini `yazim_kocu_kayit.txt` dosyasına "Siz: ... / Asistan: ..." biçiminde kaydedin.

**Beklenen sonuç:** Paragraflara kurallara uygun geri bildirim veren ve çıkışta konuşmayı dosyaya kaydeden bir chatbot.

**İpucu:** Kaydetme işini `break`'ten önce yapın. Geçmişteki her mesajın `role` değerine bakarak "Siz" veya "Asistan" yazdırabilirsiniz.

#### Çözüm

```python
# yazim_kocu.py
# Araştırmacıya dergi yazım kurallarına göre geri bildirim veren ve sohbeti kaydeden chatbot.

from openai import OpenAI

client = OpenAI()
MODEL = "gpt-5.4-mini"

TALIMAT = """Sen akademik yazım koçusun. Araştırmacı sana hakemli bir dergiye gönderilecek
makaleden paragraflar gönderecek.

Kesin kurallar:
1. Asla kaynak, künye veya doğrudan alıntı uydurma.
2. Emin olmadığın tarih, isim veya sayı için [DOĞRULANMALI] etiketi öner.
3. Kaynağı verilmemiş iddialar için [ATIF] etiketi öner.

Kontrol edeceğin yazım kuralları:
- Yüzyıllar rakamla yazılır: 18. yüzyıl.
- Yabancı terimler italik yazılır.
- Cümleler mümkünse 25 kelimeyi geçmez.
- Birinci çoğul şahıs kullanılmaz; nesnel ve temkinli akademik dil kullanılır.

Her paragraf için şu biçimde cevap ver:
1. Kural ihlalleri (madde madde)
2. Argüman ve akış için en fazla 2 öneri
3. Düzeltilmiş paragraf"""

gecmis = []

print("Akademik Yazım Koçu – çıkmak için 'çıkış' yazın.")
print()

while True:
    soru = input("Siz: ")

    if soru.lower() in ["çıkış", "cikis", "exit"]:
        # Sohbeti dosyaya kaydet
        with open("yazim_kocu_kayit.txt", "w", encoding="utf-8") as kayit:
            for mesaj in gecmis:
                if mesaj["role"] == "user":
                    kayit.write("Siz: " + mesaj["content"] + "\n\n")
                else:
                    kayit.write("Asistan: " + mesaj["content"] + "\n\n")
        print("Sohbet 'yazim_kocu_kayit.txt' dosyasına kaydedildi. Kolay gelsin!")
        break

    if soru.strip() == "":
        continue

    gecmis.append({"role": "user", "content": soru})

    try:
        cevap = client.responses.create(
            model=MODEL,
            instructions=TALIMAT,
            input=gecmis
        )
        cevap_metni = cevap.output_text
        gecmis.append({"role": "assistant", "content": cevap_metni})
        print("Asistan:", cevap_metni)
        print()
    except Exception as hata:
        print("Bir hata oluştu:", hata)
        gecmis.pop()
```

**Test:** Ders 3'teki "Onsekizinci yüzyılda..." paragrafını yapıştırın. Kural ihlallerinin listelendiğini, düzeltilmiş paragrafın verildiğini ve çıkışta dosyanın oluştuğunu kontrol edin.

#### Sık Yapılan Hatalar

**Hata 1: Geçmişi tutmadan "sohbet" beklemek**

- Hatalı: Her döngüde `input=soru` göndermek.
- Doğru: `input=gecmis` göndermek ve her soru-cevabı listeye eklemek.

**Hata 2: Sonsuz döngüden çıkış yolu bırakmamak**

- Neden hata? Program kapanmaz; zorla kapatmak gerekir (Ctrl + C).
- Düzeltme: Mutlaka bir `break` koşulu ekleyin.

**Hata 3: Girinti hatası**

Hatalı:

```python
while True:
soru = input("Siz: ")
```

Doğru:

```python
while True:
    soru = input("Siz: ")
```

**Hata 4: Çok uzun sohbetlerde maliyeti fark etmemek**

- Neden hata? Her istekte bütün geçmiş gönderildiği için token sayısı sürekli artar.
- Düzeltme: Token kullanımını yazdırın; çok uzun sohbetlerde yeni oturum başlatın veya geçmişin sadece son birkaç mesajını gönderin.

---

### Ders Özeti

Bu son derste yapay zekâya bir sohbet ekranı yerine kendi programımızdan bağlandık. API'yi bir restorandaki garsona benzettik: Programımız siparişi verir, API mutfağa iletir, cevabı geri getirir. Anaconda ile Python ortamımızı kurduk, API anahtarımızı güvenli şekilde ortam değişkeninde sakladık ve ilk isteğimizi gönderdik. Ders 3'teki araştırma talimatını `instructions` alanıyla verdik, dosyadan okuyup sonucu dosyaya yazdık. Fine-tuning'in bir modeli örneklerle yeniden eğitmek olduğunu, JSONL eğitim verisinin nasıl hazırlandığını ve OpenAI'da bu hizmetin 2026'dan itibaren kapanma sürecinde olduğunu öğrendik; işleri izlemeyi ve modelleri silmeyi gördük. Son olarak sohbet geçmişini kendimiz tutarak hatırlayan bir chatbot yazdık.

### Bu Derste Neler Öğrendik?

- API'nin iki yazılım arasında kurallı iletişim sağlayan bir kapı olduğunu öğrendik.
- OpenAI API ile ChatGPT arasındaki farkı ve token başına ücretlendirmeyi gördük.
- Anaconda, sanal ortam ve `pip install openai` ile kurulum yaptık.
- API anahtarını koda yazmadan ortam değişkeninde sakladık.
- `client.responses.create` ile ilk isteği gönderip `output_text` ile cevabı aldık.
- `instructions` ile sistem talimatı verdik; dosyadan okuyup dosyaya yazdık.
- Fine-tuning kavramını, JSONL biçimini ve eğitim verisi hazırlamayı öğrendik.
- İnce ayar işlerini izleme, iptal etme ve modelleri listeleme/silme komutlarını gördük.
- Sohbet geçmişini bir listede tutarak hatırlayan bir chatbot yazdık.

### Mini Quiz

1. **(Çoktan seçmeli)** Restoran benzetmesinde API neye karşılık gelir?
   - a) Mutfak
   - b) Garson
   - c) Yemek
   - d) Müşteri
2. **(Doğru / Yanlış)** API anahtarını kodun içine yazıp bir makalenin ek materyali olarak paylaşmak güvenlidir.
3. **(Kısa cevap)** `ModuleNotFoundError: No module named 'openai'` hatası alırsanız ilk neyi kontrol edersiniz?
4. **(Kod çıktısı tahmini)** Aşağıdaki kod ekrana ne yazar?

```python
gecmis = []
gecmis.append({"role": "user", "content": "Merhaba"})
gecmis.append({"role": "assistant", "content": "Selam!"})
print(len(gecmis))
```

5. **(Kısa cevap)** API'de sistem talimatı hangi parametreyle verilir?
6. **(Çoktan seçmeli)** Fine-tuning en çok neyi öğretmek için uygundur?
   - a) Güncel haberleri
   - b) Belirli bir biçim ve davranışı
   - c) Okunan makalelerin bütün içeriğini
   - d) İnternette arama yapmayı
7. **(Doğru / Yanlış)** Her API isteği önceki istekleri otomatik olarak hatırlar.
8. **(Küçük problem)** Chatbot'ta her soruda kullanılan token sayısı artıyor. Neden? Bir çözüm önerin.

### Mini Quiz Cevapları

1. **b.** Garson.
2. **Yanlış.** Anahtar çalınabilir ve hesabınızdan harcama yapılabilir; ortam değişkeninde saklanmalıdır.
3. Doğru ortamın (`conda activate prompt_kursu`) etkin olup olmadığını ve `pip install openai` yapılıp yapılmadığını.
4. `2`
5. `instructions`
6. **b.**
7. **Yanlış.** Geçmişi programın kendisi tutmalı ve her istekte göndermelidir.
8. Her istekte bütün sohbet geçmişi gönderildiği için. Çözüm: Belirli bir uzunluktan sonra yeni oturum başlatmak veya sadece son birkaç mesajı göndermek (örneğin `input=gecmis[-6:]`).

### Ders Sonu Uygulaması

**Senaryo:** Bir literatür taraması için `notlar` klasöründe üç farklı makale özeti var. Hepsini tek tek kopyala-yapıştır yapmak yerine, bir programın hepsini sırayla okuyup aynı şablonla okuma notu çıkarması ve sonuçları tek bir dosyada toplaması isteniyor.

**Yapılacaklar:**

1. `arastirma_asistani` klasöründe `ozet1.txt`, `ozet2.txt`, `ozet3.txt` adında üç dosya oluşturun ve içlerine kısa makale özetleri yapıştırın.
2. `toplu_okuma_notu.py` adında bir program yazın:
   - Dosya adlarını bir listede tutsun.
   - Döngüyle her dosyayı okusun.
   - Her biri için `okuma_notu.py`deki promptla okuma notu çıkarsın.
   - Bütün notları `literatur_notlari.txt` dosyasında, her birinin başında dosya adı olacak şekilde toplasın.
3. Programı çalıştırın ve sonucu kontrol edin.

**Beklenen sonuç:** Üç okuma notunu içeren tek bir `literatur_notlari.txt` dosyası.

**İpuçları:**

- Ders 5'teki `for kaynak in kaynaklar:` döngüsünü hatırlayın; burada `for dosya_adi in dosyalar:` olacak.
- Sonuç dosyasını döngüden **önce** `"w"` modunda açın; böylece döngünün içinde her notu ekleyebilirsiniz.

### Ders Sonu Uygulaması – Çözüm

```python
# toplu_okuma_notu.py
# Birden fazla metin dosyasını sırayla okuyup okuma notlarını tek dosyada toplar.

from openai import OpenAI

client = OpenAI()
MODEL = "gpt-5.4-mini"

TALIMAT = """Sen mimarlık tarihi ve konut çalışmaları alanında titiz bir araştırma asistanısın.
Sadece verilen metne dayan. Metinde olmayan bilgi ekleme.
Bulunmayan alanlar için "Metinde belirtilmemiş" yaz."""

dosyalar = ["ozet1.txt", "ozet2.txt", "ozet3.txt"]

with open("literatur_notlari.txt", "w", encoding="utf-8") as sonuc:
    for dosya_adi in dosyalar:
        print(dosya_adi + " işleniyor...")

        # Dosyayı oku
        with open(dosya_adi, "r", encoding="utf-8") as dosya:
            metin = dosya.read()

        istek = """Aşağıdaki metinden şu başlıklarla bir okuma notu hazırla:
- Ana iddia (1 cümle)
- Yöntem ve veri (1–2 cümle)
- Temel bulgular (en fazla 3 madde)
- Önemli kavramlar

Metin:
""" + metin

        cevap = client.responses.create(
            model=MODEL,
            instructions=TALIMAT,
            input=istek
        )

        # Notu, başında dosya adıyla birlikte sonuç dosyasına yaz
        sonuc.write("=== " + dosya_adi + " ===\n")
        sonuc.write(cevap.output_text + "\n\n")

print("Bütün notlar 'literatur_notlari.txt' dosyasına kaydedildi.")
```

**Beklenen ekran çıktısı:**

```text
ozet1.txt işleniyor...
ozet2.txt işleniyor...
ozet3.txt işleniyor...
Bütün notlar 'literatur_notlari.txt' dosyasına kaydedildi.
```

**Kod Nasıl Çalışıyor?**

- Dış `with` bloğu sonuç dosyasını bir kez açar; döngü boyunca açık kalır.
- `for dosya_adi in dosyalar:` her dosya için aynı adımları tekrarlar: oku → istek hazırla → API'ye gönder → sonuca yaz.
- `"=== " + dosya_adi + " ==="` her notun hangi dosyadan geldiğini gösteren bir başlık oluşturur. Bu, Ders 1'den beri vurguladığımız **kaynağı izlenebilir tutma** ilkesinin kod karşılığıdır.

> **Sonuç:** Bu küçük program, kurs boyunca öğrendiğimiz neredeyse her şeyi kullanıyor: sistem talimatı (Ders 3), okuma notu şablonu (Ders 2), uydurma yasağı (Ders 1), döngü ve dosya işlemleri (Ders 5) ve API (Ders 6). Elle saatler sürecek bir işi dakikalara indiriyor. Yine de her okuma notu, makalenin kendisiyle karşılaştırılarak kontrol edilmelidir.

---

# Kurs Sonu Bölümleri

> Aşağıdaki bölümler 6 dersin tamamını kapsar. Genel Tekrar ve Genel Tekrar Soruları son derste 15–20 dakikalık ek bir oturumda veya ödev olarak yapılabilir. Final Mini Projesi, kurs sonrası 3–4 saatlik bireysel bir çalışma olarak planlanmıştır.

## Genel Tekrar

### Ders 1 – Prompt Mühendisliğine Giriş

- **Dil modeli**, bağlama göre bir sonraki token'ı tahmin ederek metin üretir. Doğruluğu değil, olasılığı esas alır.
- **Prompt**, yapay zekâya verilen iyi tanımlanmış bir görev tanımıdır. İyi bir prompt şu soruları cevaplar: Ne? Neden? Kim için? Ne bilgiyle? Nasıl? Ne olmasın?
- **Halüsinasyon**, modelin gerçek olmayan bilgiyi (özellikle kaynak ve alıntıyı) kendinden emin şekilde üretmesidir. Akademik çalışmada her kaynak doğrulanır.
- **Bağlam penceresi**, modelin aynı anda dikkate alabileceği metin miktarıdır; uzun sohbetlerde eski talimatlar unutulabilir.
- Altın kural: Modele bilgi ürettirmek yerine **verdiğiniz bilgiyi işletin.** Yapay zekâ kullanımını kurumunuzun ve derginin kurallarına göre şeffaf biçimde belirtin.

### Ders 2 – Temel Prompt Teknikleri

- Prompt yapısı: **bağlam + rol + görev + çıktı biçimi.**
- İyi yönerge: açık, ölçülebilir, olumlu ifadeli, sıralı ve gerekçeli.
- **Few-shot:** Örnek vererek modelin kalıbı taklit etmesini sağlamak.
- **Ton** (tavır), **üslup** (yazış biçimi) ve **format** (görsel düzen) ayrı ayrı kontrol edilir; akademik metinde temkinli dil esastır.
- **Rol atama** (hakem, editör, yöntem uzmanı) bakış açısını değiştirir ama uzmanlık garantisi vermez.
- **Chain of thought:** Yöntem seçimi gibi karmaşık kararlarda adımları görünür yazdırmak hem doğruluğu hem kontrolü artırır.

### Ders 3 – İleri Prompt Teknikleri

- **Sistem mesajı / proje talimatı:** Bütün sohbet boyunca geçerli kalıcı kurallar (araştırma sorusu, yazım kuralları, uydurma yasağı).
- **Çoklu deneme:** Birden fazla seçenek üretip önceden belirlenmiş ölçütlerle karşılaştırmak; tutarsız bilgiler doğrulama önceliğidir.
- **Görsel düzenleme promptu:** Neyi değiştir, nasıl değiştir, neyi koru, hangi üslupta.
- Kanıt niteliğindeki görsel (anonimleştirme dışında) değiştirilmez; açıklayıcı görselin niteliği altyazıda belirtilir.
- **Görsel–metin entegrasyonu:** Önce metin, sonra metinden görsel prompt; tutarlılık için stil rehberi.

### Ders 4 – Görsel, Multimedya ve Yapay Sinir Ağları

- Görsel prompt bileşenleri: konu, ortam, tarz, ışık, perspektif, malzeme, kompozisyon, renk, atmosfer, teknik parametreler.
- Midjourney estetikte, GPT Image talimata sadakatte ve sohbetle düzenlemede güçlüdür. Yapay zekâ çizimleri ölçülü teknik çizim değildir.
- Ses: transkripsiyon ve seslendirme; video: metinden/görselden video. Sözlü tarih kayıtlarında izin, anonimleştirme ve doğrulama şarttır.
- **Yapay nöron:** girdiler × ağırlıklar + sapma → aktivasyon. **Öğrenme:** hata × girdi kadar ağırlık güncellemesi.
- **Token tahmini**, prompt tekniklerinin neden işe yaradığını ve modelin neden uydurabildiğini açıklar.

### Ders 5 – Sektörel Uygulamalar ve Ajanlar

- Kod promptu: dil/ortam, girdi, işlem, çıktı, seviye. Hata ayıklamada kod + hata mesajı birlikte verilir.
- Eğitim, akademik iletişim (çağrı metni, SEO), tasarım (sergi senaryosu) alanlarında aynı prompt ilkeleri geçerlidir.
- **Ajan:** hedefe göre çalışan, araç kullanan, planlayan, sınırlar içinde özerk yapay zekâ sistemi.
- **No-code / low-code** platformlar: talimat + bilgi tabanı + araçlar + tetikleyiciler.
- Bir asistan yayına alınmadan önce **beklenen davranış tablosuyla** test edilir.

### Ders 6 – API ve Chatbot

- **API**, programların yapay zekâ modeline kurallı şekilde bağlanmasını sağlar (restorandaki garson).
- API anahtarı ortam değişkeninde saklanır; harcama limiti belirlenir.
- `client.responses.create(model=..., instructions=..., input=...)` → `cevap.output_text`
- **Fine-tuning** biçim ve davranış öğretir; veri JSONL biçimindedir. OpenAI'da 2026'dan itibaren kapanma sürecindedir.
- Chatbot hafızası, sohbet geçmişinin her istekte yeniden gönderilmesiyle sağlanır.

### Kursun Büyük Resmi

| Katman | Ne öğrendik? | Nerede kullandık? |
|---|---|---|
| Düşünme | Modelin nasıl çalıştığı, sınırları, akademik etik | Kaynak doğrulama, şeffaflık |
| Prompt | Yapı, ton, rol, adım adım düşünme | Okuma notu, literatür paragrafı, hakem gözüyle okuma |
| Kalıcılık | Sistem talimatı, stil rehberi | Araştırma asistanı talimatı, sunum görsel serisi |
| Çok kiplilik | Görsel, ses, video | Poster ve sunum görselleri, sözlü tarih transkripti, yayın duyurusu |
| Otomasyon | Ajanlar, no-code akışlar | Sempozyum katılımcı destek asistanı, araştırma asistanı |
| Programlama | API, Python, chatbot | Toplu okuma notu programı, chatbot'lar |

---

## Genel Tekrar Soruları

1. **(Çoktan seçmeli)** Büyük dil modelinin cevap üretme mantığı aşağıdakilerden hangisidir?
   - a) Veri tabanından doğru cevabı bulmak
   - b) Bağlama göre bir sonraki token'ı olasılığa dayalı tahmin etmek
   - c) İnsan gibi anlamak
   - d) Her soruya önceden yazılmış cevabı getirmek
2. **(Kısa cevap)** Yapay zekâdan "bu konuda 10 akademik kaynak" istemek neden risklidir? Daha güvenli alternatifi nedir?
3. **(Kısa cevap)** Prompt yapısının dört bileşenini yazınız.
4. **(Doğru / Yanlış)** "Kısa yaz" yönergesi ölçülebilir bir yönergedir.
5. **(Küçük problem)** Aşağıdaki promptu few-shot prompta dönüştürünüz: "Tezimin kavramlar eki için madde yaz: cumba, sedir."
6. **(Çoktan seçmeli)** Aynı paragrafı hakem, yöntem uzmanı ve alan dışı okur gözüyle değerlendirtmek hangi tekniktir?
   - a) Chain of thought
   - b) Rol atama
   - c) Fine-tuning
   - d) Outpainting
7. **(Kısa cevap)** Sistem talimatı ile kullanıcı mesajı arasındaki fark nedir?
8. **(Kısa cevap)** Çoklu denemede aynı soruya üç farklı tarih geldi. Ne yapmalısınız?
9. **(Doğru / Yanlış)** Yapay zekâ ile düzenlenmiş bir saha fotoğrafı, belirtilmeden makalede "mevcut durum" fotoğrafı olarak kullanılabilir.
10. **(Kısa cevap)** Görsel düzenleme promptunda "neyi koru" bilgisi neden önemlidir?
11. **(Küçük problem)** "Bir sofa çiz" görsel promptunu en az 6 bileşenle yeniden yazınız.
12. **(Hesap)** w1 = 3, w2 = -1, b = -1 ve x1 = 1, x2 = 1 iken nöronun toplamı ve tahmini nedir? (Toplam > 0 ise 1)
13. **(Kısa cevap)** Few-shot prompting'in işe yaramasını token tahmini ile açıklayınız.
14. **(Kod çıktısı tahmini)** Aşağıdaki kodun çıktısı nedir?

```python
sayilar = {}
for kelime in ["sofa", "cumba", "sofa"]:
    if kelime in sayilar:
        sayilar[kelime] = sayilar[kelime] + 1
    else:
        sayilar[kelime] = 1
print(sayilar["sofa"])
```

15. **(Kısa cevap)** Bir yapay zekâ ajanını sohbet botundan ayıran üç özelliği yazınız.
16. **(Doğru / Yanlış)** API anahtarı ortam değişkeninde saklanmalıdır.
17. **(Kod hatası)** Aşağıdaki kodda hangi hata vardır?

```python
cevap = client.responses.create(model=MODEL, input="Eyvan nedir?")
print(cevap.output_text
```

18. **(Kısa cevap)** Chatbot'un önceki soruları "hatırlaması" nasıl sağlanır?
19. **(Çoktan seçmeli)** Okuduğunuz makalelerin içeriğini yapay zekâya kullandırmak için en uygun yöntem hangisidir?
   - a) Fine-tuning
   - b) Bilgi tabanı / dosya yükleme
   - c) Sıcaklığı artırmak
   - d) Rol atama
20. **(Küçük problem)** Yayımlanan bir araştırmayı kamuoyuna anlatan bir blog yazısı + görsel üreteceksiniz. Hangi sırayla, hangi araçlarla ilerlersiniz? 4 adımda yazınız.

## Genel Tekrar Soruları – Cevaplar

1. **b.**
2. Model gerçekçi görünen ama var olmayan kaynaklar uydurabilir. Güvenli alternatif: Akademik veri tabanlarında arama için anahtar kelime istemek; kaynakları kendiniz bulup modele özetletmek; web araması yapan araçlarda bağlantıları kontrol etmek.
3. Bağlam, rol, görev, çıktı biçimi.
4. **Yanlış.** "En fazla 150 kelime" gibi sayısal ifade ölçülebilirdir.
5. Örnek:

```text
Aşağıdaki örneğin biçimini izleyerek tanım maddesi yaz.
Örnek: **Sofa** – Odaların açıldığı ortak alan. Dolaşım ve toplanma mekânıdır. Plan tipolojisinde belirleyici öğedir.
Şimdi şu terimler için yaz: cumba, sedir.
```

6. **b.**
7. Sistem talimatı bütün sohbet boyunca geçerli temel kuralları belirler ve önceliklidir; kullanıcı mesajı o anki istektir.
8. Bilginin modelin emin olmadığı bir bilgi olduğunu kabul edip mutlaka güvenilir bir kaynaktan doğrulamak; doğrulanmadan ve atıfsız kullanmamak.
9. **Yanlış.** Kanıt niteliğindeki görseli değiştirmek araştırma etiği ihlalidir.
10. Modeller düzenleme sırasında istenmeyen yerleri (pencere sayısı, oranlar) değiştirebilir; korunacakları açıkça yazmak bunu azaltır.
11. Örnek: "Geleneksel bir Safranbolu evinin sofası (konu, ortam), göz hizasından bakış (perspektif), ahşap tavan ve kireç sıvalı duvarlar (malzeme), öğleden sonra pencereden giren yumuşak ışık (ışık), ince çizgi ve sulu boya (tarz), sıcak toprak tonları (renk), sakin (atmosfer), yatay 3:2 (teknik)."
12. toplam = (1 × 3) + (1 × -1) + (-1) = 3 - 1 - 1 = **1** → 1 > 0 → Tahmin: **1**.
13. Model, promptta gördüğü kalıbı sürdüren token'lara yüksek olasılık verir; örnekler istenen biçimdeki devamı en olası devam hâline getirir.
14. `2`
15. Araç kullanma, çok adımlı planlama, hedefe yönelik özerk çalışma, kalıcı bilgi tabanı/hafıza, insan onayı gerektiren sınırlar (herhangi üçü).
16. **Doğru.**
17. `print(cevap.output_text` satırında kapanış parantezi eksik. Doğrusu: `print(cevap.output_text)`
18. Bütün sohbet mesajları bir listede (`gecmis`) tutulur ve her API isteğinde `input=gecmis` olarak yeniden gönderilir.
19. **b.**
20. Örnek: (1) Araştırma talimatının aktif olduğu projede, makalenin bulgularını vererek blog yazısını yazdırmak ve bulgulara sadakatini kontrol etmek; (2) stil rehberini ekleyerek yazının ana fikrinden görsel prompt çıkarmak; (3) GPT Image veya Midjourney ile görseli üretip mimari kontrol ve düzeltme yapmak; (4) altyazı ve alt metin yazdırmak, görselin yapay zekâ ile üretildiğini belirtmek.

---

## Final Mini Projesi

### Senaryo

Bir araştırmacı, makale yazım sürecinde her gün aynı işleri tekrar ediyor: paragrafları dergi kurallarına göre düzeltmek, yeni okunan makalelerden okuma notu çıkarmak, makale başlığı aramak, sunum ve poster görselleri için görsel prompt yazmak ve bazen sadece bir argümanı tartışacak bir "tartışma ortağı"na ihtiyaç duymak. Bu işler için ayrı ayrı sohbet açmak, talimatları kopyalamak ve sonuçları bir yerde toplamak zaman alıyor.

Araştırmacı, bütün bu işleri tek bir menüden yapan ve bütün çıktıları tek bir dosyada biriktiren bir **"Akademik Çalışma Asistanı"** programı istiyor.

### Projenin Amacı

Bu projede kursun bütün derslerinde öğrenilenler bir araya gelir:

| Ders | Projede nerede kullanılıyor? |
|---|---|
| Ders 1 | Uydurma yasağı, "[DOĞRULANMALI]" ve "[ATIF]" etiketleri, sadece verilen metne dayanma |
| Ders 2 | Okuma notu şablonu, yapılandırılmış promptlar, akademik ton |
| Ders 3 | Sistem talimatı, çeşitli başlık üretimi (çoklu deneme), stil rehberi |
| Ders 4 | Görsel prompt bileşenleri |
| Ders 5 | Python: değişkenler, döngü, koşullar, dosya işlemleri; asistan mantığı |
| Ders 6 | OpenAI API, `instructions`, sohbet geçmişi, hata yönetimi |

### Gereksinimler

Program şu özelliklere sahip olmalıdır:

1. Başlangıçta numaralı bir menü göstermeli.
2. **Paragraf düzelt:** Kullanıcının yapıştırdığı paragrafı araştırma talimatına göre düzeltmeli ve değişiklikleri listelemeli.
3. **Okuma notu:** Adı verilen bir `.txt` dosyasını okuyup okuma notu çıkarmalı; dosya bulunamazsa program çökmemeli.
4. **Başlık önerileri:** Verilen makale konusu için birbirinden farklı türlerde 5 başlık önermeli.
5. **Görsel prompt:** Verilen sahne veya kavram için stil rehberine uygun görsel prompt yazmalı.
6. **Tartışma ortağı:** Geçmişi hatırlayan bir sohbet modu olmalı; "menü" yazınca ana menüye dönmeli.
7. Bütün sonuçları `asistan_ciktilari.txt` dosyasına başlıklarıyla birlikte **eklemeli** (öncekileri silmemeli).
8. API hatalarında program çökmemeli, anlaşılır bir mesaj vermeli.
9. "Çıkış" seçeneğiyle düzgün şekilde kapanmalı.

### Yeni Kavram: Fonksiyon

Projede kodu düzenli tutmak için **fonksiyon** kullanacağız.

**Günlük hayat örneği:** Bir laboratuvarda "numune hazırlama protokolü" her seferinde aynı adımlardan oluşur. Bu adımlar bir kez yazılır ve "protokol 3'ü uygula" denir; her seferinde adımları yeniden anlatmaya gerek kalmaz.

**Basit açıklama:** Fonksiyon, bir işi yapan kod parçasına verilen addır. Bir kez `def` ile tanımlanır, sonra adıyla istenildiği kadar çağrılır.

```python
def selamla(isim):
    # Bu fonksiyon kendisine verilen ismi selamlar
    print("Merhaba " + isim + "!")

selamla("Elif")    # Çıktı: Merhaba Elif!
selamla("Ahmet")   # Çıktı: Merhaba Ahmet!
```

Bir fonksiyon `return` ile bir sonuç da geri verebilir:

```python
def iki_kati(sayi):
    return sayi * 2

sonuc = iki_kati(5)
print(sonuc)  # Çıktı: 10
```

### Proje Adımları

Projeyi büyük bir program olarak değil, küçük ve test edilebilir parçalar hâlinde yazacağız. **Her adımdan sonra programı çalıştırıp test edin.**

#### Adım 1 – Hazırlık ve sabitler

`akademik_asistan.py` dosyasını oluşturun. OpenAI bağlantısını, model adını, araştırma talimatını (Ders 3) ve stil rehberini (Ders 3) en üste yazın.

#### Adım 2 – Yardımcı fonksiyonlar

İki fonksiyon yazın:

- `yapay_zekaya_sor(talimat, istek)`: API'ye tek seferlik istek gönderir, cevap metnini döndürür; hata olursa hata mesajını döndürür.
- `kaydet(baslik, metin)`: Sonucu `asistan_ciktilari.txt` dosyasına **ekler** (`"a"` modu).

Test: Geçici olarak `print(yapay_zekaya_sor("Kısa cevap ver.", "Sofa nedir?"))` satırını ekleyip çalıştırın, sonra silin.

#### Adım 3 – Paragraf düzeltme fonksiyonu

`paragraf_duzelt()` fonksiyonunu yazın. Kullanıcıdan paragrafı alsın, düzeltsin, ekrana yazdırsın ve kaydetsin.

#### Adım 4 – Okuma notu fonksiyonu

`okuma_notu_cikar()` fonksiyonunu yazın. Dosya adını alsın; dosya yoksa "Dosya bulunamadı" desin ve menüye dönsün.

#### Adım 5 – Başlık ve görsel prompt fonksiyonları

`baslik_oner()` ve `gorsel_prompt_yaz()` fonksiyonlarını yazın.

#### Adım 6 – Tartışma ortağı modu

`tartisma_ortagi()` fonksiyonunu Ders 6'daki chatbot mantığıyla yazın. "menü" yazınca fonksiyondan çıksın.

#### Adım 7 – Ana menü

Sonsuz bir döngüyle menüyü gösterin, kullanıcının seçimine göre ilgili fonksiyonu çağırın.

#### Adım 8 – Test

Aşağıdaki test tablosunu doldurun:

| No | Test | Beklenen | Sonuç |
|---|---|---|---|
| 1 | Menüde "1" seçip hatalı paragraf yapıştırmak | Düzeltilmiş paragraf + değişiklik listesi | |
| 2 | Menüde "2" seçip var olmayan dosya adı yazmak | "Dosya bulunamadı" mesajı, menüye dönüş | |
| 3 | Menüde "2" seçip `ozet1.txt` yazmak | Okuma notu | |
| 4 | Menüde "3" seçip bir makale konusu yazmak | 5 farklı türde başlık | |
| 5 | Menüde "4" seçip bir sahne yazmak | Stil rehberine uygun görsel prompt | |
| 6 | Tartışma modunda önceki mesaja atıf yapmak | Önceki mesajı hatırlar | |
| 7 | Menüde "9" yazmak | "Geçersiz seçim" mesajı | |
| 8 | `asistan_ciktilari.txt` dosyasını açmak | Bütün çıktılar başlıklarıyla birikmiş | |

## Final Mini Projesi – Çözüm

### Örnek Çözüm

```python
# akademik_asistan.py
# Akademik okuma, yazım ve sunum hazırlığı için menülü asistan.
# Kursun bütün derslerinde öğrenilen teknikleri bir araya getirir.

from openai import OpenAI

client = OpenAI()          # Anahtar OPENAI_API_KEY ortam değişkeninden okunur (Ders 6)
MODEL = "gpt-5.4-mini"     # Güncel model adını OpenAI belgelerinden kontrol edin
CIKTI_DOSYASI = "asistan_ciktilari.txt"

# ------------------------------------------------------------
# SABİTLER: Ders 3'teki araştırma talimatı ve görsel stil rehberi
# ------------------------------------------------------------

ARASTIRMA_TALIMATI = """Sen geleneksel konuttan apartmana geçişte mekân kullanımının dönüşümünü
inceleyen bir araştırmanın araştırma ve akademik yazım asistanısın.
Çıktılar hakemli dergi makalesi ve sempozyum bildirisi olarak hazırlanmaktadır.

KESİN KURALLAR:
1. Asla kaynak, künye, sayfa numarası, DOI veya doğrudan alıntı uydurma.
2. Emin olmadığın tarih, isim veya sayı için [DOĞRULANMALI] etiketi koy.
3. Atıf gereken ama kaynağı verilmemiş iddialar için [ATIF] etiketi koy.
4. Araştırmacının metnini düzeltirken anlamı ve atıfları değiştirme; değişiklikleri madde madde listele.

YAZIM KURALLARI:
- Yüzyıllar rakamla yazılır: 18. yüzyıl.
- Yabancı terimler italik yazılır.
- Cümleler mümkünse 25 kelimeyi geçmez.
- Birinci çoğul şahıs kullanılmaz; nesnel ve temkinli akademik dil kullanılır.

Cevaplarını Türkçe ver."""

STIL_REHBERI = """GÖRSEL STİL REHBERİ (Araştırma sunumları ve poster)
- Teknik: Beyaz zemin üzerine ince siyah çizgi + hafif sulu boya dokusu
- Renkler: Sıcak toprak tonları, krem, tek vurgu rengi olarak soluk turkuaz
- Işık: Yumuşak, doğal gün ışığı
- Kompozisyon: Göz hizasından iç mekân perspektifi veya sade şema
- İnsan figürü: Yok veya çok küçük ve silüet
- Yazı/metin: Görselde yazı olmasın"""


# ------------------------------------------------------------
# YARDIMCI FONKSİYONLAR
# ------------------------------------------------------------

def yapay_zekaya_sor(talimat, istek):
    """API'ye tek seferlik istek gönderir ve cevap metnini döndürür."""
    try:
        cevap = client.responses.create(
            model=MODEL,
            instructions=talimat,
            input=istek
        )
        return cevap.output_text
    except Exception as hata:
        # Program çökmesin; hatayı metin olarak geri ver
        return "Bir hata oluştu: " + str(hata)


def kaydet(baslik, metin):
    """Sonucu çıktı dosyasının sonuna ekler. 'a' modu eski içeriği silmez."""
    with open(CIKTI_DOSYASI, "a", encoding="utf-8") as dosya:
        dosya.write("=== " + baslik + " ===\n")
        dosya.write(metin + "\n\n")
    print("(Sonuç '" + CIKTI_DOSYASI + "' dosyasına eklendi.)")


# ------------------------------------------------------------
# MENÜ İŞLEVLERİ
# ------------------------------------------------------------

def paragraf_duzelt():
    """Ders 2 ve 3: Paragrafı araştırma talimatındaki kurallara göre düzeltir."""
    print("Düzeltilecek paragrafı tek satır olarak yapıştırın ve Enter'a basın:")
    paragraf = input("> ")
    if paragraf.strip() == "":
        print("Boş paragraf gönderilmedi.")
        return

    istek = """Aşağıdaki paragrafı kurallara göre düzelt.
Önce düzeltilmiş paragrafı ver, sonra değişiklikleri madde madde listele.

Paragraf:
""" + paragraf

    sonuc = yapay_zekaya_sor(ARASTIRMA_TALIMATI, istek)
    print()
    print(sonuc)
    kaydet("Paragraf düzeltme", sonuc)


def okuma_notu_cikar():
    """Ders 2 ve 6: Bir metin dosyasından okuma notu çıkarır."""
    dosya_adi = input("Okunacak dosyanın adı (örnek: ozet1.txt): ")

    try:
        with open(dosya_adi, "r", encoding="utf-8") as dosya:
            metin = dosya.read()
    except FileNotFoundError:
        print("Dosya bulunamadı. Dosya adını ve klasörü kontrol edin.")
        return

    istek = """Aşağıdaki metinden şu başlıklarla bir okuma notu hazırla.
Sadece metne dayan; metinde olmayan alanlar için "Metinde belirtilmemiş" yaz.
- Ana iddia (1 cümle)
- Yöntem ve veri (1–2 cümle)
- Temel bulgular (en fazla 3 madde)
- Önemli kavramlar
- Araştırma sorusuyla bağlantısı
- Sorgulanabilecek nokta

Metin:
""" + metin

    sonuc = yapay_zekaya_sor(ARASTIRMA_TALIMATI, istek)
    print()
    print(sonuc)
    kaydet("Okuma notu – " + dosya_adi, sonuc)


def baslik_oner():
    """Ders 3: Birbirinden farklı türlerde makale başlığı önerir (çoklu deneme)."""
    konu = input("Başlık önerisi istediğiniz makalenin konusu ve ana bulgusu: ")

    istek = """Şu makale için birbirinden belirgin şekilde farklı 5 başlık öner: """ + konu + """
1 tanesi "Ana başlık: Alt başlık" biçiminde, 1 tanesi soru biçiminde, 1 tanesi bir kavramı öne çıkaran,
1 tanesi dönemi ve yeri belirten açıklayıcı, 1 tanesi bir nesneye odaklı olsun.
Her biri en fazla 15 kelime olsun. "Bir inceleme", "Üzerine bir çalışma" gibi kalıp ifadelerden kaçın.
Her başlığın yanına türünü parantez içinde yaz."""

    sonuc = yapay_zekaya_sor(ARASTIRMA_TALIMATI, istek)
    print()
    print(sonuc)
    kaydet("Başlık önerileri – " + konu, sonuc)


def gorsel_prompt_yaz():
    """Ders 3 ve 4: Stil rehberine uygun görsel üretim promptu yazar."""
    sahne = input("Sunum veya posterde görselleştirmek istediğiniz sahneyi veya kavramı yazın: ")

    istek = STIL_REHBERI + """

Bu stil rehberine uygun, en fazla 80 kelimelik bir görsel üretim promptu yaz.
Promptta konu, ortam, malzeme, ışık, perspektif ve renk paleti açıkça yer alsın.
Ardından aynı promptun Midjourney için İngilizce sürümünü yaz ve sonuna
--ar 3:2 --s 100 --no people, text parametrelerini ekle.
En sonda, görsel için "temsili; yapay zekâ ile üretilmiştir" notunu içeren bir şekil altyazısı öner.

Sahne veya kavram: """ + sahne

    sonuc = yapay_zekaya_sor(ARASTIRMA_TALIMATI, istek)
    print()
    print(sonuc)
    kaydet("Görsel prompt – " + sahne, sonuc)


def tartisma_ortagi():
    """Ders 6: Geçmişi hatırlayan sohbet modu. 'menü' yazınca ana menüye döner."""
    print("Tartışma ortağı modu. Bir argümanı, yöntem kararını veya bulguyu tartışabilirsiniz.")
    print("Ana menüye dönmek için 'menü' yazın.")
    gecmis = []

    tartisma_talimati = ARASTIRMA_TALIMATI + """

TARTIŞMA MODU:
Araştırmacının argümanlarını eleştirel bir meslektaş gibi sına. Övgüye yer verme;
zayıf noktaları, alternatif açıklamaları ve olası hakem itirazlarını göster.
Kuramcı veya kaynak adı uydurma."""

    while True:
        soru = input("Siz: ")

        if soru.lower() in ["menü", "menu"]:
            # Sohbeti kaydedip menüye dön
            if len(gecmis) > 0:
                kayit_metni = ""
                for mesaj in gecmis:
                    if mesaj["role"] == "user":
                        kayit_metni = kayit_metni + "Siz: " + mesaj["content"] + "\n"
                    else:
                        kayit_metni = kayit_metni + "Asistan: " + mesaj["content"] + "\n"
                kaydet("Tartışma kaydı", kayit_metni)
            return

        if soru.strip() == "":
            continue

        gecmis.append({"role": "user", "content": soru})

        try:
            cevap = client.responses.create(
                model=MODEL,
                instructions=tartisma_talimati,
                input=gecmis
            )
            cevap_metni = cevap.output_text
            gecmis.append({"role": "assistant", "content": cevap_metni})
            print("Asistan:", cevap_metni)
            print()
        except Exception as hata:
            print("Bir hata oluştu:", hata)
            gecmis.pop()


# ------------------------------------------------------------
# ANA MENÜ
# ------------------------------------------------------------

def menuyu_goster():
    print()
    print("========== AKADEMİK ÇALIŞMA ASİSTANI ==========")
    print("1 - Paragraf düzelt")
    print("2 - Dosyadan okuma notu çıkar")
    print("3 - Makale başlığı önerileri al")
    print("4 - Sunum / poster için görsel prompt yaz")
    print("5 - Tartışma ortağı")
    print("6 - Çıkış")
    print("===============================================")


while True:
    menuyu_goster()
    secim = input("Seçiminiz (1-6): ")

    if secim == "1":
        paragraf_duzelt()
    elif secim == "2":
        okuma_notu_cikar()
    elif secim == "3":
        baslik_oner()
    elif secim == "4":
        gorsel_prompt_yaz()
    elif secim == "5":
        tartisma_ortagi()
    elif secim == "6":
        print("Kolay gelsin! Bütün çıktılarınız '" + CIKTI_DOSYASI + "' dosyasında.")
        break
    else:
        print("Geçersiz seçim. Lütfen 1 ile 6 arasında bir sayı yazın.")
```

### Kodun Açıklaması

**Sabitler bölümü**

`ARASTIRMA_TALIMATI` ve `STIL_REHBERI` programın en üstünde bir kez tanımlanır. Bütün fonksiyonlar bunları kullanır. Talimatı değiştirmek istediğinizde tek bir yeri değiştirmeniz yeterlidir; tıpkı Ders 3'teki proje talimatı gibi.

**`yapay_zekaya_sor(talimat, istek)`**

API çağrısını tek bir fonksiyonda topladık. Böylece dört farklı menü işlevi aynı kodu tekrar yazmak yerine bu fonksiyonu çağırır. `try/except` sayesinde internet kesilse bile program çökmez; hata mesajı metin olarak döner.

**`kaydet(baslik, metin)`**

`"a"` (append, ekle) modu dosyanın sonuna yazar. Ders 6'da kullandığımız `"w"` modu ise dosyayı silip baştan yazardı. Burada bütün çıktıların birikmesini istediğimiz için `"a"` kullandık. Bu dosya, yapay zekânın hangi iş için nasıl kullanıldığının da bir kaydı olur; yöntem bölümünde yapay zekâ kullanımını açıklarken işe yarar.

**`okuma_notu_cikar()`**

`except FileNotFoundError:` yalnızca "dosya bulunamadı" hatasını yakalar. `return` fonksiyondan çıkar ve program ana menüye döner.

**`baslik_oner()`**

Ders 3'teki çoklu deneme stratejisini kullanır: Başlık türlerini tanımlayarak benzer seçeneklerin önüne geçer.

**`gorsel_prompt_yaz()`**

Stil rehberini isteğin başına ekler (Ders 3) ve Ders 4'teki görsel prompt bileşenlerini ister. Hem doğal dil (GPT Image) hem Midjourney sürümünü üretir ve Ders 3'teki etik ilke gereği altyazı önerisine "temsili" notunu ekletir.

**`tartisma_ortagi()`**

Ders 6'daki chatbot'un fonksiyon hâlidir. Araştırma talimatına bir "tartışma modu" eki yapılarak Ders 2'deki "şeytanın avukatı" rolü kalıcı hâle getirilir. `gecmis` listesi fonksiyonun içinde tanımlandığı için her tartışma oturumu boş başlar. "menü" yazıldığında sohbet kaydedilir ve `return` ile ana menüye dönülür.

**Ana menü**

`while True` döngüsü menüyü sürekli gösterir. `if / elif / else` yapısı seçime göre doğru fonksiyonu çağırır. `elif`, "değilse ve bu doğruysa" demektir. Yalnızca "6" seçildiğinde `break` ile program biter.

### Beklenen Sonuç

Program çalıştırıldığında:

```text
========== AKADEMİK ÇALIŞMA ASİSTANI ==========
1 - Paragraf düzelt
2 - Dosyadan okuma notu çıkar
3 - Makale başlığı önerileri al
4 - Sunum / poster için görsel prompt yaz
5 - Tartışma ortağı
6 - Çıkış
===============================================
Seçiminiz (1-6): 3
Başlık önerisi istediğiniz makalenin konusu ve ana bulgusu: 1950-1980 apartman dairelerinde salonun temsil mekânına dönüşmesi

1. Gündelik Hayattan Vitrine: 1950–1980 Apartman Dairelerinde Salon (Ana başlık: Alt başlık)
2. Salon Kimin İçindi? Orta Sınıf Konutta Temsil ve Gündelik Hayat (soru)
3. Temsil Mekânı Olarak Salon (kavram odaklı)
4. İstanbul ve Ankara Apartman Dairelerinde Salonun Dönüşümü, 1950–1980 (açıklayıcı)
5. Vitrin, Takım Koltuk ve Kapalı Kapı: Salonun Nesneleri (nesne odaklı)
(Sonuç 'asistan_ciktilari.txt' dosyasına eklendi.)
```

Hatalı seçimde:

```text
Seçiminiz (1-6): 9
Geçersiz seçim. Lütfen 1 ile 6 arasında bir sayı yazın.
```

Var olmayan dosyada:

```text
Seçiminiz (1-6): 2
Okunacak dosyanın adı (örnek: ozet1.txt): yok.txt
Dosya bulunamadı. Dosya adını ve klasörü kontrol edin.
```

Program kapandığında `asistan_ciktilari.txt` dosyası bütün oturumun çıktılarını başlıklarıyla birlikte içerir.

### Projeyi Geliştirelim

Projeyi daha da geliştirmek için ek özellikler:

1. **Toplu okuma notu:** Menüye "Klasördeki bütün .txt dosyalarından okuma notu çıkar" seçeneği ekleyin (`os.listdir` kullanarak).
2. **Terim tutarlılık kontrolü:** Ders 3'teki terimler sözlüğünü ekleyip paragrafı terim açısından kontrol eden bir seçenek ekleyin.
3. **Hakem gözüyle okuma:** Paragrafı hakem, yöntem uzmanı ve alan dışı okur rolleriyle değerlendiren bir seçenek ekleyin (Ders 2).
4. **Bildiri özeti kontrolü:** Bir özetin kelime sayısını Python ile sayan ve amaç–yöntem–bulgular–sonuç yapısını yapay zekâya kontrol ettiren bir seçenek ekleyin.
5. **Token ve maliyet takibi:** Her istekte kullanılan token sayısını toplayıp çıkışta toplam token'ı gösterin.
6. **Tartışma geçmişi sınırı:** Tartışma modunda yalnızca son 10 mesajı gönderin.
7. **Görsel üretim:** OpenAI'ın görsel modelini (`gpt-image` ailesi) kullanarak görsel promptundan doğrudan görsel üretip dosyaya kaydedin (belgelerden güncel kullanım biçimini araştırın).
8. **Kayıt bilgisi:** Her kaydın başına tarih, saat ve kullanılan model adını ekleyin (`datetime` modülü); bu, yöntem bölümünde yapay zekâ kullanımını belgelemeyi kolaylaştırır.
9. **Sözlü tarih modu:** Bir transkript dosyasından sözlü tarih okuma notu çıkaran seçenek ekleyin (Ders 4).
10. **Ayarlar dosyası:** Model adını ve talimatları ayrı bir `ayarlar.txt` dosyasından okuyun; kodu değiştirmeden ayar yapılabilsin.

---

## Ek Alıştırmalar

### Kolay

**Alıştırma 1 – Prompt iyileştirme**

Şu promptu 6 kontrol sorusunu kullanarak iyileştirin: `Bana mimarlıkla ilgili bir makale yaz.`

**Alıştırma 2 – Ton dönüşümü**

Şu cümleyi akademik, alan dışı okura yönelik ve sosyal medya tonlarında yeniden yazdıracak tek bir prompt yazın: *"Apartman dairelerinde balkonlar zamanla camla kapatılarak odaya katıldı."*

**Alıştırma 3 – Görsel prompt tamamlama**

Şu görsel prompt eksik: `Bir cumba, sulu boya.` Eksik bileşenleri (ortam, ışık, perspektif, malzeme, renk, oran) ekleyerek bir sunum görseli için tamamlayın.

**Alıştırma 4 – Kod çıktısı tahmini**

```python
mekan = "sofa"
sayi = 3
print(mekan.upper() + " - " + str(sayi) + " kez geçti")
```

**Alıştırma 5 – Hatayı bul**

```python
kelimeler = ["sofa", "cumba", "eyvan"]
for kelime in kelimeler
    print(kelime)
```

### Orta

**Alıştırma 6 – Few-shot kavram seti**

Tezinizin kavramlar ekine "kafes, hamamlık, ocak, sergen, kerevet" terimlerini aynı biçimde ekletecek bir few-shot prompt yazın. En az iki farklı örnek kullanın.

**Alıştırma 7 – Rol ve adım adım düşünme**

Bir mimarlık tarihi makalesinde nesnel üçüncü şahıs anlatımı mı, yoksa araştırmacının konumunu görünür kılan birinci tekil şahıs ("bu çalışmada ben...") mı kullanılmalı? Bu kararı, iki rol (dergi editörü ve nitel yöntem uzmanı) ve en az 4 adımlı bir düşünce zinciriyle değerlendirtecek bir prompt yazın.

**Alıştırma 8 – Sistem talimatı yazma**

Bir mimarlık konferansına bildiri yazma sürecinde kullanılacak bir "Bildiri Asistanı" sistem talimatı yazın. Kimlik, en az 4 kesin kural ve varsayılan cevap biçimi içersin.

**Alıştırma 9 – Kelime sayacı programı**

`metin.txt` dosyasını (örneğin bir görüşme transkripti) okuyup "sofa", "salon" ve "mutfak" kelimelerinin metinde kaç kez geçtiğini yazdıran bir Python programı yazın. Büyük-küçük harf farkı önemsenmesin.

**Alıştırma 10 – Asistan test tablosu**

Ders 5'teki sempozyum katılımcı destek asistanı için **yeni** 6 test sorusu tasarlayın: 2'si SSS'de cevabı olan, 2'si SSS'de olmayan, 1'i yetki dışı (söz verme), 1'i başka dilde. Her biri için beklenen davranışı yazın.

### Nispeten Zor

**Alıştırma 11 – Klasördeki bütün dosyalar**

Ders 6'daki `toplu_okuma_notu.py` programını, dosya adlarını elle yazmak yerine bulunduğu klasördeki bütün `.txt` dosyalarını otomatik bulacak şekilde geliştirin. Sonuç dosyası (`literatur_notlari.txt`) ve SSS dosyası işlenmesin. Bir dosyada API hatası olursa program diğer dosyalarla devam etsin.

**Alıştırma 12 – Akıllı chatbot**

`sempozyum_chatbot.py`yi şu özelliklerle geliştirin:

- Sadece son 6 mesaj modele gönderilsin.
- Her cevaptan sonra o istekteki token sayısı ve oturumdaki toplam token yazdırılsın.
- Kullanıcı `/sifirla` yazarsa sohbet geçmişi temizlensin.

**Alıştırma 13 – Sözlü tarih işleme hattı**

Bir sözlü tarih transkriptini (`transkript.txt`) üç aşamada işleyen bir Python programı yazın:

1. Transkriptten okuma notu çıkarsın (mekânlar, kullanım biçimleri, katılımcının kısa alıntıları).
2. Okuma notundan, makalenin bulgular bölümü için 150 kelimelik akademik bir paragraf yazsın (alıntıları değiştirmeden).
3. Paragraftan, sunum için stil rehberine uygun bir görsel prompt yazsın.

Her aşamanın çıktısı bir sonraki aşamanın girdisi olsun ve üç çıktı da `hat_sonucu.txt` dosyasına kaydedilsin.

---

## Ek Alıştırmalar – Çözümler

**Çözüm 1**

```text
Mimarlık tarihi alanında hakemli bir dergiye gönderilecek, geleneksel Türk evindeki "hayat"
mekânının mevsimsel kullanımını inceleyen bir makalenin giriş bölümü için 400 kelimelik bir taslak yaz.
Okurlar mimarlık tarihçileri ve konut araştırmacılarıdır. Bölüm şu sırayı izlesin:
konunun önemi, literatürdeki boşluk, araştırma sorusu, yöntemin tek cümlelik özeti.
Akademik ve temkinli bir dil kullan. Kaynak, yazar adı ve tarih uydurma; atıf gereken yerlere [ATIF] yaz.
```

(Ne: giriş bölümü taslağı; Neden: hakemli dergi makalesi; Kim için: mimarlık tarihçileri; Ne bilgiyle: konu ve bölüm yapısı; Nasıl: 400 kelime, akademik ton; Ne olmasın: kaynak uydurma.)

> **Not:** Yapay zekâya bütün bir makale yazdırmak akademik etik açısından kabul edilmez. Burada istenen, araştırmacının kendi bulgularıyla dolduracağı bir taslak ve yapı önerisidir.

**Çözüm 2**

```text
Aşağıdaki cümleyi üç farklı tonda yeniden yaz:
1. Akademik (temkinli, nesnel, 1–2 cümle)
2. Alan dışı okura yönelik (sade, örnekli, 2–3 cümle)
3. Sosyal medya (anlaşılır, okura soru soran, en fazla 40 kelime, 2 hashtag)
Bilgiye sadık kal; yeni bilgi ekleme.

Cümle: "Apartman dairelerinde balkonlar zamanla camla kapatılarak odaya katıldı."
```

**Çözüm 3**

```text
19. yüzyıl İstanbul'unda dar bir sokağa taşan ahşap bir cumba (ortam), karşı kaldırımdan hafif
alttan bakış (perspektif), ahşap kaplama, kafesli pencereler, altında eğik payandalar (malzeme),
ikindi güneşinin cepheye düşen sıcak ışığı (ışık), ince çizgi ve sulu boya (tarz),
okra, krem ve soluk turkuaz tonları (renk), yatay 3:2 oran, insan figürü ve yazı yok (teknik).
```

**Çözüm 4**

```text
SOFA - 3 kez geçti
```

`upper()` metni büyük harfe çevirir; `str(sayi)` sayıyı metne dönüştürür.

**Çözüm 5**

`for` satırının sonunda iki nokta (`:`) eksiktir.

```python
kelimeler = ["sofa", "cumba", "eyvan"]
for kelime in kelimeler:
    print(kelime)
```

Çıktı:

```text
sofa
cumba
eyvan
```

**Çözüm 6**

```text
Tezimin "Kavramlar" eki için madde yazacaksın. Aşağıdaki örneklerin biçimini ve uzunluğunu
aynen izle: tanım – işlev – plan tipolojisindeki yeri, üç kısa cümle.

Örnek 1:
**Sofa** – Geleneksel Türk evinde odaların açıldığı ortak alan. Hem dolaşım hem toplanma mekânıdır. Plan tipolojisinde belirleyici öğedir.

Örnek 2:
**Yüklük** – Oda duvarına gömülü büyük dolap. Gündüz yatakların saklanmasını sağlayarak odayı çok amaçlı kılar. Odanın işlevsel esnekliğinin temel donatısıdır.

Şimdi şu terimler için madde yaz: kafes, hamamlık, ocak, sergen, kerevet.
Emin olmadığın bir terim varsa tanım uydurma; "[DOĞRULANMALI]" yaz.
```

(Not: "sergen" ve "kerevet" gibi daha az bilinen terimlerde modelin tanımları mutlaka bir mimarlık sözlüğünden doğrulanmalı ve tezde atıfla verilmelidir.)

**Çözüm 7**

```text
## BAĞLAM
Geleneksel konutta gündelik hayatı sözlü tarih görüşmeleri ve plan analiziyle inceleyen bir
mimarlık tarihi makalesi yazıyorum. Anlatım biçimine karar vermem gerekiyor:
A) Nesnel üçüncü şahıs / edilgen anlatım ("Bu çalışmada ... incelenmiştir.")
B) Araştırmacının konumunu görünür kılan birinci tekil şahıs ("Bu çalışmada ... inceledim.")

## GÖREV
Bu kararı iki rolle ve adım adım değerlendir.

Rol 1: Mimarlık tarihi alanında hakemli bir derginin editörü
Rol 2: Nitel araştırma yöntemleri uzmanı

Her rol için şu adımları izle:
1. Her seçeneğin okurla kurduğu ilişkiyi tarif et.
2. Her seçeneğin nesnellik ve güvenilirlik algısına etkisini değerlendir.
3. Sözlü tarih gibi nitel yöntemlerde araştırmacının konumunun (refleksivite) görünür olmasının önemini değerlendir.
4. Her seçenekle yazılmış birer örnek cümle ver.
5. Rolün tercihini gerekçesiyle yaz.

En sonda iki rolün görüşlerini birleştiren bir öneri yap (örneğin yöntem bölümünde birinci tekil
şahıs, bulgularda nesnel anlatım gibi karma bir kullanım mümkün mü?) ve derginin yazım
kılavuzunun belirleyici olduğunu hatırlat.
```

**Çözüm 8**

```text
# KİMLİK
Sen mimarlık alanında akademik bildiri yazımına yardım eden bir yazım asistanısın.

# KESİN KURALLAR
1. Asla kaynak, künye, DOI, sayfa numarası veya alıntı uydurma.
2. Araştırmacının verdiği veri ve bulguların dışına çıkma; yorumlarını "Öneri:" ile ayır.
3. Kesin hükümler yerine temkinli akademik dil kullan ("işaret etmektedir", "düşündürmektedir").
4. Emin olmadığın her bilgi için [DOĞRULANMALI] yaz.
5. Konferansın kelime sınırları verilmişse kesinlikle aşma ve sonunda kelime sayısını belirt.

# VARSAYILAN CEVAP BİÇİMİ
- Dil: Araştırmacı hangi dilde isterse (varsayılan Türkçe).
- Özet istenirse: Amaç – Yöntem – Bulgular – Sonuç sırasıyla.
- Düzeltme istenirse: önce düzeltilmiş metin, sonra değişiklik listesi.
- Görev belirsizse en fazla 3 netleştirici soru sor.
```

**Çözüm 9**

```python
# kelime_sayaci.py
# Bir metin dosyasında belirli kelimelerin kaç kez geçtiğini sayar.

with open("metin.txt", "r", encoding="utf-8") as dosya:
    metin = dosya.read()

# Büyük-küçük harf farkını ortadan kaldırmak için metni küçük harfe çevir
metin = metin.lower()

aranacaklar = ["sofa", "salon", "mutfak"]

for kelime in aranacaklar:
    sayi = metin.count(kelime)  # Metinde kaç kez geçtiğini sayar
    print(kelime + ": " + str(sayi) + " kez")
```

Örnek çıktı (metne göre değişir):

```text
sofa: 4 kez
salon: 2 kez
mutfak: 1 kez
```

**Kod Nasıl Çalışıyor?** `lower()` bütün metni küçük harfe çevirir, böylece "Sofa" ve "sofa" aynı sayılır. `count()` bir metin parçasının kaç kez geçtiğini sayar.

> **Dikkat:** `count()` kelimenin parçası olarak geçtiği yerleri de sayar ("sofalı", "sofada" da "sofa" olarak sayılır). Bu, Türkçe gibi eklemeli dillerde çoğu zaman istenen bir sonuçtur; ama tam kelime eşleşmesi gerekiyorsa farklı bir yöntem gerekir. Ayrıca Türkçedeki büyük "I" harfi `lower()` ile "ı" yerine "i" olabilir; "Işık" gibi kelimelerde buna dikkat edin. Akademik bir içerik analizinde bu tür sayımlar yalnızca ön keşif amaçlıdır; kodlama şeması ve nitel okuma yerine geçmez.

**Çözüm 10**

| No | Test sorusu | Tür | Beklenen davranış |
|---|---|---|---|
| 1 | Sempozyum hangi tarihlerde? | SSS'de var | "12–13 Mart, İstanbul" |
| 2 | Kabul sonuçları ne zaman açıklanıyor? | SSS'de var | "15 Ocak'ta e-posta ile" |
| 3 | Sempozyum sonrası tam metinler bir dergide yayımlanacak mı? | SSS'de yok (yalnızca bildiri kitabı var) | Bildiri kitabını söyler; dergi konusunda bilgi olmadığını belirtip yönlendirir |
| 4 | Konaklama için anlaşmalı otel var mı? | SSS'de yok | Bilgi yok, uydurmaz, yönlendirir |
| 5 | Özetimi kurula iletip kabul edilmesini sağlar mısınız? | Yetki dışı | Söz vermez; kararın kurula ait olduğunu söyler |
| 6 | Wann ist die Einreichungsfrist? | Başka dil | Almanca cevap: 15 Aralık |

**Çözüm 11**

```python
# toplu_okuma_notu_gelismis.py
# Klasördeki bütün .txt dosyalarını otomatik bulur ve okuma notu çıkarır.

import os  # İşletim sistemi işlemleri (klasör içeriğini listelemek) için
from openai import OpenAI

client = OpenAI()
MODEL = "gpt-5.4-mini"

TALIMAT = """Sen mimarlık tarihi ve konut çalışmaları alanında titiz bir araştırma asistanısın.
Sadece verilen metne dayan. Metinde olmayan bilgi ekleme.
Bulunmayan alanlar için "Metinde belirtilmemiş" yaz."""

SONUC_DOSYASI = "literatur_notlari.txt"
ATLANACAKLAR = [SONUC_DOSYASI, "sss_sempozyum.txt"]

# Klasördeki dosyalardan sadece .txt ile bitenleri ve atlanmayacakları seç
dosyalar = []
for ad in os.listdir("."):  # "." bulunduğumuz klasör demektir
    if ad.endswith(".txt") and ad not in ATLANACAKLAR:
        dosyalar.append(ad)

print(str(len(dosyalar)) + " dosya bulundu.")

basarili = 0
basarisiz = 0

with open(SONUC_DOSYASI, "w", encoding="utf-8") as sonuc:
    for dosya_adi in dosyalar:
        print(dosya_adi + " işleniyor...")

        with open(dosya_adi, "r", encoding="utf-8") as dosya:
            metin = dosya.read()

        istek = """Aşağıdaki metinden şu başlıklarla bir okuma notu hazırla:
- Ana iddia (1 cümle)
- Yöntem ve veri (1–2 cümle)
- Temel bulgular (en fazla 3 madde)
- Önemli kavramlar

Metin:
""" + metin

        try:
            cevap = client.responses.create(
                model=MODEL,
                instructions=TALIMAT,
                input=istek
            )
            sonuc.write("=== " + dosya_adi + " ===\n")
            sonuc.write(cevap.output_text + "\n\n")
            basarili = basarili + 1
        except Exception as hata:
            # Hata olursa bu dosyayı atla, diğerleriyle devam et
            print("  Hata: " + dosya_adi + " işlenemedi (" + str(hata) + ")")
            sonuc.write("=== " + dosya_adi + " ===\nİŞLENEMEDİ\n\n")
            basarisiz = basarisiz + 1

print("Bitti. Başarılı: " + str(basarili) + ", Başarısız: " + str(basarisiz))
```

**Kod Nasıl Çalışıyor?** `os.listdir(".")` klasördeki bütün dosya adlarını verir. `endswith(".txt")` yalnızca `.txt` ile bitenleri seçer. `not in ATLANACAKLAR` sonuç ve SSS dosyalarını dışarıda bırakır. `try/except` döngünün içinde olduğu için bir dosyadaki hata diğerlerini durdurmaz.

**Çözüm 12**

```python
# sempozyum_chatbot_gelismis.py
# Son 6 mesajı gönderen, token sayan ve sıfırlanabilen chatbot.

from openai import OpenAI

client = OpenAI()
MODEL = "gpt-5.4-mini"

with open("sss_sempozyum.txt", "r", encoding="utf-8") as dosya:
    sss_metni = dosya.read()

TALIMAT = """Sen "Konut ve Gündelik Hayat Sempozyumu"nun katılımcı destek asistanısın.
Sadece aşağıdaki SSS bilgilerini kullan. SSS'de olmayan bilgiyi uydurma; katılımcıyı
sempozyum@ornek-universite.edu.tr adresine yönlendir. Kabul, ücret veya süre uzatma
konusunda söz verme. Cevapların 3 cümleyi geçmesin.

SSS BİLGİLERİ:
""" + sss_metni

gecmis = []
toplam_token = 0

print("Katılımcı Asistanı – Komutlar: 'çıkış' ile kapat, '/sifirla' ile sohbeti temizle.")

while True:
    soru = input("Siz: ")

    if soru.lower() in ["çıkış", "cikis", "exit"]:
        print("Oturumdaki toplam token: " + str(toplam_token))
        break

    if soru.strip() == "/sifirla":
        gecmis = []
        print("Sohbet geçmişi temizlendi.")
        continue

    if soru.strip() == "":
        continue

    gecmis.append({"role": "user", "content": soru})

    # Sadece son 6 mesajı gönder (eski mesajlar maliyeti artırmasın)
    gonderilecek = gecmis[-6:]

    try:
        cevap = client.responses.create(
            model=MODEL,
            instructions=TALIMAT,
            input=gonderilecek
        )
        cevap_metni = cevap.output_text
        gecmis.append({"role": "assistant", "content": cevap_metni})

        bu_istek = cevap.usage.total_tokens
        toplam_token = toplam_token + bu_istek

        print("Asistan:", cevap_metni)
        print("(Bu istek: " + str(bu_istek) + " token | Toplam: " + str(toplam_token) + " token)")
        print()
    except Exception as hata:
        print("Bir hata oluştu:", hata)
        gecmis.pop()
```

**Kod Nasıl Çalışıyor?** `gecmis[-6:]` listenin son 6 elemanını alır (eksi sayılar listenin sonundan saymak demektir). Bu sayede sohbet uzasa bile gönderilen token sayısı sınırlı kalır; karşılığında model çok eski mesajları hatırlamaz. Bu, Ders 1'deki bağlam penceresi ile maliyet arasındaki dengenin kod hâlidir. `/sifirla` komutunda `gecmis = []` ile liste boşaltılır.

**Çözüm 13**

```python
# sozlu_tarih_hatti.py
# Bir transkripti üç aşamada işler: okuma notu -> bulgular paragrafı -> sunum görsel promptu.

from openai import OpenAI

client = OpenAI()
MODEL = "gpt-5.4-mini"

TALIMAT = """Sen apartmanlaşma üzerine bir sözlü tarih araştırmasının araştırma ve akademik yazım asistanısın.
Asla bilgi, tarih veya alıntı uydurma. Katılımcının sözlerini alıntılarken değiştirme.
Emin olmadığın bilgi için [DOĞRULANMALI] yaz."""

STIL_REHBERI = """Teknik: ince siyah çizgi + hafif sulu boya. Renkler: sıcak toprak tonları,
krem, soluk turkuaz. Işık: yumuşak gün ışığı. Göz hizası iç mekân perspektifi.
İnsan figürü yok. Görselde yazı yok."""


def sor(istek):
    """Tek seferlik API isteği gönderir ve cevap metnini döndürür."""
    cevap = client.responses.create(model=MODEL, instructions=TALIMAT, input=istek)
    return cevap.output_text


# Transkripti oku (transkript önceden anonimleştirilmiş olmalıdır)
with open("transkript.txt", "r", encoding="utf-8") as dosya:
    transkript = dosya.read()

# AŞAMA 1: Transkriptten okuma notu
print("1. aşama: Okuma notu çıkarılıyor...")
okuma_notu = sor("""Bu sözlü tarih transkriptinden okuma notu çıkar:
- Bahsedilen mekânlar ve eşyalar
- Mekânların kullanım biçimleri (kim, ne zaman, ne için)
- Katılımcının kendi kelimeleriyle en fazla 3 kısa alıntı (tırnak içinde, değiştirmeden)
Transkriptte olmayan hiçbir bilgi ekleme.

Transkript:
""" + transkript)

# AŞAMA 2: Okuma notundan bulgular paragrafı (1. aşamanın çıktısı girdi oluyor)
print("2. aşama: Bulgular paragrafı yazılıyor...")
paragraf = sor("""Aşağıdaki okuma notuna dayanarak, bir makalenin bulgular bölümü için 150 kelimelik
akademik bir paragraf yaz. Paragraf bir bulgu cümlesiyle başlasın. Nottaki alıntılardan en az birini
tırnak içinde, hiç değiştirmeden ve "(Katılımcı 1)" etiketiyle kullan. Notta olmayan bilgi ekleme;
tek bir görüşmeden genelleme yapma.

Okuma notu:
""" + okuma_notu)

# AŞAMA 3: Paragraftan sunum görsel promptu (2. aşamanın çıktısı girdi oluyor)
print("3. aşama: Görsel prompt yazılıyor...")
gorsel_prompt = sor("""Aşağıdaki stil rehberine uygun olarak, paragraftaki mekân kullanımını bir
konferans sunumunda anlatmak için en fazla 80 kelimelik bir görsel üretim promptu yaz.

Stil rehberi:
""" + STIL_REHBERI + """

Paragraf:
""" + paragraf)

# Üç çıktıyı dosyaya kaydet
with open("hat_sonucu.txt", "w", encoding="utf-8") as sonuc:
    sonuc.write("=== 1. OKUMA NOTU ===\n" + okuma_notu + "\n\n")
    sonuc.write("=== 2. BULGULAR PARAGRAFI ===\n" + paragraf + "\n\n")
    sonuc.write("=== 3. GÖRSEL PROMPT ===\n" + gorsel_prompt + "\n")

print("Tamamlandı. Sonuçlar 'hat_sonucu.txt' dosyasında.")
```

**Kod Nasıl Çalışıyor?** Bu programa **prompt zinciri** (prompt chaining) denir: Her aşamanın çıktısı bir sonraki aşamanın girdisi olur. Büyük bir işi tek bir dev prompt yerine küçük, kontrol edilebilir adımlara böler; Ders 3'te görsel düzenlemeyi adım adım yapmamızın kod karşılığıdır. Her aşamanın çıktısı ayrı kaydedildiği için hangi aşamada sorun çıktığı kolayca görülür.

> **Dikkat:** Zincirde ilk aşamadaki bir hata (örneğin yanlış aktarılmış bir alıntı) sonraki bütün aşamalara taşınır. Bu yüzden özellikle 1. aşamanın çıktısını transkriptle karşılaştırarak kontrol edin. Sözlü tarih kayıtları için katılımcı izni, anonimleştirme ve etik kurul kuralları burada da geçerlidir. Yapay zekâ bir nitel analiz yardımcısıdır; temaları belirleme ve yorumlama sorumluluğu araştırmacıdadır.

---

**Kursun sonu.** Altı ders boyunca akademik çalışmanın bütün aşamalarında yapay zekâyı kullanmayı öğrendik: konuyu araştırma sorusuna dönüştürmekten literatür taramasına, okuma notlarından makale ve bildiri yazımına, hakem gözüyle okumadan sunum ve poster görsellerine, kod yazmadan kurulan asistanlardan kendi programlarımıza kadar. En önemli ilke değişmedi: **Yapay zekâ güçlü bir araştırma yardımcısıdır; yargı, doğrulama, etik sorumluluk ve özgün katkı araştırmacıya aittir.**
