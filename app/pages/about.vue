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

    // Vanta background effect
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


onUnmounted(() => {
  if (vantaEffect) vantaEffect.destroy()
})

const url = useRequestURL()


const title = 'About | Gian Jalandoni'
const description =
  'Learn more about Gian Jalandoni and his background.'


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
})




</script>

<template>
  <div>
    <!-- Background element referenced by Vue ref -->
    <div id="background" ref="vantaContainer"></div>

    <!-- Main Navigation Header -->
    
<!-- Main Navigation Header -->
<header id="Navigator">

  <!-- Logo -->
  <NuxtLink to="/" class="logo">GCJ</NuxtLink>

  <!-- Desktop Navigation -->
  <nav id="Nav">
    <NuxtLink to="/about">About</NuxtLink>
    <NuxtLink to="/certificates">Certifications</NuxtLink>
    <NuxtLink to="/tech-stack">Tech Stack</NuxtLink>
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

    <NuxtLink to="/about" @click="isMenuOpen = false">
      About
    </NuxtLink>

    <NuxtLink to="/certificates" @click="isMenuOpen = false">
      Certifications
    </NuxtLink>

    <NuxtLink to="/tech-stack" @click="isMenuOpen = false">
      Tech Stack
    </NuxtLink>

  </nav>

</header>


    <!-- About -->
    <section class="about-page">
      <h2 id="title">About Me</h2>

      <div class="about-text">
        <p>
          Hi! I'm Gian Jalandoni. Growing up, I always loved art and drawing, but over time, I became interested in systems and programs and eventually pursued the field of Information Technology.
          Even though I entered IT, my passion for creativity stayed with me and now inspires the way I design and develop projects.
        </p>
        <p>
          I enjoy designing clean and creative user interfaces for websites and applications.
          I want to continue developing projects that will allow me to improve both my creativity,
          problem-solving and coding abilities. I want to experiment with different layouts, styles,
          and interactive features to make fun projects. Learning new concepts and methods is what motivates
          me to continue improving every day.
        </p>
      </div>
    </section>
  </div>
</template>

<style scoped>
</style>