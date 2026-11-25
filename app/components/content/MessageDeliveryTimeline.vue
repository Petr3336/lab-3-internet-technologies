<script setup lang="ts">
import type { TimelineItem } from '@nuxt/ui'

const events: TimelineItem[] = [
  {
    date: '10:25',
    title: 'Датчик сделал замер',
    description: 'Температура партии Р-42: +4 °C.',
    icon: 'i-lucide-thermometer'
  },
  {
    date: '10:25:02',
    title: 'Шлюз принял показание',
    description: 'Через две секунды после замера.',
    icon: 'i-lucide-inbox'
  },
  {
    date: '11:05',
    title: 'Показание появилось в приложении',
    description: 'Когда показание поступило на сервер?',
    icon: 'i-lucide-monitor'
  }
]
</script>

<template>
  <section
    class="my-8 rounded-xl border border-default bg-elevated/50 p-4 sm:p-6"
    aria-label="Путь одного замера"
  >
    <p class="mb-4 text-sm text-muted">
      Учебный пример: путь замера для партии Р-42. От замера до появления в&nbsp;приложении прошло <strong class="text-highlighted">40&nbsp;минут</strong>.
    </p>
    <UTimeline
      :items="events"
      orientation="vertical"
      :ui="{ date: 'tabular-nums' }"
    />
  </section>
</template>
