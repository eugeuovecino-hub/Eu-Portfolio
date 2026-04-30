<template>
  <section id="skills">
    <div class="container">
      <div class="section-head reveal">
      
        <h2 class="section-heading">Skills &amp; Technologies</h2>
        <p class="section-sub">Technologies I work with to build modern, scalable web and mobile applications.</p>
      </div>

      <div class="skills-grid">
        <div
          v-for="(category, idx) in skillCategories"
          :key="category.title"
          :class="['skill-card', 'reveal', `reveal-delay-${idx + 1}`]"
        >
          <div class="skill-card-header">
            <div class="skill-card-icon" :style="{ background: category.iconBg }">
              <span v-html="category.icon"></span>
            </div>
            <h3 class="skill-card-title">{{ category.title }}</h3>
          </div>

          <div class="skill-items">
            <div class="skill-item" v-for="skill in category.skills" :key="skill.name">
              <span v-if="skill.svg" class="skill-icon-svg" :style="{ color: skill.color }" v-html="skill.svg"></span>
              <i v-else :class="skill.icon" class="skill-icon-devicon" :style="{ color: skill.color }"></i>
              <span class="skill-name">{{ skill.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const canvaIcon = `<svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round"><path d="M14.5 7.5c-1.2-1.1-3-1.5-4.7-.8-2.8 1.1-4.4 4.3-3.4 7.1.9 2.7 3.9 4.2 6.7 3.5 1.5-.4 2.8-1.4 3.5-2.8.4-.8.2-1.8-.5-2.3-.7-.5-1.7-.4-2.3.2l-.6.7c-.4.4-.9.7-1.4.8-1.3.3-2.7-.4-3.2-1.7-.5-1.5.4-3.2 1.9-3.8 1-.4 2.2-.2 3 .6"/></svg>`
const vercelIcon = `<svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor"><path d="M12 5l7 12H5z"/></svg>`

const skillCategories = [
  {
    title: 'Frontend',
    iconBg: '#fff4e6',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#f97316" stroke-width="2"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>`,
    skills: [
      { name: 'HTML5', icon: 'devicon-html5-plain', color: '#e34f26' },
      { name: 'CSS3', icon: 'devicon-css3-plain', color: '#264de4' },
      { name: 'JavaScript', icon: 'devicon-javascript-plain', color: '#f7df1e' },
      { name: 'Vue.js', icon: 'devicon-vuejs-plain', color: '#42b883' },
    ]
  },
  {
    title: 'Backend',
    iconBg: '#eef6ff',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#3b82f6" stroke-width="2"><rect x="2" y="3" width="20" height="14" rx="2"/><line x1="8" y1="21" x2="16" y2="21"/><line x1="12" y1="17" x2="12" y2="21"/></svg>`,
    skills: [
      { name: 'PHP', icon: 'devicon-php-plain', color: '#777bb4' },
      { name: 'Java', icon: 'devicon-java-plain', color: '#ed8b00' },
    ]
  },
  {
    title: 'Database',
    iconBg: '#f0fdf4',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#22c55e" stroke-width="2"><ellipse cx="12" cy="5" rx="9" ry="3"/><path d="M21 12c0 1.66-4 3-9 3s-9-1.34-9-3"/><path d="M3 5v14c0 1.66 4 3 9 3s9-1.34 9-3V5"/></svg>`,
    skills: [
      { name: 'MySQL', icon: 'devicon-mysql-plain', color: '#4479a1' },
      { name: 'MongoDB', icon: 'devicon-mongodb-plain', color: '#47a248' },
      { name: 'Firebase', icon: 'devicon-firebase-plain', color: '#ffca28' },
    ]
  },
  {
    title: 'Tools',
    iconBg: '#fdf4ff',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#a855f7" stroke-width="2"><path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.77-3.77a6 6 0 0 1-7.94 7.94l-6.91 6.91a2.12 2.12 0 0 1-3-3l6.91-6.91a6 6 0 0 1 7.94-7.94l-3.76 3.76z"/></svg>`,
    skills: [
      { name: 'Git', icon: 'devicon-git-plain', color: '#f05032' },
      { name: 'GitHub', icon: 'devicon-github-original', color: '#181717' },
      { name: 'Figma', icon: 'devicon-figma-plain', color: '#f24e1e' },
      { name: 'VS Code', icon: 'devicon-vscode-plain', color: '#007acc' },
      { name: 'Canva', svg: canvaIcon, color: '#00c4cc' },
      { name: 'Vercel', svg: vercelIcon, color: '#111111' },
    ]
  },
  {
    title: 'Mobile',
    iconBg: '#eff6ff',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#2563eb" stroke-width="2"><rect x="7" y="2" width="10" height="20" rx="2"/><line x1="11" y1="18" x2="13" y2="18"/></svg>`,
    skills: [
      { name: 'Flutter', icon: 'devicon-flutter-plain', color: '#47c5fb' },
      { name: 'Java', icon: 'devicon-java-plain', color: '#ed8b00' },
    ]
  },
]
</script>

<style scoped>
.section-head {
  max-width: 560px;
  margin-bottom: 56px;
}
.skills-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}
.skill-card {
  background: var(--color-surface);
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: 32px;
  transition: transform 0.2s, box-shadow 0.2s;
}
.skill-card:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-md);
}
.skill-card-header {
  display: flex;
  align-items: center;
  gap: 14px;
  margin-bottom: 24px;
}
.skill-card-icon {
  width: 44px;
  height: 44px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.skill-card-title {
  font-family: var(--font-display);
  font-size: 1.2rem;
  font-weight: 700;
  margin-top: 2px;
}
.skill-items {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(110px, 1fr));
  gap: 12px;
}
.skill-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 14px;
  background: var(--color-bg);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  transition: border-color 0.15s, background 0.15s;
}
.skill-item:hover {
  border-color: var(--color-accent);
  background: var(--color-accent-light);
}
.skill-icon-devicon {
  font-size: 1.375rem;
  flex-shrink: 0;
}
.skill-icon-svg {
  width: 1.375rem;
  height: 1.375rem;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.skill-name {
  font-size: 0.8125rem;
  font-weight: 500;
  color: var(--color-text);
}

@media (max-width: 768px) {
  .skills-grid { grid-template-columns: 1fr; }
}
</style>
