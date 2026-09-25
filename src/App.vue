<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue'
import Card from './components/Card.vue'
import graduateIcon from './assets/icon/graduate-bachelor.svg'
import docIcon from './assets/icon/graduate-negdsen.svg'
import muisScript from './assets/muis_script.svg'
import uriaScript from './assets/uria_script.svg'
import bgPattern from './assets/bg-pattern.png'

type CardHandle = { root: HTMLElement | null } | null

const card1 = ref<CardHandle>(null)
const card2 = ref<CardHandle>(null)
const matchedHeight = ref<string | undefined>(undefined)

function syncCardHeights() {
  matchedHeight.value = undefined
  requestAnimationFrame(() => {
    const heights = [card1.value?.root?.offsetHeight, card2.value?.root?.offsetHeight].filter(
      (h): h is number => !!h,
    )
    if (heights.length < 2) return
    matchedHeight.value = `${Math.max(...heights)}px`
  })
}

let resizeTimeout: ReturnType<typeof setTimeout>
function onResize() {
  clearTimeout(resizeTimeout)
  resizeTimeout = setTimeout(syncCardHeights, 100)
}

onMounted(() => {
  syncCardHeights()
  window.addEventListener('resize', onResize)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', onResize)
  clearTimeout(resizeTimeout)
})
</script>

<template>
  <div class="relative flex min-h-screen flex-col overflow-hidden bg-slate-50 bg-repeat"
    :style="{ backgroundImage: `url(${bgPattern})` }">
    <header class="flex shrink-0 items-center justify-center">
      <div class="bg-primary p-3 pt-7.5 rounded-b-full">
        <img src="/logo.webp" alt="Монгол Улсын Их Сургууль" class="h-18 w-auto sm:h-24" />
      </div>
    </header>

    <main class="flex w-full flex-1 items-center  justify-evenly gap-2 p-2 sm:gap-4 sm:p-8">
      <img :src="muisScript" alt=""
        class="pointer-events-none hidden h-[85%] max-h-[700px] w-auto shrink-0 select-none opacity-90 lg:block"
        aria-hidden="true" />

      <div class="flex min-w-0 flex-wrap items-center justify-center gap-10 sm:gap-20">
        <Card ref="card1" :icon="graduateIcon" title="Бакалаврын өдрийн хөтөлбөрийн элсэлтийн систем"
          subtitle="Ерөнхий боловсролын сургуулийн төгсөгчид"
          href="https://burtgel.num.edu.mn/bachelor" :style="{ height: matchedHeight }" />
        <Card ref="card2" :icon="docIcon" title="Нэгдсэн бүртгэлийн систем"
          subtitle="Бакалаврын өдөр (элсэлтийн ерөнхий шалгалтын оноо шаардахгүй), бакалаврын орой, бакалаврын эчнээ, магистр, докторын хөтөлбөрийн элсэлт эсвэл бүх түвшний хөтөлбөрийн шилжилтийн үйл ажиллагаа"
          href="https://burtgel.num.edu.mn/negdsen" :style="{ height: matchedHeight }" />
      </div>

      <img :src="uriaScript" alt=""
        class="pointer-events-none hidden h-[70%] max-h-[700px] w-auto shrink-0 select-none opacity-90 lg:block"
        aria-hidden="true" />
    </main>

    <footer class="flex shrink-0 flex-col items-center gap-4 px-4 pb-6">
      <div class="flex gap-4">
        <a href="https://www.facebook.com/www.num.edu.mn" aria-label="Facebook" target="_blank" rel="noopener"
          class="grid h-10 w-10 place-items-center rounded-full bg-primary text-white transition-transform duration-200 hover:-translate-y-[3px] hover:shadow-[0_6px_14px_rgba(15,63,143,0.25)]">
          <svg class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"
            stroke-linecap="round" stroke-linejoin="round">
            <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z" />
          </svg>
        </a>
        <a href="https://www.instagram.com/num_1942" aria-label="Instagram" target="_blank" rel="noopener"
          class="grid h-10 w-10 place-items-center rounded-full bg-primary text-white transition-transform duration-200 hover:-translate-y-[3px] hover:shadow-[0_6px_14px_rgba(15,63,143,0.25)]">
          <svg class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"
            stroke-linecap="round" stroke-linejoin="round">
            <rect x="2" y="2" width="20" height="20" rx="5" ry="5" />
            <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z" />
            <line x1="17.5" y1="6.5" x2="17.51" y2="6.5" />
          </svg>
        </a>
        <a href="https://x.com/num_edu" aria-label="Twitter" target="_blank" rel="noopener"
          class="grid h-10 w-10 place-items-center rounded-full bg-primary text-white transition-transform duration-200 hover:-translate-y-[3px] hover:shadow-[0_6px_14px_rgba(15,63,143,0.25)]">
          <svg class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"
            stroke-linecap="round" stroke-linejoin="round">
            <path
              d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5a4.5 4.5 0 0 0-.08-.83A7.72 7.72 0 0 0 23 3z" />
          </svg>
        </a>
      </div>
      <p class="text-center text-xs text-secondary/80">
        © 2026 Монгол Улсын Их Сургууль. Бүх эрх хуулиар хамгаалагдсан.
      </p>
    </footer>
  </div>
</template>
