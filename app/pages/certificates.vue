
<script setup>
import { ref } from 'vue'

const selectedImage = ref(null)

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
  ogImageAlt: 'Microsoft Office Specialist PowerPoint Associate certificate',
})
</script>

<template>
  <div data-theme="black">
    <PageBackground />
    <AppNavbar />

    <section class="certifications">
      <h2>Certifications</h2>

      <div class="cert-grid">
        <PortfolioCard
          v-for="certificate in certificates"
          :key="certificate.title"
          :title="certificate.title"
          title-tag="h3"
          class="cert-card"
          body-class="items-center gap-4 text-center"
        >
          <template #media>
            <button
              type="button"
              class="btn btn-ghost h-48 min-h-0 w-full rounded-none p-0"
              :aria-label="`Preview ${certificate.title} certificate`"
              @click="openModal(certificate.image)"
            >
              <img
                :src="certificate.image"
                :alt="certificate.alt"
                class="h-full w-full object-contain p-3"
              >
            </button>
          </template>

          <div class="card-actions justify-center">
            <a
              href="https://www.certiport.com/portal/pages/credentialverification.aspx"
              target="_blank"
              rel="noopener noreferrer"
              class="btn btn-outline btn-sm"
            >
              Verify Certification
            </a>
          </div>
        </PortfolioCard>
      </div>
    </section>

    <div
      v-if="selectedImage"
      class="modal modal-open"
      role="dialog"
      aria-modal="true"
      aria-label="Certificate preview"
      @click.self="closeModal"
      @keyup.esc="closeModal"
      tabindex="-1"
    >
      <div class="modal-box max-w-5xl p-4">
        <button
          type="button"
          class="btn btn-circle btn-ghost btn-sm absolute right-2 top-2"
          aria-label="Close certificate preview"
          @click="closeModal"
        >
          ✕
        </button>
        <img
          :src="selectedImage"
          alt="Certificate preview"
          class="mx-auto max-h-[80vh] max-w-full object-contain"
        >
      </div>
      <button
        type="button"
        class="modal-backdrop"
        aria-label="Close certificate preview"
        @click="closeModal"
      ></button>
    </div>
  </div>
</template>
