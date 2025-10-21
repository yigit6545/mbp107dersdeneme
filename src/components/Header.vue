<template>
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
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'Header',
  setup() {
    const menuOpen = ref(false)
    
    const personalInfo = {
      name: "Yiğit Türkiş"
    }

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

    return {
      menuOpen,
      personalInfo,
      scrollToSection,
      toggleMenu
    }
  }
}
</script>

<style scoped>
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
}
</style>
