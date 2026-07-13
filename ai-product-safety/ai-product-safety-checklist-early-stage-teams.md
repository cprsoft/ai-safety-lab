# AI Product Safety Checklist for Early-Stage Teams

> **Proje:** ai-safety-lab · **Kapsam:** Erken Aşama Ürün Ekipleri · **Dil:** Türkçe  

---

## Executive Summary

Bu çalışma, yapay zeka veya büyük dil modeli (LLM) özelliği geliştiren erken aşama ürün ekipleri için hazırlanmış, savunma odaklı bir güvenlik kontrol listesidir. Amacı, güvenlik konusunu sonraya bırakmak yerine ürünün ilk aşamalarından itibaren ele almanın neden ve nasıl yapılması gerektiğini somut adımlarla ortaya koymaktır.

Bu içerik; geliştiriciler, ürün yöneticileri ve kurucu ortaklar dahil olmak üzere teknik ve teknik olmayan tüm ekip üyelerinin okuyabileceği bir dilde yazılmıştır. İçerdiği maddeler belirli bir model veya platforma özgü değildir; her ürün tipine uyarlanabilecek genel ilkeler üzerine kuruludur.

Listedeki tüm maddelerin aynı anda uygulanması beklenmez. Öncelikli maddeler belirlenmeli, bir sonraki çalışma dönemine eklenmeli ve zamanla kapsam genişletilmelidir. Önemli olan; güvenliği ciddiye alan, yazılı ve sürekli geliştirilen bir uygulama kültürü oluşturmaktır.

---

## Context

Birçok geleneksel yazılım bileşeni belirli koşullarda daha öngörülebilir biçimde test edilebilirken, LLM çıktıları model sürümü, bağlam, sistem talimatları ve üretim ayarlarına bağlı olarak değişkenlik gösterebilir. Bu belirsizlik, mevcut güvenlik testlerinin tek başına yeterli olmadığı anlamına gelir.

Bunun yanında, yapay zeka sistemleri "prompt injection" adıyla bilinen yeni bir saldırı türüne karşı savunmasızdır. Bu saldırı yalnızca kötü niyetli bir kullanıcının özel bir metin yazmasıyla gerçekleşmez; aynı zamanda işlenen web sitelerinden, yüklenen belgelerden, dış veri kaynaklarından veya araç çıktılarından da (dolaylı olarak) kaynaklanabilir. Geleneksel güvenlik araçları — güvenlik duvarı, statik kod analizi gibi çözümler — bu tür saldırıları büyük ölçüde fark edemez. Girdi temizleme (input cleaning) ve sistem talimatlarını kullanıcı mesajlarından ayırma faydalı kontroller olsa da, tek başlarına koruma garantisi vermezler; bu yöntemler mutlaka en az yetki, çıktı doğrulama, dış içerik izolasyonu, yüksek etkili işlemler için insan onayı ve sürekli testlerle (adversarial testing) desteklenmelidir.

Son olarak, harici bir yapay zeka servisi kullanıldığında o servisin güvenlik açıkları da ürünün sorunu haline gelir. Modeli kimin eğittiği, hangi verilerle beslendiği ve servis sağlayıcısının altyapısının ne kadar güvenli olduğu; doğrudan kontrol edilemeyen ancak ürünü doğrudan etkileyen unsurlardır.

---

## Türkiye Relevance

Türkiye'de faaliyet gösteren veya Türkiye'de kullanıcısı bulunan ürün ekipleri için yapay zeka güvenliği yalnızca teknik bir konu değil, aynı zamanda yasal bir yükümlülüktür.

**KVKK ve GDPR Etkisi:** Kişisel verilerin işlenmesi ve harici yapay zeka API sağlayıcılarına aktarılması; uygulanabilir hukuki zemin, şeffaflık yükümlülükleri, veri minimizasyonu ilkeleri ve sınır ötesi aktarım kuralları çerçevesinde değerlendirilmelidir. Açık rıza tek hukuki zemin olmayabileceği gibi, her durumda bir aktarım sözleşmesi zorunlu olmayabilir; ancak veri akışının ve bağlamın doğru analiz edilmesi şarttır. Erken aşama ekipler, gerekli durumlarda uzman hukuki görüş almalıdır. Ayrıca GDPR'ın otomatik olarak uygulanmayabileceği, kurumsal yerleşim yeri veya AB içindeki kişilere ürün/hizmet sunma ya da davranışlarını izleme gibi faktörlere bağlı olduğu unutulmamalıdır.

Türkiye'de KVKK uygulamalarının giderek güçlendiği ve denetim kapsamının genişlediği görülmektedir. Yapay zeka ürün kararlarının bu yasal çerçeve içinde değerlendirilmesi, ileride oluşabilecek idari yaptırımların önüne geçmek açısından kritik önem taşır.

---

## Safety Areas

Bu kontrol listesi aşağıdaki temel güvenlik alanlarını kapsamaktadır:

**1. Girdi ve Çıktı Denetimi:** Kullanıcıdan gelen verilerin modele iletilmeden önce doğrulanması; modelden dönen yanıtların kullanıcıya sunulmadan önce kontrol edilmesi.
**2. En Az Yetki ve Araç Sınırları (Tool Permission Boundaries):** Modellere sınırsız araç erişimi veya geniş yetkili kimlik bilgileri verilmemesi.
**3. Şeffaflık (User Transparency):** Kullanıcılara arka planda yapay zeka kullanıldığının açıkça bildirilmesi.
**4. Onay Gerektiren İşlemler:** Geri alınamaz veya yüksek etkili işlemler için kullanıcının açık onayının alınması.
**5. Kayıt ve İzleme (Logging & Monitoring):** Veri minimizasyonu prensibiyle kayıt tutulması ve olağandışı davranışların tespit edilmesi.
**6. Güvenli Hata ve Acil Durum (Fail-Safe & Incident Response):** Güvenli olmayan veya doğrulanamayan eylemlerin güvenli bir şekilde reddedilmesi ve gerektiğinde AI özelliğinin kapatılabilmesi, izole edilebilmesi veya geri alınabilmesi.
**7. Harici Servis Yönetimi:** API sağlayıcılarının güvenlik politikalarının denetlenmesi ve veri sızıntısının önlenmesi.

---

## Practical Checklist

### 1. Girdi ve Çıktı Denetimi

- [ ] **Kullanıcıdan gelen her metin, modele gönderilmeden önce kontrol edilir ve temizlenir.**  
  Girdilerin uzunluk sınırı, kabul edilebilir karakter kümesi ve içerik türü önceden tanımlanmalıdır. Kullanıcı metni hiçbir zaman doğrudan sistem talimatlarına eklenmemeli; her zaman ayrı bir kullanıcı mesajı bloğu olarak işlenmelidir.

- [ ] **Modelden gelen yanıtlar, kullanıcıya gösterilmeden veya başka bir sisteme iletilmeden önce bir denetim aşamasından geçirilir.**  
  Yapay zekanın üretebileceği zararlı içerik kategorilerinin önceden listelenmesi ve bu kategorileri yakalayan bir filtre katmanı oluşturulması önerilir. Model çıktısı otomatik olarak çalıştırılacaksa (örneğin kod veya veritabanı sorgusu), söz konusu işlem izole bir ortamda gerçekleştirilmelidir.

- [ ] **Sistem talimatları ile kullanıcı girdisi yapısal olarak birbirinden ayrılır.**  
  Şablon yapıları sabit tutulmalı; değişken içerikler yalnızca veri düzeyinde eklenmeli, talimat düzeyinde birbirine karıştırılmamalıdır. Bu ayrım faydalı bir kontrol olmakla birlikte enjeksiyonları tamamen önlemez; çıktı doğrulama ve en az yetkiyle birleştirilmelidir.

---

### 2. En Az Yetki, Şeffaflık ve Güvenli Hata

- [ ] **Modelin çağırabileceği fonksiyonlara (tools) sağlanan kimlik bilgileri en az yetki (least privilege) prensibiyle sınırlandırılır.**  
  Modele veya AI ajanlarına hiçbir zaman sisteme tam erişim (admin) yetkisi verilmemeli; yalnızca görevini yerine getirebileceği kadar kısıtlı erişim sağlanmalıdır.

- [ ] **Sistem, kullanıcılara bir yapay zeka modeliyle etkileşime girdiklerini açıkça bildirir.**  
  Kullanıcılar, bir yapay zeka ürünü kullandıkları konusunda bilgilendirilmeli ve modelin yanılıp halüsinasyon görebileceği (hallucination) şeffaf bir şekilde paylaşılmalıdır.

- [ ] **Sistem, güvensiz işlemlerde "güvenli hata" (fail-safe) modunda çalışacak şekilde tasarlanmıştır.**  
  Modelin isteği doğrulanamadığında, şüpheli bir içerik tespit edildiğinde veya belirsizlik oluştuğunda sistem varsayılan olarak eylemsiz kalmalı, işlemi güvenli bir şekilde reddetmelidir.

---

### 3. Onay Gerektiren İşlemler

- [ ] **Geri alınamaz veya yüksek etkili işlemler yapay zeka tarafından doğrudan tetiklenemez; önce kullanıcı onayı alınmalıdır.**  
  Veri silme, e-posta gönderme, ödeme başlatma ve harici servise bağlanma gibi işlemler bu kapsamdadır. Yüksek etkili işlemler için kullanıcıya yapılacak işlem açıkça özetlenmeli ve işleme devam etmek için açık bir onay talep edilmelidir.

- [ ] **Kullanıcı adına gerçekleştirilen her otomatik işlem iz bırakır.**  
  Bu kayıtlar şeffaflık açısından ve ileride yaşanabilecek sorunların geriye dönük incelenmesi için gereklidir.

---

### 4. Kayıt, İzleme ve Acil Durum (Incident Response)

- [ ] **Kayıt tutma işlemleri (logging) veri minimizasyonu ilkelerine uygun olarak yürütülür.**  
  Gerekli ve haklı bir gerekçe olmadığı sürece ham (raw) içerik kaydedilmemeli, bunun yerine içerikten bağımsız teknik metaveriler (metadata) tercih edilmelidir. Loglama zorunluysa hassas veriler maskelenmeli, rol bazlı erişim uygulanmalı ve belirli bir saklama süresi tanımlanmalıdır. Güvenlik günlükleri, kullanıcının gördüğü aktivite geçmişi ve yasal veri erişim hakları ayrı ayrı yönetilmelidir.

- [ ] **Modelin olağandışı veya zararlı görünen çıktıları için otomatik bir uyarı sistemi kurulur.**  
  Belirli içerik kategorileri tespit edildiğinde ekibi bilgilendiren bir mekanizma oluşturulmalıdır.

- [ ] **Ekiplerin bir güvenlik olayı anında sistemi kapatabileceği veya geri alabileceği bir mekanizma mevcuttur.**  
  Model kontrolden çıktığında veya bir zafiyet sömürüldüğünde, ilgili AI özelliğini tamamen kapatacak (kill switch), izole edecek veya güvenli eski bir duruma döndürecek (rollback) acil durum planı hazır olmalıdır.

---

### 5. Harici Servis Yönetimi

- [ ] **Bulut tabanlı bir yapay zeka API'sine hangi verilerin gönderildiği açıkça tanımlanır.**  
  Kullanıcı kimlik bilgileri, sözleşme içerikleri, sağlık verileri ve finansal bilgiler gibi hassas içeriklerin modele gönderilmesi teknik yöntemlerle engellenmelidir. "Yalnızca gerekli olanı gönder" ilkesi, sistem tasarımının temel kuralı haline getirilmelidir.

- [ ] **Kullanılan her harici modelin veri saklama politikası incelenir ve güvenlik testleri tekrarlanır.**  
  Sağlayıcının verileri eğitimde kullanıp kullanmadığı araştırılmalı; model veya sağlayıcı her değiştirildiğinde sistemin mevcut güvenlik kontrolleri (promt injection filtreleri vb.) yeniden test edilmelidir.

---

## Common Mistakes

Erken aşama ekiplerin güvenlik süreçlerinde en sık düştüğü pratik uygulama hataları şunlardır:

- **Sadece girdi filtrelemeye güvenmek:** Girdi temizlemeyi (input filtering) prompt injection'a karşı tam ve kusursuz bir savunma sanmak. Gerçekte bu filtreler atlatılabilir; savunma mutlaka en az yetki, izole ortamlar ve insan onayı ile desteklenmelidir.
- **Modele aşırı yetki vermek:** Modelin kullandığı araçlara (tools) veritabanını tamamen silme, sistemi okuma veya dışarıya yetkisiz istek atma gibi geniş ayrıcalıklar (excessive permissions) atamak.
- **Tüm prompt ve yanıtları varsayılan olarak loglamak:** Ham kullanıcı mesajlarını (kişisel veya hassas veri içerip içermediğine bakmaksızın) maskeleme yapmadan, saklama süresi belirlemeden kaydetmek.
- **Yüksek etkili eylemleri insan onayı olmadan çalıştırmak:** E-posta gönderme, satın alma yapma veya yetki değiştirme gibi işlemleri modelin doğrudan ve onaysız olarak yürütmesine izin vermek.
- **Kullanıcılara yapay zeka kullanıldığını bildirmemek:** Kullanıcıyı, bir insanla veya %100 kesin (deterministik) sonuç üreten bir algoritmayla iletişim kurduğuna inandırmak.
- **Kapatma (kill switch) veya olay müdahale planı oluşturmamak:** Model beklenmedik davrandığında veya saldırı altındayken özelliği hızlıca izole edecek veya kapatacak bir mekanizma (rollback/kill switch) tasarlamamak.
- **Model değiştikten sonra kontrolleri test etmemek:** Farklı bir LLM modeline veya sağlayıcıya geçildiğinde, eski modelde çalışan güvenlik ve güvenlik bariyerlerinin yeni modelde de aynı şekilde işlediğini varsaymak.

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

- Kullanıcı girdisine veya dış veri kaynaklarına hiçbir zaman doğrudan güvenilmemeli; doğrulama ve filtreleme varsayılan davranış olmalıdır.
- Maliyet ve istek hacmini pasif olarak izlemek yeterli değildir; aktif sınırlar ve otomatik uyarılar yapılandırılmalıdır.
- Yüksek etkili işlemler her zaman kullanıcı onayına bağlanmalı ve bu işlemlerin izi veri minimizasyonuna uygun biçimde kayıt altında tutulmalıdır.
- Harici servislerin güvenliği, sistem güvenliğinin ayrılmaz bir parçasıdır; sağlayıcı politikaları dikkatle incelenmeli ve model değişimlerinde testler yenilenmelidir.
- Hiçbir güvenlik önlemi kalıcı değildir; tehdit ortamı değiştikçe kontrol listesi güncellenmeli ve sürekli yeniden test edilmelidir.

---

## Sources

1. **OWASP LLM Top 10 (2025)**
   - Source title: OWASP Top 10 for Large Language Model Applications
   - Publisher / organization: OWASP Foundation
   - URL: [https://owasp.org/www-project-top-10-for-large-language-model-applications/](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
   - Archived URL, if available: [https://web.archive.org/web/2025/https://owasp.org/www-project-top-10-for-large-language-model-applications/](https://web.archive.org/web/2025/https://owasp.org/www-project-top-10-for-large-language-model-applications/)
   - Accessed date: 13 Temmuz 2026
   - Why this source is relevant: LLM uygulamalarında en sık karşılaşılan 10 güvenlik riskini kategorilere ayıran, açık kaynak topluluğu tarafından güncellenen referans belgedir. Bu kontrol listesindeki maddelerin büyük bölümü bu çerçeveyle doğrudan örtüşmektedir.

2. **NIST AI Risk Management Framework (AI RMF 1.0)**
   - Source title: Artificial Intelligence Risk Management Framework
   - Publisher / organization: National Institute of Standards and Technology (NIST)
   - URL: [https://www.nist.gov/system/files/documents/2023/01/26/AI%20RMF%201.0.pdf](https://www.nist.gov/system/files/documents/2023/01/26/AI%20RMF%201.0.pdf)
   - Archived URL, if available: [https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf](https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf)
   - Accessed date: 13 Temmuz 2026
   - Why this source is relevant: ABD Ulusal Standartlar ve Teknoloji Enstitüsü'nün yapay zeka sistemleri için hazırladığı risk yönetimi çerçevesidir. Güvenilirlik, şeffaflık ve hesap verebilirlik ilkelerini somut uygulama adımlarıyla ele alır.

3. **Anthropic — Sorumlu Ölçeklendirme Politikası**
   - Source title: Anthropic's Responsible Scaling Policy
   - Publisher / organization: Anthropic
   - URL: [https://www.anthropic.com/news/anthropics-responsible-scaling-policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy)
   - Archived URL, if available: -
   - Accessed date: 13 Temmuz 2026
   - Why this source is relevant: Anthropic'in model güvenliği, dağıtım politikaları ve güvenli sistem tasarımına ilişkin kamuya açık yaklaşımını belgeleyen birincil kaynaktır.

4. **Microsoft — Sorumlu Yapay Zeka İlkeleri**
   - Source title: Microsoft Responsible AI Principles & Practices
   - Publisher / organization: Microsoft Corporation
   - URL: [https://www.microsoft.com/en-us/ai/responsible-ai](https://www.microsoft.com/en-us/ai/responsible-ai)
   - Archived URL, if available: -
   - Accessed date: 13 Temmuz 2026
   - Why this source is relevant: Büyük ölçekli yapay zeka ürünlerinde sorumlu kullanım ilkelerini, değerlendirme araçlarını ve kurumsal uygulama rehberlerini bir arada sunan sektörel bir referanstır.

5. **MITRE ATLAS™ — Yapay Zeka Sistemlerine Yönelik Saldırı Haritası**
   - Source title: MITRE ATLAS™ (Adversarial Threat Landscape for Artificial-Intelligence Systems)
   - Publisher / organization: MITRE Corporation
   - URL: [https://atlas.mitre.org/](https://atlas.mitre.org/)
   - Archived URL, if available: -
   - Accessed date: 13 Temmuz 2026
   - Why this source is relevant: Gerçek dünyada yapay zeka ve makine öğrenmesi sistemlerine yönelik saldırı yöntemlerini belgeleyen, MITRE ATT&CK çerçevesinin yapay zekaya uyarlanmış halidir. Prompt injection dahil birçok saldırı tipini kategorilere ayırır.

6. **AB Yapay Zeka Yasası — Resmi Metin (2024)**
   - Source title: Regulation (EU) 2024/1689 — Artificial Intelligence Act
   - Publisher / organization: Avrupa Birliği
   - URL: [https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689)
   - Archived URL, if available: -
   - Accessed date: 13 Temmuz 2026
   - Why this source is relevant: Yapay zeka sistemlerini risk düzeylerine göre sınıflandıran ve aşamalı olarak uygulamaya konan (phased application) yürürlükteki yasal düzenlemedir. Türkiye'den AB pazarına yönelik hizmet sunan ekipler için doğrudan bağlayıcı olabilir.

7. **KVKK — Kişisel Verileri Koruma Kurumu**
   - Source title: 6698 Sayılı Kişisel Verilerin Korunması Kanunu
   - Publisher / organization: Kişisel Verileri Koruma Kurumu (KVKK)
   - URL: [https://www.kvkk.gov.tr/Icerik/6649/6698-SAYILI-KANUN](https://www.kvkk.gov.tr/Icerik/6649/6698-SAYILI-KANUN)
   - Archived URL, if available: -
   - Accessed date: 13 Temmuz 2026
   - Why this source is relevant: Türkiye'de kişisel verilerin işlenmesine ilişkin temel yasal çerçeveyi belirleyen kanundur. Yapay zeka API'lerine veri iletimi bu kanun kapsamında değerlendirilmeli ve uyumluluk yükümlülükleri buna göre yerine getirilmelidir.

---

*Bu yazı, [ai-safety-lab](https://github.com/TamgaTurkiye/ai-safety-lab) açık kaynak projesinin bir parçasıdır.*
