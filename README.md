# CV Portfolio - Vue.js

Modern ve responsive CV Portfolio web sitesi. Vue.js 3, Vite ve TailwindCSS kullanılarak geliştirilmiştir.

## 🚀 Özellikler

- **Responsive Tasarım**: Tüm cihazlarda mükemmel görünüm
- **Modern UI/UX**: Temiz ve profesyonel tasarım
- **Smooth Scrolling**: Yumuşak geçişler ve animasyonlar
- **İnteraktif Bileşenler**: Animasyonlu yetenek barları
- **İletişim Formu**: Kullanıcı mesajları için form
- **Sosyal Medya Entegrasyonu**: Sosyal medya linkleri

## 🛠️ Teknolojiler

- **Vue.js 3** - Frontend Framework
- **Vue Router 4** - Sayfa yönlendirme
- **Pinia** - State Management
- **Vite** - Build Tool
- **TailwindCSS** - CSS Framework
- **Font Awesome** - İkonlar

## 📦 Kurulum

```bash
# Bağımlılıkları yükle
npm install

# Geliştirme sunucusunu başlat
npm run dev

# Production build
npm run build

# Build önizleme
npm run preview
```

## 📁 Proje Yapısı

```
cv-portfolio/
├── public/
│   └── images/          # Statik resimler
├── src/
│   ├── components/      # Vue bileşenleri
│   │   ├── Header.vue
│   │   └── Footer.vue
│   ├── views/           # Sayfa bileşenleri
│   │   └── Home.vue
│   ├── router/          # Vue Router konfigürasyonu
│   │   └── index.js
│   ├── App.vue          # Ana uygulama bileşeni
│   ├── main.js          # Uygulama giriş noktası
│   └── style.css        # Global stiller
├── index.html           # HTML şablonu
├── package.json         # Proje bağımlılıkları
├── vite.config.js       # Vite konfigürasyonu
└── README.md           # Proje dokümantasyonu
```

## 🎨 Bileşenler

### Header
- Responsive navigasyon menüsü
- Mobil hamburger menü
- Smooth scroll navigasyon

### Hero Section
- Kişisel tanıtım
- Profil resmi
- Call-to-action butonları

### About Section
- Kişisel açıklama
- İstatistik kartları

### Experience Section
- Timeline formatında iş deneyimi
- Şirket bilgileri ve görevler

### Education Section
- Eğitim geçmişi kartları
- İkon ve açıklamalar

### Skills Section
- Kategorize edilmiş yetenekler
- Animasyonlu progress barları

### Contact Section
- İletişim bilgileri
- İletişim formu

### Footer
- Sosyal medya linkleri
- Copyright bilgisi

## 🚀 Deployment

### GitHub Pages
```bash
# Build oluştur
npm run build

# dist klasörünü GitHub Pages'e deploy et
```

### Netlify/Vercel
```bash
# Build komutları otomatik çalışır
npm run build
```

## 📱 Responsive Design

- **Desktop**: 1200px+ genişlik
- **Tablet**: 768px - 1199px genişlik
- **Mobile**: 767px altı genişlik

## 🎯 Özelleştirme

Kişisel bilgilerinizi güncellemek için `src/views/Home.vue` dosyasındaki `personalInfo` objesini düzenleyin:

```javascript
const personalInfo = reactive({
  name: "Adınız",
  title: "Mesleğiniz",
  description: "Kısa açıklama",
  // ... diğer bilgiler
})
```

## 📄 Lisans

Bu proje MIT lisansı altında lisanslanmıştır.

## 👨‍💻 Geliştirici

**Yiğit Türkiş**
- Email: turkissyy@gmail.com
- GitHub: [@turkissyy](https://github.com/turkissyy)
- LinkedIn: [linkedin.com/in/yigitturkis](https://linkedin.com/in/yigitturkis)
