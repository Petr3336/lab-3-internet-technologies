<script setup lang="ts">
const route = useRoute();
const tocOpen = ref(false);

const { data: page } = await useAsyncData(route.path, () =>
  queryCollection("content").path(route.path).first(),
);

if (!page.value) {
  throw createError({
    statusCode: 404,
    statusMessage: "Page not found",
  });
}

useSeoMeta({
  title: () => page.value?.title,
  description: () => page.value?.description,
  ogTitle: () => page.value?.title,
  ogDescription: () => page.value?.description,
});

const taskDescription = [
  {
    label: "Задание",
    content: `
В рамках выполнения второй лабораторной работы Вам необходимо создать лонгрид (long read) на основе материалов, подготовленных в лабораторной работе №1.\n
1. Создать необходимо мультимедиа лонгрид, который представляет собой материал, который сочетает в себе разные формы подачи информации: текст, фото, видео, графику, анимацию, аудио. Все элементы контента не просто дополняют друг друга, но и важны сами по себе, так как работают на раскрытие темы.\n
2. Минимально Ваш лонгрид должен состоять из заголовка, содержания (кликабельного), основного текста (содержащего не менее одного изображения на 5-7 тыс. слов), выводов.\n
3. В лонгрид необходимо добавить ссылки на: различные исследования по теме; экспертные статьи; практические кейсы.\n 
4. Для создания можно использовать следующие среды и сервисы: Tilda, webflow.com и др.\n
5. В качестве ответа прикрепить ссылку на выполненную работу в соответствующий раздел ЭОС.\n
`,
  },
];
</script>

<template>
  <UPage>
    <UPageBody class="mx-auto max-w-3xl">
      <UCard>
        <UAccordion
          type="multiple"
          :items="taskDescription"
          :unmount-on-hide="false"
          :default-value="['3']"
          :ui="{
            trigger: 'text-base',
            body: 'text-base',
          }"
        >
          <template #body="{ item }">
            <MDC :value="item.content" :prose="false" />
          </template>
        </UAccordion>
      </UCard>
      <ContentRenderer v-if="page" :value="page" />
    </UPageBody>
    <template v-if="page?.body?.toc?.links?.length" #right>
      <UContentToc
        v-model:open="tocOpen"
        title="Содержание"
        :links="page.body.toc.links"
        data-article-toc
        :ui="{
          item: 'ms-0',
          itemWithChildren: 'ps-0',
          link: 'before:pointer-events-none before:absolute before:inset-y-0 before:-start-4 before:w-[11px] before:bg-(--ui-border) [&.text-primary]:before:bg-primary rtl:before:-scale-x-100',
          linkText: 'text-clip whitespace-normal',
          indicator: 'hidden',
        }"
        highlight
        highlight-variant="circuit"
        @move="tocOpen = false"
      />
    </template>
  </UPage>
</template>

<style>
/* Draw against each wrapped link; the forwarded right slot does not carry this page's scope ID. */
[data-article-toc] [data-slot="link"]::before {
  --rail-column: 0px;
  --rail-start: var(--rail-column);
  --rail-end: var(--rail-column);
  --rail-enter: 0px;
  --rail-exit: 0px;

  clip-path: polygon(
    var(--rail-start) 0,
    var(--rail-column) var(--rail-enter),
    var(--rail-column) calc(100% - var(--rail-exit)),
    var(--rail-end) 100%,
    calc(var(--rail-end) + 1px) 100%,
    calc(var(--rail-column) + 1px) calc(100% - var(--rail-exit)),
    calc(var(--rail-column) + 1px) var(--rail-enter),
    calc(var(--rail-start) + 1px) 0
  );
}

[data-article-toc] li > ul > li > [data-slot="link"]::before {
  --rail-column: 10px;

  inset-inline-start: -1.75rem;
}

[data-article-toc] li > ul > li:first-child > [data-slot="link"]::before {
  --rail-start: 0px;
  --rail-enter: 6px;
}

[data-article-toc]
  li:has(+ li)
  > ul
  > li:last-child
  > [data-slot="link"]::before {
  --rail-end: 0px;
  --rail-exit: 6px;
}
</style>
