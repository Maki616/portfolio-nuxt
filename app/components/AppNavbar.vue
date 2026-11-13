<script setup>
import { ref } from 'vue'

const isMenuOpen = ref(false)

const links = [
  { label: 'About', to: '/about' },
  { label: 'Certifications', to: '/certificates' },
  { label: 'Tech Stack', to: '/tech-stack' },
]
</script>

<template>
  <header class="navbar portfolio-navbar">
    <div class="navbar-start">
      <NuxtLink to="/" class="site-logo">GCJ</NuxtLink>
    </div>

    <div class="navbar-end gap-2">
      <ul class="menu menu-horizontal hidden gap-1 lg:flex">
        <li v-for="link in links" :key="link.to">
          <NuxtLink :to="link.to">{{ link.label }}</NuxtLink>
        </li>
      </ul>

      <div
        class="dropdown dropdown-end mobile-menu-dropdown lg:hidden"
        :class="{ 'dropdown-open': isMenuOpen }"
      >
        <button
          type="button"
          class="btn btn-ghost btn-circle"
          :aria-expanded="isMenuOpen"
          aria-label="Toggle navigation"
          @click="isMenuOpen = !isMenuOpen"
        >
          <svg
            v-if="!isMenuOpen"
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
          <svg
            v-else
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18 18 6M6 6l12 12" />
          </svg>
        </button>

        <ul
          v-if="isMenuOpen"
          class="menu dropdown-content mobile-menu-panel z-20 items-center rounded-box border border-base-content/15 bg-base-200 p-3 text-center shadow-xl"
        >
          <li v-for="link in links" :key="link.to">
            <NuxtLink :to="link.to" @click="isMenuOpen = false">
              {{ link.label }}
            </NuxtLink>
          </li>
        </ul>
      </div>
    </div>
  </header>
</template>
