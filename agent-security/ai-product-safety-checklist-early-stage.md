# AI Product Safety Checklist for Early-Stage Teams

> **Proje:** ai-safety-lab · **Kapsam:** Erken Aşama Ürün Ekipleri · **Dil:** Türkçe  

---

## Giriş

Yeni bir ürün geliştirirken süre baskısı altında çalışan ekipler, yapay zeka entegre ederken güvenliği sona bırakır. "Önce çalıştıralım, güvenliği sonra hallederiz" mantığı geleneksel yazılımda bile tehlikelidir — ama yapay zeka söz konusu olduğunda bu yaklaşım çok daha büyük sorunlara yol açabilir. Çünkü bir dil modeli her seferinde aynı çıktıyı vermez, kullanıcı girdilerine bazen beklenmedik şekillerde tepki verir ve kötü niyetli kişilerin sistemi kendi çıkarları için kullanmasına fırsat verebilir. Bunların hiçbiri sıradan bir API'de bu kadar kolay ortaya çıkmaz.

Bu kontrol listesi, yapay zeka güvenliğini anlaşılır ve uygulanabilir hale getirmek için hazırlandı. İçeriği herhangi bir modele veya şirkete özgü değildir — her ekibin, her üründe uygulayabileceği genel ilkelere dayanıyor. Sadece geliştiriciler için değil, ürün yöneticileri ve kurucu ortaklar için de okunabilir olmasına özen gösterilmiştir.

Listedeki tüm maddeleri aynı anda yapmak zorunda değilsiniz. Öncelikle ürününüz veya ekibiniz ya da işletmeniz için en uygun olan maddeleri seçin, diğer maddeleri kendinize göre bir sonraki çalışma adımlarınıza ekleyin ve zamanla güvenliğinizi arttırmaya çalışın. Önemli olan mükemmel olmak değildir.Hangi birimiz öyleyiz ki şu fani dünyada — amaç zaten güvenliği ciddiye aldığınızı gösteren, yazılı ve sürekli gelişen bir alışkanlık oluşturmaktır.Sizlerde siber güvenlik farkındalığını yaratmayı amaçlamaktayız.

---

## Kontrol Listesi

### 1. Kullanıcı Girdilerini ve Model Çıktılarını Temizleme

- [ ] **Kullanıcıdan gelen her metin, modele gönderilmeden önce kontrol edilir ve temizlenir.**  
  Girdilerin ne kadar uzun olabileceğini, hangi karakterleri içerebileceğini ve hangi içerik türleri için geçerli olduğunu belirleyin. Yalnızca "beklenen formatta mı?" diye sormak yetmez — "bu sistem için uygun mu?" sorusunu da sorun. Kullanıcının yazdığı metni hiçbir zaman doğrudan sistem talimatlarına yapıştırmayın; her zaman ayrı bir "kullanıcı mesajı" olarak işleyin.

- [ ] **Modelden gelen yanıtlar, kullanıcıya gösterilmeden veya başka bir sisteme gönderilmeden önce bir kontrol aşamasından geçirilir.**  
  Yapay zekanın üretebileceği zararlı içerik türlerini (şiddet içeren ifadeler, kişisel bilgi sızıntısı, beklenmedik kod parçaları vb.) önceden listeleyin ve bu içerikleri yakalayacak bir filtre katmanı kurun. Bu filtre basit bir kural listesi olabileceği gibi başka bir modelle de yapılabilir. Eğer modelin ürettiği bir çıktı otomatik olarak çalıştırılacaksa (örneğin bir kod parçası veya veritabanı sorgusu), o işlemi izole bir ortamda gerçekleştirin.

- [ ] **Sistem talimatları ile kullanıcı girdisi birbirinden net biçimde ayrılır ve kullanıcı bu sınırı hiçbir şekilde aşamaz.**  
  Kullanıcının kontrol edebildiği içerik, asla sistem talimatlarıyla karışmamalıdır. Şablon yapılarınızı sabit tutun; değişken olan kısımları sadece veri olarak ekleyin, talimat olarak değil. Bu ayrımı hem kod incelemelerinde hem de testlerde düzenli olarak kontrol edin.

---

### 2. İstek Sayısını Sınırlama (Rate Limiting)

- [ ] **Her kullanıcı veya oturum için belirli bir zaman diliminde kaç istek yapılabileceği sınırlandırılır.**  
  Dakikalık, saatlik ve günlük istek limitleri belirleyin; bu limitleri kullanıcı kimliği, IP adresi veya oturum bilgisi üzerinden takip edin. Kısa sürede çok fazla istek gelen durumları otomatik olarak fark eden bir uyarı sistemi kurun. Limit aşıldığında kullanıcıya "429 — çok fazla istek" yanıtı döndürün ve ne zaman tekrar deneyebileceğini bildirin.

- [ ] **Yapay zekaya yapılan her çağrının maliyeti takip edilir ve bir üst sınıra bağlanır.**  
  Her token tüketimi, doğrudan para demektir. Kullanıcı başına veya hesap başına günlük ve aylık harcama limitleri belirleyin. Limitlerin yüzde seksenine ulaşıldığında ekibi otomatik olarak uyaracak bir alarm kurun. Limit aşıldığında sistemi aniden mi durduracağınıza, yoksa kullanıcıyı bilgilendirip devam mı edeceğinize önceden karar verin ve bunu kullanıcıya açıklayın.

---

### 3. Kullanıcı Onayı Gerektiren İşlemler

- [ ] **Geri alınamaz veya büyük etkisi olan işlemler (veri silme, e-posta gönderme, ödeme başlatma, dış servise bağlanma) yapay zeka tarafından doğrudan gerçekleştirilemez; önce kullanıcı onayı alınmalıdır.**  
  Yapay zekanın yapabileceği işlemleri "düşük etkili" ve "yüksek etkili" olarak ayırın. Yüksek etkili işlemler için kullanıcıya ne yapılacağını açıkça özetleyin ve devam etmesi için açık bir onay isteyin. Buradaki amaç modelin niyetini değil, somut eylemi onaylatmaktır.

- [ ] **Kullanıcı adına gerçekleştirilen her otomatik işlem, kim tarafından, ne zaman ve ne gerekçeyle yapıldığını gösteren bir kayıt bırakır.**  
  Bu kayıtlar hem şeffaflık hem de ileride sorun yaşandığında geriye dönük inceleme için gereklidir. Kayıtlara kullanıcılar erişip değiştirememelidir; sadece yetkili yöneticiler bu kayıtlara ulaşabilmelidir.

---

### 4. Kayıt Tutma (Logging)

- [ ] **Modele gönderilen mesajlar ve alınan yanıtlar, kişisel bilgiler gizlenerek kaydedilir ve belirli bir süre saklanır.**  
  Bu kayıtlar hem hata ayıklamak hem de güvenlik sorunlarını sonradan incelemek için çok önemlidir. Ancak bu kayıtlar isim, e-posta, kimlik numarası gibi kişisel bilgiler içerebilir. KVKK ve GDPR gibi veri koruma kuralları çerçevesinde bu bilgileri kaydetmeden önce gizleyin ya da anonim hale getirin. Kayıtların ne kadar süre tutulacağını ve kimlerin erişebileceğini yazılı bir politikayla belirleyin.

- [ ] **Modelin olağandışı veya zararlı görünen çıktıları için otomatik bir uyarı sistemi kurulur.**  
  Belirli içerik türlerini (manipülatif içerik, güvenlik ihlali belirtileri, açık içerik vb.) tespit ettiğinde ekibi bilgilendiren bir sistem oluşturun. Bu uyarılar e-posta, mesajlaşma uygulaması veya bir olay takip aracı aracılığıyla iletilebilir. Yanlış alarm oranını düzenli olarak gözden geçirin ve eşikleri buna göre ayarlayın.

---

### 5. Harici Yapay Zeka Servisleriyle Veri Paylaşımı

- [ ] **Bulut tabanlı yapay zeka API'sine (örneğin OpenAI, Anthropic, Google) hangi verilerin gönderildiği açıkça belirlenir; hassas ve kişisel bilgiler bu kapsamın dışında tutulur.**  
  Hangi veri türlerinin dışarıya gönderildiğini yazılı olarak kayıt altına alın. Kullanıcı şifreleri, sözleşme içerikleri, sağlık verileri veya finansal bilgiler gibi hassas içeriklerin modele iletilmesini teknik yöntemlerle (gizleme, anonimleştirme, alan bazlı filtreleme) engelleyin. "Sadece gerekli olanı gönder" ilkesini tasarımın temel kuralı haline getirin.

- [ ] **Kullandığınız her dış modelin veri saklama ve eğitim politikası incelenir; hizmet sözleşmesi güvenlik ihtiyaçlarınızla uyumlu mu diye kontrol edilir.**  
  Servis sağlayıcısının gönderdiğiniz mesajları model eğitiminde kullanıp kullanmadığını, kaç gün sakladığını ve veri işleme sözleşmesi sunup sunmadığını araştırın. Gerekiyorsa "veri saklamayan" veya kurumsal planlara geçiş yapmayı değerlendirin. Yeni bir model veya sağlayıcı eklendiğinde bu kontrolü tekrarlayın.

- [ ] **Harici servisin erişilemez olduğu durumlar için önceden bir yedek plan hazırlanır.**  
  Dışarıdan bir servise tamamen bağımlı olmak, o servis çöktüğünde tüm sisteminizin çökmesi anlamına gelir. Kritik özellikler için yedek bir model, önceden hazırlanmış bir yanıt ya da "bu özellik şu an kullanılamıyor" şeklinde kullanıcıyı bilgilendiren basit bir kural akışı tasarlayın. Bu bağımlılıkları düzenli olarak test eden otomatik bir sağlık kontrolü kurun.

---

## Bu Neden Önemli?

### Yapay Zeka Güvenliği Neden Farklı Bir Konu?

Geleneksel yazılımda bir sisteme aynı girdiyi verirseniz her zaman aynı çıktıyı alırsınız. Bu durum testleri ve güvenlik kontrollerini öngörülebilir kılar. Dil modelleri ise her seferinde farklı sonuç üretebilir.Aynı soru, farklı zamanlarda farklı yanıtlar doğurabilir. Bu da mevcut güvenlik testlerinin tek başına yeterli olmadığı anlamına gelir.Öncelikle geliştiricilerin bu durumların farkında olması gerekmektedir.

Bunun yanında, yapay zeka sistemleri "prompt injection(LLM01)" adı verilen yeni bir saldırı türüne karşı savunmasızdır. Bu saldırıda kötü niyetli bir hacker, modeli kendi istediği şekilde davranmaya zorlayan özel bir metin yazar. Güvenlik duvarı veya kod analiz araçları gibi geleneksel çözümler bu tür saldırıları genellikle fark edemez. Güvenlik artık sadece ağ katmanında değil, dilin ve anlamın kendisinde de sağlanmak zorundadır.

Son olarak, harici bir yapay zeka servisini kullandığınızda o servisin güvenlik açıkları da sizin sorununuz haline gelir. Modeli kimin eğittiği, hangi verilerle beslendiği ve servis sağlayıcısının altyapısının ne kadar güvenli olduğu — bunların hiçbiri doğrudan kontrolünüzde değildir, ama hepsi ürününüzü doğrudan etkiler.

### Önlem Almazsanız Ne Olur?

**İtibar açısından:** Yapay zeka desteğinin kötüye kullanılması veya zararlı içerik üretmesi, özellikle henüz büyüme aşamasındaki bir ürün için ciddi bir güven krizine yol açabilir. Sosyal medyada hızla yayılan bu tür olaylar, aylarca emek verilen bir ürünün imajını birkaç saatte zedeleyebilir.

Geçtiğimiz Günlerde Ortaya Çıkan Vaka:
Anthropic firmasının Fable 5 modeli, piyasaya sürülmesinden kısa süre sonra gelişmiş "jailbreak" ve "prompt injection" saldırılarına maruz kalarak ciddi güvenlik açıklarıyla gündeme gelmiştir. Saldırganlar, bağlam manipülasyonu ve rol tabanlı senaryolar kullanarak modelin katmanlı koruma sistemlerini aşmayı ve dahili sistem komut setini (system prompt) açığa çıkarmayı başarmıştır. Yaşanan bu manipülasyonlar ve artan veri güvenliği endişeleri nedeniyle, model hükümet(United States) direktifleri doğrultusunda Haziran 2026'da dünya genelinde tamamen askıya alınmıştır. Bu olay, büyük dil modellerinin güvenlik mimarilerindeki kırılganlığı ve yapay zeka ekosistemindeki acil denetim ihtiyacını bir kez daha gözler önüne sermiştir.

**Maliyet açısından:** Hız sınırı koymadan sunulan bir yapay zeka özelliği, kötü niyetli ya da dikkatsiz kullanıcıların yol açtığı aşırı token tüketimiyle beklenmedik faturalar doğurabilir. Token başına ücretlendirilen servislerde bu fatura saatler içinde çok yüksek rakamlara ulaşabilir.

**Yasal açıdan:** KVKK ve GDPR gibi yasalar, kişisel verilerin dış servislerle nasıl paylaşılabileceğini düzenler. Kullanıcı bilgilerini bir yapay zeka API'sine kontrolsüz biçimde göndermek, yalnızca teknik bir sorun değil aynı zamanda yasal bir sorumluluk da doğurur. Avrupa'daki yapay zeka düzenlemelerinin ve Türkiye'deki KVKK uygulamalarının giderek sertleştiği göz önünde bulundurulduğunda, bu riskin yakın gelecekte daha da artacağı görülmektedir.

---

## Kaynaklar

1. **OWASP LLM Top 10 (2025)**  
   Dil modeli uygulamalarında en sık karşılaşılan 10 güvenlik riskini listeleyen, açık kaynak topluluğu tarafından hazırlanan referans belge.  
   🔗 [https://owasp.org/www-project-top-10-for-large-language-model-applications/](https://owasp.org/www-project-top-10-for-large-language-model-applications/)

2. **NIST Yapay Zeka Risk Yönetimi Çerçevesi (AI RMF 1.0)**  
   ABD Ulusal Standartlar ve Teknoloji Enstitüsü'nün yapay zeka sistemleri için hazırladığı güvenilirlik ve risk yönetimi rehberi.  
   🔗 [https://www.nist.gov/system/files/documents/2023/01/26/AI%20RMF%201.0.pdf](https://www.nist.gov/system/files/documents/2023/01/26/AI%20RMF%201.0.pdf)

3. **Anthropic — Sorumlu Ölçeklendirme Politikası**  
   Anthropic'in model güvenliği ve güvenli sistem tasarımına ilişkin kamuya açık rehber belgeleri.  
   🔗 [https://www.anthropic.com/news/anthropics-responsible-scaling-policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy)

4. **Microsoft — Sorumlu Yapay Zeka İlkeleri**  
   Microsoft'un sorumlu yapay zeka kullanımı için geliştirdiği ilkeler, araçlar ve ürün güvenliği rehberleri.  
   🔗 [https://www.microsoft.com/en-us/ai/responsible-ai](https://www.microsoft.com/en-us/ai/responsible-ai)

5. **MITRE ATLAS™ — Yapay Zeka Sistemlerine Yönelik Saldırı Haritası**  
   Gerçek dünyada yapay zeka ve makine öğrenmesi sistemlerine yapılan saldırı yöntemlerini belgeleyen, MITRE ATT&CK çerçevesinin yapay zekaya uyarlanmış hali.  
   🔗 [https://atlas.mitre.org/](https://atlas.mitre.org/)

6. **AB Yapay Zeka Yasası — Resmi Metin (2024)**  
   Avrupa Birliği'nin yapay zeka sistemlerini risk seviyelerine göre sınıflandıran ve yüksek riskli uygulamalar için zorunluluklar getiren yasal düzenleme.  
   🔗 [https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689)

---

*Bu yazı,Tamga Türkiye AI Güvenliği açık kaynak kılavuzunun bir parçası olarak hazırlanmıştır. 
