<script setup>
const url = useRequestURL()
const title = 'About | Gian Jalandoni'
const description =
  'Learn more about Gian Jalandoni and his background.'
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

    <section class="about-page">
      <h2 id="title">About Me</h2>

      <PortfolioCard class="about-card" body-class="about-text">
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
      </PortfolioCard>
    </section>
  </div>
</template>