<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const background = ref(null)
let vantaEffect = null

function loadScript(src, globalName) {
  return new Promise((resolve, reject) => {
    if (window[globalName]) {
      resolve()
      return
    }

    const existingScript = document.querySelector(`script[src="${src}"]`)
    if (existingScript) {
      if (existingScript.dataset.loaded === 'true') {
        resolve()
      } else {
        existingScript.addEventListener('load', resolve, { once: true })
        existingScript.addEventListener('error', reject, { once: true })
      }
      return
    }

    const script = document.createElement('script')
    script.src = src
    script.async = true
    script.onload = () => {
      script.dataset.loaded = 'true'
      resolve()
    }
    script.onerror = reject
    document.head.appendChild(script)
  })
}

onMounted(async () => {
  try {
    await loadScript('https://cdn.jsdelivr.net/npm/three@0.134.0/build/three.min.js', 'THREE')
    await loadScript('https://cdn.jsdelivr.net/npm/vanta@0.5.24/dist/vanta.net.min.js', 'VANTA')

    if (window.VANTA && background.value) {
      vantaEffect = window.VANTA.NET({
        el: background.value,
        color: '#FFFFFF',
        backgroundColor: '#000000',
        mouseControls: true,
        touchControls: true,
        gyroControls: false,
        minHeight: 200,
        minWidth: 200,
        scale: 1,
        scaleMobile: 1,
      })
    }
  } catch (error) {
    console.error('Failed to load Vanta background scripts:', error)
  }
})

onUnmounted(() => {
  if (vantaEffect) {
    vantaEffect.destroy()
    vantaEffect = null
  }
})
</script>

<template>
  <div id="background" ref="background" aria-hidden="true"></div>
</template>
