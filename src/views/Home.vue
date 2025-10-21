<template>
  <div>
    <!-- Header Section -->
    <header class="header">
      <nav class="navbar">
        <div class="nav-brand">
          <h2>{{ personalInfo.name }}</h2>
        </div>
        <ul class="nav-menu" :class="{ active: menuOpen }">
          <li><a href="#about" @click="scrollToSection('about')">Hakkımda</a></li>
          <li><a href="#experience" @click="scrollToSection('experience')">Deneyim</a></li>
          <li><a href="#education" @click="scrollToSection('education')">Eğitim</a></li>
          <li><a href="#skills" @click="scrollToSection('skills')">Yetenekler</a></li>
          <li><a href="#contact" @click="scrollToSection('contact')">İletişim</a></li>
        </ul>
        <div class="hamburger" @click="toggleMenu">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </nav>
    </header>

    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-content">
        <div class="hero-text">
          <h1 class="hero-title">
            Merhaba, Ben <span class="highlight">{{ personalInfo.name }}</span>
          </h1>
          <p class="hero-subtitle">{{ personalInfo.title }}</p>
          <p class="hero-description">{{ personalInfo.description }}</p>
          <div class="hero-buttons">
            <button class="btn btn-primary" @click="scrollToSection('contact')">
              <i class="fas fa-envelope"></i> İletişime Geç
            </button>
            <button class="btn btn-secondary" @click="downloadCV">
              <i class="fas fa-download"></i> CV İndir
            </button>
          </div>
        </div>
        <div class="hero-image">
          <div class="profile-image">
            <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=400&h=400&fit=crop&crop=face" alt="Yiğit Türkiş"/>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="section">
      <div class="container">
        <h2 class="section-title">Hakkımda</h2>
        <div class="about-content">
          <div class="about-text">
            <p>{{ personalInfo.about }}</p>
            <div class="stats">
              <div class="stat-item" v-for="stat in personalInfo.stats" :key="stat.label">
                <div class="stat-number">{{ stat.value }}</div>
                <div class="stat-label">{{ stat.label }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="section bg-light">
      <div class="container">
        <h2 class="section-title">İş Deneyimi</h2>
        <div class="timeline">
          <div class="timeline-item" v-for="(job, index) in experience" :key="index">
            <div class="timeline-marker"></div>
            <div class="timeline-content">
              <h3 class="job-title">{{ job.position }}</h3>
              <h4 class="company-name">{{ job.company }}</h4>
              <p class="job-period">{{ job.period }}</p>
              <p class="job-description">{{ job.description }}</p>
              <div class="job-skills">
                <span class="skill-tag" v-for="skill in job.skills" :key="skill">{{ skill }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Education Section -->
    <section id="education" class="section">
      <div class="container">
        <h2 class="section-title">Eğitim</h2>
        <div class="education-grid">
          <div class="education-item" v-for="(edu, index) in education" :key="index">
            <div class="education-icon">
              <i :class="edu.icon"></i>
            </div>
            <div class="education-content">
              <h3 class="education-degree">{{ edu.degree }}</h3>
              <h4 class="education-school">{{ edu.school }}</h4>
              <p class="education-period">{{ edu.period }}</p>
              <p class="education-description">{{ edu.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="section bg-light">
      <div class="container">
        <h2 class="section-title">Yetenekler</h2>
        <div class="skills-grid">
          <div class="skill-category" v-for="(category, categoryName) in skills" :key="categoryName">
            <h3 class="category-title">{{ categoryName }}</h3>
            <div class="skill-items">
              <div class="skill-item" v-for="skill in category" :key="skill.name">
                <div class="skill-info">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-level">{{ skill.level }}%</span>
                </div>
                <div class="skill-bar">
                  <div class="skill-progress" :style="{ width: skill.level + '%' }"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="section">
      <div class="container">
        <h2 class="section-title">İletişim</h2>
        <div class="contact-content">
          <div class="contact-info">
            <div class="contact-item" v-for="contact in contactInfo" :key="contact.type">
              <div class="contact-icon">
                <i :class="contact.icon"></i>
              </div>
              <div class="contact-details">
                <h4>{{ contact.type }}</h4>
                <p>{{ contact.value }}</p>
              </div>
            </div>
          </div>
          <div class="contact-form">
            <form @submit.prevent="submitForm">
              <div class="form-group">
                <input type="text" v-model="form.name" placeholder="Adınız" required>
              </div>
              <div class="form-group">
                <input type="email" v-model="form.email" placeholder="E-posta" required>
              </div>
              <div class="form-group">
                <textarea v-model="form.message" placeholder="Mesajınız" rows="5" required></textarea>
              </div>
              <button type="submit" class="btn btn-primary">
                <i class="fas fa-paper-plane"></i> Mesaj Gönder
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import { ref, reactive, onMounted } from 'vue'

export default {
  name: 'Home',
  setup() {
    const menuOpen = ref(false)
    
    const personalInfo = reactive({
      name: "Yiğit Türkiş",
      title: "Junior Front-End Developer",
      description: "Merhaba! Ben Yiğit, kendini geliştirmeye çalışan bir Junior Front-End Developer'ım. HTML, CSS ve JavaScript ile modern ve kullanıcı dostu web siteleri tasarlamayı seviyorum.\n" +
          "Yeni teknolojiler öğrenmeye, projelerimle deneyim kazanmaya ve her gün bir adım daha ileri gitmeye çalışıyorum",
      profileImage: "https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=400&h=400&fit=crop&crop=face",
      about: "Front-End geliştirme alanında kendimi sürekli geliştiren bir Junior Developer'ım. HTML, CSS ve JavaScript teknolojilerini kullanarak modern ve responsive web arayüzleri oluşturuyorum. Amacım kullanıcı deneyimini ön planda tutan, sade ve etkileyici web siteleri tasarlamak.\n" +
          "Yeni teknolojileri öğrenmeyi, projeler üzerinden deneyim kazanmayı ve her geçen gün daha iyi işler ortaya koymayı hedefliyorum.",
      stats: [
        { value: "10+", label: "Tamamlanan Proje" },
        { value: "1+", label: "Yıl Deneyim" },
        { value: "10+", label: "Mutlu Müşteri" },
        { value: "24/7", label: "Destek" }
      ]
    })

    const experience = ref([
      {
        position: "Junior Front-End Developer",
        company: "Enrich",
        period: "2022 - 2023",
        description: "Modern ve kullanıcı dostu web arayüzleri geliştiriyorum. HTML, CSS ve JavaScript teknolojileriyle responsive tasarımlar oluşturuyor, React ve Tailwind CSS gibi araçlarla projelerimi güçlendiriyorum.\n" +
            "Kod yazarken temiz, düzenli ve ölçeklenebilir yapılar kurmaya özen gösteriyorum. Her proje benim için yeni bir öğrenme fırsatı.",
        skills: ["HTML", "CSS", "JavaScript", "React", "Vue.js", "Git"]
      },
      {
        position: "Web Developer",
        company: "Taksibul Kıbrıs",
        period: "2025 - Günümüz",
        description: "Kıbrıs genelinde taksi çağırma ve yönetim sistemini sağlayan web platformunun tam geliştirme sürecini üstlendim.\n" +
            "Vue.js kullanarak kullanıcı arayüzünü oluşturdum, PostgreSQL tabanlı veritabanı yapısını kurdum ve veri akışını yöneten API entegrasyonlarını gerçekleştirdim.\n" +
            "Kullanıcı giriş sistemi, yönetici paneli ve gerçek zamanlı konum güncelleme özelliklerini geliştirdim.\n" +
            "Proje boyunca performans, güvenlik ve kullanıcı deneyimi odaklı bir yaklaşım benimsedim.",
        skills: ["HTML", "CSS", "JavaScript", "PostgreSQL", "Vue.js", "Git", "REST API"]
      }
    ])

    const education = ref([
      {
        icon: "fas fa-graduation-cap",
        degree: "Bilgisayar Programcılığı",
        school: "Girne Üniversitesi",
        period: "2023 - Devam Ediyor",
        description: "Yazılım geliştirme, algoritma tasarımı ve veri yapıları konularında kapsamlı eğitim alıyorum."
      }
    ])

    const skills = ref({
      "Frontend Teknolojileri": [
        { name: "Vue.js", level: 60 },
        { name: "React", level: 65 },
        { name: "JavaScript", level: 60 },
        { name: "CSS3", level: 70 },
        { name: "HTML5", level: 80 }
      ],
      "Backend Teknolojileri": [
        { name: "Node.js", level: 40 },
        { name: "Python", level: 40 },
        { name: "MySQL", level: 45 }
      ],
      "Araçlar ve Platformlar": [
        { name: "Git", level: 80 },
        { name: "Webpack", level: 60 },
        { name: "VS Code", level: 90 }
      ]
    })

    const contactInfo = ref([
      {
        type: "E-posta",
        value: "turkissyy@gmail.com",
        icon: "fas fa-envelope"
      },
      {
        type: "Telefon",
        value: "+90 542 857 ** **",
        icon: "fas fa-phone"
      },
      {
        type: "Adres",
        value: "Girne, Kıbrıs",
        icon: "fas fa-map-marker-alt"
      },
      {
        type: "LinkedIn",
        value: "linkedin.com/in/yigitturkis",
        icon: "fab fa-linkedin"
      }
    ])

    const form = reactive({
      name: "",
      email: "",
      message: ""
    })

    const scrollToSection = (sectionId) => {
      const element = document.getElementById(sectionId)
      if (element) {
        element.scrollIntoView({ 
          behavior: 'smooth',
          block: 'start'
        })
      }
      menuOpen.value = false
    }

    const toggleMenu = () => {
      menuOpen.value = !menuOpen.value
    }

    const downloadCV = () => {
      alert('CV indirme özelliği yakında eklenecek!')
    }

    const submitForm = () => {
      if (form.name && form.email && form.message) {
        alert('Mesajınız başarıyla gönderildi! En kısa sürede size dönüş yapacağım.')
        form.name = ""
        form.email = ""
        form.message = ""
      } else {
        alert('Lütfen tüm alanları doldurun.')
      }
    }

    const animateSkillBars = () => {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            const skillBars = entry.target.querySelectorAll('.skill-progress')
            skillBars.forEach(bar => {
              const width = bar.style.width
              bar.style.width = '0%'
              setTimeout(() => {
                bar.style.width = width
              }, 100)
            })
          }
        })
      })
      
      const skillCategories = document.querySelectorAll('.skill-category')
      skillCategories.forEach(category => {
        observer.observe(category)
      })
    }

    const handleScroll = () => {
      const header = document.querySelector('.header')
      if (window.scrollY > 100) {
        header.style.background = 'rgba(255, 255, 255, 0.98)'
        header.style.boxShadow = '0 2px 20px rgba(0, 0, 0, 0.1)'
      } else {
        header.style.background = 'rgba(255, 255, 255, 0.95)'
        header.style.boxShadow = 'none'
      }
    }

    onMounted(() => {
      animateSkillBars()
      window.addEventListener('scroll', handleScroll)
    })

    return {
      menuOpen,
      personalInfo,
      experience,
      education,
      skills,
      contactInfo,
      form,
      scrollToSection,
      toggleMenu,
      downloadCV,
      submitForm
    }
  }
}
</script>

<style scoped>
/* Header Styles */
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  z-index: 1000;
  transition: all 0.3s ease;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.nav-brand h2 {
  color: #2563eb;
  font-weight: 700;
}

.nav-menu {
  display: flex;
  list-style: none;
  gap: 2rem;
}

.nav-menu a {
  text-decoration: none;
  color: #333;
  font-weight: 500;
  transition: color 0.3s ease;
  cursor: pointer;
}

.nav-menu a:hover {
  color: #2563eb;
}

.hamburger {
  display: none;
  flex-direction: column;
  cursor: pointer;
}

.hamburger span {
  width: 25px;
  height: 3px;
  background: #333;
  margin: 3px 0;
  transition: 0.3s;
}

/* Hero Section */
.hero {
  padding: 120px 0 80px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  min-height: 100vh;
  display: flex;
  align-items: center;
}

.hero-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.hero-title {
  font-size: 3.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  line-height: 1.2;
}

.highlight {
  color: #fbbf24;
}

.hero-subtitle {
  font-size: 1.5rem;
  font-weight: 500;
  margin-bottom: 1rem;
  color: #e5e7eb;
}

.hero-description {
  font-size: 1.1rem;
  margin-bottom: 2rem;
  color: #d1d5db;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
}

.profile-image {
  width: 300px;
  height: 300px;
  border-radius: 50%;
  overflow: hidden;
  border: 4px solid rgba(255, 255, 255, 0.2);
  margin: 0 auto;
}

.profile-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* About Section */
.about-content {
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
}

.about-text p {
  font-size: 1.1rem;
  margin-bottom: 2rem;
  color: #6b7280;
}

.stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.stat-item {
  text-align: center;
}

.stat-number {
  font-size: 2.5rem;
  font-weight: 700;
  color: #2563eb;
  margin-bottom: 0.5rem;
}

.stat-label {
  color: #6b7280;
  font-weight: 500;
}

/* Timeline Styles */
.timeline {
  position: relative;
  max-width: 800px;
  margin: 0 auto;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 50%;
  top: 0;
  bottom: 0;
  width: 2px;
  background: #e5e7eb;
  transform: translateX(-50%);
}

.timeline-item {
  position: relative;
  margin-bottom: 3rem;
  display: flex;
  align-items: center;
}

.timeline-item:nth-child(odd) .timeline-content {
  margin-right: auto;
  margin-left: 0;
  text-align: right;
  padding-right: 3rem;
}

.timeline-item:nth-child(even) .timeline-content {
  margin-left: auto;
  margin-right: 0;
  text-align: left;
  padding-left: 3rem;
}

.timeline-marker {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 16px;
  height: 16px;
  background: #2563eb;
  border-radius: 50%;
  border: 4px solid white;
  box-shadow: 0 0 0 4px #e5e7eb;
  z-index: 1;
}

.timeline-content {
  background: white;
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  width: 45%;
}

.job-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: #1f2937;
  margin-bottom: 0.5rem;
}

.company-name {
  color: #2563eb;
  font-weight: 500;
  margin-bottom: 0.5rem;
}

.job-period {
  color: #6b7280;
  font-size: 0.9rem;
  margin-bottom: 1rem;
}

.job-description {
  color: #4b5563;
  margin-bottom: 1rem;
}

.job-skills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.skill-tag {
  background: #e5e7eb;
  color: #374151;
  padding: 0.25rem 0.75rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
}

/* Education Grid */
.education-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  max-width: 1000px;
  margin: 0 auto;
}

.education-item {
  background: white;
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.education-icon {
  width: 60px;
  height: 60px;
  background: #2563eb;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 1.5rem;
  flex-shrink: 0;
}

.education-degree {
  font-size: 1.25rem;
  font-weight: 600;
  color: #1f2937;
  margin-bottom: 0.5rem;
}

.education-school {
  color: #2563eb;
  font-weight: 500;
  margin-bottom: 0.5rem;
}

.education-period {
  color: #6b7280;
  font-size: 0.9rem;
  margin-bottom: 1rem;
}

.education-description {
  color: #4b5563;
}

/* Skills Section */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  max-width: 1000px;
  margin: 0 auto;
}

.skill-category {
  background: white;
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.category-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: #1f2937;
  margin-bottom: 1.5rem;
  text-align: center;
}

.skill-item {
  margin-bottom: 1.5rem;
}

.skill-info {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
}

.skill-name {
  font-weight: 500;
  color: #374151;
}

.skill-level {
  color: #6b7280;
  font-size: 0.9rem;
}

.skill-bar {
  height: 8px;
  background: #e5e7eb;
  border-radius: 4px;
  overflow: hidden;
}

.skill-progress {
  height: 100%;
  background: linear-gradient(90deg, #2563eb, #3b82f6);
  border-radius: 4px;
  transition: width 1s ease;
}

/* Contact Section */
.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  max-width: 1000px;
  margin: 0 auto;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.contact-icon {
  width: 50px;
  height: 50px;
  background: #2563eb;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 1.2rem;
}

.contact-details h4 {
  font-weight: 600;
  color: #1f2937;
  margin-bottom: 0.25rem;
}

.contact-details p {
  color: #6b7280;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #e5e7eb;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #2563eb;
}

.form-group textarea {
  resize: vertical;
  min-height: 120px;
}

/* Responsive Design */
@media (max-width: 768px) {
  .hamburger {
    display: flex;
  }
  
  .nav-menu {
    position: fixed;
    top: 70px;
    left: -100%;
    width: 100%;
    height: calc(100vh - 70px);
    background: white;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    padding-top: 2rem;
    transition: left 0.3s ease;
  }
  
  .nav-menu.active {
    left: 0;
  }
  
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 2rem;
  }
  
  .hero-title {
    font-size: 2.5rem;
  }
  
  .hero-buttons {
    justify-content: center;
    flex-wrap: wrap;
  }
  
  .timeline::before {
    left: 20px;
  }
  
  .timeline-item:nth-child(odd) .timeline-content,
  .timeline-item:nth-child(even) .timeline-content {
    margin-left: 3rem;
    margin-right: 0;
    text-align: left;
    padding-left: 20px;
    padding-right: 20px;
    width: calc(100% - 3rem);
  }
  
  .timeline-marker {
    left: 20px;
  }
  
  .timeline-content {
    padding: 1.5rem;
    margin-left: 3rem;
    margin-right: 0;
    text-align: left;
    padding-left: 1.5rem;
    padding-right: 1.5rem;
    width: calc(100% - 3rem);
  }
  
  .contact-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .stats {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 2rem;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .stats {
    grid-template-columns: 1fr;
  }
  
  .hero-buttons {
    flex-direction: column;
    align-items: center;
  }
  
  .btn {
    width: 100%;
    max-width: 250px;
  }
}
</style>
