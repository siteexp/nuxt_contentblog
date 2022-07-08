<template>
 <div>
  <v-chip
    v-for="tag of tags"
    :key="tag.slug"
  >
    {{ tag.name }}
  </v-chip>
  {{ tags }}
</div>
</template>
<script>
export default {
   async asyncData({ $content, params }) {
      const tags = await $content('tags')
        .only(['name', 'slug'])
        .sortBy('createdAt', 'asc')
        .fetch()
      return {
        tags
      }
}

}

</script>
