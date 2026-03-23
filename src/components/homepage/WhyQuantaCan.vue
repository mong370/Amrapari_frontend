<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'
import { Sunrise, Brain, BookOpen, Code, Trophy, Moon, ArrowDown } from 'lucide-vue-next'
import { useThemeStore } from '@/stores/theme'
import { useLang } from '@/composables/useLang'

const themeStore = useThemeStore()
const { t, isBn } = useLang()

const steps = [
  {
    id: 1,
    icon: Sunrise,
    color: 'text-orange-600 dark:text-orange-400',
    bgColor: 'bg-white dark:bg-gray-900',
    accentColor: 'from-orange-400 to-orange-600 dark:from-orange-600 dark:to-orange-800',
    image: 'https://i.postimg.cc/VvbzMCXT/step1_wakeup.png'
  },
  {
    id: 2,
    icon: Brain,
    color: 'text-purple-600 dark:text-purple-400',
    bgColor: 'bg-white dark:bg-gray-900',
    accentColor: 'from-purple-400 to-purple-600 dark:from-purple-600 dark:to-purple-800',
    image: 'https://i.postimg.cc/85zR11LC/step2_meditatioin.png'
  },
  {
    id: 3,
    icon: BookOpen,
    color: 'text-blue-600 dark:text-blue-400',
    bgColor: 'bg-white dark:bg-gray-900',
    accentColor: 'from-blue-400 to-blue-600 dark:from-blue-600 dark:to-blue-800',
    image: 'https://i.postimg.cc/m2YyN6Zr/step3_study.png'
  },
  {
    id: 4,
    icon: Code,
    color: 'text-green-600 dark:text-green-400',
    bgColor: 'bg-white dark:bg-gray-900',
    accentColor: 'from-green-400 to-green-600 dark:from-green-600 dark:to-green-800',
    image: 'https://i.postimg.cc/PrjmxzW2/step4_skill.png'
  },
  {
    id: 5,
    icon: Trophy,
    color: 'text-red-600 dark:text-red-400',
    bgColor: 'bg-white dark:bg-gray-900',
    accentColor: 'from-red-400 to-red-600 dark:from-red-600 dark:to-red-800',
    image: 'https://i.postimg.cc/xjKzWJwW/step5_sports.png'
  },
  {
    id: 6,
    icon: Moon,
    color: 'text-indigo-600 dark:text-indigo-400',
    bgColor: 'bg-white dark:bg-gray-900',
    accentColor: 'from-indigo-400 to-indigo-600 dark:from-indigo-600 dark:to-indigo-800',
    image: 'https://i.postimg.cc/Gm99hHfc/step6_sleep.png'
  }
]

const backgrounds = computed(() => 
  steps.map(step => `py-20 ${themeStore.isDark ? 'bg-gray-900' : 'bg-white'} transition-colors duration-500`)
)

const current = ref(0)
const slides = ref([])
const isVisible = ref(false)

onMounted(() => {
  slides.value = document.querySelectorAll(".slide");
  window.addEventListener("scroll", handleScroll);

  // Intersection Observer for component visibility
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        isVisible.value = entry.isIntersecting;
      });
    },
    { threshold: 0.1 }
  );

  const componentElement = document.querySelector('.why-quantacan-container');
  if (componentElement) {
    observer.observe(componentElement);
  }
})

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
})

function handleScroll() {
  let currentIndex = 0;
  slides.value.forEach((slide, index) => {
    const rect = slide.getBoundingClientRect();
    if (rect.top <= window.innerHeight / 2) {
      currentIndex = index;
    }
  });
  current.value = currentIndex;
}
</script>

<template>
  <!-- INTRO SECTION -->
  <div class="py-16 sm:py-20 lg:py-24 transition-colors duration-500" :class="themeStore.isDark ? 'bg-gray-900' : 'bg-white'">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
      <div class="text-center mb-8">
        <h2 class="text-4xl sm:text-5xl mb-4 font-bold"
        :class="[
              themeStore.isDark ? 'text-gray-100' : 'text-gray-900',
            ]">
          {{ t('whyQuantarsTitle') }}
        </h2>
        <p class="text-base max-w-3xl mx-auto"
        :class="[
              themeStore.isDark ? 'text-gray-400' : 'text-gray-600',
            ]">
          {{ t('whyQuantarsSubtitle') }}
        </p>
        <div class="w-24 h-1 bg-linear-to-r from-orange-600 via-purple-600 to-blue-600 mx-auto mt-6"></div>
      </div>

      <!-- Description -->
      <div class="text-center">
        <div
          class="inline-flex items-center gap-2 bg-white dark:bg-gray-800 px-6 py-3 rounded-full shadow-md border border-gray-200 dark:border-gray-700">
          <div class="w-2 h-2 bg-orange-500 rounded-full animate-pulse"></div>
          <p class="text-sm text-gray-700 dark:text-gray-300">
            {{
              isBn
                ? 'প্রতিটি দিনের ছয়টি ধাপ অনুসরণ করে আমরা একজন কোয়ান্টা হিসেবে সফলতার পথে এগিয়ে যাই'
                : "Following six steps each day, we advance on the path of success as a Quanta"
            }}
          </p>
        </div>
      </div>
    </div>
  </div>

  <div class="relative py-10 sm:py-20 transition-colors duration-500 why-quantacan-container" :class="themeStore.isDark ? 'bg-gray-900' : 'bg-white'">
    <!-- RIGHT SIDE DOTS -->
    <div id="dots" class="fixed right-2 md:right-5 top-1/2 -translate-y-1/2 flex flex-col gap-2 md:gap-3 z-50 transition-opacity duration-300" :class="{ 'opacity-100': isVisible, 'opacity-0 pointer-events-none': !isVisible }" v-show="isVisible">
      <span v-for="(step, index) in steps" :key="step.id" class="dot w-2 h-2 md:w-3 md:h-3 rounded-full transition-all duration-300" :class="themeStore.isDark ? 'bg-gray-600' : 'bg-gray-400'" :style="{ transform: current === index ? 'scale(1.25)' : 'scale(1)', backgroundColor: current === index ? (themeStore.isDark ? '#60a5fa' : '#3b82f6') : (themeStore.isDark ? '#4b5563' : '#9ca3af') }"></span>
    </div>

    <!-- SLIDES -->
    <div class="relative">
      <section v-for="(step, index) in steps" :key="step.id" class="slide sticky top-0 h-screen flex items-center justify-center" :class="backgrounds[index]">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 w-full">
          <div :class="[
            'flex flex-col lg:flex-row items-center gap-6 sm:gap-8 lg:gap-12 px-4 sm:px-6 lg:px-8',
            index % 2 === 0 ? 'lg:flex-row' : 'lg:flex-row-reverse'
          ]">
            <!-- Text -->
            <div class="flex-1 w-full">
              <div class="max-w-xl mx-auto lg:mx-0">
                <div class="flex items-center gap-3 sm:gap-4 mb-4 sm:mb-6">
                  <div
                    :class="`w-12 h-12 sm:w-16 sm:h-16 rounded-2xl bg-linear-to-br ${step.accentColor} flex items-center justify-center shadow-xl`">
                    <span class="text-white text-lg sm:text-xl font-semibold">0{{ step.id }}</span>
                  </div>
                  <div :class="`w-10 h-10 sm:w-14 sm:h-14 rounded-full flex items-center justify-center ${step.color}`" :style="{ backgroundColor: themeStore.isDark ? '#374151' : '#f3f4f6' }">
                    <component :is="step.icon" class="w-5 h-5 sm:w-7 sm:h-7" />
                  </div>
                </div>

                <h2 class="text-2xl sm:text-3xl lg:text-4xl mb-3 sm:mb-4 font-semibold" :class="themeStore.isDark ? 'text-white' : 'text-gray-900'">
                  {{ t(`step${step.id}Title`) }}
                </h2>
                <p class="text-sm sm:text-base lg:text-lg leading-relaxed mb-4 sm:mb-6" :class="themeStore.isDark ? 'text-gray-300' : 'text-gray-700'">
                  {{ t(`step${step.id}Desc`) }}
                </p>
                <div :class="`h-1 w-16 sm:w-24 bg-linear-to-r ${step.accentColor} rounded-full`"></div>
              </div>
            </div>

            <!-- Image -->
            <div class="flex-1 w-full flex justify-center items-center">
              <div class="w-full max-w-xs">
                <img :src="step.image" :alt="step.title"
                  class="w-full h-auto object-contain drop-shadow-md dark:drop-shadow-none" />
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<style scoped>
.slide {
  min-height: 100vh;
}

@media (max-width: 1024px) {
  .slide {
    position: relative;
    min-height: auto;
    padding: 4rem 0;
  }
}

@media (max-width: 640px) {
  .slide {
    padding: 2rem 0;
  }
}
</style>
