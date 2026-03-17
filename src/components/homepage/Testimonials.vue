<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { GraduationCap, ChevronLeft, ChevronRight } from 'lucide-vue-next'
import { useThemeStore } from '@/stores/theme'
import { useLang } from '@/composables/useLang'
import testimonials from '@/assets/data/testimonials.js'

const themeStore = useThemeStore()
const { t, isBn } = useLang()

const currentPage = ref(0)
const itemsPerPage = ref(3)

const updateItemsPerPage = () => {
  if (window.innerWidth < 768) itemsPerPage.value = 1
  else if (window.innerWidth < 1024) itemsPerPage.value = 2
  else itemsPerPage.value = 3
}

const totalPages = computed(() => Math.ceil(testimonials.length / itemsPerPage.value))
const currentTestimonials = computed(() => {
  const start = currentPage.value * itemsPerPage.value
  return testimonials.slice(start, start + itemsPerPage.value)
})

const goToNextPage = () => (currentPage.value = (currentPage.value + 1) % totalPages.value)
const goToPreviousPage = () => (currentPage.value = (currentPage.value - 1 + totalPages.value) % totalPages.value)

const handleKeyDown = (e) => {
  if (e.key === 'ArrowLeft') goToPreviousPage()
  if (e.key === 'ArrowRight') goToNextPage()
}

onMounted(() => {
  updateItemsPerPage()
  window.addEventListener('resize', updateItemsPerPage)
  window.addEventListener('keydown', handleKeyDown)
})
onUnmounted(() => {
  window.removeEventListener('resize', updateItemsPerPage)
  window.removeEventListener('keydown', handleKeyDown)
})
</script>

<template>
  <section
    class="py-16 transition-colors duration-500"
    :class="themeStore.isDark
      ? 'bg-linear-to-br from-gray-900 via-gray-950 to-gray-900'
      : 'bg-linear-to-br from-blue-50 via-white to-purple-50'"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Title -->
      <div class="text-center mb-12">
        <h2
          class="text-4xl sm:text-5xl mb-3 font-bold transition-colors duration-300"
          :class="[
            themeStore.isDark ? 'text-white' : 'text-gray-900',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{ t('testimonialsTitle') }}
        </h2>
        <p
          class="text-base max-w-2xl mx-auto transition-colors duration-300"
          :class="[
            themeStore.isDark ? 'text-gray-400' : 'text-gray-600',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{ t('testimonialsSubtitle') }}
        </p>
        <div class="w-20 h-1 bg-linear-to-r from-blue-600 to-green-600 mx-auto mt-4"></div>
      </div>

      <!-- Navigation -->
      <div class="relative">
        <!-- Left -->
        <button
          @click="goToPreviousPage"
          class="absolute left-0 top-1/2 -translate-y-1/2 -translate-x-4 lg:-translate-x-12 w-10 h-10 lg:w-12 lg:h-12
                 rounded-full shadow-lg hover:shadow-xl flex items-center justify-center
                 border transition-all duration-300 hover:scale-110 z-10"
          :class="themeStore.isDark
            ? 'bg-gray-800 text-gray-300 hover:text-blue-400 border-gray-700'
            : 'bg-white text-gray-700 hover:text-blue-600 border-gray-200'"
        >
          <ChevronLeft class="w-5 h-5 lg:w-6 lg:h-6" />
        </button>

        <!-- Testimonials -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div
            v-for="testimonial in currentTestimonials"
            :key="testimonial.id"
            class="rounded-xl shadow-md hover:shadow-xl transition-all duration-300 p-6
                   border flex flex-col h-full"
            :class="themeStore.isDark
              ? 'bg-gray-800 border-gray-700'
              : 'bg-white border-gray-100'"
          >
            <!-- Profile -->
            <div class="flex justify-center mb-3 relative">
              <div
                class="w-16 h-16 rounded-full overflow-hidden shadow-md ring-2"
                :class="themeStore.isDark ? 'ring-blue-700' : 'ring-blue-100'"
              >
                <img
                  :src="testimonial.image"
                  :alt="testimonial.name[language]"
                  class="w-full h-full object-cover"
                />
              </div>
              <div
                class="absolute -bottom-1 -right-1 w-6 h-6 rounded-full flex items-center justify-center shadow-md"
                :class="themeStore.isDark
                  ? 'bg-linear-to-br from-blue-600 to-blue-800'
                  : 'bg-linear-to-br from-blue-200 to-blue-600'"
              >
                <GraduationCap class="w-3.5 h-3.5 text-white" />
              </div>
            </div>

            <!-- Name -->
            <h3
              class="text-center text-base mb-1 font-semibold transition-colors duration-300"
              :class="[
                themeStore.isDark ? 'text-gray-100' : 'text-gray-900',
                isBn ? 'bn-font' : ''
              ]"
            >
              {{ testimonial.name[isBn ? 'bn' : 'en'] }}
            </h3>
            <p
              class="text-center text-xs mb-2 transition-colors duration-300"
              :class="[
                themeStore.isDark ? 'text-gray-400' : 'text-gray-500',
                isBn ? 'bn-font' : ''
              ]"
            >
              {{ testimonial.institution[isBn ? 'bn' : 'en'] }}
            </p>
            <p
              class="text-center text-xs mb-3 transition-colors duration-300"
              :class="[
                themeStore.isDark ? 'text-blue-400' : 'text-blue-600',
                isBn ? 'bn-font' : ''
              ]"
            >
              {{ testimonial.year[isBn ? 'bn' : 'en'] }}
            </p>

            <!-- Quote -->
            <div
              class="relative mb-4 grow rounded-lg p-4 border-l-4"
              :class="[
                themeStore.isDark
                  ? 'bg-linear-to-br from-gray-700 to-gray-800 border-blue-400'
                  : 'bg-linear-to-br from-blue-50 to-blue-100 border-blue-500'
              ]"
            >
              <div class="absolute -top-1 -left-1 text-5xl leading-none font-serif"
                   :class="themeStore.isDark ? 'text-blue-600' : 'text-blue-400'"
              >"</div>
              <p
                class="text-center text-base font-bold italic leading-relaxed px-3 pt-2 transition-colors duration-300"
                :class="[
                  themeStore.isDark ? 'text-gray-100' : 'text-gray-900',
                  isBn ? 'bn-font' : ''
                ]"
              >
                {{ testimonial.quote[isBn ? 'bn' : 'en'] }}
              </p>
              <div class="absolute -bottom-2 -right-1 text-5xl leading-none font-serif rotate-180"
                   :class="themeStore.isDark ? 'text-blue-600' : 'text-blue-400'"
              ></div>
            </div>

            <!-- Session & ID -->
            <div
              class="pt-3 border-t flex flex-col items-center gap-1 text-xs"
              :class="themeStore.isDark ? 'border-gray-700' : 'border-gray-100'"
            >
              <span
                class="transition-colors duration-300"
                :class="[
                  themeStore.isDark ? 'text-gray-500' : 'text-gray-400',
                  isBn ? 'bn-font' : ''
                ]"
              >
                {{ testimonial.session[isBn ? 'bn' : 'en'] }}
              </span>
              <span
                class="font-bold transition-colors duration-300"
                :class="themeStore.isDark ? 'text-gray-200' : 'text-gray-800'"
              >
                {{ testimonial.quantaId }}
              </span>
            </div>
          </div>
        </div>

        <!-- Right -->
        <button
          @click="goToNextPage"
          class="absolute right-0 top-1/2 -translate-y-1/2 translate-x-4 lg:translate-x-12 w-10 h-10 lg:w-12 lg:h-12
                 rounded-full shadow-lg hover:shadow-xl flex items-center justify-center
                 border transition-all duration-300 hover:scale-110 z-10"
          :class="themeStore.isDark
            ? 'bg-gray-800 text-gray-300 hover:text-blue-400 border-gray-700'
            : 'bg-white text-gray-700 hover:text-blue-600 border-gray-200'"
        >
          <ChevronRight class="w-5 h-5 lg:w-6 lg:h-6" />
        </button>
      </div>

      <!-- Pagination Dots -->
      <div class="flex justify-center gap-2 mt-8">
        <button
          v-for="index in totalPages"
          :key="index"
          @click="currentPage = index - 1"
          :class="[
            'transition-all duration-300 rounded-full',
            currentPage === index - 1
              ? 'w-8 h-2 bg-linear-to-r from-blue-600 to-blue-400'
              : themeStore.isDark
                ? 'w-2 h-2 bg-gray-600 hover:bg-gray-500'
                : 'w-2 h-2 bg-gray-300 hover:bg-gray-400'
          ]"
        />
      </div>

      <!-- Footer Note -->
      <div class="mt-12 text-center">
        <p
          class="text-sm transition-colors duration-300"
          :class="[
            themeStore.isDark ? 'text-gray-400' : 'text-gray-500',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{
            isBn
              ? '💙 আরও অনেক কোয়ান্টা দেশ-বিদেশে সফলতার পথে এগিয়ে যাচ্ছে, তাদের অংশ হয়ে গর্বিত অনুভূতি জাগে।'
              : '💙 Many more Quantas are advancing toward success at home and abroad, evoking a sense of pride in being part of their journey'
          }}
        </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@400;600;700&display=swap');
.bn-font { font-family: 'Noto Sans Bengali', sans-serif; }
</style>