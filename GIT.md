# 🚀 Takım İçi Git Kullanım Standartları ve İş Akışı Rehberi

Bu döküman, projenin sürdürülebilirliği, kod geçmişinin okunabilirliği ve ekip içi senkronizasyonun en üst düzeyde tutulması amacıyla hazırlanmıştır.

---

## 1. Commit Mesajı Standartları (Conventional Commits)

Commit mesajları, projenin tarihçesidir. İyi bir mesaj, kodun **ne** yaptığından ziyade **neden** yapıldığını ve **neyi** etkilediğini anlatır. Takım içinde **Conventional Commits** yapısını kullanıyoruz.



### Format:
`<tip>(<isteğe bağlı kapsam>): <kısa açıklama>`

### Türler (Types):
*   **feat**: Yeni bir özellik eklendiğinde.
*   **fix**: Bir hata düzeltildiğinde.
*   **docs**: Sadece dökümantasyonda değişiklik yapıldığında.
*   **style**: Kodun çalışmasını etkilemeyen görsel değişiklikler (boşluklar, noktalı virgüller vb.).
*   **refactor**: Ne bir hata düzeltmesi ne de yeni bir özellik eklemeyen kod değişikliği.
*   **test**: Eksik testlerin eklenmesi veya mevcut testlerin düzeltilmesi.
*   **chore**: Build süreci, kütüphane güncellemeleri veya yardımcı araçlardaki değişiklikler.

### Kurallar:
1.  **Emir kipi kullanın:** "Düzeltildi" değil, "Düzelt" veya "Fix". (Örn: `feat: login sayfasına recaptcha ekle`)
2.  **İlk harf küçük:** Tip ve kapsamdan sonraki ilk harfi küçük tutun.
3.  **Nokta koymayın:** Mesajın sonuna nokta koymayın.
4.  **Detay gerekiyorsa:** Kısa açıklamadan sonra bir satır boşluk bırakıp detaylı paragraf yazın.

---

## 2. Branch (Dal) Yönetimi

Kaosun önüne geçmek için **Git Flow** benzeri bir yapı kullanıyoruz. Herkesin doğrudan `main` branch'ine basması kesinlikle yasaktır.



### Ana Dalların Görevleri:
*   **main**: Sadece canlıya çıkmaya hazır, stabil kod bulunur.
*   **develop**: Geliştirme sürecindeki ana daldır. Feature'lar buraya merge edilir.

### Destek Dalları:
*   **feature/`görev-adı`**: Yeni özellikler için `develop` üzerinden açılır. İş bitince `develop`'a döner.
    *   *Örn:* `feature/user-auth`
*   **bugfix/`hata-adı`**: `develop` üzerindeki hataları düzeltmek için.
*   **hotfix/`acil-hata`**: Canlıdaki (`main`) kritik hataları anında düzeltmek için `main` üzerinden açılır.
*   **release/`v1.1.0`**: Yayına hazırlık sürecinde sürüm notları ve son testler için.

---

## 3. Pull Request (PR) ve Merge Süreci

Kodun kalitesini koruyan en önemli filtre PR aşamasıdır.

### PR Göndermeden Önce:
1.  Kendi branch'inizde kodun çalıştığından ve testlerden geçtiğinden emin olun.
2.  Gereksiz `console.log` veya "todo" notlarını temizleyin.
3.  Branch'inizi güncel tutmak için `develop` dalını kendi dalınıza `rebase` veya `merge` yapın.

### PR Açıklaması:
PR açarken şu şablonu takip edin:
*   **Ne yapıldı?**: Kısa özet.
*   **İlgili Task**: Jira/Trello/Github Issue linki.
*   **Ekran Görüntüsü**: Görsel bir değişiklik varsa mutlaka eklenmeli.

### Merge Stratejisi:
*   **Squash and Merge**: Feature branch'indeki 20 tane "ufak tefek" commit'i tek bir anlamlı commit'e indirgeyerek ana dala ekler. Geçmişin temiz kalması için önerilir.

---

## 4. Hayat Kurtaran İpuçları (Tips & Tricks)

### Yarım Kalan İşleri Saklamak (`stash`)
Henüz commit atmaya hazır değilsiniz ama acilen başka bir dalda hata düzeltmeniz gerekiyor:
```bash
git stash          # Değişiklikleri geçici olarak kaldır ve sakla
git stash pop      # Geri geldiğinde kaldığın yerden devam et
```

### Son Commit'i Güncellemek (`amend`)
Commit attınız ama küçük bir yazım hatası fark ettiniz veya bir dosyayı eklemeyi unuttunuz:
```bash
git add .
git commit --amend --no-edit # Eski commit'i günceller, yeni commit oluşturmaz
```

### Git Geçmişini Görselleştirmek
Terminalden ağaç yapısını görmek için:
```bash
git log --oneline --graph --all
```

### Yanlış Dallanmayı Düzeltmek
Eğer yanlış branch'e commit attıysanız, `cherry-pick` ile o commit'i doğru branch'e "cımbızla" çekebilirsiniz:
```bash
git checkout doğru-branch
git cherry-pick <hatalı-commit-hash>
```

---
> **Not:** "Kod çalışıyorsa dokunma" değil, "Kod temizse pushla" prensibiyle ilerliyoruz. İyi geliştirmeler!
