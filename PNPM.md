# pnpm: Performant npm – Hızlı, Akıllı ve Verimli Paket Yönetimi

**pnpm**, Node.js ekosistemindeki en hızlı ve disk dostu paket yöneticisidir. npm ve yarn'ın aksine, paketleri her proje için tekrar tekrar indirmek yerine merkezi bir depoda saklayarak projeler arasında paylaştırır.

---

## 🚀 Neden pnpm Kullanmalısın?

### 1. Disk Alanı Tasarrufu
Aynı paketin 100 farklı versiyonunu 100 farklı projede kullanıyorsan, npm bunu 100 kez diske yazar. **pnpm** ise bunu merkezi bir "Content-addressable store" içinde bir kez saklar ve projelerine sadece **hard link** (sabit bağlantı) oluşturur.



### 2. İnanılmaz Hız
pnpm, kurulum sürecini aşamalara bölerek (indirme, çözümleme, yazma) bunları paralel olarak yürütür. Bu, özellikle büyük `node_modules` klasörlerine sahip e-ticaret projelerinde devasa zaman kazancı sağlar.

### 3. "Hayalet Bağımlılık" (Phantom Dependencies) Engelleme
npm ve yarn, `node_modules` yapısını düzleştirir (flatten). Bu da bazen doğrudan yüklemediğin bir paketi kodunda kullanabilmene neden olur (ve bu durum üretim ortamında hatalara yol açar). pnpm ise **strict** (katı) bir yapı kullanır; sadece `package.json` dosmanda olan paketlere erişebilirsin.

---

## 🛠️ pnpm Komut Rehberi (Cheat Sheet)

| İşlem | Komut |
| :--- | :--- |
| **Yeni Paket Ekle** | `pnpm add <paket>` |
| **Geliştirme Paketi Ekle** | `pnpm add -D <paket>` |
| **Bağımlılıkları Kur** | `pnpm install` veya `pnpm i` |
| **Paket Kaldır** | `pnpm remove <paket>` |
| **Paketleri Güncelle** | `pnpm update` veya `pnpm up` |
| **İnteraktif Güncelleme** | `pnpm up -i` |
| **Geçici Paket Çalıştır** | `pnpm dlx <paket>` (npx karşılığı) |

---


## ⚙️ İleri Düzey İpuçları

### `.npmrc` Yapılandırması
Projenin kök dizinine bir `.npmrc` dosyası ekleyerek pnpm davranışlarını özelleştirebilirsin:

```text
# Bazı eski kütüphaneler pnpm'in katı yapısında hata verirse:
# shamefully-hoist=true

# Paketleri otomatik olarak en güncel sürüme sabitlemek için:
# save-exact=true
```

### Projeyi Temizlemek
Eğer `node_modules` içinde bir şeyler ters giderse (ki pnpm'de bu çok nadirdir), şu komutla her şeyi tertemiz yapabilirsin:

```bash
# Sadece yerel node_modules'ü siler ve tekrar kurar
rm -rf node_modules && pnpm i
```

---

> **Özet:** pnpm kullanmak sadece bir tercih değil, modern web geliştirme süreçlerinde bir standart haline gelmiştir. Özellikle **Next.js + shadcn/ui + Tailwind** üçlüsüyle çalışırken sağladığı hız ve güvenilirlik paha biçilemez.
