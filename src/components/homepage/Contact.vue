<template>
  <section id="contact" class="py-8 transition-colors duration-500"
    :class="themeStore.isDark ? 'bg-gray-950' : 'bg-white'"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Title -->
      <div class="text-center mb-6">
        <h2
          class="text-2xl sm:text-3xl mb-2 font-bold transition-colors duration-300"
          :class="[
            themeStore.isDark ? 'text-gray-100' : 'text-gray-900',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{ t('contactTitle') }}
        </h2>
        <div
          class="w-16 h-0.5 mx-auto rounded-full transition-colors duration-300"
          :class="themeStore.isDark
            ? 'bg-linear-to-r from-green-400 to-blue-400'
            : 'bg-linear-to-r from-green-600 to-blue-600'"
        ></div>
      </div>

      <!-- Contact Section -->
      <div
        class="rounded-xl p-6 border shadow-sm transition-colors duration-300"
        :class="themeStore.isDark
          ? 'border-gray-700 bg-linear-to-br from-gray-900/30 via-gray-900/20 to-gray-900/30'
          : 'border-gray-200 bg-linear-to-br from-blue-50 via-purple-50 to-blue-50'"
      >
        <!-- Contact Info Cards -->
        <div class="grid md:grid-cols-3 gap-4 mb-6">
          <div v-for="(item, index) in contactInfo" :key="index"
            class="rounded-lg p-4 text-center transition-shadow hover:shadow-md"
            :class="themeStore.isDark ? 'bg-gray-800' : 'bg-white'"
          >
            <div :class="[
              'inline-flex items-center justify-center w-12 h-12 rounded-full mb-3',
              themeStore.isDark
                ? (item.bg === 'bg-green-50' ? 'bg-green-900' :
                   item.bg === 'bg-blue-50' ? 'bg-blue-900' :
                   'bg-purple-900')
                : item.bg
            ]">
              <component :is="item.icon" :class="[
                'w-6 h-6',
                themeStore.isDark
                  ? (item.color === 'text-green-600' ? 'text-green-400' :
                     item.color === 'text-blue-600' ? 'text-blue-400' :
                     'text-purple-400')
                  : item.color
              ]" />
            </div>
            <h3
              class="text-sm mb-1 transition-colors duration-300"
              :class="themeStore.isDark ? 'text-gray-100' : 'text-gray-900'"
            >
              {{ item.title }}
            </h3>
            <p
              class="text-xs transition-colors duration-300"
              :class="themeStore.isDark ? 'text-gray-400' : 'text-gray-600'"
            >
              {{ item.info }}
            </p>
          </div>
        </div>

        <!-- Map Section -->
        <div
          class="rounded-lg p-6 border-t-2 mb-6 transition-colors duration-300"
          :class="themeStore.isDark
            ? 'border-blue-400 bg-gray-800'
            : 'border-blue-600 bg-white'"
        >
          <div class="flex items-center justify-center gap-2 mb-4">
            <MapPin class="w-5 h-5 text-blue-600 dark:text-blue-400" />
            <h3
              class="text-lg transition-colors duration-300"
              :class="themeStore.isDark ? 'text-gray-100' : 'text-gray-900'"
            >
              {{ isBn ? 'ক্যাম্পাসের অবস্থান' : 'Campus Locations' }}
            </h3>
          </div>

          <!-- Campus Buttons -->
          <div class="flex flex-wrap justify-center gap-2 mb-4">
            <button v-for="campus in campuses" :key="campus.id" @click="selectedCampus = campus.id" :class="[
              'px-4 py-2 rounded-full text-sm transition-all',
              selectedCampus === campus.id ? campus.active : campus.inactive
            ]">
              {{ t(campus.label) }}
            </button>
          </div>

          <!-- Map Type Toggle -->
          <div class="flex justify-center gap-2 mb-4">
            <button @click="mapType = 'roadmap'" :class="[
              'flex items-center gap-2 px-4 py-2 rounded-lg text-sm transition-all',
              mapType === 'roadmap'
                ? 'bg-blue-800 text-white shadow-md'
                : themeStore.isDark
                  ? 'bg-gray-700 text-gray-300 hover:bg-gray-600'
                  : 'bg-gray-100 text-gray-700 hover:bg-gray-200'
            ]">
              <Map class="w-4 h-4" />
              {{ isBn ? 'ম্যাপ' : 'Map' }}
            </button>

            <button @click="mapType = 'satellite'" :class="[
              'flex items-center gap-2 px-4 py-2 rounded-lg text-sm transition-all',
              mapType === 'satellite'
                ? 'bg-blue-800 text-white shadow-md'
                : themeStore.isDark
                  ? 'bg-gray-700 text-gray-300 hover:bg-gray-600'
                  : 'bg-gray-100 text-gray-700 hover:bg-gray-200'
            ]">
              <Satellite class="w-4 h-4" />
              {{ isBn ? 'স্যাটেলাইট' : 'Satellite' }}
            </button>
          </div>

          <!-- Google Maps -->
          <div
            class="relative w-full h-96 rounded-lg overflow-hidden shadow-lg border-2 transition-colors duration-300"
            :class="themeStore.isDark ? 'border-gray-700' : 'border-gray-200'"
          >
            <!-- Hikman Campus -->
            <iframe v-if="selectedCampus === 'hikman'"
              :src="`https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3662.624580079725!2d92.2129743!3d21.6662477!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x30adc4a6a98b1cb9%3A0x45da12b8ad78d4b9!2sQuantum%20Cosmo%20School%20Lama!5e${mapType === 'satellite' ? '1' : '0'}!3m2!1sen!2sbd!4v1730364476374!5m2!1sen!2sbd`"
              class="w-full h-full border-0" allowfullscreen loading="lazy"
              referrerpolicy="no-referrer-when-downgrade"></iframe>

            <!-- Fikran Campus -->
            <iframe v-else-if="selectedCampus === 'fikran'"
              :src="`https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3662.7245099923517!2d92.2124624!3d21.6622351!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x30adc4a735abcf59%3A0x248b69d2a1b9a849!2sQuantum%20Lama%20Fikran%20Campus!5e${mapType === 'satellite' ? '1' : '0'}!3m2!1sen!2sbd!4v1730364584180!5m2!1sen!2sbd`"
              class="w-full h-full border-0" allowfullscreen loading="lazy"
              referrerpolicy="no-referrer-when-downgrade"></iframe>

            <!-- Ikran Campus -->
            <iframe v-else
              :src="`https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3662.693845564644!2d92.2105344!3d21.6633008!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x30adc4a7b9cf9a5f%3A0x1e017f7b3c83f9d5!2sQuantum%20Lama%20Ikran%20Campus!5e${mapType === 'satellite' ? '1' : '0'}!3m2!1sen!2sbd!4v1730364685340!5m2!1sen!2sbd`"
              class="w-full h-full border-0" allowfullscreen loading="lazy"
              referrerpolicy="no-referrer-when-downgrade"></iframe>
          </div>

          <!-- Location Info -->
          <div class="mt-4 text-center">
            <p
              class="text-sm mb-1 transition-colors duration-300"
              :class="themeStore.isDark ? 'text-gray-300' : 'text-gray-700'"
            >
              {{ t('address') }}
            </p>
            <p
              class="text-xs mb-3 transition-colors duration-300"
              :class="themeStore.isDark ? 'text-gray-400' : 'text-gray-500'"
            >
              {{ isBn ? 'বান্দরবানের সুন্দর পাহাড়ে অবস্থিত' : 'Nestled in the beautiful hills of Bandarban' }}
            </p>

            <a :href="getMapLink" target="_blank" rel="noopener noreferrer"
              class="inline-flex items-center gap-2 px-4 py-2 rounded-lg text-sm transition-all shadow-md hover:shadow-lg text-white"
              :class="themeStore.isDark
                ? 'bg-blue-500 hover:bg-blue-600'
                : 'bg-blue-600 hover:bg-blue-700'"
            >
              <MapPin class="w-4 h-4" />
              {{ isBn ? 'গুগল ম্যাপে খুলুন' : 'Open in Google Maps' }}
            </a>
          </div>
        </div>

        <!-- Get in Touch -->
        <div class="mt-6 text-center">
          <a href="mailto:cosmoschool@quantummethod.org.bd"
            class="inline-flex items-center gap-2 px-5 py-2 bg-gradient-to-r from-green-600 to-blue-600 dark:from-green-500 dark:to-blue-500 text-white rounded-full hover:shadow-lg transition-all text-sm">
            <Mail class="w-4 h-4" />
            Send Email
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@400;600;700&display=swap');
.bn-font { font-family: 'Noto Sans Bengali', sans-serif; }
</style>

<script setup>
import { ref, computed } from 'vue'
import { useThemeStore } from '@/stores/theme'
import { useLang } from '@/composables/useLang'
import { Mail, MapPin, Phone, Satellite, Map } from 'lucide-vue-next'

const themeStore = useThemeStore()
const { t, isBn } = useLang()

const selectedCampus = ref('hikman')
const mapType = ref('roadmap')

const campuses = [
  {
    id: 'hikman',
    label: 'campus1',
    active: 'bg-green-600 text-white shadow-md dark:bg-green-500',
    inactive: 'bg-green-100 text-green-700 hover:bg-green-200 dark:bg-green-900 dark:text-green-400 dark:hover:bg-green-800',
  },
  {
    id: 'fikran',
    label: 'campus2',
    active: 'bg-blue-600 text-white shadow-md dark:bg-blue-500',
    inactive: 'bg-blue-100 text-blue-700 hover:bg-blue-200 dark:bg-blue-900 dark:text-blue-400 dark:hover:bg-blue-800',
  },
  {
    id: 'ikran',
    label: 'campus3',
    active: 'bg-purple-600 text-white shadow-md dark:bg-purple-500',
    inactive: 'bg-purple-100 text-purple-700 hover:bg-purple-200 dark:bg-purple-900 dark:text-purple-400 dark:hover:bg-purple-800',
  },
]

const contactInfo = [
  {
    icon: MapPin,
    title: 'Address',
    info: t('address'),
    color: 'text-green-600',
    bg: 'bg-green-50',
  },
  {
    icon: Mail,
    title: 'Email',
    info: 'cosmoschool@quantummethod.org.bd',
    color: 'text-blue-600',
    bg: 'bg-blue-50',
  },
  {
    icon: Phone,
    title: 'Phone',
    info: '+880 160 4490 060',
    color: 'text-purple-600',
    bg: 'bg-purple-50',
  },
]

const getMapLink = computed(() => {
  if (selectedCampus.value === 'hikman') return 'https://maps.app.goo.gl/nx5rtthSGjBWydcw9'
  if (selectedCampus.value === 'fikran') return 'https://maps.app.goo.gl/FNJ8BVthHgbguNSc9'
  return 'https://maps.app.goo.gl/qBxSAsnXaZVdewN8A'
})
</script>
