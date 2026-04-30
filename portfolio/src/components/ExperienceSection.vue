<template>
  <section id="experience">
    <div class="container">
      <div class="section-head reveal">
        
        <h2 class="section-heading">Experience &amp; Involvement</h2>
        <p class="section-sub">From on-the-job training to student leadership, a record of growth beyond the classroom.</p>
      </div>

      <div class="exp-layout">
        <div class="exp-timeline">
          <div
            v-for="(item, idx) in experiences"
            :key="idx"
            :class="['exp-item', 'reveal', `reveal-delay-${(idx % 3) + 1}`, { active: activeIdx === idx }]"
            @click="activeIdx = idx"
          >
            <div class="exp-dot" :style="{ background: item.color }"></div>
            <div class="exp-item-content">
              <div class="exp-type-tag" :style="{ background: item.tagBg, color: item.tagColor }">{{ item.type }}</div>
              <h3 class="exp-title">{{ item.role }}</h3>
              <p class="exp-org">{{ item.org }}</p>
              <p class="exp-date">{{ item.date }}</p>
            </div>
            <svg class="exp-chevron" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="9 18 15 12 9 6"/></svg>
          </div>
        </div>

        <div class="exp-detail reveal reveal-delay-2" v-if="selected">
          <div class="exp-detail-header">
            <div class="exp-detail-icon" :style="{ background: selected.iconBg }">
              <span v-html="selected.icon"></span>
            </div>
            <div>
              <h3 class="exp-detail-role">{{ selected.role }}</h3>
              <p class="exp-detail-org">{{ selected.org }}</p>
              <p class="exp-detail-date">{{ selected.date }}</p>
            </div>
          </div>

          <p class="exp-detail-desc">{{ selected.description }}</p>

          <div class="exp-highlights">
            <div class="highlight-item" v-for="highlight in selected.highlights" :key="highlight">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="var(--color-accent)" stroke-width="2.5"><polyline points="20 6 9 17 4 12"/></svg>
              <span>{{ highlight }}</span>
            </div>
          </div>

          <div class="exp-skills-used" v-if="selected.skills">
            <div class="detail-skills-label">Skills applied</div>
            <div class="detail-skills-list">
              <span v-for="skill in selected.skills" :key="skill" class="tech-tag">{{ skill }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

const activeIdx = ref(0)

const experiences = [
  {
    type: 'Venture',
    role: 'Co-Founder / AI Automation Builder',
    org: 'PhaseOps AI',
    date: 'Present',
    color: '#14b8a6',
    tagBg: '#ecfeff',
    tagColor: '#0f766e',
    iconBg: '#ecfeff',
    icon: `<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#14b8a6" stroke-width="2"><path d="M12 3l1.9 3.86L18 9l-4.1 2.14L12 15l-1.9-3.86L6 9l4.1-2.14L12 3z"/><path d="M5 16l.95 1.95L8 19l-2.05 1.05L5 22l-.95-1.95L2 19l2.05-1.05L5 16z"/><path d="M19 14l1.2 2.4L22.6 17l-2.4 1.2L19 20.6l-1.2-2.4L15.4 17l2.4-1.2L19 14z"/></svg>`,
    description: 'Co-founded PhaseOps AI, an AI automation agency focused on building practical systems that reduce repetitive work and make business operations run more smoothly.',
    highlights: [
      'Helped deliver 15+ automation workflows across different business use cases',
      'Built automations for content posting, customer support replies, smart inbox management, and email sorting',
      'Learned how to turn messy manual processes into reliable AI-assisted workflows with clearer steps and fewer bottlenecks',
      'Worked directly on identifying automation opportunities, shaping solutions, and communicating value in a way clients could act on quickly',
    ],
    skills: ['AI Automation', 'Workflow Design', 'Prompt Engineering', 'Operations Thinking', 'Client Communication']
  },
  {
    type: 'Internship',
    role: 'IT Intern / Quality Assurance',
    org: 'IREPLY BACK OFFICE SERVICES, INC.',
    date: 'Jan 2026 - Apr 2026',
    color: '#1a5cff',
    tagBg: '#eef2ff',
    tagColor: '#1a5cff',
    iconBg: '#eef2ff',
    icon: `<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#1a5cff" stroke-width="2"><rect x="2" y="7" width="20" height="14" rx="2"/><path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"/></svg>`,
    description: 'Completed 500-hour on-the-job training at IREPLY BACK OFFICE SERVICES, INC., supporting quality assurance work for internal systems and release-ready testing.',
    highlights: [
      'Executed manual testing for internal tools and documented defects clearly for the development team',
      'Reproduced reported issues, verified fixes, and helped improve release readiness before deployment',
      'Prepared bug reports with steps, expected behavior, and actual results to speed up debugging',
      'Collaborated with teammates to keep test coverage aligned with project requirements and timelines',
    ],
    skills: ['Quality Assurance', 'Manual Testing', 'Bug Reporting', 'Documentation', 'Team Collaboration']
  },
  {
    type: 'Leadership',
    role: 'LEAF President',
    org: 'LEAF Organization, USLS',
    date: '2025 - 2026',
    color: '#f97316',
    tagBg: '#fff7ed',
    tagColor: '#ea580c',
    iconBg: '#fff7ed',
    icon: `<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#f97316" stroke-width="2"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>`,
    description: 'Served as President of LEAF, overseeing organizational direction, events, and a team of student officers.',
    highlights: [
      'Led a team of 15+ officers and 100+ student members',
      'Organized 6 major events including seminars, outreaches, and socials',
      'Managed organization budget and logistics end-to-end',
      'Represented the organization in inter-college and university-level activities',
    ],
    skills: ['Leadership', 'Project Management', 'Communication', 'Event Planning']
  },
  {
    type: 'Leadership',
    role: 'CCS Council Secretary',
    org: 'College of Computer Studies Student Council, USLS',
    date: '2025 - 2026',
    color: '#a855f7',
    tagBg: '#fdf4ff',
    tagColor: '#9333ea',
    iconBg: '#fdf4ff',
    icon: `<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#a855f7" stroke-width="2"><path d="M12 20h9"/><path d="M16.5 3.5a2.121 2.121 0 0 1 3 3L7 19l-4 1 1-4L16.5 3.5z"/></svg>`,
    description: 'Served as Secretary of the CCS Student Council, handling official documentation, communications, and administrative support for council operations.',
    highlights: [
      'Maintained official minutes and records for all council meetings',
      'Drafted formal communications to faculty and administration',
      'Coordinated with department heads for academic and student affairs',
      'Assisted in organizing CCS Week and tech-related student events',
    ],
    skills: ['Documentation', 'Communication', 'Organization', 'Administrative Work']
  },
]

const selected = computed(() => experiences[activeIdx.value])
</script>

<style scoped>
.section-head { max-width: 560px; margin-bottom: 56px; }

.exp-layout {
  display: grid;
  grid-template-columns: 320px 1fr;
  gap: 24px;
  align-items: start;
}

.exp-timeline {
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.exp-item {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 16px 18px;
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-md);
  background: var(--color-surface);
  cursor: pointer;
  transition: border-color 0.15s, box-shadow 0.15s, background 0.15s;
}
.exp-item:hover, .exp-item.active {
  border-color: var(--color-accent);
  background: var(--color-accent-light);
}
.exp-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  flex-shrink: 0;
}
.exp-item-content { flex: 1; min-width: 0; }
.exp-type-tag {
  display: inline-block;
  padding: 2px 8px;
  border-radius: 100px;
  font-size: 0.6875rem;
  font-weight: 600;
  margin-bottom: 4px;
}
.exp-title {
  font-family: var(--font-display);
  font-size: 0.9375rem;
  font-weight: 700;
  line-height: 1.3;
  color: var(--color-text);
}
.exp-org, .exp-date {
  font-size: 0.8125rem;
  color: var(--color-text-muted);
}
.exp-chevron {
  color: var(--color-text-faint);
  flex-shrink: 0;
  transition: color 0.15s;
}
.exp-item.active .exp-chevron { color: var(--color-accent); }

.exp-detail {
  background: var(--color-surface);
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: 32px;
  position: sticky;
  top: 88px;
}
.exp-detail-header {
  display: flex;
  gap: 16px;
  margin-bottom: 20px;
  align-items: flex-start;
}
.exp-detail-icon {
  width: 48px;
  height: 48px;
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.exp-detail-role {
  font-family: var(--font-display);
  font-size: 1.35rem;
  font-weight: 700;
  line-height: 1.25;
  margin-bottom: 4px;
}
.exp-detail-org { font-weight: 500; color: var(--color-text-muted); font-size: 0.9rem; }
.exp-detail-date { font-size: 0.8125rem; color: var(--color-text-faint); margin-top: 2px; }

.exp-detail-desc {
  font-size: 0.9375rem;
  color: var(--color-text-muted);
  line-height: 1.7;
  margin-bottom: 24px;
  padding-bottom: 24px;
  border-bottom: 1px solid var(--color-border);
}
.exp-highlights {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 24px;
}
.highlight-item {
  display: flex;
  gap: 10px;
  align-items: flex-start;
  font-size: 0.875rem;
  color: var(--color-text);
}
.detail-skills-label {
  font-size: 0.6875rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-text-faint);
  margin-bottom: 10px;
}
.detail-skills-list { display: flex; flex-wrap: wrap; gap: 6px; }

@media (max-width: 900px) {
  .exp-layout { grid-template-columns: 1fr; }
  .exp-detail { position: static; }
}
</style>
