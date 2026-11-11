
<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

defineProps({
  error: Object
})

const handleError = () => {
  clearError({ redirect: '/' })
}

// Vanta background
const vantaBackground = ref(null)
let vantaEffect = null

// Load external scripts
const loadScript = (src) => {
  return new Promise((resolve, reject) => {
    const existingScript = document.querySelector(
      `script[src="${src}"]`
    )

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

// Initialize Vanta
onMounted(async () => {
  try {
    await loadScript(
      'https://cdn.jsdelivr.net/npm/three@0.134.0/build/three.min.js'
    )

    await loadScript(
      'https://cdn.jsdelivr.net/npm/vanta@0.5.24/dist/vanta.net.min.js'
    )

    if (window.VANTA && vantaBackground.value) {
      vantaEffect = window.VANTA.NET({
        el: vantaBackground.value,
        color: '#FFFFFF',
        backgroundColor: '#000000',

        // Disable cursor and touch interaction
        mouseControls: false,
        touchControls: false,
        gyroControls: false,

        minHeight: 200,
        minWidth: 200,
        scale: 1,
        scaleMobile: 1
      })
    }
  } catch (error) {
    console.error('Failed to load Vanta background scripts:', error)
  }
})

// Clean up Vanta when leaving the error page
onUnmounted(() => {
  if (vantaEffect) {
    vantaEffect.destroy()
    vantaEffect = null
  }
})
</script>

<template>
  <main class="error-page">

    <!-- Vanta Background -->
    <div
      ref="vantaBackground"
      class="error-background"
    ></div>

    <!-- Error Card -->
    <div class="error-card">

      <p class="error-label">GCJ | SYSTEM ERROR</p>

      <h1 class="error-code">
        {{ error?.statusCode || 404 }}
      </h1>

      <h2 class="error-title">
        Oops! Page Not Found.
      </h2>

      <p class="error-description">
        Looks like you've wandered into an unknown space.
        The page you're looking for doesn't exist or may have
        been moved.
      </p>

      <div class="error-divider"></div>

      <button class="home-button" @click="handleError">
        <span>←</span> Back to Home
      </button>

      <p class="error-footer">
        Gian Jalandoni · Portfolio
      </p>

    </div>

  </main>
</template>

<style scoped>
@import '@/assets/style.css';

.error-page {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  position: relative;
  overflow: hidden;
  background: #000;
  color: white;
  font-family: "M PLUS U", sans-serif;
}

/* Vanta Background */
.error-background {
  position: fixed;
  inset: 0;
  z-index: 0;
  pointer-events: none;
}

/* Error Card */
.error-card {
  position: relative;
  z-index: 1;
  width: 100%;
  max-width: 550px;
  padding: 55px 40px;
  text-align: center;

  background: rgba(255, 255, 255, 0.04);
  border: 1.5px solid rgba(255, 255, 255, 0.45);
  border-radius: 22px;

  backdrop-filter: blur(12px);

  box-shadow:
    0 0 20px rgba(255, 255, 255, 0.12),
    0 0 50px rgba(255, 255, 255, 0.05);
}

/* Label */
.error-label {
  font-size: 12px;
  letter-spacing: 4px;
  opacity: 0.6;
  margin-bottom: 15px;
}

/* Error Code */
.error-code {
  font-size: clamp(90px, 20vw, 150px);
  font-weight: 900;
  line-height: 1;
  margin: 0;
  letter-spacing: -8px;

  text-shadow:
    0 0 15px rgba(255, 255, 255, 0.25),
    0 0 40px rgba(255, 255, 255, 0.1);
}

/* Title */
.error-title {
  font-size: 24px;
  font-weight: 800;
  margin: 20px 0 12px;
}

/* Description */
.error-description {
  max-width: 390px;
  margin: 0 auto;
  font-size: 14px;
  line-height: 1.9;
  opacity: 0.7;
}

/* Divider */
.error-divider {
  width: 60px;
  height: 2px;
  background: white;
  margin: 30px auto;
  opacity: 0.5;
}

/* Home Button */
.home-button {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 13px 25px;

  background: white;
  color: #0a0a0a;

  border: 1px solid white;
  border-radius: 10px;

  font-family: inherit;
  font-size: 14px;
  font-weight: 800;

  cursor: pointer;
  transition: 0.3s ease;
}

.home-button:hover {
  background: transparent;
  color: white;
  box-shadow: 0 0 20px rgba(255, 255, 255, 0.2);
}

.home-button span {
  font-size: 18px;
}

/* Footer */
.error-footer {
  font-size: 11px;
  opacity: 0.4;
  margin: 35px 0 0;
  letter-spacing: 1px;
}

/* Mobile */
@media (max-width: 600px) {
  .error-card {
    padding: 45px 22px;
  }

  .error-title {
    font-size: 20px;
  }

  .error-description {
    font-size: 13px;
  }
}
</style>
