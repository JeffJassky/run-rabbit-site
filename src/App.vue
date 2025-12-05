<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const sectionId = {
  HERO: 'hero',
  TRAILER: 'trailer',
  SYNOPSIS: 'synopsis',
  CREDITS: 'credits',
  CONTACT: 'contact',
}

const navItems = [
  { label: 'Trailer', href: `#${sectionId.TRAILER}` },
  { label: 'Story', href: `#${sectionId.SYNOPSIS}` },
  { label: 'Team', href: `#${sectionId.CREDITS}` },
  { label: 'Contact', href: `#${sectionId.CONTACT}` },
]

const isOpen = ref(false)
const scrolled = ref(false)
const currentYear = new Date().getFullYear()

const toggleMenu = () => {
  isOpen.value = !isOpen.value
}

const closeMenu = () => {
  isOpen.value = false
}

const handleScroll = () => {
  scrolled.value = window.scrollY > 50
}

onMounted(() => {
  handleScroll()
  window.addEventListener('scroll', handleScroll)
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <div
    class="min-h-screen bg-prison text-off-black selection:bg-off-black selection:text-prison overflow-x-hidden"
  >
    <nav
      :class="[
        'fixed top-0 left-0 w-full z-50 transition-all duration-300',
        scrolled ? 'py-4 bg-prison/95 backdrop-blur-sm shadow-md' : 'py-6 bg-transparent',
      ]"
    >
      <div class="container mx-auto px-6 flex justify-between items-center">
        <a
          href="#"
          class="font-lexend font-black text-2xl tracking-tighter text-off-black z-50 hover:opacity-80 transition-opacity"
        >
          CARCOSA
        </a>

        <div class="hidden md:flex space-x-8">
          <a
            v-for="item in navItems"
            :key="item.label"
            :href="item.href"
            class="font-mono font-bold text-off-black hover:bg-off-black hover:text-off-white px-2 py-1 transition-all uppercase text-sm tracking-wider"
          >
            {{ item.label }}
          </a>
        </div>

        <button
          type="button"
          @click="toggleMenu"
          class="md:hidden text-off-black z-50 focus:outline-none"
          aria-label="Toggle menu"
        >
          <svg
            v-if="isOpen"
            xmlns="http://www.w3.org/2000/svg"
            width="32"
            height="32"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <line x1="18" y1="6" x2="6" y2="18" />
            <line x1="6" y1="6" x2="18" y2="18" />
          </svg>
          <svg
            v-else
            xmlns="http://www.w3.org/2000/svg"
            width="32"
            height="32"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <line x1="4" y1="6" x2="20" y2="6" />
            <line x1="4" y1="12" x2="20" y2="12" />
            <line x1="4" y1="18" x2="20" y2="18" />
          </svg>
        </button>

        <div
          :class="[
            'fixed inset-0 bg-prison flex flex-col items-center justify-center space-y-8 transition-transform duration-300 ease-in-out transform md:hidden',
            isOpen ? 'translate-x-0' : 'translate-x-full',
          ]"
        >
          <a
            v-for="item in navItems"
            :key="item.label"
            :href="item.href"
            @click="closeMenu"
            class="font-syne font-bold text-4xl text-off-black hover:text-white transition-colors"
          >
            {{ item.label }}
          </a>
        </div>
      </div>
    </nav>

    <main>
      <section
        :id="sectionId.HERO"
        class="min-h-screen flex flex-col items-center justify-center pt-20 pb-10 px-4 relative overflow-hidden"
      >
        <div
          class="absolute -bottom-[0%] -right-[20%] md:-right-[10%] w-[80vw] md:w-[35vw] pointer-events-none select-none z-0 rotate-12"
        >
          <img
            src="/prison-bracelet.png"
            alt="Prison Bracelet"
            class="w-full h-auto object-contain drop-shadow-2xl"
          />
        </div>
        <div
          class="hidden md:block absolute left-0 top-1/2 -translate-y-1/2 -rotate-90 origin-center z-20"
        >
          <span
            :class="['inline-block font-mono bg-off-black text-off-white px-2 py-1 uppercase tracking-wide', 'text-sm tracking-[0.2em]']"
            style="color:#ff5400; margin-left: -6rem;"
            >Prisoner #92-8312</span
          >
        </div>

        <div class="text-center z-10 max-w-full w-full relative">
          <h1
            class="font-syne font-extrabold text-[9vw] leading-[0.8] tracking-tighter text-off-black select-none pointer-events-none drop-shadow-xl w-full text-center"
          >
            RUN RABBIT
          </h1>

          <div class="mt-8 md:mt-12 flex flex-col items-center space-y-8">
            <span
              :class="['inline-block font-mono bg-off-black text-off-white px-2 py-1 uppercase font-bold tracking-wide', 'text-lg md:text-2xl px-4 py-2 rotate-1']"
              >Rebel with a cause</span
            >

            <a
              :href="`#${sectionId.TRAILER}`"
              class="group relative inline-flex items-center justify-center px-8 py-3 overflow-hidden font-bold transition duration-300 ease-out hover:-translate-y-1"
            >
              <span
                class="absolute inset-0 w-full h-full group-hover:opacity-100 transition-opacity"
              ></span>
              <span
                class="relative flex items-center gap-3 font-mono text-sm md:text-base tracking-widest uppercase"
              >
                <span>Watch Trailer</span>
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="16"
                  height="16"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <polygon points="5 3 19 12 5 21 5 3"></polygon>
                </svg>
              </span>
            </a>
          </div>
        </div>

        <div class="absolute bottom-10 animate-bounce z-20">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="text-off-black"
          >
            <path d="M7 13l5 5 5-5M7 6l5 5 5-5" />
          </svg>
        </div>
      </section>

      <section
        :id="sectionId.TRAILER"
        class="py-20 px-4 md:px-8 border-t-4 border-off-black relative overflow-visible"
      >
        <div
          class="absolute bottom-[-23%] md:bottom-[-22%] -left-[10%] w-[70vw] md:w-[35vw] pointer-events-none select-none z-0 -rotate-12"
        >
          <img
            src="/mallo-cups.webp"
            alt="Mallo Cup"
            class="w-full h-auto object-contain drop-shadow-2xl"
          />
        </div>

        <div class="container mx-auto max-w-6xl relative z-10">
          <div class="mb-8 flex items-end gap-4">
            <h2
              class="font-syne font-black text-4xl md:text-6xl text-off-black uppercase leading-none"
            >
              Trailer
            </h2>
            <div class="h-2 bg-off-black flex-grow mb-2 md:mb-3"></div>
          </div>

          <div
            class="relative w-full aspect-video bg-off-black shadow-2xl border-off-black"
          >
            <iframe
              src="https://player.vimeo.com/video/1140979814?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479"
              frameborder="0"
              allow="autoplay; fullscreen; picture-in-picture; clipboard-write"
              title="Benji - Trailer"
              class="absolute top-0 left-0 w-full h-full"
            ></iframe>
          </div>

          <div class="mt-12 flex justify-center">
            <a
              href="#"
              @click.prevent="() => {}"
              class="inline-block border-4 border-off-black bg-white text-off-black font-syne font-bold text-xl md:text-3xl px-8 py-4 uppercase hover:bg-off-black hover:text-white transition-colors duration-300 transform hover:-translate-y-1 shadow-[8px_8px_0px_0px_rgba(18,18,18,1)]"
            >
              Watch Full Film
            </a>
          </div>
          <p class="text-center mt-4 font-mono text-xs opacity-60 uppercase">
            Coming Soon to Festivals
          </p>
        </div>
      </section>

      <div class="flex flex-col">
        <section
          :id="sectionId.SYNOPSIS"
          class="py-24 px-4 md:px-8 bg-off-black text-white"
        >
          <div class="container mx-auto max-w-4xl">
            <div class="mb-12 border-b-2 border-prison/30 pb-4">
              <h2
                class="font-syne font-black text-4xl md:text-6xl text-prison uppercase"
              >
                Synopsis
              </h2>
            </div>

            <div
              class="prose prose-lg md:prose-2xl prose-invert font-roboto font-light leading-relaxed"
            >
              <p>
                Benji breaks out of prison and begins a desperate chase to reach
                someone he loves before it's too late.
              </p>
              <p>
                With police closing in and old connections in his path, Benji
                fights to find out where this person ended up. His journey leads
                to a final encounter with police, where the truth behind his
                escape finally comes into view.
              </p>
            </div>
          </div>
        </section>

        <section class="flex flex-col md:flex-row border-t-4 border-off-black">
          <div
            :id="sectionId.CREDITS"
            class="flex-1 py-20 px-8 border-b-4 md:border-b-0 md:border-r-4 border-off-black bg-prison"
          >
            <div class="max-w-md mx-auto h-full flex flex-col">
              <div class="mb-8">
                <h3
                  class="font-syne font-bold text-3xl uppercase text-off-black border-b-4 border-off-black inline-block"
                >
                  Credits
                </h3>
              </div>
              <ul class="space-y-6 flex-grow font-roboto">
                <li
                  class="flex flex-col md:flex-row md:items-baseline justify-between border-b border-off-black/20 pb-2"
                >
                  <span
                    class="font-bold text-off-black uppercase tracking-wider"
                    >Production Co.</span
                  >
                  <span class="font-lexend font-black text-xl">CARCOSA</span>
                </li>
                <li
                  class="flex flex-col md:flex-row md:items-baseline justify-between border-b border-off-black/20 pb-2"
                >
                  <span
                    class="font-bold text-off-black uppercase tracking-wider"
                    >Written &amp; Directed By</span
                  >
                  <span class="font-mono">Adam Danger Smith</span>
                </li>
                <li
                  class="flex flex-col md:flex-row md:items-baseline justify-between border-b border-off-black/20 pb-2"
                >
                  <span
                    class="font-bold text-off-black uppercase tracking-wider"
                    >Starring</span
                  >
                  <span class="font-mono">Shane Ali</span>
                </li>
              </ul>
            </div>
          </div>

          <div
            :id="sectionId.CONTACT"
            class="flex-1 py-20 px-8 bg-white relative overflow-hidden"
          >
            <div
              class="max-w-md mx-auto relative z-10 h-full flex flex-col justify-center"
            >
              <h3 class="font-syne font-bold text-3xl mb-4 text-off-black">
                Festivals &amp; Screenings
              </h3>
              <p class="font-roboto text-gray-600 mb-8 leading-relaxed">
                For press kits, screener links, and festival programming
                inquiries, please contact our production team directly.
              </p>

              <a
                href="mailto:carcosaproductions@gmail.com"
                class="inline-block group"
              >
                <span
                  class="font-mono text-lg md:text-xl border-b-2 border-off-black pb-1 group-hover:bg-off-black group-hover:text-white transition-all"
                >
                  carcosaproductions@gmail.com
                </span>
              </a>
            </div>
          </div>
        </section>
      </div>
    </main>

    <footer
      class="py-8 bg-off-black text-white/50 text-center font-mono text-xs uppercase tracking-widest"
    >
      <div class="container mx-auto px-4">
        <p>
          &copy; {{ currentYear }} CARCOSA Productions. All Rights Reserved.
        </p>
      </div>
    </footer>
  </div>
</template>
