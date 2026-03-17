<script setup>
import { useThemeStore } from '@/stores/theme'
import { useLang } from '@/composables/useLang'
import { PlayCircle, Code2, Beaker, Paintbrush, Wrench } from 'lucide-vue-next'
import { computed } from 'vue'
import { RouterLink } from 'vue-router'

const themeStore = useThemeStore()
const { t, isBn } = useLang()

const tutorialCategories = computed(() => [
  {
    icon: Code2,
    titleKey: 'programming',
    videos: '45+',
    colorLight: 'text-blue-600',
    colorDark: 'text-blue-400',
    bgLight: 'bg-blue-50',
    bgDark: 'bg-blue-900/30'
  },
  {
    icon: Beaker,
    titleKey: 'scienceExperiments',
    videos: '30+',
    colorLight: 'text-purple-600',
    colorDark: 'text-purple-400',
    bgLight: 'bg-purple-50',
    bgDark: 'bg-purple-900/30'
  },
  {
    icon: Paintbrush,
    titleKey: 'creativeArts',
    videos: '25+',
    colorLight: 'text-pink-600',
    colorDark: 'text-pink-400',
    bgLight: 'bg-pink-50',
    bgDark: 'bg-pink-900/30'
  },
  {
    icon: Wrench,
    titleKey: 'skillsProjects',
    videos: '35+',
    colorLight: 'text-green-600',
    colorDark: 'text-green-400',
    bgLight: 'bg-green-50',
    bgDark: 'bg-green-900/30'
  }
])
</script>

<template>
  <section id="tutorials"
    class="py-12 transition-colors duration-500"
    :class="themeStore.isDark
      ? 'bg-linear-to-b from-gray-950 via-gray-900 to-gray-950'
      : 'bg-white'"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Header -->
      <div class="text-center mb-8">
        <h2
          class="text-2xl sm:text-3xl font-semibold mb-2 bg-clip-text text-transparent transition-colors duration-300"
          :class="[
            themeStore.isDark
              ? 'bg-linear-to-r from-green-400 via-blue-400 to-purple-400'
              : 'bg-linear-to-r from-green-600 via-blue-600 to-purple-600',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{ t('tutorialsTitle') }}
        </h2>
        <div
          class="w-20 h-0.5 mx-auto mb-3 rounded-full transition-colors duration-300"
          :class="themeStore.isDark
            ? 'bg-linear-to-r from-green-400 to-blue-400'
            : 'bg-linear-to-r from-green-600 to-blue-600'"
        ></div>
        <p
          class="text-sm max-w-2xl mx-auto transition-colors duration-300"
          :class="[
            themeStore.isDark ? 'text-gray-400' : 'text-gray-600',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{ t('tutorialsDesc') }}
        </p>
      </div>

      <!-- Tutorials Grid -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-8">
        <div
          v-for="(category, index) in tutorialCategories"
          :key="index"
          class="group rounded-xl p-4 text-center border transition-all duration-300 hover:-translate-y-1 hover:shadow-lg cursor-pointer"
          :class="[
            themeStore.isDark
              ? 'border-gray-700 bg-gray-900/50 hover:bg-gray-800/50 hover:shadow-blue-500/10'
              : 'border-gray-100 bg-white hover:bg-gray-50/50 hover:shadow-blue-500/10',
            'backdrop-blur-sm'
          ]"
        >
          <!-- Icon -->
          <div
            :class="[
              'w-12 h-12 rounded-lg flex items-center justify-center mb-3 mx-auto group-hover:scale-110 transition-transform duration-300',
              themeStore.isDark ? category.bgDark : category.bgLight
            ]"
          >
            <component
              :is="category.icon"
              :class="[
                'w-6 h-6 transition-colors duration-300',
                themeStore.isDark ? category.colorDark : category.colorLight
              ]"
            />
          </div>

          <!-- Title -->
          <h3
            class="text-sm mb-2 transition-colors duration-300"
            :class="[
              themeStore.isDark ? 'text-gray-100 group-hover:text-white' : 'text-gray-900 group-hover:text-gray-800',
              isBn ? 'bn-font' : ''
            ]"
          >
            {{ t(category.titleKey) }}
          </h3>

          <!-- Videos Count -->
          <div
            class="flex items-center justify-center gap-1.5 transition-colors duration-300"
            :class="themeStore.isDark ? 'text-gray-400 group-hover:text-gray-300' : 'text-gray-600 group-hover:text-gray-700'"
          >
            <PlayCircle class="w-4 h-4" />
            <span class="text-xs">{{ category.videos }} {{ t('videos') }}</span>
          </div>
        </div>
      </div>

      <!-- Explore Button -->
      <div class="text-center">
        <RouterLink
          to="/tutorials"
          class="inline-block px-6 py-2 rounded-full shadow-md text-sm transition-all duration-300 hover:scale-105"
          :class="[
            themeStore.isDark
              ? 'bg-blue-500 hover:bg-blue-400 text-white'
              : 'bg-blue-600 hover:bg-blue-700 text-white',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{ t('exploreTutorials') }}
        </RouterLink>
      </div>
    </div>
  </section>
</template>
