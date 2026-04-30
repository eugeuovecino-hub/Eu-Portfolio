<template>
  <section id="projects" class="projects-section">
    <div class="container">
      <div class="section-head reveal">
        
        <h2 class="section-heading">Featured Projects</h2>
        <p class="section-sub">A selection of work that demonstrates my approach to solving real-world problems with thoughtful engineering.</p>
      </div>

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
          <div
            class="project-visual"
            :class="{ 'has-gallery': project.gallery?.length }"
            :style="{ background: project.visualBg }"
            :role="project.gallery?.length ? 'button' : undefined"
            :tabindex="project.gallery?.length ? 0 : undefined"
            @click="openGallery(project)"
            @keyup.enter="openGallery(project)"
            @keyup.space.prevent="openGallery(project)"
          >
            <template v-if="project.gallery?.length">
              <div class="project-gallery-preview" :class="{ single: project.gallery.length === 1 }">
                <div class="gallery-shot primary">
                  <img :src="project.gallery[0].src" :alt="project.gallery[0].alt" />
                </div>
                <div v-if="project.gallery.length > 1" class="gallery-side-stack">
                  <div class="gallery-shot" v-for="image in project.gallery.slice(1, 3)" :key="image.src">
                    <img :src="image.src" :alt="image.alt" />
                  </div>
                </div>
              </div>
              <div class="gallery-open-badge">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <rect x="3" y="3" width="18" height="18" rx="2"></rect>
                  <circle cx="8.5" cy="8.5" r="1.5"></circle>
                  <path d="m21 15-5-5L5 21"></path>
                </svg>
                View images
              </div>
            </template>
            <template v-else>
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
              <div v-if="project.demo || project.github" class="project-overlay">
                <a v-if="project.demo" :href="project.demo" target="_blank" class="btn btn-primary btn-sm">
                  <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
                  Live Demo
                </a>
                <a v-if="project.github" :href="project.github" target="_blank" class="btn btn-outline btn-sm">
                  <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/></svg>
                  GitHub
                </a>
              </div>
            </template>
            <div v-if="project.featured" class="featured-badge">
              Featured
            </div>
          </div>

          <div class="project-body">
            <div class="project-meta">
              <span v-for="tag in project.tags" :key="tag" class="tech-tag">{{ tag }}</span>
            </div>

            <h3 class="project-title">{{ project.name }}</h3>
            <p class="project-role" v-if="project.role">
              <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
              {{ project.role }}
            </p>
            <p class="project-summary" v-if="project.summary">{{ project.summary }}</p>
            <button v-if="project.gallery?.length" class="gallery-body-btn" @click="openGallery(project)">
              <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <rect x="3" y="3" width="18" height="18" rx="2"></rect>
                <circle cx="8.5" cy="8.5" r="1.5"></circle>
                <path d="m21 15-5-5L5 21"></path>
              </svg>
              View project images
            </button>

            <div class="project-problem">
              <div class="problem-label">Problem Solved</div>
              <p>{{ project.problem }}</p>
            </div>

            <div class="project-details" v-if="project.expanded || project.featured">
              <div class="detail-row">
                <svg class="detail-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M9 18h6"></path>
                  <path d="M10 22h4"></path>
                  <path d="M12 2a7 7 0 0 0-4 12.75c.63.45 1 1.16 1 1.89V18h6v-1.36c0-.73.37-1.44 1-1.89A7 7 0 0 0 12 2z"></path>
                </svg>
                <div>
                  <strong>Solution</strong>
                  <p>{{ project.solution }}</p>
                </div>
              </div>
              <div class="detail-row" v-if="project.result">
                <svg class="detail-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <line x1="12" y1="20" x2="12" y2="10"></line>
                  <line x1="18" y1="20" x2="18" y2="4"></line>
                  <line x1="6" y1="20" x2="6" y2="14"></line>
                </svg>
                <div>
                  <strong>Result</strong>
                  <p>{{ project.result }}</p>
                </div>
              </div>
              <div class="detail-row" v-if="project.challenge">
                <svg class="detail-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"></polygon>
                </svg>
                <div>
                  <strong>Key Challenge</strong>
                  <p>{{ project.challenge }}</p>
                </div>
              </div>
              <div class="detail-row" v-if="project.learned">
                <svg class="detail-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <circle cx="12" cy="12" r="8"></circle>
                  <circle cx="12" cy="12" r="2.5"></circle>
                </svg>
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
                <span v-for="icon in project.stackIcons" :key="icon.name" class="stack-chip" :title="icon.name">
                  <i :class="icon.cls" class="stack-icon"></i>
                  <span>{{ icon.name }}</span>
                </span>
              </div>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>

  <Teleport to="body">
    <div v-if="galleryProject" class="gallery-modal" @click.self="closeGallery">
      <div class="gallery-dialog" role="dialog" aria-modal="true" :aria-label="`${galleryProject.name} image gallery`">
        <div class="gallery-header">
          <div>
            <p class="gallery-kicker">Project Gallery</p>
            <h3>{{ galleryProject.name }}</h3>
          </div>
          <button class="gallery-close" type="button" aria-label="Close gallery" @click="closeGallery">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <line x1="18" y1="6" x2="6" y2="18"></line>
              <line x1="6" y1="6" x2="18" y2="18"></line>
            </svg>
          </button>
        </div>

        <div class="gallery-stage" v-if="activeGalleryImage">
          <button class="gallery-nav prev" type="button" aria-label="Previous image" @click="showPreviousImage">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="15 18 9 12 15 6"></polyline>
            </svg>
          </button>
          <img :src="activeGalleryImage.src" :alt="activeGalleryImage.alt" />
          <button class="gallery-nav next" type="button" aria-label="Next image" @click="showNextImage">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="9 18 15 12 9 6"></polyline>
            </svg>
          </button>
        </div>

        <div class="gallery-footer" v-if="activeGalleryImage">
          <div>
            <strong>{{ activeGalleryImage.title }}</strong>
            <p>{{ activeGalleryImage.caption }}</p>
          </div>
          <span>{{ activeGalleryIndex + 1 }} / {{ galleryProject.gallery.length }}</span>
        </div>

        <div class="gallery-thumbs">
          <button
            v-for="(image, imageIndex) in galleryProject.gallery"
            :key="image.src"
            type="button"
            :class="['gallery-thumb', { active: activeGalleryIndex === imageIndex }]"
            :aria-label="`Show ${image.title}`"
            @click="activeGalleryIndex = imageIndex"
          >
            <img :src="image.src" :alt="image.alt" />
          </button>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<script setup>
import { ref, computed, reactive } from 'vue'
import produceVendorDashboard from '../assets/projects/produce/vendor-dashboard.png'
import produceCustomerMarket from '../assets/projects/produce/customer-market.png'
import produceAdminAnalytics from '../assets/projects/produce/admin-analytics.png'
import smartCityHeroHome from '../assets/projects/smart-city/hero-home.png'
import smartCityIntroduction from '../assets/projects/smart-city/introduction.png'
import smartCityTransportation from '../assets/projects/smart-city/transportation.png'
import smartCityAiDriven from '../assets/projects/smart-city/ai-driven.png'
import smartCitySpaceAge from '../assets/projects/smart-city/space-age.png'
import smartCityGreenTech from '../assets/projects/smart-city/green-tech.png'
import masskaraFestivalHero from '../assets/projects/masskara/festival-hero.png'
import masskaraFestivalHistory from '../assets/projects/masskara/festival-history.png'
import masskaraFestivalLocations from '../assets/projects/masskara/festival-locations.png'
import masskaraFestivalHighlights from '../assets/projects/masskara/festival-highlights.png'
import hrisLoginScreen from '../assets/projects/hris/login-screen.png'
import kohiMenuDuo from '../assets/projects/kohi/menu-duo.png'
import kohiProductCarousel from '../assets/projects/kohi/product-carousel.png'
import kohiCoffeeShowcase from '../assets/projects/kohi/coffee-showcase.png'
import kohiTeaFruitShowcase from '../assets/projects/kohi/tea-fruit-showcase.png'

const activeFilter = ref('All')
const galleryProject = ref(null)
const activeGalleryIndex = ref(0)
const filterTags = ['All', 'E-Commerce', 'Web App', 'Full Stack', 'Frontend', 'Animation', 'Mobile', 'React']

const projects = reactive([
  {
    id: 1,
    name: 'ProDuce: E-Commerce Platform',
    featured: true,
    expanded: false,
    tags: ['E-Commerce', 'Full Stack', 'Mobile'],
    role: 'Project Manager',
    summary: 'ProDuce connects public market vendors and customers through a streamlined buying flow designed to reduce waste and improve accessibility.',
    visualBg: 'linear-gradient(135deg, #eef8e8 0%, #d8f3dc 100%)',
    screenBg: '#f8fff5',
    accentColor: '#2f9e44',
    problem: 'Public market vendors often lose potential sales because customers need to visit stalls physically, while unsold produce can go to waste when demand is hard to predict.',
    solution: 'Led the team in shaping an e-commerce flow where vendors can list produce, customers can browse and order more easily, and product availability is clearer before market trips.',
    result: 'Produced a working platform concept that made vendor inventory more discoverable, improved the customer buying path, and framed waste reduction as a core product goal.',
    challenge: 'Balancing a simple customer experience with vendor-side workflows that needed to stay practical for busy public market sellers.',
    learned: 'Strengthened my project management skills by coordinating scope, priorities, communication, and technical tradeoffs across web, mobile, and database work.',
    gallery: [
      {
        src: produceVendorDashboard,
        title: 'Vendor dashboard',
        alt: 'ProDuce vendor dashboard showing weekly food reduction and recent transactions',
        caption: 'Vendor tools for posting produce, managing listings, reviewing history, and tracking weekly food reduction.'
      },
      {
        src: produceCustomerMarket,
        title: 'Customer marketplace',
        alt: 'ProDuce marketplace screen showing categories and produce listings',
        caption: 'Customer browsing flow with produce categories, listings, prices, quantities, and quick purchase actions.'
      },
      {
        src: produceAdminAnalytics,
        title: 'Admin analytics',
        alt: 'ProDuce admin analytics dashboard with claims, listings, users, and collected food metrics',
        caption: 'Admin dashboard for monitoring users, listings, claims, expired produce, and collected food data.'
      },
    ],
    stackIcons: [
      { name: 'HTML', cls: 'devicon-html5-plain' },
      { name: 'CSS', cls: 'devicon-css3-plain' },
      { name: 'JavaScript', cls: 'devicon-javascript-plain' },
      { name: 'PHP', cls: 'devicon-php-plain' },
      { name: 'Flutter', cls: 'devicon-flutter-plain' },
      { name: 'Dart', cls: 'devicon-dart-plain' },
      { name: 'MySQL', cls: 'devicon-mysql-plain' },
    ]
  },
  {
    id: 2,
    name: 'HRIS Attendance System',
    featured: false,
    expanded: false,
    tags: ['Web App', 'Full Stack', 'React'],
    role: 'Quality Assurance',
    summary: 'A multi role-based employee management system for attendance, scheduling, and controlled access across multiple teams.',
    visualBg: 'linear-gradient(135deg, #e8f4fd 0%, #dbeafe 100%)',
    screenBg: '#f6fbff',
    accentColor: '#2563eb',
    problem: 'Teams needed a more reliable way to track attendance, schedules, employee records, and role-specific access without relying on scattered manual processes.',
    solution: 'Tested a role-based HRIS workflow covering attendance logging, schedule visibility, account permissions, and employee management across different user types.',
    result: 'Helped improve release confidence by catching workflow gaps, validating access behavior, and ensuring core attendance features behaved consistently before deployment.',
    challenge: 'Testing the system from multiple roles required careful scenario planning so that permissions, navigation, and data visibility stayed correct for each user type.',
    learned: 'Built stronger QA habits around test cases, edge cases, regression checks, and communicating defects in a way that helped developers fix issues faster.',
    gallery: [
      {
        src: hrisLoginScreen,
        title: 'Login screen',
        alt: 'HRIS login screen with Fireply branding and username and password fields',
        caption: 'The HRIS entry point uses a clean login screen with focused form inputs and a simple branded interface for secure role-based access.'
      },
    ],
    stackIcons: [
      { name: 'HTML', cls: 'devicon-html5-plain' },
      { name: 'CSS', cls: 'devicon-css3-plain' },
      { name: 'PHP', cls: 'devicon-php-plain' },
      { name: 'React', cls: 'devicon-react-original' },
      { name: 'MySQL', cls: 'devicon-mysql-plain' },
      { name: 'Vite', cls: 'devicon-vitejs-plain' },
      { name: 'Vercel', cls: 'devicon-vercel-original' },
    ]
  },
  {
    id: 3,
    name: 'Smart City: A Web Animation Project',
    featured: false,
    expanded: false,
    tags: ['Web App', 'Frontend', 'Animation'],
    role: 'Frontend Designer',
    summary: 'A web animation project created to explore motion, interaction, and animated storytelling in a browser-based experience.',
    visualBg: 'linear-gradient(135deg, #f0f9ff 0%, #ccfbf1 100%)',
    screenBg: '#f5fffd',
    accentColor: '#0891b2',
    problem: 'Static web pages can struggle to communicate energy, depth, and movement, especially when the goal is to present a futuristic city concept.',
    solution: 'Designed and built an animated Smart City scene using HTML, CSS, and JavaScript to experiment with timing, visual hierarchy, and interactive motion.',
    result: 'Created a more engaging front-end experience that demonstrated animation principles while keeping the page lightweight and browser-friendly.',
    challenge: 'Making the animation feel alive without overloading the page or distracting users from the visual story.',
    learned: 'Improved my understanding of animation timing, layered layouts, CSS transitions, JavaScript-driven effects, and how motion can support a page concept.',
    gallery: [
      {
        src: smartCityHeroHome,
        title: 'Landing page hero',
        alt: 'Smart City project homepage showing The New Bacolod hero section with animated background particles',
        caption: 'The main landing section introduces the New Bacolod concept with a full-screen city backdrop, large typography, and animated visual effects.'
      },
      {
        src: smartCityIntroduction,
        title: 'Introduction section',
        alt: 'Smart City introduction section describing Smart Bacolod connected and sustainable',
        caption: 'This section frames the project vision and uses motion with a curved dotted path to guide the visitor through the narrative.'
      },
      {
        src: smartCityTransportation,
        title: 'Transportation concept',
        alt: 'Smart City transportation section about better transportation in Bacolod',
        caption: 'A storytelling section focused on connected transport, showing how motion and layout help explain the city plan clearly.'
      },
      {
        src: smartCityAiDriven,
        title: 'AI-driven traffic concept',
        alt: 'Smart City AI-driven section with animated traffic intersection graphic',
        caption: 'An interactive visual exploring AI-assisted traffic management, combining illustration-style animation with supporting copy.'
      },
      {
        src: smartCitySpaceAge,
        title: 'Space age concept',
        alt: 'Smart City space age section showing an astronaut illustration for Bacolodnons in space',
        caption: 'A more playful concept section that uses a stylized astronaut graphic to push the futuristic tone of the project.'
      },
      {
        src: smartCityGreenTech,
        title: 'Green tech section',
        alt: 'Smart City green tech section describing a carbon-zero future',
        caption: 'The closing concept section highlights sustainability goals and shows how the site carries the same dark, motion-led visual language throughout.'
      },
    ],
    stackIcons: [
      { name: 'HTML', cls: 'devicon-html5-plain' },
      { name: 'CSS', cls: 'devicon-css3-plain' },
      { name: 'JavaScript', cls: 'devicon-javascript-plain' },
    ]
  },
  {
    id: 4,
    name: 'MassKara 2023 Exhibit',
    featured: false,
    expanded: false,
    tags: ['Web App', 'Frontend', 'Animation'],
    role: 'Frontend Designer',
    summary: 'A static experience built to showcase the 2023 MassKara Festival with a stronger visual story and more polished presentation.',
    visualBg: 'linear-gradient(135deg, #fff7ed 0%, #ffedd5 100%)',
    screenBg: '#fffaf5',
    accentColor: '#f97316',
    problem: 'Festival content can feel flat when presented as plain text and images, especially for an event known for color, movement, and celebration.',
    solution: 'Built a visually led static exhibit using structured sections, front-end animation, and GSAP-enhanced motion to present the MassKara story with more energy.',
    result: 'Delivered a polished exhibit-style webpage that better captured the festival atmosphere and gave viewers a more memorable browsing experience.',
    challenge: 'Finding the right balance between expressive animation and a clean presentation that still felt easy to scan.',
    learned: 'Gained more confidence using GSAP, sequencing animations, and designing static pages that feel dynamic without needing a complex backend.',
    gallery: [
      {
        src: masskaraFestivalHero,
        title: 'Festival landing hero',
        alt: 'MassKara 2023 Exhibit homepage with aerial hero image and festival navigation',
        caption: 'The landing section opens with a strong festival visual, bold navigation, and a high-energy first impression for the MassKara showcase.'
      },
      {
        src: masskaraFestivalHistory,
        title: 'History section',
        alt: 'MassKara 2023 Exhibit history section with archival collage and festival background text',
        caption: 'This section introduces the origins of the festival through a warm editorial layout, archival imagery, and readable long-form storytelling.'
      },
      {
        src: masskaraFestivalLocations,
        title: 'Location guide',
        alt: 'MassKara 2023 Exhibit location section showing festival-related destinations on circular map layouts',
        caption: 'The location guide highlights important places around Bacolod with map-based visuals and destination images to make the exhibit more informative.'
      },
      {
        src: masskaraFestivalHighlights,
        title: 'Festival highlights',
        alt: 'MassKara 2023 Exhibit highlights section with event cards for festival attractions and activities',
        caption: 'The highlights grid organizes featured events and experiences into a lively card layout that helps visitors browse the festival program quickly.'
      },
    ],
    stackIcons: [
      { name: 'HTML', cls: 'devicon-html5-plain' },
      { name: 'CSS', cls: 'devicon-css3-plain' },
      { name: 'JavaScript', cls: 'devicon-javascript-plain' },
      { name: 'GSAP', cls: 'devicon-greensock-plain' },
    ]
  },
  {
    id: 5,
    name: 'KOHI: Food and Beverage E-commerce',
    featured: false,
    expanded: false,
    tags: ['E-Commerce', 'Web App', 'Frontend'],
    role: 'Frontend Designer',
    summary: 'A highly visual food and beverage site for Kōhī, a Japanese coffees and teas brand showcasing specialty drinks, matcha, fruit teas, and desserts like Taiyaki.',
    visualBg: 'linear-gradient(135deg, #fff1f2 0%, #fce7f3 100%)',
    screenBg: '#fff8fb',
    accentColor: '#db2777',
    problem: 'Kōhī needed a web presence that made its menu feel appetizing, premium, and easy to explore while supporting an e-commerce-style product experience.',
    solution: 'Designed a visual front-end experience focused on product presentation, menu browsing, brand atmosphere, and clear pathways from discovery to purchase intent.',
    result: 'Created a more polished and appetizing storefront concept that highlighted the brand identity and made the menu easier for customers to understand.',
    challenge: 'Translating a food and beverage brand into a web interface that looked attractive while keeping product information readable and organized.',
    learned: 'Learned how much visual hierarchy, spacing, product imagery, and microcopy matter when designing e-commerce pages for food and beverage brands.',
    gallery: [
      {
        src: kohiMenuDuo,
        title: 'Dessert and drink pairing',
        alt: 'KOHI product page showing taiyaki and green tea dessert visuals in a clean menu layout',
        caption: 'A product-focused composition pairing desserts with bold splashes and generous white space to keep the menu feeling premium and visual.'
      },
      {
        src: kohiProductCarousel,
        title: 'Homepage product carousel',
        alt: 'KOHI homepage carousel featuring multiple drinks and desserts with large product photography',
        caption: 'This wider carousel view shows how the site presents multiple signature items at once while keeping the brand identity front and center.'
      },
      {
        src: kohiCoffeeShowcase,
        title: 'Coffee showcase',
        alt: 'KOHI menu section featuring strawberry genma coffee and traditional Japanese coffee',
        caption: 'A cleaner two-product layout focused on coffee offerings, using large imagery and minimal text to keep the products as the main attraction.'
      },
      {
        src: kohiTeaFruitShowcase,
        title: 'Tea and fruit drink showcase',
        alt: 'KOHI menu section featuring yuzu fruit tea and green tea drink options',
        caption: 'This section highlights lighter drink options and keeps the same playful splash treatment across the menu experience.'
      },
    ],
    stackIcons: [
      { name: 'HTML', cls: 'devicon-html5-plain' },
      { name: 'CSS', cls: 'devicon-css3-plain' },
      { name: 'JavaScript', cls: 'devicon-javascript-plain' },
      { name: 'PHP', cls: 'devicon-php-plain' },
    ]
  },
])

const filteredProjects = computed(() => {
  if (activeFilter.value === 'All') return projects
  return projects.filter((project) => project.tags.includes(activeFilter.value))
})

const activeGalleryImage = computed(() => galleryProject.value?.gallery?.[activeGalleryIndex.value])

const openGallery = (project) => {
  if (!project.gallery?.length) return
  galleryProject.value = project
  activeGalleryIndex.value = 0
}

const closeGallery = () => {
  galleryProject.value = null
  activeGalleryIndex.value = 0
}

const showPreviousImage = () => {
  if (!galleryProject.value?.gallery?.length) return
  activeGalleryIndex.value =
    (activeGalleryIndex.value - 1 + galleryProject.value.gallery.length) % galleryProject.value.gallery.length
}

const showNextImage = () => {
  if (!galleryProject.value?.gallery?.length) return
  activeGalleryIndex.value = (activeGalleryIndex.value + 1) % galleryProject.value.gallery.length
}
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

.project-visual {
  position: relative;
  height: 220px;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}
.project-card.featured .project-visual { height: auto; min-height: 300px; }
.project-visual.has-gallery {
  cursor: pointer;
  padding: 32px;
}
.project-visual.has-gallery:focus-visible {
  outline: 3px solid var(--color-accent);
  outline-offset: -6px;
}
.project-card.featured .project-visual.has-gallery { min-height: 380px; }

.project-gallery-preview {
  width: min(92%, 520px);
  min-height: 310px;
  display: grid;
  grid-template-columns: 0.88fr 0.78fr;
  gap: 12px;
  align-items: stretch;
  transition: transform 0.25s ease;
}
.project-gallery-preview.single {
  width: min(88%, 420px);
  grid-template-columns: 1fr;
}
.project-gallery-preview.single .gallery-shot.primary {
  min-height: 310px;
}
.project-visual.has-gallery:hover .project-gallery-preview {
  transform: translateY(-4px);
}
.gallery-shot {
  background: var(--color-surface);
  border: 1px solid rgba(255, 255, 255, 0.75);
  border-radius: 18px;
  overflow: hidden;
  box-shadow: var(--shadow-lg);
}
.gallery-shot img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top center;
}
.gallery-side-stack {
  display: grid;
  grid-template-rows: 1fr 1fr;
  gap: 12px;
}
.gallery-open-badge {
  position: absolute;
  right: 18px;
  bottom: 18px;
  display: inline-flex;
  align-items: center;
  gap: 7px;
  padding: 8px 12px;
  background: rgba(26, 25, 23, 0.86);
  color: #fff;
  border-radius: 100px;
  font-size: 0.8125rem;
  font-weight: 600;
  box-shadow: var(--shadow-md);
}

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
  width: 8px;
  height: 8px;
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
  background: rgba(0, 0, 0, 0.07);
  border-radius: 4px;
}
.screen-row:last-child { width: 60%; }
.screen-sidebar {
  width: 28px;
  margin-top: 22px;
  background: rgba(0, 0, 0, 0.06);
  border-radius: 4px;
}

.project-overlay {
  position: absolute;
  inset: 0;
  background: rgba(10, 10, 10, 0.6);
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
  margin-bottom: 10px;
}
.project-summary {
  font-size: 0.9rem;
  color: var(--color-text-muted);
  line-height: 1.6;
  margin-bottom: 16px;
}
.gallery-body-btn {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  padding: 9px 14px;
  margin-bottom: 16px;
  background: var(--color-text);
  color: var(--color-bg);
  border-radius: 100px;
  font-size: 0.8125rem;
  font-weight: 600;
  transition: transform 0.2s, box-shadow 0.2s, background 0.2s;
}
.gallery-body-btn:hover {
  background: #2d2b28;
  transform: translateY(-1px);
  box-shadow: var(--shadow-sm);
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
.detail-icon {
  width: 16px;
  height: 16px;
  color: var(--color-accent);
  flex-shrink: 0;
  margin-top: 2px;
}
.detail-row strong {
  display: block;
  font-weight: 600;
  font-size: 0.8125rem;
  margin-bottom: 2px;
}
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
  align-items: flex-start;
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
  padding-top: 5px;
  flex-shrink: 0;
}
.stack-icons {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  align-items: center;
}
.stack-chip {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  padding: 4px 9px;
  background: var(--color-bg);
  border: 1px solid var(--color-border);
  border-radius: 100px;
  font-size: 0.75rem;
  font-weight: 500;
  color: var(--color-text-muted);
}
.stack-icon {
  font-size: 1rem;
  opacity: 0.8;
  transition: opacity 0.15s;
}
.stack-chip:hover .stack-icon { opacity: 1; }

.gallery-modal {
  position: fixed;
  inset: 0;
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
  background: rgba(26, 25, 23, 0.68);
  backdrop-filter: blur(6px);
}
.gallery-dialog {
  width: min(1040px, 100%);
  max-height: 92vh;
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-hover);
  overflow: hidden;
  display: flex;
  flex-direction: column;
}
.gallery-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  padding: 18px 22px;
  border-bottom: 1px solid var(--color-border);
}
.gallery-kicker {
  font-size: 0.6875rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-accent);
  margin-bottom: 2px;
}
.gallery-header h3 {
  font-family: var(--font-display);
  font-size: 1.25rem;
  line-height: 1.2;
}
.gallery-close {
  width: 38px;
  height: 38px;
  border-radius: 50%;
  display: grid;
  place-items: center;
  color: var(--color-text-muted);
  background: var(--color-bg);
  border: 1px solid var(--color-border);
  flex-shrink: 0;
  transition: color 0.15s, border-color 0.15s;
}
.gallery-close:hover {
  color: var(--color-text);
  border-color: var(--color-text);
}
.gallery-stage {
  position: relative;
  min-height: 430px;
  padding: 20px 68px;
  background: var(--color-surface-alt);
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}
.gallery-stage img {
  max-width: 100%;
  max-height: 62vh;
  object-fit: contain;
  background: #fff;
  border-radius: 14px;
  box-shadow: var(--shadow-lg);
}
.gallery-nav {
  position: absolute;
  top: 50%;
  width: 42px;
  height: 42px;
  transform: translateY(-50%);
  border-radius: 50%;
  display: grid;
  place-items: center;
  background: rgba(255, 255, 255, 0.92);
  color: var(--color-text);
  border: 1px solid var(--color-border);
  box-shadow: var(--shadow-sm);
  transition: transform 0.15s, border-color 0.15s;
}
.gallery-nav:hover {
  border-color: var(--color-accent);
  transform: translateY(-50%) scale(1.04);
}
.gallery-nav.prev { left: 18px; }
.gallery-nav.next { right: 18px; }
.gallery-footer {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 18px;
  padding: 16px 22px;
  border-top: 1px solid var(--color-border);
}
.gallery-footer strong {
  display: block;
  font-size: 0.95rem;
  margin-bottom: 3px;
}
.gallery-footer p {
  max-width: 720px;
  color: var(--color-text-muted);
  font-size: 0.875rem;
  line-height: 1.5;
}
.gallery-footer span {
  font-size: 0.8125rem;
  font-weight: 700;
  color: var(--color-text-faint);
  white-space: nowrap;
}
.gallery-thumbs {
  display: flex;
  gap: 10px;
  padding: 0 22px 22px;
  overflow-x: auto;
}
.gallery-thumb {
  width: 96px;
  height: 64px;
  padding: 0;
  border-radius: 10px;
  overflow: hidden;
  border: 2px solid transparent;
  background: var(--color-bg);
  flex: 0 0 auto;
}
.gallery-thumb.active {
  border-color: var(--color-accent);
}
.gallery-thumb img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top center;
}

@media (max-width: 840px) {
  .project-card.featured { grid-template-columns: 1fr; }
  .projects-grid { grid-template-columns: 1fr; }
  .project-card.featured .project-visual.has-gallery { min-height: 340px; }
  .project-gallery-preview {
    width: min(100%, 420px);
    min-height: 260px;
  }
  .gallery-modal { padding: 14px; }
  .gallery-stage {
    min-height: 360px;
    padding: 18px 54px;
  }
  .gallery-footer {
    flex-direction: column;
    gap: 8px;
  }
}
@media (max-width: 560px) {
  .project-visual.has-gallery { padding: 24px 18px; }
  .project-gallery-preview {
    grid-template-columns: 1fr;
    min-height: auto;
  }
  .gallery-side-stack {
    grid-template-columns: 1fr 1fr;
    grid-template-rows: none;
  }
  .gallery-shot.primary { height: 240px; }
  .gallery-side-stack .gallery-shot { height: 120px; }
  .gallery-stage {
    min-height: 300px;
    padding: 16px;
  }
  .gallery-nav {
    top: auto;
    bottom: 14px;
    transform: none;
  }
  .gallery-nav:hover { transform: scale(1.04); }
  .gallery-nav.prev { left: 16px; }
  .gallery-nav.next { right: 16px; }
  .gallery-header { padding: 16px; }
  .gallery-footer { padding: 14px 16px; }
  .gallery-thumbs { padding: 0 16px 16px; }
}
</style>
