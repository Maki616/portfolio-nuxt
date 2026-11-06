<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const vantaContainer = ref(null)
let vantaEffect = null

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


const technologies = [
  {
    name: 'Java',
    image: '/images/Java.png'
  },
  {
    name: 'C',
    image: '/images/C_Programming_Language.png'
  },
  {
    name: 'HTML',
    image: '/images/HTML.webp'
  },
  {
    name: 'CSS',
    image: '/images/CSS.webp'
  },
  {
    name: 'JavaScript',
    image: '/images/javascript.png'
  },
  {
    name: 'PostgreSQL',
    image: '/images/Postgresql_elephant.png'
  },
  {
    name: 'Git',
    image: '/images/Git.webp'
  },
  {
    name: 'GitHub',
    image: '/images/github-white-icon.webp'
  },
  {
    name: 'VS Code',
    image: '/images/vscode.webp'
  }
]
</script>

<template>
  <div>
    <div id="background" ref="vantaContainer"></div>

    <header id="Navigator">
      <NuxtLink to="/" class="logo">GCJ</NuxtLink>
      <nav id="Nav">
        <NuxtLink to="/about">About</NuxtLink>
        <NuxtLink to="/certificates">Certificates</NuxtLink>
        <NuxtLink to="/tech-stack">Tech Stack</NuxtLink>
      </nav>
    </header>

    <section class="techstack">

      <h2>Tech Stack</h2>

      <div class="tech-container">

        <div
          v-for="technology in technologies"
          :key="technology.name"
          class="tech-card"
        >
          <img
            :src="technology.image"
            :alt="technology.name"
          >

          <p>{{ technology.name }}</p>
        </div>

      </div>

    </section>
  </div>
</template>
