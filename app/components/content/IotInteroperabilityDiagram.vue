<script setup lang="ts">
const { app: { baseURL } } = useRuntimeConfig()
const diagramSrc = `${baseURL.replace(/\/$/, '')}/diagrams/iot-interoperability.svg`
</script>

<template>
  <figure class="my-8 rounded-xl border border-default bg-elevated/50 p-2 sm:p-6">
    <img
      :src="diagramSrc"
      alt="Одно приложение видит светильник. Включение срабатывает: светильник загорается. Регулировка яркости в&nbsp;том же приложении недоступна."
      class="mx-auto block h-auto w-full max-w-sm"
      width="360"
      height="226"
      loading="lazy"
    >
    <figcaption class="mx-auto mt-4 max-w-prose text-sm leading-relaxed text-muted">
      В&nbsp;этом примере подключение одно и&nbsp;то же: светильник включается, но регулировка яркости в&nbsp;приложении недоступна.
    </figcaption>
  </figure>
</template>
