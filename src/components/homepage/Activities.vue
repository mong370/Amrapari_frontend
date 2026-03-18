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
      <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-8">
        <div v-for="(activity, index) in activities" :key="index"
          class="holographic-card group rounded-2xl backdrop-blur-sm p-5 transition-all duration-300 hover:-translate-y-1 hover:shadow-lg"
          :class="[
            themeStore.isDark ? 'theme-dark' : 'theme-light',
            themeStore.isDark
              ? 'border border-gray-700 bg-gray-800/40 hover:shadow-blue-500/10'
              : 'bg-gray-50 hover:shadow-gray-500/10'
          ]"
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
            class="text-sm font-semibold mb-1 mt-2 line-clamp-2 transition-colors duration-300"
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
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@400;600;700&display=swap');
.bn-font { font-family: 'Noto Sans Bengali', sans-serif; }

.holographic-container {
  display: flex;
  justify-content: center;
  align-items: center;

  background: #000;
}

.holographic-card {
  overflow: hidden;
  transition: all 0.5s ease;
}

.holographic-card h2 {
  color: #0ff;
  font-size: 2rem;
  position: relative;
  z-index: 2;
}

.holographic-card::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: linear-gradient(
    0deg, 
    transparent, 
    transparent 30%, 
    rgba(0,255,255,0.3)
  );
  transform: rotate(-45deg);
  transition: all 0.5s ease;
  opacity: 0;
}

.holographic-card:hover {
  transform: scale(1.01);
  box-shadow: 0 0 20px rgba(0,255,255,0.5);
}

.holographic-card:hover::before {
  opacity: 1;
  transform: rotate(-45deg) translateY(100%);
}
</style>
