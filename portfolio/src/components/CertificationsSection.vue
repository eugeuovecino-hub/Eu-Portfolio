<template>
  <section id="certifications" class="certs-section">
    <div class="container">
      <div class="section-head reveal">
        <div class="section-tag">Credentials</div>
        <h2 class="section-heading">Certifications</h2>
        <p class="section-sub">Industry-recognized credentials demonstrating technical expertise and continuous learning.</p>
      </div>

      <div class="certs-grid">
        <div
          v-for="(cert, idx) in certifications"
          :key="cert.id"
          :class="['cert-card', 'reveal', `reveal-delay-${(idx % 4) + 1}`]"
        >
          <div class="cert-logo-wrap" :style="{ background: cert.logoBg }">
            <div class="cert-logo-text" :style="{ color: cert.logoColor }">{{ cert.logoText }}</div>
          </div>
          <div class="cert-body">
            <div class="cert-issuer">{{ cert.issuer }}</div>
            <h3 class="cert-name">{{ cert.name }}</h3>
            <p class="cert-date">
              <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg>
              {{ cert.date }}
            </p>
            <div class="cert-badge" :style="{ background: cert.badgeBg, color: cert.badgeColor }">
              {{ cert.status }}
            </div>
          </div>
          <a v-if="cert.link" :href="cert.link" target="_blank" class="cert-verify-btn">
            Verify
            <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const certifications = [
  {
    id: 1,
    issuer: 'Cisco Networking Academy',
    name: 'Introduction to Cybersecurity',
    date: '2024',
    logoText: 'CISCO',
    logoBg: '#e8f4fd',
    logoColor: '#0070d2',
    badgeBg: '#eef2ff',
    badgeColor: '#1a5cff',
    status: '✓ Verified',
    link: '#'
  },
  {
    id: 2,
    issuer: 'Cisco Networking Academy',
    name: 'Networking Basics',
    date: '2024',
    logoText: 'CISCO',
    logoBg: '#e8f4fd',
    logoColor: '#0070d2',
    badgeBg: '#eef2ff',
    badgeColor: '#1a5cff',
    status: '✓ Verified',
    link: '#'
  },
  {
    id: 3,
    issuer: 'TESDA',
    name: 'Computer Systems Servicing NC II',
    date: '2023',
    logoText: 'TESDA',
    logoBg: '#fff7ed',
    logoColor: '#c2410c',
    badgeBg: '#f0fdf4',
    badgeColor: '#16a34a',
    status: '✓ Certified',
    link: '#'
  },
  {
    id: 4,
    issuer: 'Google',
    name: 'Foundations of Cybersecurity',
    date: '2024',
    logoText: 'Google',
    logoBg: '#fef9ee',
    logoColor: '#4285f4',
    badgeBg: '#eef2ff',
    badgeColor: '#1a5cff',
    status: '✓ Verified',
    link: '#'
  },
  {
    id: 5,
    issuer: 'Google',
    name: 'Google IT Support Fundamentals',
    date: '2023',
    logoText: 'Google',
    logoBg: '#fef9ee',
    logoColor: '#ea4335',
    badgeBg: '#eef2ff',
    badgeColor: '#1a5cff',
    status: '✓ Verified',
    link: '#'
  },
  {
    id: 6,
    issuer: 'Microsoft',
    name: 'Azure Fundamentals (AZ-900)',
    date: '2025',
    logoText: 'MSFT',
    logoBg: '#eff6ff',
    logoColor: '#0078d4',
    badgeBg: '#f0fdf4',
    badgeColor: '#16a34a',
    status: '✓ Certified',
    link: '#'
  },
  {
    id: 7,
    issuer: 'freeCodeCamp',
    name: 'Responsive Web Design',
    date: '2023',
    logoText: 'fCC',
    logoBg: '#f0fff4',
    logoColor: '#0a3a2a',
    badgeBg: '#eef2ff',
    badgeColor: '#1a5cff',
    status: '✓ Verified',
    link: '#'
  },
  {
    id: 8,
    issuer: 'University of St. La Salle',
    name: 'Most Outstanding IT Student',
    date: '2026',
    logoText: 'USLS',
    logoBg: '#fff4e6',
    logoColor: '#b45309',
    badgeBg: '#fffbeb',
    badgeColor: '#b45309',
    status: '★ Award',
    link: null
  },
]
</script>

<style scoped>
.certs-section { background: var(--color-surface-alt); }
.section-head { max-width: 560px; margin-bottom: 56px; }

.certs-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 18px;
}

.cert-card {
  background: var(--color-surface);
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  transition: transform 0.2s, box-shadow 0.2s;
  position: relative;
}
.cert-card:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-md);
}

.cert-logo-wrap {
  width: 52px;
  height: 52px;
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.cert-logo-text {
  font-family: var(--font-display);
  font-weight: 800;
  font-size: 0.75rem;
  letter-spacing: 0.05em;
}
.cert-body { flex: 1; }
.cert-issuer {
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--color-text-faint);
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: 6px;
}
.cert-name {
  font-family: var(--font-display);
  font-size: 1rem;
  font-weight: 700;
  line-height: 1.35;
  margin-bottom: 8px;
}
.cert-date {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 0.8125rem;
  color: var(--color-text-muted);
  margin-bottom: 12px;
}
.cert-badge {
  display: inline-flex;
  align-items: center;
  padding: 3px 10px;
  border-radius: 100px;
  font-size: 0.75rem;
  font-weight: 600;
}
.cert-verify-btn {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 0.8125rem;
  font-weight: 500;
  color: var(--color-accent);
  padding-top: 14px;
  border-top: 1px solid var(--color-border);
  transition: opacity 0.15s;
}
.cert-verify-btn:hover { opacity: 0.7; }
</style>
