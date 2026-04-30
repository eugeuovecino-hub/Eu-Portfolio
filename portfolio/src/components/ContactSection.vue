<template>
  <section id="contact" class="contact-section">
    <div class="container">
      <div class="contact-layout">
        <div class="contact-left reveal">
          <h2 class="section-heading">Let's work<br /><em style="font-style:italic; color: var(--color-accent)">together.</em></h2>
          <p class="body-lg contact-sub">
            I'm open to full-time positions, freelance projects, and collaborations.
            Whether you have a role in mind or just want to say hi — my inbox is always open.
          </p>

          <div class="contact-links">
            <a
              v-for="link in contactLinks"
              :key="link.label"
              :href="link.href"
              :target="link.external ? '_blank' : undefined"
              class="contact-link-item"
            >
              <div class="contact-link-icon" :style="{ background: link.bg }">
                <span v-html="link.icon"></span>
              </div>
              <div class="contact-link-body">
                <div class="contact-link-label">{{ link.label }}</div>
                <div class="contact-link-val">{{ link.value }}</div>
              </div>
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="contact-link-arrow"><path d="M5 12h14"/><path d="M12 5l7 7-7 7"/></svg>
            </a>
          </div>

          <div class="availability-badge">
            <span class="avail-dot"></span>
            <div>
              <strong>Available for opportunities</strong>
              <p>Based in Bacolod City — open to remote work</p>
            </div>
          </div>
        </div>

        <div class="contact-right reveal reveal-delay-2">
          <div class="contact-form-card">
            <h3 class="form-title">Send a Message</h3>
            <p class="form-sub">I'll get back to you within 24–48 hours.</p>

            <div v-if="submitted" class="form-success">
              <div class="success-icon">✓</div>
              <h4>Message sent!</h4>
              <p>Thank you for reaching out. I'll reply as soon as I can.</p>
              <button class="btn btn-outline btn-sm" @click="submitted = false; resetForm()">Send another</button>
            </div>

            <form v-else class="contact-form" @submit.prevent="handleSubmit">
              <div class="form-row">
                <div class="form-group">
                  <label for="name">Name</label>
                  <input id="name" v-model="form.name" type="text" placeholder="Your name" required />
                </div>
                <div class="form-group">
                  <label for="email">Email</label>
                  <input id="email" v-model="form.email" type="email" placeholder="your@email.com" required />
                </div>
              </div>
              <div class="form-group">
                <label for="subject">Subject</label>
                <input id="subject" v-model="form.subject" type="text" placeholder="What's this about?" required />
              </div>
              <div class="form-group">
                <label for="message">Message</label>
                <textarea id="message" v-model="form.message" rows="5" placeholder="Tell me about your project or opportunity..." required></textarea>
              </div>
              <button type="submit" class="btn btn-primary submit-btn" :disabled="submitting">
                <svg v-if="!submitting" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
                <span v-if="submitting" class="spinner"></span>
                {{ submitting ? 'Sending...' : 'Send Message' }}
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, reactive } from 'vue'

const submitted = ref(false)
const submitting = ref(false)

const form = reactive({ name: '', email: '', subject: '', message: '' })

const resetForm = () => { form.name = ''; form.email = ''; form.subject = ''; form.message = '' }

const handleSubmit = async () => {
  submitting.value = true
  await new Promise(r => setTimeout(r, 1200))
  submitting.value = false
  submitted.value = true
}

const contactLinks = [
  {
    label: 'Email',
    value: 'eugeuovec.professional@gmail.com',
    href: 'mailto:eugeuovec.professional@gmail.com',
    external: false,
    bg: '#fff1f2',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#ef4444" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>`
  },
  {
    label: 'LinkedIn',
    value: 'linkedin.com/in/eu-geuo-vecino',
    href: 'https://www.linkedin.com/in/eu-geuo-vecino-a64a83406/',
    external: true,
    bg: '#eef2ff',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="#0a66c2"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/><rect x="2" y="9" width="4" height="12"/><circle cx="4" cy="4" r="2"/></svg>`
  },
  {
    label: 'GitHub',
    value: 'github.com/eugeuovecino-hub',
    href: 'https://github.com/eugeuovecino-hub',
    external: true,
    bg: '#f3f4f6',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/></svg>`
  },
  {
    label: 'Phone (optional)',
    value: '+63 991 949 0401',
    href: 'tel:+639919490401',
    external: false,
    bg: '#f0fdf4',
    icon: `<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#16a34a" stroke-width="2"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.69 13a19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 3.6 2h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"/></svg>`
  },
]
</script>

<style scoped>
.contact-section { background: var(--color-surface-alt); }
.contact-layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 64px;
  align-items: start;
}
.contact-sub { color: var(--color-text-muted); margin-bottom: 36px; margin-top: 16px; }

.contact-links {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 36px;
}
.contact-link-item {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 14px 18px;
  background: var(--color-surface);
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-md);
  text-decoration: none;
  transition: border-color 0.15s, transform 0.15s;
}
.contact-link-item:hover {
  border-color: var(--color-accent);
  transform: translateX(3px);
}
.contact-link-icon {
  width: 40px;
  height: 40px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.contact-link-body { flex: 1; }
.contact-link-label { font-size: 0.75rem; font-weight: 600; text-transform: uppercase; letter-spacing: 0.08em; color: var(--color-text-faint); }
.contact-link-val { font-size: 0.9rem; font-weight: 500; color: var(--color-text); }
.contact-link-arrow { color: var(--color-text-faint); flex-shrink: 0; }

.availability-badge {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 16px 20px;
  background: #edfaf3;
  border: 1px solid #c6f0d8;
  border-radius: var(--radius-md);
}
.avail-dot {
  width: 10px;
  height: 10px;
  background: #2ecc71;
  border-radius: 50%;
  flex-shrink: 0;
  animation: pulse 2s ease-in-out infinite;
}
@keyframes pulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:.6;transform:scale(.85)} }
.availability-badge strong { font-size: 0.9rem; color: #1a7a46; display: block; }
.availability-badge p { font-size: 0.8125rem; color: #2d9d5e; margin-top: 2px; }

/* Form */
.contact-form-card {
  background: var(--color-surface);
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: 32px;
}
.form-title {
  font-family: var(--font-display);
  font-size: 1.4rem;
  font-weight: 700;
  margin-bottom: 4px;
}
.form-sub { font-size: 0.875rem; color: var(--color-text-muted); margin-bottom: 28px; }

.contact-form { display: flex; flex-direction: column; gap: 18px; }
.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
.form-group { display: flex; flex-direction: column; gap: 6px; }
.form-group label {
  font-size: 0.8125rem;
  font-weight: 600;
  color: var(--color-text);
}
.form-group input,
.form-group textarea {
  width: 100%;
  padding: 11px 14px;
  border: 1.5px solid var(--color-border);
  border-radius: var(--radius-md);
  font-family: var(--font-body);
  font-size: 0.9375rem;
  background: var(--color-bg);
  color: var(--color-text);
  transition: border-color 0.15s, box-shadow 0.15s;
  outline: none;
  resize: vertical;
}
.form-group input:focus,
.form-group textarea:focus {
  border-color: var(--color-accent);
  box-shadow: 0 0 0 3px rgba(26,92,255,0.1);
}
.submit-btn {
  width: 100%;
  justify-content: center;
}
.submit-btn:disabled { opacity: 0.65; cursor: not-allowed; transform: none !important; }
.spinner {
  width: 14px; height: 14px;
  border: 2px solid rgba(255,255,255,0.4);
  border-top-color: white;
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }

.form-success {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 10px;
  padding: 32px 0;
}
.success-icon {
  width: 52px;
  height: 52px;
  border-radius: 50%;
  background: #edfaf3;
  color: #16a34a;
  font-size: 1.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid #c6f0d8;
}
.form-success h4 { font-family: var(--font-display); font-size: 1.25rem; font-weight: 700; }
.form-success p { font-size: 0.875rem; color: var(--color-text-muted); }

@media (max-width: 900px) {
  .contact-layout { grid-template-columns: 1fr; gap: 40px; }
  .form-row { grid-template-columns: 1fr; }
}
</style>
