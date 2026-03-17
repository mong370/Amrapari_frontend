<script setup>
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
    bgColor: 'bg-orange-50 dark:bg-orange-900/30',
    accentColor: 'from-orange-400 to-orange-600 dark:from-orange-600 dark:to-orange-800',
    image: 'https://i.postimg.cc/hvrcN1pB/step1-weakup.png'
  },
  {
    id: 2,
    icon: Brain,
    color: 'text-purple-600 dark:text-purple-400',
    bgColor: 'bg-purple-50 dark:bg-purple-900/30',
    accentColor: 'from-purple-400 to-purple-600 dark:from-purple-600 dark:to-purple-800',
    image: 'https://i.postimg.cc/zv5qdcwj/step2-meditatioin-vec.png'
  },
  {
    id: 3,
    icon: BookOpen,
    color: 'text-blue-600 dark:text-blue-400',
    bgColor: 'bg-blue-50 dark:bg-blue-900/30',
    accentColor: 'from-blue-400 to-blue-600 dark:from-blue-600 dark:to-blue-800',
    image: 'https://i.postimg.cc/hvrcN1MT/step3-study.png'
  },
  {
    id: 4,
    icon: Code,
    color: 'text-green-600 dark:text-green-400',
    bgColor: 'bg-green-50 dark:bg-green-900/30',
    accentColor: 'from-green-400 to-green-600 dark:from-green-600 dark:to-green-800',
    image: 'https://i.postimg.cc/C5YwvQC4/step4-skill.png'
  },
  {
    id: 5,
    icon: Trophy,
    color: 'text-red-600 dark:text-red-400',
    bgColor: 'bg-red-50 dark:bg-red-900/30',
    accentColor: 'from-red-400 to-red-600 dark:from-red-600 dark:to-red-800',
    image: 'https://i.postimg.cc/T2qdyTG1/step5-sports.png'
  },
  {
    id: 6,
    icon: Moon,
    color: 'text-indigo-600 dark:text-indigo-400',
    bgColor: 'bg-indigo-50 dark:bg-indigo-900/30',
    accentColor: 'from-indigo-400 to-indigo-600 dark:from-indigo-600 dark:to-indigo-800',
    image: 'https://i.postimg.cc/44bfKXZt/step6-sleep.png'
  }
]
</script>

<template>
  <section
    class="py-20 transition-colors duration-500"
    :class="themeStore.isDark
      ? 'bg-linear-to-b from-gray-950 via-gray-900 to-gray-950'
      : 'bg-linear-to-b from-gray-50 to-white'"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Title -->
      <div class="text-center mb-16">
        <h2
          class="text-4xl sm:text-5xl mb-4 font-bold transition-colors duration-300"
          :class="[
            themeStore.isDark ? 'text-white' : 'text-gray-900',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{ t('whyQuantarsTitle') }}
        </h2>
        <p
          class="text-base max-w-3xl mx-auto transition-colors duration-300"
          :class="[
            themeStore.isDark ? 'text-gray-400' : 'text-gray-600',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{ t('whyQuantarsSubtitle') }}
        </p>
        <div class="w-24 h-1 bg-linear-to-r from-orange-600 via-purple-600 to-blue-600 mx-auto mt-6"></div>
      </div>

      <!-- Description -->
      <div class="text-center mb-16">
        <div
          class="inline-flex items-center gap-2 px-6 py-3 rounded-full shadow-md border transition-colors duration-300"
          :class="themeStore.isDark
            ? 'bg-gray-800 border-gray-700'
            : 'bg-white border-gray-200'"
        >
          <div class="w-2 h-2 bg-orange-500 rounded-full animate-pulse"></div>
          <p
            class="text-sm transition-colors duration-300"
            :class="[
              themeStore.isDark ? 'text-gray-300' : 'text-gray-700',
              isBn ? 'bn-font' : ''
            ]"
          >
            {{
              isBn
                ? 'প্রতিটি দিনের ছয়টি ধাপ অনুসরণ করে আমরা একজন কোয়ান্টা হিসেবে সফলতার পথে এগিয়ে যাই'
                : "Following six steps each day, we advance on the path of success as a Quanta"
            }}
          </p>
        </div>
      </div>

      <!-- Steps -->
      <div class="space-y-12 lg:space-y-20">
        <div v-for="(step, index) in steps" :key="step.id" class="relative">
          <div :class="[
            'flex flex-col lg:flex-row items-center gap-8 lg:gap-12',
            index % 2 === 0 ? 'lg:flex-row' : 'lg:flex-row-reverse'
          ]">
            <!-- Text -->
            <div class="flex-1 w-full">
              <div class="max-w-xl mx-auto lg:mx-0">
                <div class="flex items-center gap-4 mb-6">
                  <div
                    :class="`w-16 h-16 rounded-2xl bg-linear-to-br ${step.accentColor} flex items-center justify-center shadow-xl`">
                    <span class="text-white text-xl font-semibold">0{{ step.id }}</span>
                  </div>
                  <div :class="`w-14 h-14 rounded-full ${step.bgColor} flex items-center justify-center ${step.color}`">
                    <component :is="step.icon" class="w-7 h-7" />
                  </div>
                </div>

                <h3
                  class="text-3xl sm:text-4xl mb-4 font-semibold transition-colors duration-300"
                  :class="[
                    themeStore.isDark ? 'text-white' : 'text-gray-900',
                    isBn ? 'bn-font' : ''
                  ]"
                >
                  {{ t(`step${step.id}Title`) }}
                </h3>
                <p
                  class="text-base sm:text-lg leading-relaxed mb-6 transition-colors duration-300"
                  :class="[
                    themeStore.isDark ? 'text-gray-400' : 'text-gray-600',
                    isBn ? 'bn-font' : ''
                  ]"
                >
                  {{ t(`step${step.id}Desc`) }}
                </p>
                <div :class="`h-1.5 w-24 bg-gradient-to-r ${step.accentColor} rounded-full`"></div>
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

          <!-- Connector -->
          <div v-if="index !== steps.length - 1" class="animate-bounce flex justify-center mt-12 lg:mt-16">
            <div
              :class="`w-12 h-12 rounded-full ${step.bgColor} flex items-center justify-center ${step.color} shadow-lg dark:shadow-none`">
              <ArrowDown class="w-6 h-6" />
            </div>
          </div>
        </div>
      </div>

      <!-- Bottom Message -->
      <div class="mt-20 text-center">
        <div
          class="inline-block rounded-3xl px-10 py-8 border-2 shadow-xl transition-colors duration-500"
          :class="themeStore.isDark
            ? 'bg-linear-to-r from-gray-800 via-gray-900 to-gray-800 border-gray-700'
            : 'bg-linear-to-r from-orange-50 via-purple-50 to-blue-50 border-gray-200'"
        >
          <div class="flex items-center justify-center gap-3 mb-3">
            <div
              class="w-12 h-12 rounded-full flex items-center justify-center shadow-lg"
              :class="themeStore.isDark
                ? 'bg-linear-to-r from-orange-600 to-purple-800'
                : 'bg-linear-to-r from-orange-400 to-purple-600'"
            >
              <Trophy class="w-6 h-6 text-white" />
            </div>
            <p
              class="text-xl sm:text-2xl transition-colors duration-300"
              :class="[
                themeStore.isDark ? 'text-white' : 'text-gray-900',
                isBn ? 'bn-font' : ''
              ]"
            >
              {{ isBn
                  ? 'এই পথ ধরে আমরা আমাদের স্বপ্নের দিকে এগিয়ে চলি এবং আমরা হয়ে উঠছি সৃজনশীল ও দক্ষ ব্যক্তি'
                  : 'By following this path, we are progressing toward our dreams and becoming creative and skilled individuals' }}
            </p>
          </div>
          <p
            class="text-lg sm:text-xl transition-colors duration-300"
            :class="[
              themeStore.isDark ? 'text-gray-300' : 'text-gray-800',
              isBn ? 'bn-font' : ''
            ]"
          >
            {{
              isBn
                ? 'আমরা আত্মবিশ্বাসী, দক্ষ এবং মানবিক নেতা হয়ে উঠি'
                : 'We become confident, skilled, and compassionate leaders'
            }}
          </p>
        </div>
      </div>

      <!-- Info Cards -->
      <div class="mt-16 grid grid-cols-1 md:grid-cols-3 gap-6">
        <div
          class="rounded-2xl p-8 shadow-lg border hover:shadow-xl transition-shadow duration-300"
          :class="themeStore.isDark
            ? 'bg-gray-800 border-gray-700'
            : 'bg-white border-gray-100'"
        >
          <BookOpen class="w-10 h-10 mb-4 mx-auto text-indigo-500" />
          <h4
            class="text-center mb-2 transition-colors duration-300"
            :class="[
              themeStore.isDark ? 'text-white' : 'text-gray-900',
              isBn ? 'bn-font' : ''
            ]"
          >
            {{ isBn ? 'সকাল থেকে সন্ধ্যা' : 'Morning to Evening' }}
          </h4>
          <p
            class="text-sm text-center transition-colors duration-300"
            :class="[
              themeStore.isDark ? 'text-gray-400' : 'text-gray-600',
              isBn ? 'bn-font' : ''
            ]"
          >
            {{
              isBn
                ? 'সম্পূর্ণ দিনের পরিকল্পিত রুটিন'
                : 'Complete daily structured routine'
            }}
          </p>
        </div>

        <div
          class="rounded-2xl p-8 shadow-lg border hover:shadow-xl transition-shadow duration-300"
          :class="themeStore.isDark
            ? 'bg-gray-800 border-gray-700'
            : 'bg-white border-gray-100'"
        >
          <Brain class="w-10 h-10 mb-4 mx-auto text-green-500" />
          <h4
            class="text-center mb-2 transition-colors duration-300"
            :class="[
              themeStore.isDark ? 'text-white' : 'text-gray-900',
              isBn ? 'bn-font' : ''
            ]"
          >
            {{ isBn ? 'পরিকল্পিত শিক্ষা' : 'Structured Learning' }}
          </h4>
          <p
            class="text-sm text-center transition-colors duration-300"
            :class="[
              themeStore.isDark ? 'text-gray-400' : 'text-gray-600',
              isBn ? 'bn-font' : ''
            ]"
          >
            {{ isBn ? 'প্রতিটি ধাপে নির্দিষ্ট লক্ষ্য' : 'Clear objectives at every step' }}
          </p>
        </div>

        <div
          class="rounded-2xl p-8 shadow-lg border hover:shadow-xl transition-shadow duration-300"
          :class="themeStore.isDark
            ? 'bg-gray-800 border-gray-700'
            : 'bg-white border-gray-100'"
        >
          <Code class="w-10 h-10 mb-4 mx-auto text-yellow-500" />
          <h4
            class="text-center mb-2 transition-colors duration-300"
            :class="[
              themeStore.isDark ? 'text-white' : 'text-gray-900',
              isBn ? 'bn-font' : ''
            ]"
          >
            {{ isBn ? 'সার্বিক উন্নয়ন' : 'Holistic Development' }}
          </h4>
          <p
            class="text-sm text-center transition-colors duration-300"
            :class="[
              themeStore.isDark ? 'text-gray-400' : 'text-gray-600',
              isBn ? 'bn-font' : ''
            ]"
          >
            {{
              isBn
                ? 'শারীরিক ও মানসিক বিকাশ'
                : 'Physical and mental growth'
            }}
          </p>
        </div>
      </div>
    </div>
    <div>
    </div>
  </section>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@400;600;700&display=swap');
.bn-font { font-family: 'Noto Sans Bengali', sans-serif; }
</style>
