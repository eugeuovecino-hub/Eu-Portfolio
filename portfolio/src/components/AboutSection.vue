<template>
  <section id="about">
    <div class="container">
      <div class="about-layout">
        <div class="about-left reveal">
          <div class="section-tag">About Me</div>
          <h2 class="section-heading">Building solutions that<br /><em style="font-style:italic; color: var(--color-accent)">actually matter.</em></h2>
          <p class="body-lg about-lead">
            I'm Eu Geuo — an IT graduate from the University of St. La Salle Bacolod who
            believes good software is less about code and more about understanding people.
          </p>
          <div class="about-paras">
            <p>
              Throughout college, I gravitated toward projects that solved tangible problems:
              inventory systems for local businesses, event platforms for student organizations,
              civic-tech tools for community services. That hands-on focus earned me the
              Most Outstanding IT Student distinction and Magna Cum Laude honors — but more
              importantly, it gave me the confidence to ship real things.
            </p>
            <p>
              Beyond coding, I led the LEAF organization and served as CCS Council Secretary,
              learning that the best tech solutions come from teams who communicate clearly
              and care about the people they build for. My faith anchors that perspective —
              <em>Soli Deo Gloria</em>, glory to God alone, in everything I do.
            </p>
            <p>
              I'm looking to join a team where I can grow as a developer, contribute to
              meaningful products, and keep building things that bridge technology and
              real human needs. Whether it's a startup with a bold idea or an established
              team with a hard problem — I'm ready.
            </p>
          </div>

          <div class="about-values">
            <div class="value-item" v-for="v in values" :key="v.label">
              <div class="value-icon" :style="{ background: v.bg }">{{ v.icon }}</div>
              <div>
                <div class="value-label">{{ v.label }}</div>
                <div class="value-desc">{{ v.desc }}</div>
              </div>
            </div>
          </div>
        </div>

        <div class="about-right reveal reveal-delay-2">
          <div class="about-card">
            <div class="about-photo-area">
              <div class="about-photo-placeholder">
                <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" opacity="0.25"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
                <span>Professional Photo</span>
              </div>
            </div>

            <div class="about-quick-facts">
              <div class="fact-item" v-for="f in facts" :key="f.label">
                <span class="fact-label">{{ f.label }}</span>
                <span class="fact-val">{{ f.value }}</span>
              </div>
            </div>
          </div>

          <div class="about-interests">
            <div class="interests-label">Interests &amp; Hobbies</div>
            <div class="interests-grid">
              <div class="interest-chip" v-for="i in interests" :key="i.label">
                {{ i.emoji }} {{ i.label }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const values = [
  { icon: '🔍', bg: '#eef2ff', label: 'Problem-First Thinking', desc: 'Understanding the "why" before touching code.' },
  { icon: '🤝', bg: '#f0fdf4', label: 'Collaborative by Default', desc: 'Best solutions come from teams, not lone developers.' },
  { icon: '📐', bg: '#fff7ed', label: 'Clean &amp; Purposeful Code', desc: 'Readable, maintainable, and intentional.' },
]

const facts = [
  { label: 'Location', value: 'Bacolod City, Philippines' },
  { label: 'Degree', value: 'B.S. Information Technology' },
  { label: 'University', value: 'Univ. of St. La Salle Bacolod' },
  { label: 'Graduation', value: 'Class of 2026' },
  { label: 'Honors', value: 'Magna Cum Laude' },
  { label: 'Status', value: 'Open to Opportunities' },
]

const interests = [
  { emoji: '⛪', label: 'Faith &amp; Community' },
  { emoji: '🎮', label: 'Gaming' },
  { emoji: '📚', label: 'Tech Reading' },
  { emoji: '🎵', label: 'Music' },
  { emoji: '🏀', label: 'Basketball' },
  { emoji: '☕', label: 'Coffee' },
  { emoji: '🌐', label: 'Open Source' },
  { emoji: '✈️', label: 'Travel' },
]
</script>

<style scoped>
.about-layout {
  display: grid;
  grid-template-columns: 1fr 360px;
  gap: 64px;
  align-items: start;
}
.about-lead {
  color: var(--color-text);
  margin-bottom: 24px;
  margin-top: 20px;
}
.about-paras {
  display: flex;
  flex-direction: column;
  gap: 16px;
  color: var(--color-text-muted);
  font-size: 0.9375rem;
  line-height: 1.75;
  margin-bottom: 36px;
  padding-bottom: 36px;
  border-bottom: 1px solid var(--color-border);
}
.about-values {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
.value-item {
  display: flex;
  gap: 14px;
  align-items: flex-start;
}
.value-icon {
  width: 40px;
  height: 40px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.125rem;
  flex-shrink: 0;
}
.value-label {
  font-weight: 600;
  font-size: 0.9375rem;
  margin-bottom: 2px;
}
.value-desc { font-size: 0.875rem; color: var(--color-text-muted); }

/* Right column */
.about-card {
  background: var(--color-surface);
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-lg);
  overflow: hidden;
  margin-bottom: 20px;
}
.about-photo-area {
  height: 200px;
  background: var(--color-surface-alt);
  display: flex;
  align-items: center;
  justify-content: center;
  border-bottom: 1px solid var(--color-border);
}
.about-photo-placeholder {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  color: var(--color-text-faint);
}
.about-photo-placeholder span { font-size: 0.8125rem; font-weight: 500; }

.about-quick-facts {
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.fact-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 0.875rem;
  padding-bottom: 10px;
  border-bottom: 1px solid var(--color-border);
}
.fact-item:last-child { border-bottom: none; padding-bottom: 0; }
.fact-label { color: var(--color-text-muted); font-weight: 400; }
.fact-val { font-weight: 600; color: var(--color-text); text-align: right; max-width: 180px; }

.about-interests {
  background: var(--color-surface);
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: 20px;
}
.interests-label {
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-text-faint);
  margin-bottom: 14px;
}
.interests-grid { display: flex; flex-wrap: wrap; gap: 8px; }
.interest-chip {
  padding: 6px 12px;
  background: var(--color-bg);
  border: 1px solid var(--color-border);
  border-radius: 100px;
  font-size: 0.8125rem;
  font-weight: 500;
  color: var(--color-text-muted);
}

@media (max-width: 900px) {
  .about-layout { grid-template-columns: 1fr; gap: 40px; }
}
</style>
