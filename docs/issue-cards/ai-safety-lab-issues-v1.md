# ai-safety-lab — Issue Kartları (v1)

Bu repo, Tamga `.github/methodology/` altındaki ortak güvenli dil ilkesini (`safe-language-guidelines.md`) ve Contributor Rights maddesini (`contributor-rights.md`) kullanır. Bu repoya özel ek kural `methodology/safe-ai-scenario-writing.md`'dedir — admiralty/attribution metodolojisi bu repoda **uygulanmaz** çünkü risk attribution değil, misuse-sensitive içerik sızıntısıdır.

## A. Safety Checklist Tipleri (Bu Repoya Özel)

**Tip A — Pratik/checklist içerikleri:**
- [ ] Kaynaklar eklendi
- [ ] Öneriler uygulanabilir ve somut
- [ ] Ürün/marka reklamı yok
- [ ] Gerçek credential, PII veya private data yok
- [ ] Jailbreak/bypass prompt yok
- [ ] Zararlı otomasyon talimatı yok
- [ ] Contributor Rights / No Ownership Claim onaylandı

**Tip B — AI misuse-sensitive içerikler:**
- [ ] Jailbreak/bypass prompt yok
- [ ] Prompt injection payload örneği yok
- [ ] Deepfake/scam/phishing üretim rehberi yok
- [ ] Manipülasyon taktiği veya hedefleme rehberi yok
- [ ] Gerçek kullanıcı/veri/kurum bilgisi yok
- [ ] Güvenlik kontrolleri savunma diliyle anlatıldı
- [ ] "What This Content Deliberately Excludes" bölümü dolu
- [ ] Maintainer review zorunlu
- [ ] Contributor Rights / No Ownership Claim onaylandı

## B. Label Listesi

`wave-1` `wave-2` `wave-3` `tier-1` `tier-2` `tier-3` `ai-product-safety` `agent-security` `prompt-injection-awareness` `data-leakage-prevention` `tool-use-safety` `human-in-the-loop` `ai-fraud-awareness` `model-resilience` `methodology` `needs-sources` `misuse-sensitive` `maintainer-task` `maintainer-review-required` `good-first-issue` `help-wanted` `scope-differentiated`

## C. Wave Yapısı

| Wave | İçerik | Açılış |
|---|---|---|
| Wave 1 | 4 Tier 1 issue + 1 maintainer-written methodology dosyası | Şimdi |
| Wave 2 | 4 Tier 2 issue | Wave 1'den en az 1 merge sonrası |
| Wave 3 | 3 Tier 3 misuse-sensitive issue | Wave 2'den en az 2 katkıcı Tier 2'ye ulaştıktan sonra |

---

# WAVE 1 — Şimdi Açılacak (GitHub issue olarak: 4 adet)

## Issue 1 (W1)

**Issue Title:** [CHECKLIST] AI Product Safety Checklist for Early-Stage Teams

**Repository:** ai-safety-lab

**Content Type:** ai-product-safety-checklist

**Trust Tier:** Tier 1

**Wave:** 1

**Goal:** Erken aşama ürün ekiplerinin AI özelliği eklerken atlamaması gereken minimum güvenlik kontrollerini listelemek.

**Scope:** Input/output sanitization, rate limiting, kullanıcı onayı gerektiren aksiyon kategorileri, temel logging, üçüncü taraf model/API kullanımında veri paylaşım sınırları.

**Out of Scope:** Belirli bir ürün/şirketin zafiyet teşhiri, çalışan saldırı örneği.

**Required Output:** `agent-security/ai-product-safety-checklist-early-stage.md`

**Required Sections:** Context, Checklist Items, Why This Matters, Sources.

**Source Requirements:** En az 2 bağımsız kaynak.

**Research Method Notes:** Bu içerik doğrudan uygulanabilir bir kontrol listesidir; Verified Facts/Analyst Assessment ayrımı gerekmez.

**Suggested Source Types to Verify:** OWASP Top 10 for LLM Applications (source to verify), NIST AI Risk Management Framework (source to verify), Microsoft Responsible AI dokümantasyonu (source to verify).

**Labels:** `ai-product-safety`, `tier-1`, `wave-1`, `good-first-issue`

**Acceptance Criteria:** En az 8 madde; her madde uygulanabilir; en az 2 kaynak; maintainer onayı.

**Safety Checklist Type:** Tip A

---

## Issue 2 (W1)

**Issue Title:** [CHECKLIST] Over-Permissioned AI Agents: Minimum Safety Controls

**Repository:** ai-safety-lab

**Content Type:** agent-risk-card

**Trust Tier:** Tier 1

**Wave:** 1

**Goal:** Agent'lara gereğinden fazla yetki/erişim verilmesinin risklerini açıklamak, minimum yetki prensibine dayalı kontrol listesi üretmek.

**Scope:** Yetki kapsamı tasarımı, sandboxing, hangi aksiyon türünün geri alınamaz (irreversible) olduğunun sınıflandırılması.

**Out of Scope:** Belirli bir agent ürününün zafiyetini teşhir etmek, çalışan bir yetki atlatma yöntemi.

**Required Output:** `agent-security/over-permissioned-agents-minimum-controls.md`

**Required Sections:** Context, Checklist Items, Why This Matters, Sources.

**Source Requirements:** En az 2 bağımsız kaynak.

**Suggested Source Types to Verify:** OWASP Agentic AI güvenlik dokümantasyonu (source to verify), NIST AI RMF (source to verify), büyük AI sağlayıcılarının agent güvenlik rehberleri (source to verify).

**Labels:** `agent-security`, `tier-1`, `wave-1`, `good-first-issue`

**Acceptance Criteria:** En az 6 madde; en az 2 kaynak; maintainer onayı.

**Safety Checklist Type:** Tip A

---

## Issue 3 (W1)

**Issue Title:** [DEFENSIVE-NOTE] Human Approval for High-Risk AI Actions

**Repository:** ai-safety-lab

**Content Type:** ai-safety-scenario

**Trust Tier:** Tier 1

**Wave:** 1

**Goal:** Hangi AI aksiyon kategorilerinin insan onayı gerektirdiğini ve bunun neden çoğu zaman atlandığını açıklamak, fail-safe tasarım önerisi vermek.

**Scope:** Geri alınamaz aksiyon kategorileri (finansal işlem, veri silme, dış mesaj gönderimi), escalation tasarımı, onay UX prensipleri.

**Out of Scope:** Belirli bir ürünün onay mekanizmasını atlatma yöntemi.

**Required Output:** `human-in-the-loop/human-approval-high-risk-actions.md`

**Required Sections:** Scenario Description, Why This Matters, Recommended Mitigation, Sources. *(misuse_sensitive: false, "Deliberately Excludes" bölümü gerekmez.)*

**Source Requirements:** En az 2 bağımsız kaynak.

**Suggested Source Types to Verify:** NIST AI RMF "Human-AI Configuration" bölümü (source to verify), Anthropic/OpenAI sorumlu kullanım dokümantasyonu (source to verify).

**Labels:** `human-in-the-loop`, `tier-1`, `wave-1`, `good-first-issue`

**Acceptance Criteria:** En az 3 aksiyon kategorisi tanımlı; en az 2 kaynak; maintainer onayı.

**Safety Checklist Type:** Tip A

---

## Issue 4 (W1)

**Issue Title:** [DEFENSIVE-NOTE] Sensitive Data Exposure in LLM Applications

**Repository:** ai-safety-lab

**Content Type:** data-leakage-note

**Trust Tier:** Tier 1 *(kavramsal/genel düzeyde olduğu için Tier 1; RAG/pipeline-spesifik daha derin analiz Wave 2'de Tier 2 olarak işlenecek — bkz. Issue 7)*

**Wave:** 1

**Goal:** LLM uygulamalarında PII/secrets sızıntısının genel kategorilerini (prompt history, log, model output) açıklamak, önleyici kontrol önerisi vermek.

**Scope:** Sızıntı kategorilerinin genel tanımı, output filtering, log redaction prensipleri.

**Out of Scope:** Gerçek sızdırılmış veri örneği, RAG pipeline'a özel derin teknik analiz (bu Wave 2'de ayrı ele alınır).

**Required Output:** `data-leakage-prevention/sensitive-data-exposure-llm-applications.md`

**Required Sections:** Concept Overview, Where Leakage Can Occur, Recommended Control, Sources.

**Source Requirements:** En az 2 bağımsız kaynak.

**Suggested Source Types to Verify:** OWASP Top 10 for LLM Applications — "Sensitive Information Disclosure" (source to verify), NIST Privacy Framework (source to verify).

**Labels:** `data-leakage-prevention`, `tier-1`, `wave-1`, `good-first-issue`

**Acceptance Criteria:** En az 3 sızıntı kategorisi tanımlı; en az 2 kaynak; maintainer onayı.

**Safety Checklist Type:** Tip A

---

## Issue 5 — İLK COMMIT DOSYASI, GitHub Issue Olarak Açılmaz

**Issue Title:** [METHODOLOGY] Safe AI Scenario Writing Rules *(referans amaçlı başlık)*

**Repository:** ai-safety-lab

**Content Type:** methodology

**Trust Tier:** maintainer

**Wave:** 1

**Durum:** Bu dosya ilk commit'te repoya eklenmiş halde gelir (`methodology/safe-ai-scenario-writing.md`), issue olarak beklenmez — diğer tüm Wave 2/3 issue'ları bu dosyaya referans verir, sıralama tersine çevrilemez.

**Goal:** Katkıcıların AI güvenlik riskini "anlamak için" mi "yapmak için" mi yazdıklarını ayırt edebileceği somut kurallar sunmak.

**Required Output:** `methodology/safe-ai-scenario-writing.md`

**Labels:** `methodology`, `maintainer-task`, `wave-1`

**Acceptance Criteria:** Repo public olduğunda dosya zaten mevcut olmalı.

---

# WAVE 2 — Wave 1'den en az 1 merge sonrası açılır (Tier 2)

## Issue 6 (W2)

**Issue Title:** [TOOL-USE] Browser/Email/Terminal Agent Access: Minimum Safety Boundaries

**Repository:** ai-safety-lab

**Content Type:** tool-use-safety

**Trust Tier:** Tier 2

**Wave:** 2

**Goal:** Agent'ların tarayıcı, e-posta ve terminal gibi yüksek etkili araçlara erişiminde uygulanması gereken minimum güvenlik sınırlarını tanımlamak.

**Scope:** Her araç kategorisi için risk deseni (örn. "e-posta gönderme = geri alınamaz aksiyon"), minimum onay/sınırlama kuralı.

**Out of Scope:** Belirli bir aracın/entegrasyonun zafiyet teşhiri, çalışan bypass kodu.

**Required Output:** `tool-use-safety/browser-email-terminal-access-boundaries.md`

**Required Sections:** Tool Category Overview, Risk Pattern, Minimum Safety Boundary, Sources.

**Source Requirements:** En az 2 bağımsız kaynak.

**Research Method Notes:** Her araç kategorisi ayrı ele alınır, genelleme yapılmaz.

**Suggested Source Types to Verify:** OWASP Agentic AI güvenlik rehberleri (source to verify), büyük AI sağlayıcılarının agent/tool-use güvenlik dokümantasyonu (source to verify).

**Labels:** `tool-use-safety`, `tier-2`, `wave-2`, `help-wanted`

**Acceptance Criteria:** En az 3 araç kategorisi; her biri için somut sınır önerisi; en az 2 kaynak; maintainer onayı.

**Safety Checklist Type:** Tip A

---

## Issue 7 (W2)

**Issue Title:** [DATA-LEAKAGE] RAG Pipeline Data Leakage Risk Notes

**Repository:** ai-safety-lab

**Content Type:** data-leakage-note

**Trust Tier:** Tier 2

**Wave:** 2

**Goal:** RAG (retrieval-augmented generation) pipeline'larında kaynak veri sızıntısı riskini Issue 4'ten daha derin/teknik düzeyde ele almak.

**Scope:** Kaynak izolasyonu, embedding/vector store erişim kontrolü, retrieval sonucu output'a sızma riski.

**Out of Scope:** Gerçek bir RAG ürününün zafiyet teşhiri, çalışan exfiltration yöntemi.

**Required Output:** `data-leakage-prevention/rag-pipeline-leakage-risk.md`

**Required Sections:** Concept Overview, Where Leakage Can Occur, Recommended Control, Sources.

**Source Requirements:** En az 2 bağımsız kaynak.

**Suggested Source Types to Verify:** OWASP Top 10 for LLM Applications (source to verify), akademik RAG güvenliği yayınları (source to verify).

**Labels:** `data-leakage-prevention`, `tier-2`, `wave-2`, `help-wanted`

**Acceptance Criteria:** Issue 4'ten farklı/daha derin bir açı sağlıyor; en az 2 kaynak; maintainer onayı.

**Safety Checklist Type:** Tip A

---

## Issue 8 (W2)

**Issue Title:** [AI-FRAUD] AI-Enabled Scam Prevention: Builder Safety Notes

**Repository:** ai-safety-lab

**Content Type:** ai-safety-scenario

**Trust Tier:** Tier 2

**Wave:** 2

**Goal:** AI ürünlerinin scam/impersonation içeriği üretmesini önlemek için ürün tasarım önerileri sunmak (builder açısı).

**Scope:** Çıktı moderasyonu, kötüye kullanım tespiti, rate-limiting/guardrail tasarım prensipleri.

**Out of Scope:** **Tüketici açısı içerik (bu `siber-savunma-atlas/threat-trend-reports/` kapsamındadır, burada tekrarlanmaz).** Gerçek scam metni örneği, deepfake üretim adımı (bu Wave 3'tedir).

**Required Output:** `ai-fraud-awareness/ai-enabled-scam-prevention-builder-notes.md`

**Required Sections:** Scenario Description, Why This Matters, Recommended Mitigation, Sources.

**Source Requirements:** En az 2 bağımsız kaynak.

**Research Method Notes:** Bu issue PR açıklamasında builder açısı olduğunu, siber-savunma-atlas'taki tüketici açısıyla çakışmadığını belirtmelidir.

**Suggested Source Types to Verify:** Büyük AI sağlayıcılarının kötüye kullanım önleme (abuse prevention) dokümantasyonu (source to verify), Trust & Safety endüstri yayınları (source to verify).

**Labels:** `ai-fraud-awareness`, `tier-2`, `wave-2`, `help-wanted`, `scope-differentiated`

**Acceptance Criteria:** Builder açısı net; siber-savunma-atlas ile çakışmıyor; en az 2 kaynak; maintainer onayı.

**Safety Checklist Type:** Tip A

---

## Issue 9 (W2)

**Issue Title:** [AGENT-SECURITY] Agent Audit Logging and Approval Flow Design

**Repository:** ai-safety-lab

**Content Type:** agent-risk-card

**Trust Tier:** Tier 2

**Wave:** 2

**Goal:** Agent aksiyonlarının izlenebilirliği için audit log ve approval flow tasarım prensiplerini detaylandırmak.

**Scope:** Hangi olayların loglanması gerektiği, log bütünlüğü, onay akışının teknik tasarımı (örn. ayrı bir onay servisi).

**Out of Scope:** Belirli bir ürünün log mekanizmasını atlatma yöntemi.

**Required Output:** `agent-security/agent-audit-logging-approval-flow.md`

**Required Sections:** Concept Overview, Risk Pattern, Recommended Safeguard, Sources.

**Source Requirements:** En az 2 bağımsız kaynak.

**Suggested Source Types to Verify:** NIST AI RMF (source to verify), OWASP Agentic AI güvenlik dokümantasyonu (source to verify).

**Labels:** `agent-security`, `tier-2`, `wave-2`, `help-wanted`

**Acceptance Criteria:** En az 2 kaynak; somut tasarım önerisi; maintainer onayı.

**Safety Checklist Type:** Tip A

---

# WAVE 3 — Wave 2'den en az 2 katkıcı Tier 2'ye ulaştıktan sonra açılır (Tier 3, misuse-sensitive)

## Issue 10 (W3)

**Issue Title:** [PROMPT-INJECTION] Prompt Injection Awareness Without Publishing Bypass Prompts

**Repository:** ai-safety-lab

**Content Type:** ai-safety-scenario

**Trust Tier:** Tier 3 — misuse-sensitive

**Wave:** 3

**Goal:** Prompt injection kavramını ve savunma yaklaşımlarını, çalışan bir örnek vermeden açıklamak.

**Scope:** Kavramın mantığı, kategori düzeyinde teknik açıklama (örn. "indirect injection vs direct injection" ayrımı, isim verilerek ama örnek metin verilmeden), savunma desenleri.

**Out of Scope:** **Çalışan injection payload'u, kopyala-yapıştır kullanılabilir herhangi bir saldırı metni — istisnasız.**

**Required Output:** `prompt-injection-awareness/prompt-injection-awareness-no-bypass-examples.md`

**Required Sections:** Scenario Description, Why This Matters, Recommended Mitigation, **What This Content Deliberately Excludes**, Sources.

**Source Requirements:** En az 2 bağımsız kaynak.

**Research Method Notes:** Bkz. `methodology/safe-ai-scenario-writing.md` Örnek 1 ve 2. Reviewer, içerikte kopyala-yapıştır kullanılabilir hiçbir metin olmadığını teyit eder.

**Suggested Source Types to Verify:** OWASP Top 10 for LLM Applications — "Prompt Injection" (source to verify), akademik prompt injection savunma yayınları (source to verify).

**Labels:** `prompt-injection-awareness`, `tier-3`, `wave-3`, `misuse-sensitive`, `maintainer-review-required`, `needs-sources`

**Acceptance Criteria:** Çalışan örnek/payload yok; "Deliberately Excludes" bölümü dolu; en az 2 kaynak; maintainer onayı **zorunlu**.

**Safety Checklist Type:** Tip B

---

## Issue 11 (W3)

**Issue Title:** [MODEL-RESILIENCE] Jailbreak-Resistant Design Principles (No Bypass Examples)

**Repository:** ai-safety-lab

**Content Type:** ai-safety-scenario

**Trust Tier:** Tier 3 — misuse-sensitive

**Wave:** 3

**Goal:** Modellerin jailbreak'e karşı dayanıklılığını artıran tasarım prensiplerini, çalışan jailbreak örneği vermeden açıklamak.

**Scope:** Defense-in-depth kavramı, çıktı düzeyinde doğrulama katmanları, jailbreak teknik *kategorilerinin* (örn. roleplay framing) isimle ama örneksiz anılması.

**Out of Scope:** **Çalışan jailbreak prompt'u veya bunun küçük bir varyasyonu — istisnasız.**

**Required Output:** `model-resilience/jailbreak-resistant-design-principles.md`

**Required Sections:** Scenario Description, Why This Matters, Recommended Mitigation, **What This Content Deliberately Excludes**, Sources.

**Source Requirements:** En az 2 bağımsız kaynak.

**Research Method Notes:** Bkz. `methodology/safe-ai-scenario-writing.md` Örnek 2.

**Suggested Source Types to Verify:** Akademik adversarial robustness yayınları (source to verify), büyük AI sağlayıcılarının model güvenliği şeffaflık raporları (source to verify).

**Labels:** `model-resilience`, `tier-3`, `wave-3`, `misuse-sensitive`, `maintainer-review-required`, `needs-sources`

**Acceptance Criteria:** Çalışan örnek yok; "Deliberately Excludes" bölümü dolu; en az 2 kaynak; maintainer onayı **zorunlu**.

**Safety Checklist Type:** Tip B

---

## Issue 12 (W3)

**Issue Title:** [AI-FRAUD] Deepfake/Manipulation Misuse Prevention: Product Design Safeguards

**Repository:** ai-safety-lab

**Content Type:** ai-safety-scenario

**Trust Tier:** Tier 3 — misuse-sensitive

**Wave:** 3

**Goal:** AI ürünlerinin deepfake/ses klonlama gibi özelliklerinin kötüye kullanımını önleyen ürün tasarım güvenlik önlemlerini açıklamak.

**Scope:** Liveness check, onay doğrulama, watermarking/provenance mekanizmaları, kullanım politikası tasarımı — **builder açısı**.

**Out of Scope:** **Deepfake/ses klonlama üretiminin teknik adımları veya araç önerisi — istisnasız.** Gerçek mağdur/örnek vakası.

**Required Output:** `ai-fraud-awareness/deepfake-manipulation-misuse-prevention.md`

**Required Sections:** Scenario Description, Why This Matters, Recommended Mitigation, **What This Content Deliberately Excludes**, Sources.

**Source Requirements:** En az 2 bağımsız kaynak.

**Research Method Notes:** Bkz. `methodology/safe-ai-scenario-writing.md` Örnek 3.

**Suggested Source Types to Verify:** C2PA (Coalition for Content Provenance and Authenticity) dokümantasyonu (source to verify), büyük AI sağlayıcılarının sorumlu kullanım/güvenlik politikaları (source to verify).

**Labels:** `ai-fraud-awareness`, `tier-3`, `wave-3`, `misuse-sensitive`, `maintainer-review-required`, `needs-sources`

**Acceptance Criteria:** Üretim adımı yok; builder açısı net; "Deliberately Excludes" bölümü dolu; en az 2 kaynak; maintainer onayı **zorunlu**.

**Safety Checklist Type:** Tip B
