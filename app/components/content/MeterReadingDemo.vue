<script setup lang="ts">
const meters = [
  {
    label: 'Накопительный итог',
    reading: '12,000 → 12,300 м³',
    calculation: '12,300 − 12,000 = 0,300 м³ = 300 л',
    description: 'Вычитаем начальное показание из конечного и переводим кубометры в литры.'
  },
  {
    label: 'Расход за интервал',
    reading: '300 л',
    calculation: '300 л за интервал',
    description: 'Счётчик уже передал расход за интервал в литрах. Вычитать ничего не нужно.'
  }
]

const revealed = ref(false)
const resultId = useId()
</script>

<template>
  <section
    class="my-8 grid gap-4 rounded-xl border border-default bg-elevated/50 p-4 sm:p-6"
    aria-label="Сравнение показаний двух счётчиков"
  >
    <p class="text-sm text-muted">
      Два счётчика передают поле <code class="font-mono text-highlighted">volume</code>. Какой расход в&nbsp;литрах показывает каждый счётчик за один и&nbsp;тот же интервал?
    </p>
    <dl class="grid gap-3 text-sm sm:grid-cols-2">
      <div
        v-for="meter in meters"
        :key="meter.label"
        class="border-t border-default pt-3"
      >
        <dt class="text-muted">
          {{ meter.label }}
        </dt>
        <dd class="mt-1 font-semibold text-highlighted tabular-nums">
          {{ meter.reading }}
        </dd>
      </div>
    </dl>
    <UButton
      type="button"
      :label="revealed ? 'Скрыть расчёт' : 'Показать расчёт'"
      :aria-expanded="revealed"
      :aria-controls="resultId"
      class="min-h-11 justify-self-start"
      @click="revealed = !revealed"
    />
    <div
      :id="resultId"
      role="status"
    >
      <dl
        v-if="revealed"
        class="grid gap-3 border-t border-default pt-4 text-sm"
      >
        <div
          v-for="meter in meters"
          :key="meter.label"
        >
          <dt class="font-medium text-highlighted">
            {{ meter.label }}
          </dt>
          <dd>
            <p>{{ meter.description }}</p>
            <p class="font-semibold text-highlighted tabular-nums">
              {{ meter.calculation }}
            </p>
          </dd>
        </div>
      </dl>
    </div>
  </section>
</template>
