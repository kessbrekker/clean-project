# 📘 Proje Geliştirme Standartları & Rehber

Bu depo, projemizdeki geliştirme süreçlerini standartlaştırmak, yeni ekip üyelerinin adaptasyonunu (onboarding) hızlandırmak ve kod kalitesini en üst seviyede tutmak için oluşturulmuş **merkezi bilgi kaynağıdır.**

Lütfen geliştirmeye başlamadan önce ilgili dokümanları gözden geçirin.

---

## 🏗️ Dokümantasyon Dizini

Aşağıdaki bağlantılar üzerinden projenin farklı alanlarındaki standartlarımıza ulaşabilirsiniz:

| Dosya | Açıklama |
| :--- | :--- |
| [**GIT.md**](./GIT.md) | Git akışı, commit mesajı standartları ve PR süreçleri. |
| [**STRUCTURE.md**](./STRUCTURE.md) | Proje klasör yapısı ve dosya isimlendirme kuralları. |
| [**PNPM.md**](./PNPM.md) | Paket yönetimi ve `pnpm` özelindeki iş akışımız. |
| [**ICONS.md**](./ICONS.md) | React ve Next.js projelerinde ikon kullanımı ve optimizasyonu. |
| [**SHADCNUI.md**](./SHADCNUI.md) | UI bileşenlerinin kullanımı ve özelleştirme rehberi. |
| [**LARAVEL.md**](./LARAVEL.md) | Laravel ile React/Next.js entegrasyonu ve API standartları. |
| [**SEMANTIC.md**](./SEMANTIC.md) | Versiyonlama (Versioning) ve sürüm yönetimi kuralları. |

---

## 🚀 Temel İlkelerimiz

1.  **Tutarlılık:** Kodun hangi elden çıktığı değil, projenin standartlarına ne kadar uyduğu önemlidir.
2.  **Okunabilirlik:** "Kod bir kez yazılır, onlarca kez okunur." Prensibini unutmayın.
3.  **Dokümantasyon:** Yeni bir özellik veya karmaşık bir yapı eklediğinizde, ilgili `.md` dosyasını güncellemeyi ihmal etmeyin.

---

## 🛠️ Geliştirme Ortamı

Projeyi yerel ortamınızda ayağa kaldırmak için:

```bash
# Bağımlılıkları yükleyin
pnpm install

# Geliştirme sunucusunu başlatın
pnpm dev
```

> **Not:** Eğer bu dokümanlarda eksik veya hatalı bir bilgi görürseniz, lütfen bir PR açarak güncellenmesine yardımcı olun. Birlikte daha iyiyiz! ⚡
