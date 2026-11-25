<script setup lang="ts">
const choices = [
  {
    label: 'Принять партию по совпадению хешей',
    feedback: 'Совпадения недостаточно для приёмки: сверка хешей проверяет версию файла, но не точность и не актуальность замера.'
  },
  {
    label: 'Проверить температуру при разгрузке',
    feedback: 'Контрольный замер даёт показание на момент разгрузки. Совпадение хешей помогает сверить версию файла, но само по себе не говорит о температуре при приёмке.'
  }
]

const choice = shallowRef<(typeof choices)[number] | null>(null)
const question = ref<HTMLParagraphElement | null>(null)
const questionId = useId()

function resetChoice() {
  choice.value = null
  question.value?.focus()
}
</script>

<template>
  <section
    class="my-8 grid gap-4 rounded-xl border border-default bg-elevated/50 p-4 sm:p-6"
    aria-label="Проверка записи перед приёмкой"
  >
    <p class="text-sm text-muted">
      В&nbsp;предъявленном файле для партии Р-42 указан замер: <strong class="text-highlighted">+4&nbsp;°C в&nbsp;10:25</strong>. Буква A условно обозначает хеш.
    </p>
    <dl class="grid grid-cols-2 gap-3 border-t border-default pt-3 text-sm">
      <div>
        <dt class="text-muted">
          Хеш в&nbsp;журнале
        </dt>
        <dd class="mt-1 font-mono font-semibold text-highlighted">
          A
        </dd>
      </div>
      <div>
        <dt class="text-muted">
          Хеш файла
        </dt>
        <dd class="mt-1 font-mono font-semibold text-highlighted">
          A
        </dd>
      </div>
    </dl>
    <p
      :id="questionId"
      ref="question"
      tabindex="-1"
      class="text-sm font-medium text-highlighted"
    >
      Достаточно ли совпадения хешей для приёмки партии?
    </p>
    <div
      role="group"
      :aria-labelledby="questionId"
      class="flex flex-wrap gap-2"
    >
      <UButton
        v-for="option in choices"
        :key="option.label"
        type="button"
        :label="option.label"
        :color="choice === option ? 'primary' : 'neutral'"
        variant="outline"
        :aria-pressed="choice === option"
        class="min-h-11 max-w-full text-left"
        @click="choice = option"
      />
    </div>
    <div role="status">
      <div
        v-if="choice"
        class="space-y-2 border-t border-default pt-4 text-sm"
      >
        <p>{{ choice.feedback }}</p>
        <p>
          <strong class="text-highlighted">Контрольный замер при разгрузке: +7&nbsp;°C.</strong>
          Его сделали в&nbsp;другое время и&nbsp;в других условиях. Разница показаний сама по себе не доказывает неисправность датчика.
        </p>
      </div>
    </div>
    <UButton
      v-if="choice"
      type="button"
      label="Сбросить выбор"
      color="neutral"
      variant="ghost"
      class="min-h-11 justify-self-start"
      @click="resetChoice"
    />
  </section>
</template>
