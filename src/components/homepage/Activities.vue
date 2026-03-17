<script setup>
import { useThemeStore } from '@/stores/theme'
import { useLang } from '@/composables/useLang'
import { Code, Beaker, Palette, Trophy, Music } from 'lucide-vue-next'
import { computed } from 'vue'

const themeStore = useThemeStore()
const { t, isBn } = useLang()

const activities = computed(() => [
  {
    icon: Code,
    title: t('ictTitle'),
    description: t('ictDesc'),
    color: 'from-blue-500 to-cyan-500',
    lightBg: 'bg-blue-50',
    darkBg: 'bg-blue-900/30',
    iconColorLight: 'text-blue-600',
    iconColorDark: 'text-blue-400'
  },
  {
    icon: Beaker,
    title: t('scienceTitle'),
    description: t('scienceDesc'),
    color: 'from-purple-500 to-pink-500',
    lightBg: 'bg-purple-50',
    darkBg: 'bg-purple-900/30',
    iconColorLight: 'text-purple-600',
    iconColorDark: 'text-purple-400'
  },
  {
    icon: Palette,
    title: t('creativityTitle'),
    description: t('creativityDesc'),
    color: 'from-orange-500 to-red-500',
    lightBg: 'bg-orange-50',
    darkBg: 'bg-orange-900/30',
    iconColorLight: 'text-orange-600',
    iconColorDark: 'text-orange-400'
  },
  {
    icon: Trophy,
    title: t('sportsTitle'),
    description: t('sportsDesc'),
    color: 'from-green-500 to-emerald-500',
    lightBg: 'bg-green-50',
    darkBg: 'bg-green-900/30',
    iconColorLight: 'text-green-600',
    iconColorDark: 'text-green-400'
  },
  {
    icon: Music,
    title: t('bandTitle'),
    description: t('bandDesc'),
    color: 'from-indigo-500 to-blue-500',
    lightBg: 'bg-indigo-50',
    darkBg: 'bg-indigo-900/30',
    iconColorLight: 'text-indigo-600',
    iconColorDark: 'text-indigo-400'
  }
])
</script>

<template>
  <section id="activities"
    class="py-12 transition-colors duration-500"
    :class="themeStore.isDark
      ? 'bg-linear-to-b from-gray-950 via-gray-900 to-gray-950 text-gray-100'
      : 'bg-white text-gray-900'"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Section Title -->
      <div class="text-center mb-8">
        <h2
          class="text-2xl sm:text-3xl mb-2 font-semibold bg-clip-text text-transparent transition-colors duration-300"
          :class="[
            themeStore.isDark
              ? 'bg-linear-to-r from-green-400 via-blue-400 to-purple-400'
              : 'bg-linear-to-r from-green-600 via-blue-600 to-purple-600',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{ t('activitiesTitle') }}
        </h2>
        <div
          class="w-20 h-0.5 mx-auto rounded-full transition-colors duration-300"
          :class="themeStore.isDark
            ? 'bg-linear-to-r from-green-400 to-blue-400'
            : 'bg-linear-to-r from-green-600 to-blue-600'"
        ></div>
      </div>

      <!-- Activities Grid -->
      <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-5">
        <div v-for="(activity, index) in activities" :key="index"
          class="group rounded-xl backdrop-blur-sm p-5 transition-all duration-300 hover:-translate-y-1 hover:shadow-lg hover:shadow-blue-500/10"
          :class="themeStore.isDark
            ? 'border-gray-700 bg-gray-800/40'
            : 'border-gray-100 bg-white/80'"
        >
          <!-- Icon -->
          <div :class="[
            'w-12 h-12 rounded-lg flex items-center justify-center mb-3 transition-transform group-hover:scale-110',
            themeStore.isDark ? activity.darkBg : activity.lightBg
          ]">
            <component :is="activity.icon" :class="[
              'w-6 h-6 transition-colors',
              themeStore.isDark ? activity.iconColorDark : activity.iconColorLight
            ]" />
          </div>

          <!-- Title -->
          <h3
            class="text-sm font-semibold mb-1 line-clamp-2 transition-colors duration-300"
            :class="[
              themeStore.isDark ? 'text-gray-100' : 'text-gray-900',
              isBn ? 'bn-font' : ''
            ]"
          >
            {{ activity.title }}
          </h3>

          <!-- Description -->
          <p
            class="text-xs line-clamp-2 transition-colors duration-300"
            :class="[
              themeStore.isDark ? 'text-gray-400' : 'text-gray-600',
              isBn ? 'bn-font' : ''
            ]"
          >
            {{ activity.description }}
          </p>
          <!-- Explore Button -->
          <div class="text-center">
            <router-link
              to="/tutorials"
              class="inline-block px-4 py-2 bg-gradient-to-r from-blue-500 to-purple-500 text-white text-xs font-semibold rounded-lg hover:from-blue-600 hover:to-purple-600 transition-all duration-300 transform hover:scale-105"
            >
              {{ t('activities.exploreActivity') }}
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@400;600;700&display=swap');
.bn-font { font-family: 'Noto Sans Bengali', sans-serif; }
</style>
