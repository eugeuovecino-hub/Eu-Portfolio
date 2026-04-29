<template>
  <section id="projects" class="projects-section">
    <div class="container">
      <div class="section-head reveal">
        <div class="section-tag">Portfolio</div>
        <h2 class="section-heading">Featured Projects</h2>
        <p class="section-sub">A selection of work that demonstrates my approach to solving real-world problems with thoughtful engineering.</p>
      </div>

      <!-- Filter tabs -->
      <div class="filter-tabs reveal">
        <button
          v-for="tag in filterTags"
          :key="tag"
          :class="['filter-btn', { active: activeFilter === tag }]"
          @click="activeFilter = tag"
        >{{ tag }}</button>
      </div>

      <div class="projects-grid">
        <article
          v-for="(project, idx) in filteredProjects"
          :key="project.id"
          :class="['project-card', 'reveal', `reveal-delay-${(idx % 3) + 1}`, { featured: project.featured }]"
        >
          <!-- Screenshot area -->
          <div class="project-visual" :style="{ background: project.visualBg }">
            <div class="project-visual-inner">
              <div class="browser-bar">
                <span></span><span></span><span></span>
              </div>
              <div class="project-screen" :style="{ background: project.screenBg }">
                <div class="screen-content">
                  <div class="screen-header" :style="{ background: project.accentColor }"></div>
                  <div class="screen-rows">
                    <div class="screen-row" v-for="n in 4" :key="n"></div>
                  </div>
                  <div class="screen-sidebar"></div>
                </div>
              </div>
            </div>
            <div class="project-overlay">
              <a v-if="project.demo" :href="project.demo" target="_blank" class="btn btn-primary btn-sm">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
                Live Demo
              </a>
              <a v-if="project.github" :href="project.github" target="_blank" class="btn btn-outline btn-sm">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/></svg>
                GitHub
              </a>
            </div>
            <div v-if="project.featured" class="featured-badge">
              ★ Featured
            </div>
          </div>

          <!-- Content -->
          <div class="project-body">
            <div class="project-meta">
              <span v-for="tag in project.tags" :key="tag" class="tech-tag">{{ tag }}</span>
            </div>

            <h3 class="project-title">{{ project.name }}</h3>
            <p class="project-role" v-if="project.role">
              <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
              {{ project.role }}
            </p>

            <div class="project-problem">
              <div class="problem-label">Problem Solved</div>
              <p>{{ project.problem }}</p>
            </div>

            <div class="project-details" v-if="project.expanded || project.featured">
              <div class="detail-row">
                <div class="detail-icon">💡</div>
                <div>
                  <strong>Solution</strong>
                  <p>{{ project.solution }}</p>
                </div>
              </div>
              <div class="detail-row" v-if="project.result">
                <div class="detail-icon">📈</div>
                <div>
                  <strong>Result</strong>
                  <p>{{ project.result }}</p>
                </div>
              </div>
              <div class="detail-row" v-if="project.challenge">
                <div class="detail-icon">⚡</div>
                <div>
                  <strong>Key Challenge</strong>
                  <p>{{ project.challenge }}</p>
                </div>
              </div>
              <div class="detail-row" v-if="project.learned">
                <div class="detail-icon">🎯</div>
                <div>
                  <strong>What I Learned</strong>
                  <p>{{ project.learned }}</p>
                </div>
              </div>
            </div>

            <button class="expand-btn" @click="project.expanded = !project.expanded" v-if="!project.featured">
              {{ project.expanded ? 'Show less' : 'Read more' }}
              <svg :style="{ transform: project.expanded ? 'rotate(180deg)' : '' }" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" style="transition: transform 0.2s"><polyline points="6 9 12 15 18 9"/></svg>
            </button>

            <div class="project-stack">
              <span class="stack-label">Stack:</span>
              <div class="stack-icons">
                <i v-for="icon in project.stackIcons" :key="icon.name" :class="icon.cls" :title="icon.name" class="stack-icon"></i>
              </div>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, reactive } from 'vue'

const activeFilter = ref('All')
const filterTags = ['All', 'Web App', 'Mobile', 'Full Stack', 'Laravel', 'React']

const projects = reactive([
  {
    id: 1,
    name: 'Business Inventory Management System',
    featured: true,
    expanded: false,
    tags: ['Web App', 'Full Stack', 'Laravel'],
    role: 'Full Stack Developer (Team Lead)',
    visualBg: 'linear-gradient(135deg, #e8f4fd 0%, #dbeafe 100%)',
    screenBg: '#f0f8ff',
    accentColor: '#3b82f6',
    problem: 'Local businesses struggled with manual, error-prone inventory tracking, leading to stock discrepancies, overstocking, and revenue loss.',
    solution: 'Built a web-based inventory management system with real-time stock monitoring, automated low-stock alerts, sales reporting, and role-based access for staff.',
    result: 'Reduced manual tracking time by 50% and eliminated stock discrepancy errors across all product categories.',
    challenge: 'Designing a database schema flexible enough to handle multiple product variants and suppliers while keeping queries fast.',
    learned: 'Learned the importance of database normalization and query optimization early in the design phase. Also gained experience managing a small dev team with Git branching strategies.',
    demo: '#',
    github: '#',
    stackIcons: [
      { name: 'Laravel', cls: 'devicon-laravel-plain' },
      { name: 'MySQL', cls: 'devicon-mysql-plain' },
      { name: 'Bootstrap', cls: 'devicon-bootstrap-plain' },
      { name: 'PHP', cls: 'devicon-php-plain' },
    ]
  },
  {
    id: 2,
    name: 'Campus Event Management App',
    featured: false,
    expanded: false,
    tags: ['Web App', 'Full Stack', 'React'],
    role: 'Frontend Developer & UI/UX Designer',
    visualBg: 'linear-gradient(135deg, #f0fdf4 0%, #dcfce7 100%)',
    screenBg: '#f7fff8',
    accentColor: '#22c55e',
    problem: 'Student organizations at USLS had no centralized platform to announce events, manage registrations, or track attendance.',
    solution: 'Developed a responsive web app for event creation, QR-code-based attendance tracking, and a public event discovery feed for students.',
    result: 'Streamlined event management for 10+ student organizations, cutting manual attendance processing from 30 minutes to under 2 minutes per event.',
    challenge: 'Implementing real-time QR code scanning that worked reliably on both Android and iOS browsers without a native app.',
    learned: 'Deepened understanding of browser camera APIs and WebSockets for real-time updates. Learned about accessibility requirements for student-facing platforms.',
    demo: '#',
    github: '#',
    stackIcons: [
      { name: 'React', cls: 'devicon-react-original' },
      { name: 'Node.js', cls: 'devicon-nodejs-plain' },
      { name: 'Firebase', cls: 'devicon-firebase-plain' },
    ]
  },
  {
    id: 3,
    name: 'Student Grade Tracker & Analytics',
    featured: false,
    expanded: false,
    tags: ['Web App', 'Full Stack'],
    role: 'Full Stack Developer',
    visualBg: 'linear-gradient(135deg, #fdf4ff 0%, #f3e8ff 100%)',
    screenBg: '#fefaff',
    accentColor: '#a855f7',
    problem: 'Students and instructors lacked a simple, visual way to track academic performance over a semester, leading to surprise failing grades.',
    solution: 'Created a grade management dashboard with semester GPA projections, subject-by-subject breakdowns, and instructor grade upload tools.',
    result: 'Used by over 80 students in a pilot run, with reported improvement in academic awareness and early intervention by instructors.',
    challenge: 'Ensuring accurate GPA calculation logic across different grading systems (percentage-based vs. transmuted grades).',
    learned: 'Learned how to translate complex business logic (grading policies) into reliable backend computations. Improved skills in data visualization with Chart.js.',
    demo: '#',
    github: '#',
    stackIcons: [
      { name: 'Vue.js', cls: 'devicon-vuejs-plain' },
      { name: 'Laravel', cls: 'devicon-laravel-plain' },
      { name: 'MySQL', cls: 'devicon-mysql-plain' },
    ]
  },
  {
    id: 4,
    name: 'Mobile Barangay Services Portal',
    featured: false,
    expanded: false,
    tags: ['Mobile', 'Full Stack'],
    role: 'Backend Developer & Mobile Developer',
    visualBg: 'linear-gradient(135deg, #fff7ed 0%, #ffedd5 100%)',
    screenBg: '#fffaf5',
    accentColor: '#f97316',
    problem: 'Residents of a local barangay had to physically visit the barangay hall for document requests, certificates, and complaints — causing long wait times.',
    solution: 'Developed a mobile-first portal allowing residents to request documents, track status, and submit complaints from their phones, with admin dashboard for staff.',
    result: 'Digitized 6 types of document requests, reducing average processing time from 3 days to same-day digital approval.',
    challenge: 'Balancing security and accessibility for elderly users who are not digitally literate, requiring a very simple, large-text UI.',
    learned: 'Gained empathy-driven design experience. Learned the nuances of building for low-tech users and the importance of clear error messaging in mobile forms.',
    demo: '#',
    github: '#',
    stackIcons: [
      { name: 'React', cls: 'devicon-react-original' },
      { name: 'Node.js', cls: 'devicon-nodejs-plain' },
      { name: 'MongoDB', cls: 'devicon-mongodb-plain' },
    ]
  },
  {
    id: 5,
    name: 'E-Commerce Platform for Local Sellers',
    featured: false,
    expanded: false,
    tags: ['Web App', 'Full Stack', 'Laravel'],
    role: 'Full Stack Developer',
    visualBg: 'linear-gradient(135deg, #fff1f2 0%, #ffe4e6 100%)',
    screenBg: '#fff8f8',
    accentColor: '#ef4444',
    problem: 'Small local sellers in Bacolod had no affordable online storefront — existing platforms had high fees and no support for local payment methods.',
    solution: 'Built a lightweight multi-vendor e-commerce platform with store management, product listings, order tracking, and GCash/COD payment support.',
    result: 'Onboarded 5 local seller accounts in a prototype phase, enabling digital sales for sellers previously limited to walk-in customers only.',
    challenge: 'Integrating payment gateway APIs (GCash via Paymongo) and handling webhook reliability for order confirmation flows.',
    learned: 'First deep dive into payment processing and financial transaction security. Learned about idempotency and race conditions in order creation.',
    demo: '#',
    github: '#',
    stackIcons: [
      { name: 'Laravel', cls: 'devicon-laravel-plain' },
      { name: 'MySQL', cls: 'devicon-mysql-plain' },
      { name: 'JavaScript', cls: 'devicon-javascript-plain' },
      { name: 'Bootstrap', cls: 'devicon-bootstrap-plain' },
    ]
  },
])

const filteredProjects = computed(() => {
  if (activeFilter.value === 'All') return projects
  return projects.filter(p => p.tags.includes(activeFilter.value))
})
</script>

<style scoped>
.projects-section { background: var(--color-surface-alt); }

.section-head { max-width: 560px; margin-bottom: 32px; }

.filter-tabs {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 48px;
}
.filter-btn {
  padding: 7px 18px;
  border-radius: 100px;
  font-size: 0.875rem;
  font-weight: 500;
  background: var(--color-surface);
  border: 1.5px solid var(--color-border);
  color: var(--color-text-muted);
  transition: all 0.15s;
}
.filter-btn:hover { border-color: var(--color-accent); color: var(--color-accent); }
.filter-btn.active {
  background: var(--color-text);
  border-color: var(--color-text);
  color: var(--color-bg);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
  gap: 24px;
}

.project-card {
  background: var(--color-surface);
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-lg);
  overflow: hidden;
  transition: transform 0.25s, box-shadow 0.25s;
}
.project-card:hover { transform: translateY(-4px); box-shadow: var(--shadow-hover); }
.project-card.featured {
  grid-column: 1 / -1;
  display: grid;
  grid-template-columns: 1fr 1fr;
}

/* Visual / Mock screenshot */
.project-visual {
  position: relative;
  height: 220px;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}
.project-card.featured .project-visual { height: auto; min-height: 300px; }

.project-visual-inner {
  width: 76%;
  transform: perspective(800px) rotateX(4deg) rotateY(-4deg);
  border-radius: 10px;
  overflow: hidden;
  box-shadow: var(--shadow-lg);
  transition: transform 0.3s ease;
}
.project-card:hover .project-visual-inner {
  transform: perspective(800px) rotateX(0deg) rotateY(0deg);
}
.browser-bar {
  height: 24px;
  background: #e8e6e2;
  display: flex;
  align-items: center;
  gap: 5px;
  padding: 0 10px;
}
.browser-bar span {
  width: 8px; height: 8px;
  border-radius: 50%;
  background: #ccc;
}
.browser-bar span:nth-child(1) { background: #ff6b6b; }
.browser-bar span:nth-child(2) { background: #ffd93d; }
.browser-bar span:nth-child(3) { background: #6bcb77; }
.project-screen {
  height: 100px;
  padding: 8px;
  position: relative;
  overflow: hidden;
}
.screen-content {
  display: flex;
  height: 100%;
  gap: 6px;
  position: relative;
}
.screen-header {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 16px;
  opacity: 0.7;
  border-radius: 3px;
}
.screen-rows {
  display: flex;
  flex-direction: column;
  gap: 5px;
  margin-top: 22px;
  flex: 1;
}
.screen-row {
  height: 8px;
  background: rgba(0,0,0,0.07);
  border-radius: 4px;
}
.screen-row:last-child { width: 60%; }
.screen-sidebar {
  width: 28px;
  margin-top: 22px;
  background: rgba(0,0,0,0.06);
  border-radius: 4px;
}

.project-overlay {
  position: absolute;
  inset: 0;
  background: rgba(10,10,10,0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  opacity: 0;
  transition: opacity 0.25s;
}
.project-card:hover .project-overlay { opacity: 1; }

.featured-badge {
  position: absolute;
  top: 14px;
  left: 14px;
  background: #1a5cff;
  color: #fff;
  padding: 4px 12px;
  border-radius: 100px;
  font-size: 0.75rem;
  font-weight: 600;
}

/* Body */
.project-body {
  padding: 24px;
}
.project-meta { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 12px; }
.project-title {
  font-family: var(--font-display);
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 6px;
  line-height: 1.3;
}
.project-role {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 0.8125rem;
  color: var(--color-text-muted);
  margin-bottom: 16px;
}
.project-problem {
  background: var(--color-bg);
  border-left: 3px solid var(--color-accent);
  padding: 10px 14px;
  border-radius: 0 var(--radius-sm) var(--radius-sm) 0;
  margin-bottom: 16px;
  font-size: 0.875rem;
  color: var(--color-text-muted);
}
.problem-label {
  font-size: 0.6875rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-accent);
  margin-bottom: 4px;
}
.project-details {
  display: flex;
  flex-direction: column;
  gap: 14px;
  margin-bottom: 16px;
  padding-top: 4px;
}
.detail-row {
  display: flex;
  gap: 12px;
  font-size: 0.875rem;
}
.detail-icon { font-size: 1rem; flex-shrink: 0; margin-top: 1px; }
.detail-row strong { display: block; font-weight: 600; font-size: 0.8125rem; margin-bottom: 2px; }
.detail-row p { color: var(--color-text-muted); line-height: 1.55; }

.expand-btn {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 0.8125rem;
  font-weight: 500;
  color: var(--color-accent);
  margin-bottom: 16px;
  padding: 0;
  background: none;
  border: none;
}
.expand-btn:hover { opacity: 0.75; }

.project-stack {
  display: flex;
  align-items: center;
  gap: 10px;
  padding-top: 16px;
  border-top: 1px solid var(--color-border);
}
.stack-label {
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--color-text-faint);
  text-transform: uppercase;
  letter-spacing: 0.08em;
}
.stack-icons { display: flex; gap: 8px; align-items: center; }
.stack-icon { font-size: 1.375rem; opacity: 0.75; transition: opacity 0.15s; }
.stack-icon:hover { opacity: 1; }

@media (max-width: 840px) {
  .project-card.featured { grid-template-columns: 1fr; }
  .projects-grid { grid-template-columns: 1fr; }
}
</style>
