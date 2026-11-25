<script setup lang="ts">
const route = useRoute()
const tocOpen = ref(false)

const { data: page } = await useAsyncData(
  route.path,
  () => queryCollection('content').path(route.path).first()
)

if (!page.value) {
  throw createError({
    statusCode: 404,
    statusMessage: 'Page not found'
  })
}

useSeoMeta({
  title: () => page.value?.title,
  description: () => page.value?.description,
  ogTitle: () => page.value?.title,
  ogDescription: () => page.value?.description
})
</script>

<template>
  <UPage>
    <UPageBody class="mx-auto max-w-3xl">
      <ContentRenderer
        v-if="page"
        :value="page"
      />
    </UPageBody>
    <template
      v-if="page?.body?.toc?.links?.length"
      #right
    >
      <UContentToc
        v-model:open="tocOpen"
        title="Содержание"
        :links="page.body.toc.links"
        :ui="{ linkText: 'text-clip whitespace-normal' }"
        @move="tocOpen = false"
        highlight
        highlight-variant="circuit"
      />
    </template>
  </UPage>
</template>
