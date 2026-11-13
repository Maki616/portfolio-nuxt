<script setup>
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

const url = useRequestURL()
const title = 'Tech Stack | Gian Jalandoni'
const description =
  'Tech Stack used by Gian Jalandoni in his projects and development work.'
const image = `${url.origin}/images/profile.jpg`

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
  ogImageAlt: 'Gian Jalandoni Personal Portfolio',
})
</script>

<template>
  <div data-theme="black">
    <PageBackground />
    <AppNavbar />

    <section class="techstack">
      <h2>Tech Stack</h2>

      <div class="tech-container">
        <PortfolioCard
          v-for="technology in technologies"
          :key="technology.name"
          :title="technology.name"
          title-tag="h3"
          class="tech-card"
          body-class="items-center text-center"
        >
          <template #media>
            <img
              :src="technology.image"
              :alt="technology.name"
              class="mt-6 h-16 w-16 object-contain"
            >
          </template>
        </PortfolioCard>
      </div>
    </section>
  </div>
</template>
