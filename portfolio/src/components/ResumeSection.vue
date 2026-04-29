<template>
  <section id="resume" class="resume-section">
    <div class="container">
      <div class="resume-layout">
        <div class="resume-text reveal">
          <div class="section-tag">Resume</div>
          <h2 class="section-heading">Curriculum Vitae</h2>
          <p class="section-sub" style="margin-bottom: 32px;">
            A comprehensive view of my academic background, technical skills, project experience, and achievements.
          </p>

          <div class="resume-highlights">
            <div class="rh-item" v-for="h in highlights" :key="h.label">
              <div class="rh-icon" :style="{ background: h.bg }">
                <span v-html="h.icon"></span>
              </div>
              <div>
                <div class="rh-label">{{ h.label }}</div>
                <div class="rh-val">{{ h.value }}</div>
              </div>
            </div>
          </div>

          <div class="resume-actions">
            <a href="/resume.pdf" download class="btn btn-primary">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
              Download PDF Resume
            </a>
            <a href="/resume.pdf" target="_blank" class="btn btn-outline">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/><circle cx="12" cy="12" r="3"/></svg>
              Preview Online
            </a>
          </div>

          <p class="resume-note">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="12"/><line x1="12" y1="16" x2="12.01" y2="16"/></svg>
            Last updated: April 2026 · PDF, A4 format
          </p>
        </div>

        <div class="resume-preview reveal reveal-delay-2">
          <div class="cv-mockup">
            <div class="cv-header-strip"></div>
            <div class="cv-body">
              <div class="cv-name-block">
                <div class="cv-line cv-line-name"></div>
                <div class="cv-line cv-line-role"></div>
              </div>
              <div class="cv-section-group" v-for="n in 3" :key="n">
                <div class="cv-section-title"></div>
                <div class="cv-line" v-for="i in 3" :key="i" :style="{ width: `${70 + Math.random() * 25}%` }"></div>
              </div>
            </div>
            <div class="cv-download-overlay">
              <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="1.5"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
              <span>Click to Download</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const highlights = [
  {
    label: 'Academic Standing',
    value: 'Magna Cum Laude — Class of 2026',
    bg: '#fffbeb',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#b45309" stroke-width="2"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>`
  },
  {
    label: 'Key Achievement',
    value: 'Most Outstanding IT Student Award',
    bg: '#eef2ff',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#1a5cff" stroke-width="2"><circle cx="12" cy="8" r="6"/><path d="M15.477 12.89L17 22l-5-3-5 3 1.523-9.11"/></svg>`
  },
  {
    label: 'Experience',
    value: '500+ hours OJT + Freelance projects',
    bg: '#f0fdf4',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#16a34a" stroke-width="2"><rect x="2" y="7" width="20" height="14" rx="2"/><path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"/></svg>`
  },
  {
    label: 'Certifications',
    value: '7+ industry credentials earned',
    bg: '#fdf4ff',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#9333ea" stroke-width="2"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg>`
  },
]
</script>

<style scoped>
.resume-section { background: var(--color-bg); }
.resume-layout {
  display: grid;
  grid-template-columns: 1fr 340px;
  gap: 64px;
  align-items: center;
}

.resume-highlights {
  display: flex;
  flex-direction: column;
  gap: 14px;
  margin-bottom: 36px;
  padding-bottom: 36px;
  border-bottom: 1px solid var(--color-border);
}
.rh-item {
  display: flex;
  align-items: center;
  gap: 14px;
}
.rh-icon {
  width: 42px;
  height: 42px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.rh-label { font-size: 0.75rem; font-weight: 600; text-transform: uppercase; letter-spacing: 0.08em; color: var(--color-text-faint); margin-bottom: 2px; }
.rh-val { font-size: 0.9375rem; font-weight: 500; color: var(--color-text); }

.resume-actions { display: flex; gap: 12px; flex-wrap: wrap; margin-bottom: 20px; }

.resume-note {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 0.8125rem;
  color: var(--color-text-faint);
}

/* CV Mockup */
.cv-mockup {
  background: var(--color-surface);
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-md);
  position: relative;
  transition: transform 0.25s, box-shadow 0.25s;
  cursor: pointer;
}
.cv-mockup:hover {
  transform: translateY(-4px) scale(1.01);
  box-shadow: var(--shadow-hover);
}
.cv-mockup:hover .cv-download-overlay { opacity: 1; }

.cv-header-strip {
  height: 72px;
  background: linear-gradient(135deg, #1a2f6f 0%, #1a5cff 100%);
}
.cv-body {
  padding: 20px 24px;
  display: flex;
  flex-direction: column;
  gap: 18px;
}
.cv-name-block { display: flex; flex-direction: column; gap: 6px; }
.cv-line {
  height: 7px;
  background: var(--color-border);
  border-radius: 4px;
}
.cv-line-name { width: 55%; height: 12px; }
.cv-line-role { width: 38%; }
.cv-section-group { display: flex; flex-direction: column; gap: 7px; padding-top: 14px; border-top: 1px solid var(--color-border); }
.cv-section-title { height: 8px; width: 28%; background: #c0bdb8; border-radius: 4px; margin-bottom: 2px; }

.cv-download-overlay {
  position: absolute;
  inset: 0;
  background: rgba(26,47,111,0.75);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  opacity: 0;
  transition: opacity 0.25s;
  color: white;
  font-size: 0.875rem;
  font-weight: 600;
  letter-spacing: 0.04em;
}

@media (max-width: 900px) {
  .resume-layout { grid-template-columns: 1fr; gap: 40px; }
  .resume-preview { display: none; }
}
</style>
