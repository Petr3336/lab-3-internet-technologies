<script setup lang="ts">
</script>

<template>
  <UHeader :toggle="false">
    <template #left>
      Лабораторная работа №3 по Интернет-технологиям
    </template>
    <template #right>
      <UColorModeButton />

      <UButton
        to=""
        target="_blank"
        icon="i-simple-icons-github"
        aria-label="GitHub"
        color="neutral"
        variant="ghost"
      />
    </template>
  </UHeader>

  <UMain>
    <UContainer>
      <slot />
    </UContainer>
  </UMain>

  <USeparator icon="i-simple-icons-nuxtdotjs" />

  <UFooter>
    <template #left>
      <p class="text-sm text-muted">
        Выполнено студентом группы ИДМ-26-01 Козыревом Петром Михайловичем
      </p>
    </template>

    <template #right>
      <UButton
        to=""
        target="_blank"
        icon="i-simple-icons-github"
        aria-label="GitHub"
        color="neutral"
        variant="ghost"
      />
    </template>
  </UFooter>
</template>
