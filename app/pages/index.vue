<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const vantaContainer = ref(null)
let vantaEffect = null

// Hamburger Menu
const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

// Load external script
const loadScript = (src) => {
  return new Promise((resolve, reject) => {
    if (document.querySelector(`script[src="${src}"]`)) {
      resolve()
      return
    }
    const script = document.createElement('script')
    script.src = src
    script.onload = resolve
    script.onerror = reject
    document.head.appendChild(script)
  })
}

onMounted(async () => {
  try {

    await loadScript('https://cdn.jsdelivr.net/npm/three@0.134.0/build/three.min.js')
    await loadScript('https://cdn.jsdelivr.net/npm/vanta@0.5.24/dist/vanta.net.min.js')

    // 3. Initialize Vanta background effect
    if (window.VANTA && vantaContainer.value) {
      vantaEffect = window.VANTA.NET({
        el: vantaContainer.value,
        color: '#FFFFFF',
        backgroundColor: '#000000',
        mouseControls: true,
        touchControls: true,
        gyroControls: false,
        minHeight: 200.00,
        minWidth: 200.00,
        scale: 1.00,
        scaleMobile: 1.00
      })
    }
  } catch (error) {
    console.error('Failed to load Vanta background scripts:', error)
  }
})

// Clean up Vanta instance on unmount to prevent memory leaks
onUnmounted(() => {
  if (vantaEffect) vantaEffect.destroy()
})

const url = useRequestURL()


const title = 'Home | Gian Jalandoni'
const description =
  'Certifications earned by Gian Jalandoni: Word Associate, PowerPoint Associate'


useHead({
  title,
  link: [{ rel: 'canonical', href: url.href }],
})


useSeoMeta({
  description,
  ogTitle: title,
  ogDescription: description,
  ogType: 'website',
  ogUrl: url.href,
  ogImage: `${url.origin}/images/profile.jpg`, 
  ogImageAlt: 'Gian Jalandoni Personal Portfolio',
})

</script>

<template>
  <div>
    <!-- Background -->
    <div id="background" ref="vantaContainer"></div>

    <!-- Main Navigation Header -->
    <header id="Navigator">

  <!-- Logo -->
  <router-link to="/" class="logo">GCJ</router-link>

  <!-- Desktop Navigation -->
  <nav id="Nav" class="desktop-nav">
    <router-link to="/about">About</router-link>
    <router-link to="/certificates">Certifications</router-link>
    <router-link to="/tech-stack">Tech Stack</router-link>
  </nav>

  <!-- Hamburger Button -->
  <button
    class="hamburger"
    @click="toggleMenu"
    :aria-expanded="isMenuOpen"
    aria-label="Toggle navigation"
  >
    <span v-if="!isMenuOpen">☰</span>
    <span v-else>✕</span>
  </button>

  <!-- Mobile Navigation -->
  <nav v-if="isMenuOpen" class="mobile-nav">

    <router-link to="/about" @click="isMenuOpen = false">
      About
    </router-link>

    <router-link to="/certificates" @click="isMenuOpen = false">
      Certifications
    </router-link>

    <router-link to="/tech-stack" @click="isMenuOpen = false">
      Tech Stack
    </router-link>
  </nav>

</header>

    <!-- Main Profile Section -->
    <section class="main-page">
      <router-link to="/about" class="card-link">
        <div id="card-container">
          <div class="card">
            <img src="/images/profile.jpg" alt="Profile Picture" class="profile-pic" />
            <h1 class="name">Gian Jalandoni</h1>
            <p class="subtitle">Aspiring UI Designer</p>
          </div>
        </div>
      </router-link>
    </section>
  </div>
</template>

<style scoped>

@import '@/assets/style.css';
</style>