<template>
  <footer class="footer">
    <div class="container footer-inner">
      <div class="footer-brand">
        <div class="logo-initials-sm">EV</div>
        <div>
          <div class="footer-name">Eu Geuo B. Vecino</div>
          <div class="footer-tagline">Web &amp; Mobile Developer | Bacolod City, PH</div>
        </div>
      </div>

      <nav class="footer-nav">
        <a v-for="item in footerLinks" :key="item.id" :href="`#${item.id}`" @click.prevent="scrollTo(item.id)" class="footer-link">
          {{ item.label }}
        </a>
      </nav>

      <div class="footer-social">
        <a href="https://github.com/eugeuovecino-hub" target="_blank" class="social-btn" aria-label="GitHub">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/></svg>
        </a>
        <a href="https://www.linkedin.com/in/eu-geuo-vecino-a64a83406/" target="_blank" class="social-btn" aria-label="LinkedIn">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/><rect x="2" y="9" width="4" height="12"/><circle cx="4" cy="4" r="2"/></svg>
        </a>
        <a href="mailto:eugeuovec.professional@gmail.com" class="social-btn" aria-label="Email">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
        </a>
      </div>
    </div>

    <div class="footer-bottom">
      <div class="container">
        <p>Copyright {{ new Date().getFullYear() }} Eu Geuo B. Vecino | Built with Vue 3 | <em>Soli Deo Gloria</em></p>
      </div>
    </div>
  </footer>
</template>

<script setup>
const footerLinks = [
  { id: 'home', label: 'Home' },
  { id: 'projects', label: 'Projects' },
  { id: 'skills', label: 'Skills' },
  { id: 'experience', label: 'Experience' },
  { id: 'resume', label: 'Resume' },
  { id: 'contact', label: 'Contact' },
]

const scrollTo = (id) => {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}
</script>

<style scoped>
.footer {
  background: var(--color-text);
  color: var(--color-bg);
}
.footer-inner {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
  padding-top: 40px;
  padding-bottom: 40px;
}
.footer-brand { display: flex; align-items: center; gap: 12px; }
.logo-initials-sm {
  width: 36px;
  height: 36px;
  background: rgba(255, 255, 255, 0.12);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-display);
  font-weight: 700;
  font-size: 0.875rem;
  color: white;
}
.footer-name { font-weight: 600; font-size: 0.9375rem; }
.footer-tagline { font-size: 0.8125rem; opacity: 0.5; }

.footer-nav {
  display: flex;
  flex-wrap: wrap;
  gap: 4px;
}
.footer-link {
  padding: 5px 12px;
  border-radius: 100px;
  font-size: 0.8125rem;
  color: rgba(255, 255, 255, 0.6);
  transition: color 0.15s, background 0.15s;
}
.footer-link:hover { color: white; background: rgba(255, 255, 255, 0.08); }

.footer-social { display: flex; gap: 8px; }
.social-btn {
  width: 36px;
  height: 36px;
  border-radius: 10px;
  background: rgba(255, 255, 255, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  color: rgba(255, 255, 255, 0.7);
  transition: background 0.15s, color 0.15s;
}
.social-btn:hover { background: rgba(255, 255, 255, 0.2); color: white; }

.footer-bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding: 16px 0;
}
.footer-bottom p {
  font-size: 0.8125rem;
  color: rgba(255, 255, 255, 0.4);
  text-align: center;
}
.footer-bottom em { font-style: italic; color: rgba(255, 255, 255, 0.5); }

@media (max-width: 768px) {
  .footer-inner { flex-direction: column; align-items: flex-start; }
  .footer-nav { display: none; }
}
</style>
