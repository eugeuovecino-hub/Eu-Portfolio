<template>
  <section class="hero" id="home">
    <div class="container hero-container">
      <div class="hero-content">
        <div class="hero-badge reveal">
          <span class="badge-dot"></span>
          Available for opportunities
        </div>

        <h1 class="hero-name display-xl reveal reveal-delay-1">
          Eu Geuo<br />
          <em>B. Vecino</em>
        </h1>

        <p class="hero-role reveal reveal-delay-2">
          Web &amp; Mobile Developer
        </p>

        <p class="hero-intro body-lg reveal reveal-delay-3">
          Recent IT graduate from the University of St. La Salle Bacolod, specializing
          in web development and practical software solutions. I craft responsive,
          purposeful applications that bridge real-world problems with clean technology.
        </p>

        <div class="hero-actions reveal reveal-delay-4">
          <a href="#projects" class="btn btn-primary" @click.prevent="scrollTo('projects')">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/></svg>
            View Projects
          </a>
          <a href="#resume" class="btn btn-outline" @click.prevent="scrollTo('resume')">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
            Download Resume
          </a>
          <a href="#contact" class="btn btn-outline" @click.prevent="scrollTo('contact')">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
            Contact Me
          </a>
        </div>
      </div>

      <div class="hero-visual reveal reveal-delay-2">
        <div class="photo-frame">
          <div class="photo-placeholder">
            <img :src="heroPhoto" alt="Portrait of Eu Geuo B. Vecino" class="photo-image" />
          </div>
        </div>

        <div class="tech-orbit">
          <span class="orbit-tag" v-for="tech in orbitTechs" :key="tech">{{ tech }}</span>
        </div>
      </div>
    </div>

    <div class="hero-scroll-hint">
      <div class="scroll-line"></div>
      <span>Scroll</span>
    </div>
  </section>
</template>

<script setup>
import heroPhoto from '../assets/eu-photo.JPG'

const orbitTechs = ['Vue.js', 'Laravel', 'React', 'Node.js', 'MySQL', 'Firebase']

const scrollTo = (id) => {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}
</script>

<style scoped>
.hero {
  padding-top: 120px;
  padding-bottom: 80px;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  background: var(--color-bg);
  position: relative;
  overflow: hidden;
}
.hero::before {
  content: '';
  position: absolute;
  top: -200px;
  right: -100px;
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, rgba(26,92,255,0.06) 0%, transparent 65%);
  pointer-events: none;
}
.hero-container {
  display: grid;
  grid-template-columns: 1fr 420px;
  gap: 64px;
  align-items: center;
}

/* LEFT */
.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 6px 14px;
  background: #edfaf3;
  border: 1px solid #c6f0d8;
  border-radius: 100px;
  font-size: 0.8125rem;
  font-weight: 500;
  color: #1a7a46;
  margin-bottom: 28px;
}
.badge-dot {
  width: 7px;
  height: 7px;
  background: #2ecc71;
  border-radius: 50%;
  animation: pulse 2s ease-in-out infinite;
}
@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.6; transform: scale(0.85); }
}

.hero-name {
  color: var(--color-text);
  margin-bottom: 16px;
}
.hero-name em {
  font-style: italic;
  color: var(--color-accent);
  font-weight: 300;
}

.hero-role {
  font-family: var(--font-body);
  font-size: 1.125rem;
  font-weight: 500;
  color: var(--color-text-muted);
  letter-spacing: 0.04em;
  text-transform: uppercase;
  margin-bottom: 24px;
}

.hero-intro {
  color: var(--color-text-muted);
  max-width: 520px;
  margin-bottom: 40px;
}

.hero-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-bottom: 48px;
}

/* RIGHT - Visual */
.hero-visual {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 28px;
}

.photo-frame {
  position: relative;
  width: 320px;
}

.photo-placeholder {
  width: 320px;
  height: 360px;
  border-radius: var(--radius-xl);
  background: var(--color-surface-alt);
  border: 1.5px solid var(--color-border);
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  position: relative;
}
.photo-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 46% 14%;
  display: block;
  transform: scale(1.16);
}

.tech-orbit {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  justify-content: center;
}
.orbit-tag {
  padding: 6px 14px;
  background: var(--color-surface);
  border: 1.5px solid var(--color-border);
  border-radius: 100px;
  font-size: 0.8125rem;
  font-weight: 500;
  color: var(--color-text-muted);
  transition: border-color 0.2s, color 0.2s;
}
.orbit-tag:hover {
  border-color: var(--color-accent);
  color: var(--color-accent);
}

.hero-scroll-hint {
  position: absolute;
  bottom: 32px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  opacity: 0.4;
}
.scroll-line {
  width: 1px;
  height: 36px;
  background: var(--color-text);
  animation: scrollDown 2s ease-in-out infinite;
  transform-origin: top;
}
@keyframes scrollDown {
  0% { transform: scaleY(0); opacity: 0; }
  40% { transform: scaleY(1); opacity: 1; }
  100% { transform: scaleY(1); opacity: 0; }
}
.hero-scroll-hint span {
  font-size: 0.6875rem;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}

@media (max-width: 960px) {
  .hero-container {
    grid-template-columns: 1fr;
    gap: 48px;
  }
  .hero-visual {
    display: none;
  }
}
@media (max-width: 600px) {
  .hero { padding-top: 100px; }
  .hero-actions { flex-direction: column; }
  .hero-actions .btn { justify-content: center; }
}
</style>
