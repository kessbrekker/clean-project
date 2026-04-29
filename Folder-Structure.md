# 📂 Proje Klasör Yapısı (Master Template)

Bu yapı, ölçeklenebilir, bakımı kolay ve modern Next.js (App Router) standartlarına uygun olarak tasarlanmıştır.

```text
src/
├── app/                    # ROUTING & PAGES (Next.js App Router)
│   ├── (auth)/             # Route Group: URL'de gözükmez, mantıksal gruplama (örn: /login)
│   │   ├── login/
│   │   └── register/
│   ├── (dashboard)/        # Route Group: Panel sayfaları ve ortak layoutlar
│   │   ├── layout.tsx      # Dashboard'a özel sidebar, navbar vb.
│   │   └── profile/
│   ├── api/                # API Route Handlers (Backend endpointleri)
│   ├── layout.tsx          # Global Root Layout (Html, Body, Fontlar)
│   ├── page.tsx            # Ana Sayfa (Landing Page)
│   ├── error.tsx           # Global hata yakalama sayfası
│   └── loading.tsx         # Global loading skeletonları
│
├── components/             # SHARED COMPONENTS (Genel UI Bileşenleri)
│   ├── ui/                 # Atomik bileşenler (Shadcn/UI, Button, Input, Modal)
│   ├── forms/              # Genel form elemanları (React Hook Form yapıları)
│   ├── layout/             # Genel Header, Footer, Sidebar bileşenleri
│   └── common/             # Çok amaçlı minik bileşenler (Spinner, Badge)
│
├── features/               # FEATURE-BASED MODULES (Uygulamanın Kalbi)
│   ├── [feature-name]/     # Örn: 'cart', 'products', 'auth'
│   │   ├── api/            # O özelliğe özel fetch fonksiyonları / server actions
│   │   ├── components/     # O özelliğe özel karmaşık UI (ProductCard, CartList)
│   │   ├── hooks/          # O özelliğe özel logicler (useCart, useProductFilter)
│   │   ├── types/          # TypeScript interface/type tanımları
│   │   └── index.ts        # Public API: Dışarıya açılacak olanları buradan export et
│
├── hooks/                  # GLOBAL HOOKS (Birden fazla feature tarafından kullanılanlar)
│   ├── use-debounce.ts
│   ├── use-local-storage.ts
│   └── use-window-size.ts
│
├── lib/                    # SDK & CONFIG (Dış kütüphane konfigürasyonları)
│   ├── prisma.ts           # Veritabanı clientı
│   ├── stripe.ts           # Ödeme sistemleri
│   ├── lucia.ts            # Auth kütüphanesi ayarları
│   └── utils.ts            # Shadcn'in kullandığı 'cn' gibi yardımcılar
│
├── services/               # GLOBAL SERVICES (Feature dışı genel dış servisler)
│   └── mail-service.ts
│
├── store/                  # STATE MANAGEMENT (Global state: Zustand, Redux vb.)
│   └── use-global-store.ts
│
├── types/                  # GLOBAL TYPES (Uygulama genelinde paylaşılan tipler)
│   └── index.d.ts
│
├── utils/                  # HELPERS (Saf fonksiyonlar - Pure Functions)
│   ├── format-date.ts
│   ├── format-currency.ts
│   └── validate-email.ts
│
├── providers/              # CONTEXT PROVIDERS (Client-side sarmalayıcılar)
│   ├── theme-provider.tsx
│   ├── query-provider.tsx  # React Query gibi yapılar için
│   └── auth-provider.tsx
│
└── styles/                 # STYLES (Global CSS)
    └── globals.css
```

---

## 🛠 Temel Kurallar ve İpuçları

1. **Colocation (Yakınlık İlkesi):** Bir dosya sadece bir yerde kullanılıyorsa, onu kullandığın yere en yakın klasörde tut. Eğer başka yerler de ihtiyaç duyarsa yukarıdaki genel klasörlere (`components`, `hooks` vb.) taşı.
2. **Features Klasörü:** Uygulamanın asıl iş mantığı burada döner. Bir feature klasörü kendi içinde bağımsız olmalıdır. Mesela `features/cart` klasörünü kopyalayıp başka projeye attığında minimum değişiklikle çalışabilmelidir.
3. **Route Groups `()`:** Klasör isimlerini parantez içinde yazmak URL yapısını bozmaz. Projeyi bölümlere ayırmak (Auth sayfaları vs. Mağaza sayfaları) için mükemmeldir.
4. **Shadcn/UI Kullanımı:** Shadcn bileşenlerini her zaman `components/ui` altında tut. Onlara dokunmaktan korkma, onlar artık senin kodun!
5. **Index.ts Kullanımı:** Feature klasörleri içindeki `index.ts` dosyaları bir "kapı" görevi görür. Dışarıdaki bir dosya o feature içinden bir şey import edecekse sadece `index.ts` üzerinden erişmelidir.
