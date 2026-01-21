<template>
  <div class="app">
    <header class="navbar">
      <div class="navbar-container">
        <router-link to="/" class="navbar-brand">
          <span class="brand-name">个人博客</span>
        </router-link>
        <nav class="navbar-nav">
          <router-link to="/" class="nav-link">首页</router-link>
          <router-link to="/blog" class="nav-link">博客</router-link>
          <router-link to="/about" class="nav-link">关于我</router-link>
          <button class="theme-toggle" @click="toggleTheme">
            <Sun v-if="isDarkMode" />
            <Moon v-else />
          </button>
        </nav>
      </div>
    </header>

    <main class="main-content">
      <router-view v-slot="{ Component }">
        <transition name="fade" mode="out-in">
          <component :is="Component" />
        </transition>
      </router-view>
    </main>

    <footer class="footer">
      <div class="footer-container">
        <p>&copy; {{ new Date().getFullYear() }} 个人博客. 保留所有权利.</p>
        <div class="footer-links">
          <router-link to="/" class="footer-link">首页</router-link>
          <router-link to="/blog" class="footer-link">博客</router-link>
          <router-link to="/about" class="footer-link">关于我</router-link>
        </div>
        <div class="footer-tech">
          <span class="tech-badge">Vue 3</span>
          <span class="tech-badge">Vite</span>
          <span class="tech-badge">GitHub Pages</span>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Sun, Moon } from 'lucide-vue-next'

const isDarkMode = ref(false)

const toggleTheme = () => {
  isDarkMode.value = !isDarkMode.value
  if (isDarkMode.value) {
    document.documentElement.classList.add('dark')
  } else {
    document.documentElement.classList.remove('dark')
  }
  localStorage.setItem('darkMode', isDarkMode.value)
}

onMounted(() => {
  const savedMode = localStorage.getItem('darkMode')
  if (savedMode !== null) {
    isDarkMode.value = savedMode === 'true'
  } else {
    isDarkMode.value = window.matchMedia('(prefers-color-scheme: dark)').matches
  }
  if (isDarkMode.value) {
    document.documentElement.classList.add('dark')
  }
})
</script>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background: var(--bg-light);
  color: var(--text-dark);
  transition: all 0.3s ease;
}

.navbar {
  background: var(--bg-card);
  box-shadow: var(--shadow-sm);
  position: sticky;
  top: 0;
  z-index: 100;
  border-bottom: 1px solid var(--border-color);
}

.navbar-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.navbar-brand {
  text-decoration: none;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.brand-name {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--primary);
  transition: all 0.3s ease;
}

.brand-name:hover {
  color: var(--primary-dark);
  text-shadow: 0 0 10px rgba(59, 130, 246, 0.3);
}

.navbar-nav {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.nav-link {
  text-decoration: none;
  color: var(--text-dark);
  font-weight: 500;
  transition: all 0.3s ease;
  position: relative;
  padding: 0.5rem 0;
}

.nav-link:hover {
  color: var(--primary);
}

.nav-link.router-link-active {
  color: var(--primary);
}

.nav-link.router-link-active::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 2px;
  background: var(--primary);
  border-radius: 2px;
  animation: scan 2s linear infinite;
}

.theme-toggle {
  background: none;
  border: 1px solid var(--border-color);
  color: var(--text-dark);
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
}

.theme-toggle:hover {
  background: var(--primary-light);
  border-color: var(--primary);
  transform: rotate(180deg);
}

.main-content {
  flex: 1;
  animation: fadeIn 0.5s ease-in-out;
}

.footer {
  background: var(--bg-card);
  color: var(--text-dark);
  padding: 3rem 2rem 1rem;
  margin-top: auto;
  border-top: 1px solid var(--border-color);
  transition: all 0.3s ease;
}

.footer-container {
  max-width: 1200px;
  margin: 0 auto;
  text-align: center;
}

.footer-links {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin: 1rem 0 2rem;
}

.footer-link {
  color: var(--text-muted);
  text-decoration: none;
  transition: all 0.3s ease;
}

.footer-link:hover {
  color: var(--primary);
}

.footer-tech {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-top: 2rem;
}

.tech-badge {
  font-size: 0.8rem;
  padding: 0.3rem 0.8rem;
  background: var(--primary-light);
  color: var(--primary);
  border-radius: 20px;
  font-weight: 500;
  border: 1px solid var(--border-color);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 768px) {
  .navbar-container {
    padding: 1rem;
  }

  .navbar-nav {
    gap: 1rem;
  }

  .footer {
    padding: 2rem 1rem 1rem;
  }

  .footer-links {
    gap: 1rem;
  }

  .footer-tech {
    flex-wrap: wrap;
  }
}
</style>