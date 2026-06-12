<template>
  <header class="navbar-header" :class="{ 'scrolled': isScrolled }">
    <div class="navbar-container">
      <router-link to="/" class="logo-link">
        <img src="../assets/logobebek.png" alt="Bebek Haji Slamet Logo" class="logo-img" />
      </router-link>

      <!-- Desktop Nav -->
      <nav class="nav-desktop">
        <router-link to="/" class="nav-link">Home</router-link>
        <router-link to="/menu" class="nav-link">Menu</router-link>
        <router-link to="/outlets" class="nav-link">Cabang</router-link>
        <router-link to="/about-contact" class="nav-link">Tentang & Kontak</router-link>
      </nav>

      <!-- Mobile Nav Toggle -->
      <button class="mobile-toggle" @click="toggleMobileMenu" aria-label="Toggle Menu">
        <span class="hamburger" :class="{ 'open': mobileMenuOpen }"></span>
      </button>
    </div>

    <!-- Mobile Drawer -->
    <transition name="drawer-fade">
      <div v-if="mobileMenuOpen" class="mobile-drawer" @click.self="closeMobileMenu">
        <nav class="mobile-nav">
          <router-link to="/" class="mobile-nav-link" @click="closeMobileMenu">Home</router-link>
          <router-link to="/menu" class="mobile-nav-link" @click="closeMobileMenu">Menu</router-link>
          <router-link to="/outlets" class="mobile-nav-link" @click="closeMobileMenu">Cabang</router-link>
          <router-link to="/about-contact" class="mobile-nav-link" @click="closeMobileMenu">Tentang & Kontak</router-link>
        </nav>
      </div>
    </transition>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const mobileMenuOpen = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 20
}

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
  if (mobileMenuOpen.value) {
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = ''
  }
}

const closeMobileMenu = () => {
  mobileMenuOpen.value = false
  document.body.style.overflow = ''
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.navbar-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  background-color: var(--primary);
  box-shadow: var(--shadow-sm);
  transition: all 0.3s ease;
  padding: 8px 0;
}

.navbar-header.scrolled {
  background-color: var(--primary);
  backdrop-filter: blur(10px);
  box-shadow: var(--shadow-md);
  padding: 4px 0;
}

.navbar-container {
  max-width: 1200px;
  margin: -12px auto;
  padding: 0 24px;
  display: flex;
  align-items: center;
  
}

.logo-link {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo-img {
  height: 80px;
  width: auto;
  object-fit: contain;
  transition: transform 0.3s ease;
  margin-left: -8vh;
}

.logo-link:hover .logo-img {
  transform: scale(1.05);
}

.brand-name {
  font-family: var(--heading);
  font-size: 1.5rem;
  font-weight: 700;
  color: #ffffff;
  letter-spacing: 0.5px;
}

.nav-desktop {
  display: flex;
  gap: 24px;
  margin-left: 340px;
}

.nav-link {
  color: rgba(255, 255, 255, 0.85);
  font-weight: 600;
  font-size: 0.95rem;
  padding: 8px 12px;
  border-radius: var(--radius-sm);
  position: relative;
}

.nav-link:hover {
  color: #ffffff;
}

/* Active State indicator */
.nav-link.router-link-active {
  color: #ffffff;
}

.nav-link.router-link-active::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 12px;
  right: 12px;
  height: 3px;
  background-color: var(--secondary);
  border-radius: var(--radius-full);
}

/* Mobile Toggle */
.mobile-toggle {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 10px;
  z-index: 1001;
}

.hamburger {
  display: block;
  width: 24px;
  height: 2px;
  background-color: #ffffff;
  position: relative;
  transition: background-color 0.3s;
}

.hamburger::before,
.hamburger::after {
  content: '';
  position: absolute;
  width: 24px;
  height: 2px;
  background-color: #ffffff;
  transition: transform 0.3s;
}

.hamburger::before {
  top: -6px;
}

.hamburger::after {
  top: 6px;
}

.hamburger.open {
  background-color: transparent;
}

.hamburger.open::before {
  transform: rotate(45deg);
  top: 0;
}

.hamburger.open::after {
  transform: rotate(-45deg);
  top: 0;
}

/* Mobile Drawer */
.mobile-drawer {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(4px);
  z-index: 999;
  display: flex;
  justify-content: flex-end;
}

.mobile-nav {
  background-color: var(--bg-card);
  width: 280px;
  height: 100%;
  padding: 100px 32px 32px;
  display: flex;
  flex-direction: column;
  gap: 20px;
  box-shadow: -10px 0 25px rgba(0,0,0,0.1);
}

.mobile-nav-link {
  color: var(--text-light);
  font-size: 1.15rem;
  font-weight: 600;
  padding: 10px 0;
  border-bottom: 1px solid var(--border);
}

.mobile-nav-link:hover,
.mobile-nav-link.router-link-active {
  color: var(--primary);
  border-bottom-color: var(--primary);
}

/* Transitions */
.drawer-fade-enter-active,
.drawer-fade-leave-active {
  transition: opacity 0.3s ease;
}

.drawer-fade-enter-active .mobile-nav,
.drawer-fade-leave-active .mobile-nav {
  transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.drawer-fade-enter-from {
  opacity: 0;
}

.drawer-fade-enter-from .mobile-nav {
  transform: translateX(100%);
}

.drawer-fade-leave-to {
  opacity: 0;
}

.drawer-fade-leave-to .mobile-nav {
  transform: translateX(100%);
}

@media (max-width: 768px) {
  .mobile-toggle {
    display: block;
  }

  .nav-desktop {
    display: none;
  }
}
</style>