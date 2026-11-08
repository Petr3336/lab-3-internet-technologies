<script setup lang="ts">
const route = useRoute()

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
</script>

<template>
  <ContentRenderer v-if="page" :value="page" />
  <div v-else>Страница не найдена</div>
</template>