<template>
 <div>
  <v-chip
    v-for="category of categories"
    :key="category.slug"
  >
    {{ category.name }}
  </v-chip>
</div>
</template>
<script>
export default {
   async asyncData({ $content, params }) {
      const catgories = await $content('categories')
        .only(['name', 'slug'])
        .sortBy('createdAt', 'asc')
        .fetch()
      return {
        catgories
      }
}

}

</script>
