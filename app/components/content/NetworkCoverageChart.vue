<script setup lang="ts">
const coverage = [
  { group: 'Мир', percentage: 55 },
  { group: 'Страны с высоким доходом', percentage: 84 },
  { group: 'Страны с низким доходом', percentage: 4 }
]
</script>

<template>
  <figure class="my-8 rounded-xl border border-default bg-elevated/50 p-4 sm:p-6">
    <figcaption class="mb-4 font-semibold text-highlighted">
      Доля населения в зоне покрытия 5G в 2025 году
    </figcaption>

    <ul
      class="grid gap-4"
      role="list"
    >
      <li
        v-for="{ group, percentage } in coverage"
        :key="group"
      >
        <div class="mb-1 flex justify-between gap-3 text-sm">
          <span>{{ group }}</span>
          <span class="font-semibold tabular-nums text-highlighted">{{ percentage }}%</span>
        </div>
        <div
          class="h-3 overflow-hidden rounded-full bg-accented"
          aria-hidden="true"
        >
          <div
            class="h-full rounded-full bg-primary"
            :style="{ width: percentage + '%' }"
          />
        </div>
      </li>
    </ul>

    <div
      class="mt-2 grid grid-cols-3 text-xs tabular-nums text-muted"
      aria-hidden="true"
    >
      <span>0%</span>
      <span class="text-center">50%</span>
      <span class="text-right">100%</span>
    </div>

    <p class="mt-4 text-sm text-muted">
      Источник&nbsp;—
      <a
        href="https://www.itu.int/itu-d/reports/statistics/2025/10/15/ff25-mobile-network-coverage/"
        class="font-medium text-primary underline underline-offset-2"
      >оценки Международного союза электросвязи (МСЭ)</a>.
    </p>
  </figure>
</template>
