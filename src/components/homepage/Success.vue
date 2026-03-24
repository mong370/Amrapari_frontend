<script setup>
import { useThemeStore } from '@/stores/theme'
import { useLang } from '@/composables/useLang'
import { Trophy, Award, Medal, Star } from 'lucide-vue-next'
import { ref, onMounted } from 'vue'

defineProps({
  onNavigateToSuccess: Function
})

const themeStore = useThemeStore()
const { t, isBn } = useLang()

const targetAchievements = [
  { icon: Trophy, label: 'National Sports', count: 15, colorLight: 'text-green-600', colorDark: 'text-green-400', bgLight: 'bg-green-50', bgDark: 'bg-green-900/30' },
  { icon: Award, label: 'Science Fairs', count: 20, colorLight: 'text-blue-600', colorDark: 'text-blue-400', bgLight: 'bg-blue-50', bgDark: 'bg-blue-900/30' },
  { icon: Medal, label: 'Cultural Events', count: 25, colorLight: 'text-purple-600', colorDark: 'text-purple-400', bgLight: 'bg-purple-50', bgDark: 'bg-purple-900/30' },
  { icon: Star, label: 'Debate Competitions', count: 10, colorLight: 'text-orange-600', colorDark: 'text-orange-400', bgLight: 'bg-orange-50', bgDark: 'bg-orange-900/30' }
]

const achievements = ref(targetAchievements.map(a => ({ ...a, displayCount: 0 })))
const sectionRef = ref(null)
let animated = false

function easeOutQuad(t) {
  return t * (2 - t)
}

function startEasingAnimation() {
  const duration = 1500 // total animation time in ms
  const startTime = performance.now()

  function animate(time) {
    const elapsed = time - startTime
    const progress = Math.min(elapsed / duration, 1)
    const eased = easeOutQuad(progress)

    achievements.value.forEach((achievement) => {
      achievement.displayCount = Math.floor(achievement.count * eased)
    })

    if (progress < 1) {
      requestAnimationFrame(animate)
    } else {
      // Ensure final value is exact
      achievements.value.forEach(a => (a.displayCount = a.count))
    }
  }

  requestAnimationFrame(animate)
}

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      const entry = entries[0]
      if (entry.isIntersecting) {
        if (!animated) {
          animated = true
          startEasingAnimation()
        }
      } else {
        animated = false
        achievements.value.forEach(a => (a.displayCount = 0))
      }
    },
    { threshold: 0.3 } // triggers when 30% of section is visible
  )

  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
})
</script>

<template>
  <section id="success" ref="sectionRef"
    class="py-12 transition-colors duration-500"
    :class="themeStore.isDark
      ? 'bg-linear-to-b from-gray-950 via-gray-900 to-gray-950'
      : 'bg-gray-50'"
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
          {{ t('successTitle') }}
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
          {{ t('successDesc') }}
        </p>
      </div>

      <!-- Achievements Grid -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-8">
        <div v-for="(achievement, index) in achievements" :key="index"
          class="holographic-card rounded-xl p-5 text-center transition-all duration-300 hover:-translate-y-1 hover:shadow-lg hover:shadow-blue-500/10"
          :class="themeStore.isDark
            ? 'border-gray-700 bg-gray-800/40 ' + achievement.bgDark
            : 'border-gray-100 ' + achievement.bgLight"
        >
          <component :is="achievement.icon" :class="[
            'w-8 h-8 mx-auto mb-2 transition-colors',
            themeStore.isDark ? achievement.colorDark : achievement.colorLight
          ]" />
          <div
            class="text-2xl font-semibold mb-1 transition-colors duration-300"
            :class="themeStore.isDark ? 'text-gray-100' : 'text-gray-900'"
          >
            {{ achievement.displayCount }}+
          </div>
          <p
            class="text-xs mb-3 transition-colors duration-300"
            :class="themeStore.isDark ? 'text-gray-400' : 'text-gray-600'"
          >
            {{ achievement.label }}
          </p>

          
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@400;600;700&display=swap');
.bn-font { font-family: 'Noto Sans Bengali', sans-serif; }

.holographic-card {
  position: relative;
  overflow: hidden;
}

.holographic-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    120deg,
    transparent 30%,
    rgba(0,255,255,0.3),
    transparent 70%
  );
  transform: translateX(-100%);
  transition: 0.6s;
}
.holographic-card:hover {
  transform: scale(1.01);
  box-shadow: 0 0 20px rgba(0,255,255,0.5);
}
.holographic-card:hover::before {
  transform: translateX(100%);
}
</style>
