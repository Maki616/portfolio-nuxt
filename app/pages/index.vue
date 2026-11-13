<script setup>
const url = useRequestURL()
const title = 'Home | Gian Jalandoni'
const description =
  'Welcome to the personal portfolio of Gian Jalandoni, an aspiring UI designer showcasing his skills, certifications, and tech stack.'
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

    <section class="main-page">
      <NuxtLink to="/about" class="card-link">
        <PortfolioCard
          title="Gian Jalandoni"
          title-tag="h1"
          title-class="name"
          class="profile-card"
          body-class="profile-card-body"
        >
          <template #media>
            <img src="/images/profile.jpg" alt="Profile Picture" class="profile-pic" />
          </template>
          <p class="subtitle">Aspiring UI Designer</p>
        </PortfolioCard>
      </NuxtLink>
    </section>
  </div>
</template>