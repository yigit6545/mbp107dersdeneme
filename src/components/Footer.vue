<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <p>&copy; 2024 {{ personalInfo.name }}. Tüm hakları saklıdır.</p>
        <div class="social-links">
          <a :href="social.url" v-for="social in socialLinks" :key="social.name" :title="social.name">
            <i :class="social.icon"></i>
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  setup() {
    const personalInfo = {
      name: "Yiğit Türkiş"
    }

    const socialLinks = [
      {
        name: "GitHub",
        url: "https://github.com/turkissyy",
        icon: "fab fa-github"
      },
      {
        name: "LinkedIn",
        url: "https://linkedin.com",
        icon: "fab fa-linkedin"
      },
      {
        name: "Twitter",
        url: "https://twitter.com",
        icon: "fab fa-twitter"
      },
      {
        name: "Instagram",
        url: "https://instagram.com/turkissyy",
        icon: "fab fa-instagram"
      }
    ]

    return {
      personalInfo,
      socialLinks
    }
  }
}
</script>

<style scoped>
.footer {
  background: #1f2937;
  color: white;
  padding: 2rem 0;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-links a {
  width: 40px;
  height: 40px;
  background: #374151;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  text-decoration: none;
  transition: all 0.3s ease;
}

.social-links a:hover {
  background: #2563eb;
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    gap: 1rem;
    text-align: center;
  }
}
</style>
