# AI Product Safety Checklist for Early-Stage Teams

> **Proje:** ai-safety-lab · **Kapsam:** Erken Aşama Ürün Ekipleri · **Dil:** Türkçe  

---

## Executive Summary

Bu çalışma, yapay zeka veya büyük dil modeli (LLM) özelliği geliştiren erken aşama ürün ekipleri için hazırlanmış, savunma odaklı bir güvenlik kontrol listesidir. Amacı, güvenlik konusunu sonraya bırakmak yerine ürünün ilk aşamalarından itibaren ele almanın neden ve nasıl yapılması gerektiğini somut adımlarla ortaya koymaktır.

Bu içerik; geliştiriciler, ürün yöneticileri ve kurucu ortaklar dahil olmak üzere teknik ve teknik olmayan tüm ekip üyelerinin okuyabileceği bir dilde yazılmıştır. İçerdiği maddeler belirli bir model veya platforma özgü değildir; her ürün tipine uyarlanabilecek genel ilkeler üzerine kuruludur.

Listedeki tüm maddelerin aynı anda uygulanması beklenmez. Öncelikli maddeler belirlenmeli, bir sonraki çalışma dönemine eklenmeli ve zamanla kapsam genişletilmelidir. Önemli olan; güvenliği ciddiye alan, yazılı ve sürekli geliştirilen bir uygulama kültürü oluşturmaktır.

---

## Context

Geleneksel yazılımda bir sisteme aynı girdi verildiğinde her zaman aynı çıktı alınır. Bu durum testleri ve güvenlik kontrollerini öngörülebilir kılar. Dil modelleri ise aynı soruya farklı zamanlarda farklı yanıtlar üretebilir. Bu belirsizlik, mevcut güvenlik testlerinin tek başına yeterli olmadığı anlamına gelir.

Bunun yanında, yapay zeka sistemleri "prompt injection" adıyla bilinen yeni bir saldırı türüne karşı savunmasızdır. Bu saldırıda kötü niyetli bir kullanıcı, modeli istenmeyen biçimlerde davranmaya yönlendiren özel bir metin yazar. Geleneksel güvenlik araçları — güvenlik duvarı, statik kod analizi gibi çözümler — bu tür saldırıları büyük ölçüde fark edemez. Güvenlik artık yalnızca ağ ve uygulama katmanında değil, dilin ve anlamın kendisinde de sağlanmak zorundadır.

Son olarak, harici bir yapay zeka servisi kullanıldığında o servisin güvenlik açıkları da ürünün sorunu haline gelir. Modeli kimin eğittiği, hangi verilerle beslendiği ve servis sağlayıcısının altyapısının ne kadar güvenli olduğu; doğrudan kontrol edilemeyen ancak ürünü doğrudan etkileyen unsurlardır.

---

## Türkiye Relevance

Türkiye'de faaliyet gösteren veya Türkiye'de kullanıcısı bulunan ürün ekipleri için yapay zeka güvenliği yalnızca teknik bir konu değil, aynı zamanda yasal bir yükümlülüktür.

**KVKK (Kişisel Verileri Koruma Kanunu):** 6698 sayılı KVKK, kişisel verilerin toplanması, işlenmesi ve üçüncü taraflarla paylaşılması konusunda net yükümlülükler getirir. Kullanıcı verilerinin bir yapay zeka API'sine kontrolsüz biçimde gönderilmesi, teknik bir sorunun ötesinde doğrudan yasal sorumluluk doğurabilir. Veri işleme faaliyetlerinin belgelenmesi, açık rıza alınması ve veri aktarım sözleşmelerinin yapılması bu kapsamda zorunludur.

**GDPR Etkisi:** Avrupa Birliği'ndeki kullanıcılara hizmet verilmesi durumunda GDPR hükümleri de geçerli olur. Her iki düzenleme de veri minimizasyonunu, amaca sınırlılığı ve güvenli veri aktarımını temel ilke olarak benimsemektedir.

**Düzenleyici Ortam:** Türkiye'de KVKK uygulamalarının giderek güçlendiği ve denetim kapsamının genişlediği görülmektedir. Yapay zeka ürün kararlarının bu yasal çerçeve içinde değerlendirilmesi, ileride oluşabilecek idari yaptırımların önüne geçmek açısından kritik önem taşır.

---

## Safety Areas

Bu kontrol listesi beş temel güvenlik alanını kapsamaktadır:

**1. Girdi ve Çıktı Denetimi:** Kullanıcıdan gelen verilerin modele iletilmeden önce doğrulanması; modelden dönen yanıtların kullanıcıya sunulmadan önce kontrol edilmesi.

**2. İstek Hacmi Kontrolü (Rate Limiting):** Hem kötüye kullanımı hem de beklenmedik maliyetleri önlemek amacıyla kullanıcı ve oturum bazında istek sayısının sınırlandırılması.

**3. Onay Gerektiren İşlemler:** Geri alınamaz veya yüksek etkili işlemler için kullanıcının açık onayının alınması ve bu işlemlerin kayıt altına alınması.

**4. Kayıt ve İzleme (Logging & Monitoring):** Model etkileşimlerinin kişisel veri korumasına uygun biçimde günlüklenmesi ve olağandışı davranışların otomatik olarak tespit edilmesi.

**5. Harici Servis Yönetimi:** Harici yapay zeka API'leriyle paylaşılan verilerin sınırlandırılması, sağlayıcı sözleşmelerinin incelenmesi ve servisin ulaşılamadığı durumlara karşı hazırlıklı olunması.

---

## Practical Checklist

### 1. Girdi ve Çıktı Denetimi

- [ ] **Kullanıcıdan gelen her metin, modele gönderilmeden önce kontrol edilir ve temizlenir.**  
  Girdilerin uzunluk sınırı, kabul edilebilir karakter kümesi ve içerik türü önceden tanımlanmalıdır. "Beklenen formatta mı?" sorusunun yanı sıra "bu sistem bağlamı için uygun mu?" sorusu da değerlendirilmelidir. Kullanıcı metni hiçbir zaman doğrudan sistem talimatlarına eklenmemeli; her zaman ayrı bir kullanıcı mesajı bloğu olarak işlenmelidir.

- [ ] **Modelden gelen yanıtlar, kullanıcıya gösterilmeden veya başka bir sisteme iletilmeden önce bir denetim aşamasından geçirilir.**  
  Yapay zekanın üretebileceği zararlı içerik kategorilerinin önceden listelenmesi ve bu kategorileri yakalayan bir filtre katmanı oluşturulması önerilir. Bu katman kural tabanlı olabileceği gibi başka bir modelle de uygulanabilir. Model çıktısı otomatik olarak çalıştırılacaksa (örneğin kod veya veritabanı sorgusu), söz konusu işlem izole bir ortamda gerçekleştirilmelidir.

- [ ] **Sistem talimatları ile kullanıcı girdisi yapısal olarak birbirinden ayrılır ve kullanıcı bu sınırı aşamaz.**  
  Şablon yapıları sabit tutulmalı; değişken içerikler yalnızca veri düzeyinde eklenmeli, talimat düzeyinde birbirine karıştırılmamalıdır. Bu ayrımın kod incelemelerinde ve testlerde düzenli olarak doğrulandığından emin olunmalıdır.

---

### 2. İstek Hacmi Kontrolü (Rate Limiting)

- [ ] **Her kullanıcı veya oturum için belirli bir zaman diliminde yapılabilecek istek sayısı sınırlandırılır.**  
  Dakikalık, saatlik ve günlük istek kotaları belirlenmeli; bu kotalar kullanıcı kimliği, IP adresi veya oturum bilgisi üzerinden takip edilmelidir. Anormal istek artışlarını otomatik olarak tespit eden bir uyarı mekanizması kurulmalıdır. Limit aşımlarında kullanıcıya standart HTTP 429 yanıtı döndürülmeli ve yeniden deneme süresi bildirilmelidir.

- [ ] **Yapay zeka çağrılarının toplam maliyeti sistem genelinde izlenir ve bir üst sınıra bağlanır.**  
  Her token tüketimi doğrudan bir maliyete karşılık gelir. Kullanıcı veya hesap başına günlük ve aylık harcama limitleri tanımlanmalıdır. Limitlerin yüzde seksenine ulaşıldığında ekibi uyaran bir alarm kurulmalıdır. Limit aşımında sistemin nasıl davranacağı (sert durdurma ya da kullanıcıyı bilgilendirerek devam etme) önceden belirlenmeli ve kayıt altına alınmalıdır.

---

### 3. Onay Gerektiren İşlemler

- [ ] **Geri alınamaz veya yüksek etkili işlemler yapay zeka tarafından doğrudan tetiklenemez; önce kullanıcı onayı alınmalıdır.**  
  Veri silme, e-posta gönderme, ödeme başlatma ve harici servise bağlanma gibi işlemler bu kapsamdadır. Yapay zekanın gerçekleştirebileceği tüm işlemler "düşük etkili" ve "yüksek etkili" olarak sınıflandırılmalıdır. Yüksek etkili işlemler için kullanıcıya yapılacak işlem açıkça özetlenmeli ve işleme devam etmek için açık bir onay talep edilmelidir.

- [ ] **Kullanıcı adına gerçekleştirilen her otomatik işlem, kim tarafından, ne zaman ve hangi gerekçeyle yapıldığını gösteren bir kayıt bırakır.**  
  Bu kayıtlar şeffaflık açısından ve ileride yaşanabilecek sorunların geriye dönük incelenmesi için gereklidir. Kayıtlara kullanıcılar tarafından erişilememeli ve değiştirilememeli; yalnızca yetkili sistem yöneticileri bu kayıtlara ulaşabilmelidir.

---

### 4. Kayıt ve İzleme (Logging & Monitoring)

- [ ] **Modele gönderilen mesajlar ve alınan yanıtlar, kişisel bilgiler gizlenerek kaydedilir ve belirli bir süre saklanır.**  
  Bu kayıtlar hem hata ayıklamak hem de güvenlik olaylarını ilerleyen dönemde incelemek için gereklidir. KVKK ve GDPR kapsamında isim, e-posta, kimlik numarası gibi kişisel veriler kaydedilmeden önce gizlenmeli veya anonim hale getirilmelidir. Kayıtların saklama süresi ve erişim yetkileri yazılı bir politikayla belirlenmelidir.

- [ ] **Modelin olağandışı veya zararlı görünen çıktıları için otomatik bir uyarı sistemi kurulur.**  
  Belirli içerik kategorileri tespit edildiğinde ekibi bilgilendiren bir mekanizma oluşturulmalıdır. Bu uyarılar e-posta, anlık mesajlaşma veya bir olay takip aracı aracılığıyla iletilebilir. Yanlış alarm oranı düzenli olarak gözden geçirilmeli ve uyarı eşikleri buna göre ayarlanmalıdır.

---

### 5. Harici Servis Yönetimi

- [ ] **Bulut tabanlı bir yapay zeka API'sine hangi verilerin gönderildiği açıkça tanımlanır; hassas ve kişisel veriler bu kapsamın dışında tutulur.**  
  Hangi veri kategorilerinin dışarıya iletildiği yazılı olarak belgelenmelidir. Kullanıcı kimlik bilgileri, sözleşme içerikleri, sağlık verileri ve finansal bilgiler gibi hassas içeriklerin modele gönderilmesi teknik yöntemlerle engellenmelidir. "Yalnızca gerekli olanı gönder" ilkesi, sistem tasarımının temel kuralı haline getirilmelidir.

- [ ] **Kullanılan her harici modelin veri saklama ve eğitim politikası incelenir; hizmet sözleşmesinin güvenlik gereksinimleriyle uyumlu olduğu doğrulanır.**  
  Sağlayıcının gönderilen mesajları model eğitiminde kullanıp kullanmadığı, ne kadar süre sakladığı ve veri işleme sözleşmesi sunup sunmadığı araştırılmalıdır. Gerektiğinde veri saklamayan veya kurumsal planlara geçiş değerlendirilmelidir. Yeni bir model veya sağlayıcı eklendiğinde bu kontroller tekrarlanmalıdır.

- [ ] **Harici servisin çalışmadığı durumlar için önceden alternatif bir plan tasarlanmalıdır.**  
  Harici bir servise tamamen bağımlı olmak, o servis çöktüğünde tüm sisteminizin de durması anlamına gelir. Kritik özellikler için yedek bir model, önceden hazırlanmış bir yanıt veya kullanıcıyı bilgilendiren basit bir alternatif akış tasarlanmalıdır. Bu bağımlılıkları düzenli aralıklarla test eden otomatik bir sağlık kontrolü kurulmalıdır.

---

## Common Mistakes

Bu bölüm, güvenlik önlemlerinin alınmadığı veya geç alındığı durumlarda erken aşama ürün ekiplerinin sıkça karşılaştığı üç risk alanını özetlemektedir.

**İtibar riski:** Yapay zeka özelliğinin kötüye kullanılması veya zararlı içerik üretmesi, özellikle büyüme aşamasındaki bir ürün için ciddi bir güven krizine yol açabilir. Kullanıcı tabanı henüz küçük olan bir üründe bu tür bir olay, aylarca süren büyüme çabasını kısa sürede geri alabilir.

**Maliyet riski:** İstek sınırı uygulanmadan sunulan bir yapay zeka özelliği, kötü niyetli veya dikkatsiz kullanıcıların yol açtığı aşırı tüketimle beklenmedik faturalar doğurabilir. Token başına ücretlendirilen servislerde bu maliyet saatler içinde önemli rakamlara ulaşabilir; özellikle kullanıcı sayısının hızla arttığı dönemlerde bu risk belirginleşir.

**Yasal risk:** KVKK ve GDPR gibi düzenlemeler, kişisel verilerin üçüncü taraflarla — harici yapay zeka sağlayıcıları dahil — nasıl paylaşılabileceğini belirler. Kullanıcı verilerinin kontrolsüz biçimde bir API'ye iletilmesi, yalnızca teknik bir güvenlik açığı değil aynı zamanda hukuki bir sorumluluk doğurur. Türkiye'de KVKK denetimlerinin kapsamının genişlemesi ve AB'deki yapay zeka düzenlemelerinin gelişmeye devam etmesi, bu riskin yakın vadede artacağına işaret etmektedir.

---

## What This Content Deliberately Excludes

Bu içerik, aşağıdaki konuları kasıtlı olarak dışlamaktadır:

- Jailbreak prompt'ları
- Bypass talimatları veya teknikleri
- Prompt injection payload örnekleri
- Dolandırıcılık iş akışları veya senaryoları
- Deepfake kötüye kullanım rehberliği
- Zararlı otomasyon örnekleri
- Gerçek kullanıcı verileri
- Gizli anahtarlar, token'lar veya kimlik bilgileri
- Bu kontrol listesinin yapay zeka güvenliğini yüzde yüz garanti ettiğine dair her türlü iddia

Bu çalışmanın amacı saldırı yöntemlerini öğretmek değil, savunma odaklı bir güvenlik kültürü oluşturmak için somut bir başlangıç noktası sunmaktır.

---

## Defensive Takeaways

Yapay zeka güvenliği; ürün tamamlandıktan sonra eklenen bir katman değil, baştan beri sistemin parçası olan bir tasarım kararıdır. Aşağıdaki çıkarımlar, bu listedeki maddelerin ortak paydası olarak değerlendirilebilir:

- Kullanıcı girdisine hiçbir zaman doğrudan güvenilmemeli; doğrulama ve filtreleme varsayılan davranış olarak tasarlanmalıdır.
- Maliyet ve istek hacmini pasif olarak izlemek yeterli değildir; aktif sınırlar ve otomatik uyarılar yapılandırılmalıdır.
- Yüksek etkili işlemler her zaman kullanıcı onayına bağlanmalı ve bu işlemlerin izi kayıt altında tutulmalıdır.
- Harici servislerin güvenliği, sistem güvenliğinin ayrılmaz bir parçasıdır; sağlayıcı politikaları sözleşme aşamasında dikkatle incelenmelidir.
- Hiçbir güvenlik önlemi kalıcı değildir; tehdit ortamı değiştikçe kontrol listesi güncellenmeli ve yeniden test edilmelidir.

**Sektörden Bir Örnek:** <cite index="2-1,3-1">Haziran 2026'da ABD hükümeti, ulusal güvenlik gerekçesiyle Anthropic'in Fable 5 ve Mythos 5 modellerine tüm yabancı uyruklular için erişimi askıya alan bir ihracat kontrol direktifi yayımladı.</cite> Sınır tanımayan yapay zeka modellerine erişim, "jailbreak" endişeleri ve hükümet müdahaleleri etrafındaki bu kamuoyu tartışmaları, yapay zeka ürün ekiplerinin model güvenliği, izleme, erişim kontrolü ve olay müdahalesini isteğe bağlı özelliklerden ziyade ürün düzeyinde riskler olarak ele alması gerektiğini göstermektedir.

---

## Sources

1. **OWASP LLM Top 10 (2025)**
   - Source title: OWASP Top 10 for Large Language Model Applications
   - Publisher / organization: OWASP Foundation
   - URL: [https://owasp.org/www-project-top-10-for-large-language-model-applications/](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
   - Archived URL, if available: [https://web.archive.org/web/2025/https://owasp.org/www-project-top-10-for-large-language-model-applications/](https://web.archive.org/web/2025/https://owasp.org/www-project-top-10-for-large-language-model-applications/)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: LLM uygulamalarında en sık karşılaşılan 10 güvenlik riskini kategorilere ayıran, açık kaynak topluluğu tarafından güncellenen referans belgedir. Bu kontrol listesindeki maddelerin büyük bölümü bu çerçeveyle doğrudan örtüşmektedir.

2. **NIST AI Risk Management Framework (AI RMF 1.0)**
   - Source title: Artificial Intelligence Risk Management Framework
   - Publisher / organization: National Institute of Standards and Technology (NIST)
   - URL: [https://www.nist.gov/system/files/documents/2023/01/26/AI%20RMF%201.0.pdf](https://www.nist.gov/system/files/documents/2023/01/26/AI%20RMF%201.0.pdf)
   - Archived URL, if available: [https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf](https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: ABD Ulusal Standartlar ve Teknoloji Enstitüsü'nün yapay zeka sistemleri için hazırladığı risk yönetimi çerçevesidir. Güvenilirlik, şeffaflık ve hesap verebilirlik ilkelerini somut uygulama adımlarıyla ele alır.

3. **Anthropic — Sorumlu Ölçeklendirme Politikası**
   - Source title: Anthropic's Responsible Scaling Policy
   - Publisher / organization: Anthropic
   - URL: [https://www.anthropic.com/news/anthropics-responsible-scaling-policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: Anthropic'in model güvenliği, dağıtım politikaları ve güvenli sistem tasarımına ilişkin kamuya açık yaklaşımını belgeleyen birincil kaynaktır.

4. **Microsoft — Sorumlu Yapay Zeka İlkeleri**
   - Source title: Microsoft Responsible AI Principles & Practices
   - Publisher / organization: Microsoft Corporation
   - URL: [https://www.microsoft.com/en-us/ai/responsible-ai](https://www.microsoft.com/en-us/ai/responsible-ai)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: Büyük ölçekli yapay zeka ürünlerinde sorumlu kullanım ilkelerini, değerlendirme araçlarını ve kurumsal uygulama rehberlerini bir arada sunan sektörel bir referanstır.

5. **MITRE ATLAS™ — Yapay Zeka Sistemlerine Yönelik Saldırı Haritası**
   - Source title: MITRE ATLAS™ (Adversarial Threat Landscape for Artificial-Intelligence Systems)
   - Publisher / organization: MITRE Corporation
   - URL: [https://atlas.mitre.org/](https://atlas.mitre.org/)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: Gerçek dünyada yapay zeka ve makine öğrenmesi sistemlerine yönelik saldırı yöntemlerini belgeleyen, MITRE ATT&CK çerçevesinin yapay zekaya uyarlanmış halidir. Prompt injection dahil birçok saldırı tipini kategorilere ayırır.

6. **AB Yapay Zeka Yasası — Resmi Metin (2024)**
   - Source title: Regulation (EU) 2024/1689 — Artificial Intelligence Act
   - Publisher / organization: Avrupa Birliği
   - URL: [https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: Yapay zeka sistemlerini risk düzeylerine göre sınıflandıran ve yüksek riskli uygulamalar için zorunlu gereksinimler getiren yasal düzenlemedir. Türkiye'den AB pazarına yönelik hizmet sunan ekipler için doğrudan bağlayıcı olabilir.

7. **KVKK — Kişisel Verileri Koruma Kurumu**
   - Source title: 6698 Sayılı Kişisel Verilerin Korunması Kanunu
   - Publisher / organization: Kişisel Verileri Koruma Kurumu (KVKK)
   - URL: [https://www.kvkk.gov.tr/Icerik/6649/6698-SAYILI-KANUN](https://www.kvkk.gov.tr/Icerik/6649/6698-SAYILI-KANUN)
   - Accessed date: Temmuz 2026
   - Why this source is relevant: Türkiye'de kişisel verilerin işlenmesine ilişkin temel yasal çerçeveyi belirleyen kanundur. Yapay zeka API'lerine veri iletimi bu kanun kapsamında değerlendirilmeli ve uyumluluk yükümlülükleri buna göre yerine getirilmelidir.

---

*Bu içerik, [ai-safety-lab](https://github.com/ai-safety-lab) açık kaynak projesinin bir parçasıdır. Katkı sağlamak için projenin `CONTRIBUTING.md` dosyasını inceleyebilirsiniz.*
