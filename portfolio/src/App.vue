<template>
  <div id="portfolio">
    <NavBar :active-section="activeSection" />
    <main>
      <HeroSection id="home" />
      <hr class="divider" />
      <SkillsSection id="skills" />
      <hr class="divider" />
      <ProjectsSection id="projects" />
      <hr class="divider" />
      <ExperienceSection id="experience" />
      <hr class="divider" />
      <CertificationsSection id="certifications" />
      <hr class="divider" />
      <AboutSection id="about" />
      <hr class="divider" />
      <ResumeSection id="resume" />
      <hr class="divider" />
      <ContactSection id="contact" />
    </main>
    <FooterBar />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import CertificationsSection from './components/CertificationsSection.vue'
import AboutSection from './components/AboutSection.vue'
import ResumeSection from './components/ResumeSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterBar from './components/FooterBar.vue'

const activeSection = ref('home')

const handleScroll = () => {
  const sections = ['home','skills','projects','experience','certifications','about','resume','contact']
  for (let i = sections.length - 1; i >= 0; i--) {
    const el = document.getElementById(sections[i])
    if (el && el.getBoundingClientRect().top <= 80) {
      activeSection.value = sections[i]
      break
    }
  }
  // Reveal on scroll
  document.querySelectorAll('.reveal').forEach(el => {
    if (el.getBoundingClientRect().top < window.innerHeight - 60) {
      el.classList.add('visible')
    }
  })
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
  handleScroll()
})
onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style>
#portfolio {
  min-height: 100vh;
}
</style>
