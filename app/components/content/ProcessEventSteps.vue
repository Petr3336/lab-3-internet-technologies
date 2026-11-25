<script setup lang="ts">
const events = [
  {
    title: 'Наблюдение',
    description: 'Датчик на складе фиксирует температуру. Показание содержит значение, единицу измерения и время замера.',
    icon: 'i-lucide-thermometer'
  },
  {
    title: 'Событие',
    description: 'Склад фиксирует приёмку. В записи есть идентификатор партии, время приёмки и ссылка на измерение.',
    icon: 'i-lucide-clipboard-list'
  },
  {
    title: 'Обмен',
    description: 'Склад и поставщик используют согласованный формат события. В общий реестр можно внести ключевые сведения и хеш документа, а сам документ хранить отдельно.',
    icon: 'i-lucide-arrow-right-left'
  },
  {
    title: 'Проверка',
    description: 'Участник сверяет историю событий. Если у него есть документ, он может сравнить его хеш с записью в реестре. Точность измерения зависит от датчика и условий замера.',
    icon: 'i-lucide-shield-check'
  }
]
</script>

<template>
  <section
    class="my-8 rounded-xl border border-default bg-elevated/50 p-4 sm:p-6"
    aria-label="Как измерение становится частью общей истории"
  >
    <p class="mb-4 text-sm text-muted">
      Учебный пример приёмки партии.
    </p>
    <UTimeline
      :items="events"
      orientation="vertical"
    />
  </section>
</template>
