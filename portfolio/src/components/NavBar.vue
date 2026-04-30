<template>
  <header :class="['navbar', { scrolled: isScrolled }]">
    <div class="nav-inner container">
      <a href="#home" class="nav-logo" @click.prevent="scrollTo('home')">
        <span class="logo-initials">EV</span>
        <span class="logo-name">Eu Geuo Vecino</span>
      </a>

      <nav class="nav-links" :class="{ open: menuOpen }">
        <a
          v-for="item in navItems"
          :key="item.id"
          :href="`#${item.id}`"
          :class="['nav-link', { active: activeSection === item.id }]"
          @click.prevent="() => { scrollTo(item.id); menuOpen = false }"
        >{{ item.label }}</a>
        <a href="#contact" class="btn btn-primary btn-sm nav-cta" @click.prevent="() => { scrollTo('contact'); menuOpen = false }">
          Hire Me
        </a>
      </nav>

      <button class="hamburger" @click="menuOpen = !menuOpen" :aria-label="menuOpen ? 'Close menu' : 'Open menu'">
        <span :class="{ active: menuOpen }"></span>
        <span :class="{ active: menuOpen }"></span>
        <span :class="{ active: menuOpen }"></span>
      </button>
    </div>
  </header>

  <div class="nav-backdrop" v-if="menuOpen" @click="menuOpen = false" />
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({ activeSection: String })

const isScrolled = ref(false)
const menuOpen = ref(false)

const navItems = [
  { id: 'home', label: 'Home' },
  { id: 'skills', label: 'Skills' },
  { id: 'projects', label: 'Projects' },
  { id: 'experience', label: 'Experience' },
  { id: 'resume', label: 'Resume' },
  { id: 'contact', label: 'Contact' },
]

const scrollTo = (id) => {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

const handleScroll = () => { isScrolled.value = window.scrollY > 20 }
onMounted(() => window.addEventListener('scroll', handleScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  transition: background 0.3s ease, box-shadow 0.3s ease, backdrop-filter 0.3s ease;
  background: transparent;
}
.navbar.scrolled {
  background: rgba(250, 250, 248, 0.88);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  box-shadow: 0 1px 0 var(--color-border);
}
.nav-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 68px;
}
.nav-logo {
  display: flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
}
.logo-initials {
  width: 36px;
  height: 36px;
  background: var(--color-text);
  color: var(--color-bg);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-display);
  font-weight: 700;
  font-size: 0.9rem;
  letter-spacing: 0.05em;
}
.logo-name {
  font-family: var(--font-body);
  font-weight: 500;
  font-size: 0.9375rem;
  color: var(--color-text);
}
.nav-links {
  display: flex;
  align-items: center;
  gap: 4px;
}
.nav-link {
  padding: 6px 14px;
  border-radius: 100px;
  font-size: 0.875rem;
  font-weight: 450;
  color: var(--color-text-muted);
  transition: color 0.15s, background 0.15s;
}
.nav-link:hover {
  color: var(--color-text);
  background: var(--color-surface-alt);
}
.nav-link.active {
  color: var(--color-text);
  font-weight: 500;
}
.nav-cta { margin-left: 8px; }

.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  padding: 4px;
  background: none;
  border: none;
  cursor: pointer;
}
.hamburger span {
  display: block;
  width: 22px;
  height: 2px;
  background: var(--color-text);
  border-radius: 2px;
  transition: transform 0.25s ease, opacity 0.25s ease;
  transform-origin: center;
}
.hamburger span:nth-child(1).active { transform: translateY(7px) rotate(45deg); }
.hamburger span:nth-child(2).active { opacity: 0; }
.hamburger span:nth-child(3).active { transform: translateY(-7px) rotate(-45deg); }

.nav-backdrop {
  display: none;
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.2);
  z-index: 999;
}

@media (max-width: 840px) {
  .hamburger { display: flex; z-index: 1001; }
  .nav-backdrop { display: block; }
  .nav-links {
    position: fixed;
    top: 0;
    right: -280px;
    width: 260px;
    height: 100vh;
    background: var(--color-surface);
    flex-direction: column;
    align-items: flex-start;
    padding: 90px 24px 32px;
    gap: 4px;
    box-shadow: var(--shadow-lg);
    transition: right 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
    z-index: 1000;
  }
  .nav-links.open { right: 0; }
  .nav-link { width: 100%; padding: 10px 16px; font-size: 1rem; border-radius: var(--radius-md); }
  .nav-cta { margin-left: 0; margin-top: 16px; }
}
</style>
