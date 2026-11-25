<script setup lang="ts">
const { app: { baseURL } } = useRuntimeConfig()
const diagramSrc = `${baseURL.replace(/\/$/, '')}/diagrams/business-event-history.svg`
</script>

<template>
  <figure class="my-8 rounded-xl border border-default bg-elevated/50 p-2 sm:p-6">
    <img
      :src="diagramSrc"
      alt="Поставщик вычисляет хеш своей копии акта партии P-42 и&nbsp;берёт сохранённый хеш из записи при подписании. На сверку поступают оба хеша; в&nbsp;этом примере они совпали."
      class="mx-auto block h-auto w-full max-w-sm"
      width="360"
      height="260"
      loading="lazy"
    >
    <figcaption class="mx-auto mt-4 max-w-prose text-sm leading-relaxed text-muted">
      Если хеши совпали, у&nbsp;поставщика та же версия акта, которую подписал склад. Сколько коробок прибыло, проверяют при разгрузке.
    </figcaption>
  </figure>
</template>
