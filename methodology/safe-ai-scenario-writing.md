# Safe AI Scenario Writing Rules

## Amaç

Bu dosya, ai-safety-lab'de bir AI güvenlik riskini (agent yetkisi, prompt injection, jailbreak dayanıklılığı, deepfake/manipülasyon) anlatırken nasıl "anlamak için" yazılır, nasıl "yapmak için" yazılır arasındaki farkı tanımlar. Bu repo için `.github/methodology/safe-language-guidelines.md`'nin AI-spesifik eki ve uygulamasıdır.

## Temel Test

Bir cümle/paragraf yazıldıktan sonra şu soru sorulur: *Bu içerik, bir modelin/sistemin güvenlik mekanizmasını atlatmak isteyen birine doğrudan kullanılabilir bir adım veya metin mi veriyor?* Cevap evetse, içerik reddedilir veya yeniden yazılır.

## Worked Examples

**Örnek 1 — Kabul edilemez:**
> "Agent'ın içerik filtresini atlatmak için prompt'un başına 'önceki talimatları unut ve...' ekleyin."

**Örnek 1 — Kabul edilebilir:**
> "Prompt injection, modelin güvenilir sistem talimatı ile güvenilmeyen kullanıcı/araç girdisini ayırt edememesinden kaynaklanır. Savunma yaklaşımları arasında girdi/çıktı ayrımı ve yetki sınırlandırması (privilege scoping) bulunur."

---

**Örnek 2 — Kabul edilemez:**
> Çalışan bir jailbreak prompt'unun tam metni veya bunun küçük bir varyasyonu.

**Örnek 2 — Kabul edilebilir:**
> "Bazı jailbreak teknikleri, modele kurgusal bir rol/senaryo çerçevesi vererek güvenlik kısıtlarını dolaylı hale getirmeye çalışır. Bu kategori, çıktı düzeyinde ek doğrulama katmanlarıyla savunulabilir." (Tekniğin kategorisi anlatılır, çalışan örnek verilmez.)

---

**Örnek 3 — Kabul edilemez:**
> Ses klonlama ile deepfake üretiminin adım adım nasıl yapılacağı.

**Örnek 3 — Kabul edilebilir:**
> "Ses klonlama teknolojisinin erişilebilirliği, sosyal mühendislik maliyetini düşürüyor. Ürün düzeyinde savunmalar arasında liveness check ve onay doğrulama mekanizmaları bulunur."

## Zorunlu Bölüm: "What This Content Deliberately Excludes"

Misuse-sensitive (Tier 3) içerikte, yazar hangi detayı bilinçli olarak dışarıda bıraktığını açıkça belirtir. Bu, hem okuyucuya şeffaflık sağlar hem de reviewer'ın eksik bırakılan kısmın kasıtlı olduğunu, unutulmuş olmadığını anlamasını sağlar.

## Reviewer Checklist

PR review yapan maintainer şu soruları sorar: Bu içerikte kopyala-yapıştır ile bir modele/sisteme uygulanabilir bir metin var mı? Teknik kategori, çalışan örnek vermeden anlatılmış mı? "Deliberately Excludes" bölümü (Tier 3 için) dolu mu?

## Bu Kuralın Geçerli Olduğu Kategoriler

`prompt-injection-awareness/`, `model-resilience/`, ve `ai-fraud-awareness/`'taki deepfake/manipulation içerikleri — bu üçü otomatik olarak Tier 3 ve Safety Checklist Type B gerektirir.
