# İçerik Politikası — ai-safety-lab

## Ana Çizgi

How to attack değil, how to understand and defend. Bu repo AI güvenliğini ürün geliştirici, araştırmacı ve savunmacı bakış açısıyla ele alır.

## Kesin Yasaklar (İstisnasız)

- Çalışan bypass/jailbreak prompt'u
- Prompt injection payload örneği (kopyala-yapıştır kullanılabilir saldırı metni)
- Deepfake, scam veya phishing üretim rehberi/adımı
- Zararlı otomasyon talimatı veya çalışan kötüye kullanım akışı
- Manipülasyon taktiği veya hedefleme rehberi
- Gerçek hedef, mağdur, kullanıcı, kurum bilgisi, credential veya özel veri
- Model güvenlik mekanizmalarını atlatma adım adım talimatı

## Kabul Edilen İçerik

- Agent/tool-use güvenliği kavramları ve savunma tasarım desenleri
- Veri sızıntısı risk kategorileri ve önleyici kontroller
- Human-in-the-loop / fail-safe tasarım prensipleri
- AI ürün güvenliği checklist'leri
- Prompt injection / model dayanıklılığı kavramlarının **savunma odaklı**, örnek payload içermeyen açıklaması

## Güvenli Yazım Kuralı

Tüm katkılar `methodology/safe-ai-scenario-writing.md`'ye uyar. Bu dosya, bir riski "nasıl anlatılır" ile "nasıl uygulanır" arasındaki farkı somut örneklerle tanımlar ve bu repo için zorunludur.

## Kategori Sınırları

- **`ai-fraud-awareness/`**: Builder/ürün açısı. Son kullanıcı dolandırıcılık farkındalığı `siber-savunma-atlas` kapsamındadır, burada işlenmez.
- **`prompt-injection-awareness/`**, **`model-resilience/`**: Kavram ve savunma farkındalığı. Çalışan örnek/payload hiçbir biçimde kabul edilmez, bu kategori türleri otomatik olarak Tier 3 + maintainer-review-required'dır.

## Wave 3 — Misuse-Sensitive İçerik

Prompt injection, jailbreak-resistant design, deepfake/manipulation prevention ve high-risk automation safety konuları Wave 3'te, yalnızca maintainer onayıyla ve `Safety Checklist Type B` ile işlenir. Bu konularda hiçbir koşulda çalışan bypass promptu, jailbreak örneği, manipülasyon metni veya phishing/deepfake üretim adımı yazılmaz.
