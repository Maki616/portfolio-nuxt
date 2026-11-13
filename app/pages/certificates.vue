
<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const vantaContainer = ref(null)
let vantaEffect = null
const selectedImage = ref(null)

// Hamburger Menu
const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const certificates = [
  {
    title: 'PowerPoint Associate',
    image: '/images/PPTCert.jpg',
    alt: 'PowerPoint Associate Certificate'
  },
  {
    title: 'MS Word Associate',
    image: '/images/WordCert.jpg',
    alt: 'MS Word Associate Certificate'
  }
]

function openModal(image) {
  selectedImage.value = image
}

function closeModal() {
  selectedImage.value = null
}

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


const title = 'Certifications | Gian Jalandoni'
const description =
  'Certifications earned by Gian Jalandoni: Word Associate, PowerPoint Associate'
const image = `${url.origin}/images/PPTCert.jpg`


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
  ogImage: image,
  ogImageAlt: 'Microsoft Office Specialist Word Associate badge',

})


</script>

<template>
  <div>
    <div id="background" ref="vantaContainer"></div>

   
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


    <section class="certifications">
      <h2>Certifications</h2>

      <div class="cert-grid">
        <div
          v-for="certificate in certificates"
          :key="certificate.title"
          class="cert-card"
        >
          <img
            :src="certificate.image"
            :alt="certificate.alt"
            class="cert-image"
            @click="openModal(certificate.image)"
          >

          <p class="cert-title">{{ certificate.title }}</p>

          <a
            href="https://www.certiport.com/portal/pages/credentialverification.aspx"
            target="_blank"
            rel="noopener noreferrer"
            class="cert-verify"
          >
            Verify Certification
          </a>
        </div>
      </div>
    </section>

    <div
      v-if="selectedImage"
      id="imageModal"
      @click="closeModal"
    >
      <img
        :src="selectedImage"
        id="modalImg"
        alt="Certificate Preview"
        @click.stop
      >
    </div>
  </div>
</template>
