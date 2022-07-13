<template>
  <div>
    <p v-if="$fetchState.pending">Loading....</p>
    <p v-else-if="$fetchState.error">Error while fetching mountains</p>
    <div v-else>
      <v-chip 
        v-for="(mountain, index) in mountains" 
        :key="index" 
      >
        <NuxtLink 
         :to="`/blog/category/${mountain.slug}`" class=""
        > 
         {{ mountain.name }}
        </NuxtLink>
      </v-chip>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        mountains: []
      }
    },
    async fetch() {
      this.mountains = await fetch(
        'https://www.gfgm.net/_content/categories'
      ).then(res => res.json())
    }
  }
</script>

<style scoped>
a {
 text-decoration: none;
 color: white;
}
</style>
