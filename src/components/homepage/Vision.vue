<script setup lang="ts">
import { useThemeStore } from '@/stores/theme'
import { useLang } from '@/composables/useLang'
import { QuoteIcon, TargetIcon, LightbulbIcon, TrendingUpIcon } from 'lucide-vue-next'

const themeStore = useThemeStore()
const { t, isBn } = useLang()
</script>

<template>
  <section
    id="vision"
    class="py-8 relative overflow-hidden transition-colors duration-500"
    :class="themeStore.isDark
      ? 'bg-linear-to-r from-gray-900 via-gray-900 to-gray-900'
      : 'bg-linear-to-r from-green-50 via-blue-50 to-purple-50'"
  >
    <!-- Background decorations -->
    <div
      class="absolute inset-0"
      :class="themeStore.isDark ? 'opacity-10' : 'opacity-5'"
    >
      <div
        class="absolute top-0 left-1/4 w-64 h-64 bg-blue-500 rounded-full blur-3xl"
        :class="themeStore.isDark ? 'dark:bg-blue-400/30' : ''"
      ></div>
      <div
        class="absolute bottom-0 right-1/4 w-64 h-64 bg-green-500 rounded-full blur-3xl"
        :class="themeStore.isDark ? 'dark:bg-green-400/30' : ''"
      ></div>
    </div>

    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
      <div class="text-center">
        <!-- Quote Icon -->
        <div
          class="inline-flex items-center justify-center w-12 h-12 rounded-full mb-3 transition-colors duration-300"
          :class="themeStore.isDark
            ? 'bg-blue-900/40'
            : 'bg-blue-100'"
        >
          <QuoteIcon
            class="w-6 h-6 transition-colors duration-300"
            :class="themeStore.isDark
              ? 'text-blue-400'
              : 'text-blue-600'"
          />
        </div>

        <!-- Title -->
        <h2
          class="text-2xl sm:text-3xl mb-3 font-semibold bg-clip-text text-transparent transition-colors duration-300"
          :class="[
            themeStore.isDark
              ? 'bg-linear-to-r from-green-400 via-blue-400 to-purple-400'
              : 'bg-linear-to-r from-green-600 via-blue-600 to-purple-600',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{ t('visionTitle') }}
        </h2>

        <!-- Quote -->
        <blockquote
          class="text-lg sm:text-xl lg:text-2xl leading-relaxed italic mb-4 max-w-4xl mx-auto transition-colors duration-300"
          :class="[
            themeStore.isDark ? 'text-gray-300' : 'text-gray-700',
            isBn ? 'bn-font' : ''
          ]"
        >
          {{ t('visionQuote') }}
        </blockquote>

        <!-- Badges -->
        <div class="flex justify-center gap-2 flex-wrap">
          <div
            class="backdrop-blur-sm px-4 py-1.5 rounded-full border shadow-sm flex items-center gap-1.5 transition-colors duration-300"
            :class="themeStore.isDark
              ? 'bg-gray-800/60 border-yellow-700/50'
              : 'bg-white/80 border-yellow-200'"
          >
            <LightbulbIcon
              class="w-3.5 h-3.5 transition-colors duration-300"
              :class="themeStore.isDark
                ? 'text-yellow-400'
                : 'text-yellow-600'"
            />
            <span
              class="text-sm transition-colors duration-300"
              :class="[
                themeStore.isDark ? 'text-yellow-300' : 'text-yellow-700',
                isBn ? 'bn-font' : ''
              ]"
            >
              {{ t('innovation') }}
            </span>
          </div>

          <div
            class="backdrop-blur-sm px-4 py-1.5 rounded-full border shadow-sm flex items-center gap-1.5 transition-colors duration-300"
            :class="themeStore.isDark
              ? 'bg-gray-800/60 border-green-700/50'
              : 'bg-white/80 border-green-200'"
          >
            <TrendingUpIcon
              class="w-3.5 h-3.5 transition-colors duration-300"
              :class="themeStore.isDark
                ? 'text-green-400'
                : 'text-green-600'"
            />
            <span
              class="text-sm transition-colors duration-300"
              :class="[
                themeStore.isDark ? 'text-green-300' : 'text-green-700',
                isBn ? 'bn-font' : ''
              ]"
            >
              {{ t('excellence') }}
            </span>
          </div>

          <div
            class="backdrop-blur-sm px-4 py-1.5 rounded-full border shadow-sm flex items-center gap-1.5 transition-colors duration-300"
            :class="themeStore.isDark
              ? 'bg-gray-800/60 border-blue-700/50'
              : 'bg-white/80 border-blue-200'"
          >
            <TargetIcon
              class="w-3.5 h-3.5 transition-colors duration-300"
              :class="themeStore.isDark
                ? 'text-blue-400'
                : 'text-blue-600'"
            />
            <span
              class="text-sm transition-colors duration-300"
              :class="[
                themeStore.isDark ? 'text-blue-300' : 'text-blue-700',
                isBn ? 'bn-font' : ''
              ]"
            >
              {{ t('impact') }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
