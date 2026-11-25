<script setup>
import { ru } from '@nuxt/ui/locale'

const { app } = useRuntimeConfig()

useHead({
  meta: [
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
  link: [
    { rel: 'icon', href: `${app.baseURL}favicon.ico` }
  ],
  htmlAttrs: {
    lang: 'ru'
  }
})

const title = 'Задание по лабораторной работе №3'
const description = 'Задание по лабораторной работе №3 выполненное студентом группы ИДМ-26-01 Козыревом Петром'

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description
})
</script>

<template>
  <UApp :locale="ru">
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </UApp>
</template>
