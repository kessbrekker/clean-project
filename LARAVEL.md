# React/Next.js ve Laravel Entegrasyon Rehberi: Modern Web Mimarisi

React (veya Next.js) ile Laravel'i birleştirmek, günümüzün en popüler ve güçlü "full-stack" yaklaşımlarından biridir. Laravel'in sağlam backend yeteneklerini, React'in dinamik kullanıcı arayüzü gücüyle birleştirerek ölçeklenebilir uygulamalar geliştirebilirsiniz.

Genel olarak iki ana yaklaşım mevcuttur: **Decoupled (Bağımsız API)** ve **Inertia.js (Bütünleşik Yapı)**.

---

## 1. Yaklaşım: Bağımsız API (Headless Architecture)

Bu yöntemde Laravel sadece bir veri kaynağı (API) görevi görür. Next.js ise tamamen bağımsız bir proje olarak bu veriyi tüketir.

### Laravel Tarafı (Backend)
* **Laravel Sanctum:** API tabanlı kimlik doğrulama (Token-based Auth) için en iyi çözümdür.
* **API Resources:** Veritabanı modellerini JSON formatına dönüştürmek için kullanılır.
* **CORS Ayarları:** `config/cors.php` dosyasında Next.js uygulamanızın URL'ine izin vermeniz gerekir.

### Next.js Tarafı (Frontend)
* **Data Fetching:** Sunucu tarafında `fetch` veya `axios` kullanarak Laravel API'sine istek atılır.
* **Server Components:** Veriyi sunucuda çekerek SEO avantajı sağlar.
* **Client Components:** Kullanıcı etkileşimi (form gönderimi, sepet işlemleri) için kullanılır.



---

## 2. Yaklaşım: Inertia.js (Modern Monolith)

Inertia.js, Laravel'den ayrılmadan "Single Page Application" (SPA) deneyimi yaşamanızı sağlar. Laravel rotalarını kullanmaya devam ederken, görünüm (View) dosyası olarak React bileşenlerini kullanırsınız.

### Neden Inertia.js?
* **API Yazma Zorunluluğu Yok:** Veriyi doğrudan controller içinden props olarak React'e gönderirsiniz.
* **Routing Laravel'de Kalır:** Next.js routing yapısıyla uğraşmanıza gerek kalmaz.
* **SEO ve Hız:** Klasik Laravel uygulaması gibi çalışır ancak sayfa geçişleri yenilenmeden gerçekleşir.

```php
// Laravel Controller Örneği (Inertia)
public function index() {
    return Inertia::render('Home', [
        'users' => User::all()
    ]);
}
```

---

## 3. Kimlik Doğrulama (Authentication) Stratejileri

Bağlantının en kritik noktası kullanıcı oturum yönetimidir.

| Yöntem | Kullanım Alanı | Açıklama |
| :--- | :--- | :--- |
| **Sanctum (Stateful)** | Aynı domain altında (örn: api.site.com ve site.com) | Cookie tabanlı güvenli oturum. En kolayıdır. |
| **Sanctum (Tokens)** | Mobil uygulamalar veya farklı domainler | API Token üretilir ve her istekte Header'da gönderilir. |
| **JWT (Json Web Token)** | Tamamen bağımsız mikroservisler | Stateless bir yapı sunar, Laravel tarafında `tymon/jwt-auth` gibi paketler gerektirir. |

---

## 4. Proje Türüne Göre Seçim Tablosu

Hangi yolu seçmelisiniz? İhtiyaca göre karar verin:

| İhtiyaç | Tercih Edilen Yapı | Neden? |
| :--- | :--- | :--- |
| **E-Ticaret / Blog** | Next.js + Laravel API | Üstün SEO ve ISR (Incremental Static Regeneration) desteği. |
| **Yönetim Paneli / SaaS** | Laravel + Inertia.js + React | Çok hızlı geliştirme süreci ve karmaşık form yönetimi. |
| **Mobil Uygulama Destekli** | Laravel API (Headless) | Aynı API hem web hem mobil uygulama tarafından kullanılabilir. |

---

## 5. Kritik İpuçları

1.  **Environment Variables (.env):** Next.js tarafında `NEXT_PUBLIC_API_URL` değişkenini tanımlayarak Laravel API'nize erişin.
2.  **Validation Hataları:** Laravel'in döndürdüğü 422 hatalarını React tarafında bir global handler (interceptor) ile yakalamak kullanıcı deneyimini artırır.
3.  **Image Optimization:** Laravel'den gelen görselleri Next.js `Image` bileşeni ile kullanırken, Laravel domainini `next.config.js` içinde `images.remotePatterns` kısmına eklemeyi unutmayın.

---

## Özet Akış Şeması



Bu mimariyi kurarken **pnpm** kullanıyorsan, Next.js projenin bağımlılıklarını çok daha hızlı yönetebilirsin. Laravel tarafında ise `composer` paketlerini güncel tutman yeterli olacaktır.
