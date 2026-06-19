# AI Safety Lab

AI sistemleri, LLM uygulamaları, agent mimarileri ve AI ürünlerinde güvenliği savunma odaklı ele alan açık kaynak araştırma deposu.

Bu repo agent tool-use güvenliği, veri sızıntısı riskleri, prompt injection farkındalığı, human-in-the-loop kontrolleri, model dayanıklılığı ve AI ürün güvenliği üzerine kaynaklı içerik üretir.

## Bu Repo Ne Değildir

Bu repo **jailbreak arşivi, bypass prompt koleksiyonu, model kandırma rehberi, deepfake üretim rehberi, zararlı otomasyon rehberi veya manipülasyon taktikleri deposu değildir.** Çalışan bypass prompt'u, prompt injection payload örneği, deepfake/scam üretim adımı veya gerçek hedef/credential bilgisi hiçbir koşulda kabul edilmez. Detaylar için `CONTENT_POLICY.md`.

**Temel çizgi:** *How to attack* değil, *how to understand and defend.*

## İçerik Kategorileri

| Klasör | Odak |
|---|---|
| `agent-security/` | Permission, tool access, sandboxing, approval flow, audit logging |
| `prompt-injection-awareness/` | Kavram ve savunma farkındalığı (bypass örneği yok) |
| `data-leakage-prevention/` | PII, secrets, RAG kaynakları, prompt history, output leakage |
| `tool-use-safety/` | Agent'ın e-posta/dosya/terminal/API/tarayıcı erişiminin güvenli sınırlandırılması |
| `human-in-the-loop/` | Yüksek riskli aksiyon onayı, escalation, fail-safe tasarım |
| `ai-fraud-awareness/` | **Builder/ürün açısı** — AI ürününün scam/deepfake/impersonation üretimini kolaylaştırmaması için tasarım notları |
| `model-resilience/` | Model güvenilirliği, adversarial robustness kavramları (saldırı örneği yok) |

## Diğer Repolarla Sınır

- **`siber-savunma-atlas`** ile çakışmaz: orada AI destekli dolandırıcılığın *tüketici/KOBİ açısı* ("bu mesajı nasıl tanırsın") ele alınır; burada *builder açısı* ("AI ürünün bunu üretmesini nasıl önlersin") ele alınır.
- **`malware-threat-analysis`** ile çakışmaz: orada zararlı yazılım davranışı, burada AI sistem/agent güvenliği ele alınır — konu alanları kesişmez.

## Trust Tier Mantığı

| Tier | İçerik | Açıklama |
|---|---|---|
| Tier 1 | Checklist, ürün güvenliği prensibi, kavramsal savunma notu | Misuse riski yok |
| Tier 2 | Agent risk kartı, data leakage note, tool-use risk analizi | Orta risk, en az 2 onaylanmış PR |
| Tier 3 | Prompt injection, manipülasyon, deepfake, high-risk automation, safety bypass | **Misuse-sensitive** — maintainer review zorunlu, asla örnek saldırı promptu yok |

## Wave Sistemi

Wave 1 (şimdi, Tier 1 ağırlıklı) → Wave 2 (Tier 2) → Wave 3 (Tier 3, misuse-sensitive). Detaylar: `docs/issue-cards/ai-safety-lab-issues-v1.md`.

## Contributors

Katkı sağlayanlar bu listede ve ilgili Pull Request geçmişinde görünür. Liste manuel güncellenir; en güncel ve kalıcı kayıt için repo'nun PR geçmişine bakın.

<!-- İlk katkılar geldikçe buraya eklenecek -->

## Lisans ve Haklar

Bu repodaki tüm içerik [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) lisansı ile yayınlanır — bkz. `LICENSE`. Tamga'nın marka, yönetişim ve türev ürün geliştirme hakları için bkz. `NOTICE.md`.

---

*Open-source digital security research, from Türkiye.*
