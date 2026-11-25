<script setup lang="ts"></script>

<template>
  <div class="flex min-h-dvh flex-col">
    <UHeader :toggle="false">
      <template #left>
        Лабораторная работа №3 по Интернет-технологиям
      </template>
      <template #right>
        <UColorModeButton />
      </template>
    </UHeader>

    <UMain :ui="{ base: 'min-h-0 flex-1' }">
      <UContainer>
        <slot />
      </UContainer>
    </UMain>

    <USeparator />

    <UFooter>
      <template #left>
        <p class="text-sm text-muted">
          Выполнено студентом <br>
          группы ИДМ-26-01 <br>
          Козыревом Петром Михайловичем
        </p>
      </template>
    </UFooter>
  </div>
</template>
